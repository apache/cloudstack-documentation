.. Licensed to the Apache Software Foundation (ASF) under one
   or more contributor license agreements.  See the NOTICE file
   distributed with this work for additional information
   regarding copyright ownership.  The ASF licenses this file
   to you under the Apache License, Version 2.0 (the
   "License"); you may not use this file except in compliance
   with the License.  You may obtain a copy of the License at
   http://www.apache.org/licenses/LICENSE-2.0
   Unless required by applicable law or agreed to in writing,
   software distributed under the License is distributed on an
   "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
   KIND, either express or implied.  See the License for the
   specific language governing permissions and limitations
   under the License.


Quick Installation Guide
========================

Overview
--------

What exactly are we building?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Infrastructure-as-a-Service (IaaS) clouds can be a complex thing to build, and 
by definition they have a plethora of options, which often lead to confusion 
for even experienced admins who are newcomers to building cloud platforms. The 
goal for this runbook is to provide a straightforward set of instructions to 
get you up and running with CloudStack with a minimum amount of trouble.


.. warning::
      This guide is meant to be used to build CloudStack test/demo cloud only, 
      as certain networking choices have been made to get you up and running with 
      minimal amount of time. This guide can NOT be used for production setup.
      
.. warning::
      In case you don't have physical server to "play with", you can use e.g. Oracle VirtualBox 6.1+. 
      The requirement is that you enable "Enable Nested VT-x/AMD-V" as the Extended Feature on the System page of the Settings of the Instance.
      You will want to create an Instance of "Red Hat (64-bit)" type and 40+GB disk space.
      You will need to have 1 NIC in your Instance, bridged to the NIC of your laptop/desktop
      (wifi or wired NIC, doesn't matter), and optimally to set Adapter Type="Paravirtualized Network (virtio-net)"
      for somewhat better network performance (Settings of Instance, Network section, Adapter1,
      expand "Advanced"). Make sure the NIC on your Instance is configured as promiscuous (in VirtualBox,
      choose "Allow All" or just "Allow Instances" as the Promiscuous Mode), so that it can pass traffic from
      CloudStack's system VMs to the gateway. Also, make sure you have allowed enough ram (6G+) and
      enough CPU cores (3+) for demo purposes.
      
      
High level overview of the process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This guide will focus on building a CloudStack cloud using KVM on CentOS 
7.9 with NFS storage and layer-2 isolation using VLANs,
(flat home network can be used for this as well) and on a single piece of 
hardware (server/VM)

KVM, or Kernel-based Virtual Machine is a virtualization technology for the 
Linux kernel. KVM supports native virtualization atop processors with hardware 
virtualization extensions.


Prerequisites
~~~~~~~~~~~~~

To complete this guide you'll need the following items:

#. At least one computer which supports and has enabled hardware virtualization.

#. An `CentOS 7.9 minimal x86_64 install ISO, on bootable media
   <http://isoredirect.centos.org/centos/7/isos/x86_64/>`_

#. A /24 network with the gateway being at (e.g.) xxx.xxx.xxx.1, no DHCP is needed 
   on this network and none of the computers running CloudStack will have a 
   dynamic address. Again this is done for the sake of simplicity.


Environment
-----------

Before you begin , you need to prepare the environment before you install 
CloudStack. We will go over the steps to prepare now.


Operating System
~~~~~~~~~~~~~~~~

Using the CentOS 7.9.2009 minimal x86_64 install ISO, you'll need to install
CentOS 7 on your hardware. The defaults will generally be acceptable for this
installation - but make sure to configure IP address/parameters so that you can later install needed
packages from the internet. Later, we will change the Network configuration as needed.

Once this installation is complete, you'll want to gain access to your
server - through SSH. 

It is always wise to update the system before starting: 

.. parsed-literal::
   # yum -y upgrade


.. _conf-network:

Configuring the Network
^^^^^^^^^^^^^^^^^^^^^^^

Before going any further, make sure that "bridge-utils" and "net-tools" are installed and available:

.. parsed-literal::
   # yum install bridge-utils net-tools -y

Connecting via the console or SSH, you should login as root. We will start by creating
the bridge that Cloudstack will use for networking. Create and open
/etc/sysconfig/network-scripts/ifcfg-cloudbr0 and add the following settings:

.. note:: 
   IP Addressing - Throughout this document we are assuming that you will have 
   a /24 network for your CloudStack implementation. This can be any RFC 1918 
   Network. However, we are assuming that you will match the machine address
   that we are using. Thus we may use 172.16.10.2 and because you might be 
   using e.g. 192.168.55.0/24 network you would use 192.168.55.2. Another example
   would be if you are using i.e. VirtualBox on your local home network on 192.168.1.0/24 network - 
   in this case you can use a single free IP address from your home range (VirtualBox NIC for this Instance
   should be in bridged mode for correct functioning)
   
::

   DEVICE=cloudbr0
   TYPE=Bridge
   ONBOOT=yes
   BOOTPROTO=static
   IPV6INIT=no
   IPV6_AUTOCONF=no
   DELAY=5
   IPADDR=172.16.10.2 #(or e.g. 192.168.1.2)
   GATEWAY=172.16.10.1 #(or e.g. 192.168.1.1 - this would be your physical/home router)
   NETMASK=255.255.255.0
   DNS1=8.8.8.8
   DNS2=8.8.4.4
   STP=yes
   USERCTL=no
   NM_CONTROLLED=no

Save the configuration and exit. We will then edit the NIC so that it
makes use of this bridge.
   
Open the configuration file of your NIC (e.g. /etc/sysconfig/network-scripts/ifcfg-eth0)
and edit it as follows:

.. note::
   Interface name (eth0) used as example only. Replace eth0 with your default ethernet interface name.

.. parsed-literal::
   TYPE=Ethernet
   BOOTPROTO=none
   DEFROUTE=yes
   NAME=eth0
   DEVICE=eth0
   ONBOOT=yes
   BRIDGE=cloudbr0

.. note::
   If your physical nic (eth0 in the case of our example) has already been
   setup before following this guide, make sure that there is no duplication
   between IP configuration of /etc/config/network-scripts/ifcfg-cloudbr0 and
   /etc/sysconfig/network-scripts/ifcfg-eth0 which will cause a failure that
   would prevent the network from starting. Basically, IP configuration
   of eth0 should be moved to the bridge and eth0 will be added to the bridge.


Now that we have the configuration files properly set up, we need to run a few 
commands to start up the network: 

.. parsed-literal::

   # systemctl disable NetworkManager; systemctl stop NetworkManager
   # systemctl enable network
   # reboot
 
.. _conf-hostname:

Hostname
^^^^^^^^

CloudStack requires that the hostname is properly set. If you used the default 
options in the installation, then your hostname is currently set to 
localhost.localdomain. To test this we will run:

.. parsed-literal::

   # hostname --fqdn

At this point it will likely return: 

.. parsed-literal::

   localhost

To rectify this situation - we'll set the hostname by editing the /etc/hosts 
file so that it follows a similar format to this example (remember to replace
the IP with your IP which might be e.g. 192.168.1.2):

.. parsed-literal::

   127.0.0.1 localhost localhost.localdomain localhost4 localhost4.localdomain4
   ::1 localhost localhost.localdomain localhost6 localhost6.localdomain6
   172.16.10.2 srvr1.cloud.priv

After you've modified that file, go ahead and restart the network using:

.. parsed-literal::

   # systemctl restart network

Now recheck with the

.. parsed-literal::

   # hostname --fqdn

and ensure that it returns a FQDN response


.. _conf-selinux:

SELinux
^^^^^^^

At the moment, for CloudStack to work properly SELinux must be set to 
permissive or disabled. We want to both configure this for future boots and modify it in 
the current running system.

To configure SELinux to be permissive in the running system we need to run the 
following command:

.. parsed-literal::

   # setenforce 0

To ensure that it remains in that state we need to configure the file 
/etc/selinux/config to reflect the permissive state, as shown in this example:

.. parsed-literal::

   # This file controls the state of SELinux on the system.
   # SELINUX= can take one of these three values:
   # enforcing - SELinux security policy is enforced.
   # permissive - SELinux prints warnings instead of enforcing.
   # disabled - No SELinux policy is loaded.
   SELINUX=permissive
   # SELINUXTYPE= can take one of these two values:
   # targeted - Targeted processes are protected,
   # mls - Multi Level Security protection.
   SELINUXTYPE=targeted


.. _conf-ntp:

NTP
^^^

NTP configuration is a necessity for keeping all of the clocks in your cloud 
servers in sync. However, NTP is not installed by default. So we'll install 
and and configure NTP at this stage. Installation is accomplished as follows:

.. parsed-literal::

   # yum -y install ntp

The actual default configuration is fine for our purposes, so we merely need 
to enable it and set it to start on boot as follows:

.. parsed-literal::

   # systemctl enable ntpd
   # systemctl start ntpd


.. _qigconf-pkg-repo:

Configuring the CloudStack Package Repository
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We need to configure the machine to use a CloudStack package repository. 

.. note:: 
   The Apache CloudStack official releases are source code. As such there are 
   no 'official' binaries available. The full installation guide describes how 
   to take the source release and generate RPMs and and yum repository. This 
   guide attempts to keep things as simple as possible, and thus we are using 
   one of the community-provided yum repositories. Furthermore, this example 
   assumes a |release| Cloudstack install - substitute versions as needed.

To add the CloudStack repository, create /etc/yum.repos.d/cloudstack.repo and 
insert the following information.

.. parsed-literal::

   [cloudstack]
   name=cloudstack
   baseurl=http://download.cloudstack.org/centos/$releasever/|version|/
   enabled=1
   gpgcheck=0


NFS
~~~

Our configuration is going to use NFS for both primary and secondary storage. 
We are going to go ahead and setup two NFS shares for those purposes. We'll 
start out by installing nfs-utils.

.. parsed-literal::

   # yum -y install nfs-utils

We now need to configure NFS to serve up two different shares. This is handled 
in the /etc/exports file. You should ensure that it has the following content:

.. parsed-literal::

   /export/secondary \*(rw,async,no_root_squash,no_subtree_check)
   /export/primary \*(rw,async,no_root_squash,no_subtree_check)

You will note that we specified two directories that don't exist (yet) on the 
system. We'll go ahead and create those directories and set permissions 
appropriately on them with the following commands:

.. parsed-literal::

   # mkdir -p /export/primary
   # mkdir /export/secondary

CentOS 7.x releases use NFSv4 by default. NFSv4 requires that domain setting 
matches on all clients. In our case, the domain is cloud.priv, so ensure that 
the domain setting in /etc/idmapd.conf is uncommented and set as follows:

.. parsed-literal::
   Domain = cloud.priv

Now you'll need to add the configuration values at the bottom in the file 
/etc/sysconfig/nfs (or merely uncomment and set them)

.. parsed-literal::

   LOCKD_TCPPORT=32803
   LOCKD_UDPPORT=32769
   MOUNTD_PORT=892
   RQUOTAD_PORT=875
   STATD_PORT=662
   STATD_OUTGOING_PORT=2020

For simplicity, we need to disable the firewall, so that it will not block connections.

.. note::

   Configuration of the firewall on CentOS7 is beyond the purview of this
   guide.
   
To do so, simply use the following two commands: 

.. parsed-literal::

   # systemctl stop firewalld
   # systemctl disable firewalld

We now need to configure the nfs service to start on boot and actually start 
it on the host by executing the following commands:

.. parsed-literal::

   # systemctl enable rpcbind
   # systemctl enable nfs
   # systemctl start rpcbind
   # systemctl start nfs


Management Server Installation
------------------------------

We're going to install the CloudStack management server and surrounding tools. 


Database Installation and Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We'll start with installing MySQL and configuring some options to ensure it 
runs well with CloudStack. 

First, as CentOS 7 no longer provides the MySQL binaries, we need to add a MySQL community repository,
that will provide MySQL Server (and the Python MySQL connector later) : 

.. parsed-literal::
   # yum -y install wget
   # wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
   # rpm -ivh mysql-community-release-el7-5.noarch.rpm

Install by running the following command: 

.. parsed-literal::

   # yum -y install mysql-server

This should install MySQL 5.x, as of the time of writing this guide.
With MySQL now installed we need to make a few configuration changes to 
/etc/my.cnf. Specifically we need to add the following options to the [mysqld] 
section:

.. parsed-literal::

   innodb_rollback_on_timeout=1
   innodb_lock_wait_timeout=600
   max_connections=350
   log-bin=mysql-bin
   binlog-format = 'ROW'

.. note::

   For Ubuntu 16.04 and later, make sure you specify a ``server-id`` in your ``.cnf`` file for binary logging. Set the     ``server-id`` according to your database setup.
    
.. parsed-literal::

   server-id=source-01
   innodb_rollback_on_timeout=1
   innodb_lock_wait_timeout=600
   max_connections=350
   log-bin=mysql-bin
   binlog-format = 'ROW'

Now that MySQL is properly configured we can start it and configure it to 
start on boot as follows:

.. parsed-literal:: 

   # systemctl enable mysqld
   # systemctl start mysqld


MySQL Connector Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Install Python MySQL connector from the MySQL community repository (which we've added previously):

.. parsed-literal:: 

   # yum -y install mysql-connector-python
   
Please note that the previously required ``mysql-connector-java`` library is now bundled with CloudStack
Management server and is no longer required to be installed separately.

Installation
~~~~~~~~~~~~

We are now going to install the management server. We do that by executing the 
following command:

.. parsed-literal::

   # yum -y install cloudstack-management

CloudStack |version| requires Java 17 JRE. Installing the management server
will automatically install Java 17, but it's good to explicitly confirm that Java 17
is the selected/active one (in case you had a previous Java version already installed):

   .. parsed-literal::

      $ alternatives --config java
      
Make sure that Java 17 is selected.

With the application itself installed we can now setup the database, we'll do 
that with the following command and options:

.. parsed-literal::

   # cloudstack-setup-databases cloud:password@localhost --deploy-as=root

When this process is finished, you should see a message like "CloudStack has 
successfully initialized the database."

Now that the database has been created, we can take the final step in setting 
up the management server by issuing the following command:

.. parsed-literal::

   # cloudstack-setup-management


System Template Setup
~~~~~~~~~~~~~~~~~~~~~

CloudStack uses a number of system VMs to provide functionality for accessing 
the console of Instances, providing various networking services, and
managing various aspects of storage. 

We need to download the systemVM Template and deploy that to the secondary storage.
We will use the local path (/export/secondary) since we are already on the NFS server itself,
but otherwise you would need to mount your Secondary Storage to a temporary mount point, and use
that mount point instead of the /export/secondary path.

Execute the following script:

.. parsed-literal::
  
   /usr/share/cloudstack-common/scripts/storage/secondary/cloud-install-sys-tmplt \
   -m /export/secondary \
   -u |sysvm64-url-kvm| \
   -h kvm -F


That concludes our setup of the management server. We still need to configure 
CloudStack, but we will do that after we get our hypervisor set up.


KVM Setup and Installation
--------------------------

Prerequisites
~~~~~~~~~~~~~

We are using the management server as a compute node as well, which 
means that we have already performed many of the prerequisite steps when 
setting up the management server, but we will list them here for clarity. 
Those steps are:

:ref:`conf-network`

:ref:`conf-hostname`

:ref:`conf-selinux`

:ref:`conf-ntp`

:ref:`qigconf-pkg-repo`

You don't need to do that for the management server now as we've already done that.


Installation
~~~~~~~~~~~~

Installation of the KVM agent is trivial with just a single command, but 
afterwards we'll need to configure a few things. We need to install the EPEL repository also.

.. parsed-literal::

   # yum -y install epel-release
   # yum -y install cloudstack-agent


KVM Configuration
~~~~~~~~~~~~~~~~~~~~

We have two different parts of KVM to configure, libvirt, and QEMU.


QEMU Configuration
^^^^^^^^^^^^^^^^^^^

We need to edit the QEMU VNC configuration. This is done by editing /etc/libvirt/qemu.conf 
and ensuring the following line is present and uncommented.

::

   vnc_listen=0.0.0.0


Libvirt Configuration
^^^^^^^^^^^^^^^^^^^^^^^

CloudStack uses libvirt for managing Instances. Therefore it is vital
that libvirt is configured correctly. Libvirt is a dependency of cloud-agent 
and should already be installed.

#. Even though we are using a single host, the following steps are recommended
   to get faimilar with the general requirements.
   In order to have live migration working libvirt has to listen for unsecured 
   TCP connections. We also need to turn off libvirts attempt to use Multicast 
   DNS advertising. Both of these settings are in /etc/libvirt/libvirtd.conf

   Set the following paramaters:
   
   ::
   
      listen_tls = 0
      listen_tcp = 1
      tcp_port = "16509"
      auth_tcp = "none"
      mdns_adv = 0

#. Turning on "listen_tcp" in libvirtd.conf is not enough, we have to change 
   the parameters as well we also need to modify /etc/sysconfig/libvirtd:

   Uncomment the following line:

   :: 

      #LIBVIRTD_ARGS="--listen"

#. Restart libvirt

   .. parsed-literal::

      # systemctl restart libvirtd


KVM configuration complete
^^^^^^^^^^^^^^^^^^^^^^^^^^^
For the sake of completeness, you should check if KVM is running OK on your 
machine (you should see kvm_intel or kvm_amd modules shown as loaded):

   .. parsed-literal::
   
      # lsmod | grep kvm
      kvm_intel              55496  0
      kvm                   337772  1 kvm_intel
      kvm_amd # if you are in AMD cpu

That concludes our installation and configuration of KVM, and we'll now move 
to using the CloudStack UI for the actual configuration of our cloud.


Configuration
-------------

UI Access
~~~~~~~~~

To get access to CloudStack's web interface, merely point your browser to 
the IP address of your machine e.g. http://172.16.10.2:8080/client
The default username is 'admin', and the default password is 'password'.

Setting up a Zone
-----------------

Zone Type
~~~~~~~~~

A zone is the largest organization entity in CloudStack - and we'll be
creating one.

.. warning::
      We will be configuring an Advanced Zone in a way that will allow us to access both
      the "Management" network of the cloud as well as the "Public" network - we will do so
      by using the same CIDR (but different part of it, i.e. different IP ranges) for both 
      "Management" (Pod) and "Public" networks - which is something your would NEVER do 
      in a production - this is done strictly for testing purposes only in this guide!

Click "Continue with Installation" to continue - you will be offered to change your 
root admin password - please do so, and click on OK.

A new Zone wizard will pop-up. Please chose Advanced (don't tick the "Security Groups") and click on Next.

Zone Details
~~~~~~~~~~~~

On this page, we enter where our DNS servers are located.
CloudStack distinguishes between internal and public DNS. Internal DNS is
assumed to be capable of resolving internal-only hostnames, such as your
NFS server’s DNS name. Public DNS is provided to the guest Instances to resolve
public IP addresses. You can enter the same DNS server for both types, but
if you do so, you must make sure that both internal and public IP addresses
can route to the DNS server. In our specific case we will not use any names
for resources internally, and we will indeed set them to look to the same
external resource so as to not add a nameserver setup to our list of
requirements.

#. Name - we will set this to the ever-descriptive 'Zone1' for our cloud.

#. IPv4 DNS 1 - we will set this to ``8.8.8.8`` for our cloud.

#. IPV4 DNS 2 - we will set this to ``8.8.4.4`` for our cloud.

#. Internal DNS1 - we will also set this to ``8.8.8.8`` for our cloud.

#. Internal DNS2 - we will also set this to ``8.8.4.4`` for our cloud.

#. Hypervisor - this will be the primary hypervisor used in this zone. In our
   case, we will select KVM.

Click "Next" to continue.

Physical Network
~~~~~~~~~~~~~~~~
There are various network isolation methods supported by Cloudstack. The
default VLAN option will be sufficient for our purposes. For improved
performance and/or security, Cloudstack allows different traffic types to run
over specifically dedicated network interface cards attached to hypervisors.
We will not be making any changes here, the default settings are fine
for this demo installation of Cloudstack.

Click "Next" to continue.


Public Traffic
~~~~~~~~~~~~~~
Publicly-accessible IPs must be allocated for this purpose in normal/public cloud installations,
but since we are deploying merely a demo/test env, we will use a PART of our local network (e.g. from .11 to .20 or other free range)

#. Gateway - We'll use ``172.16.10.1`` #or whatever is your physical gateway e.g. 192.168.1.1

#. Netmask - We'll use ``255.255.255.0``

#. VLAN/VNI - We'll leave this one empty

#. Start IP - We'll use ``172.16.10.11`` # (or e.g. 192.168.1.11)

#. End IP - We'll use ``172.16.10.20`` # (or e.g. 192.168.1.20)

Click "Add" to add the range.

Click "Next" to continue.

Pod Configuration
~~~~~~~~~~~~~~~~~

Here we will configure a range for Cloudstack's internal management traffic - CloudStack
will assign IPs from this range to system VMs. This will also be part of our local network
(i.e. different part of your local home network, from .21 to .30), with the rest of the IP parameters
(netmaks/gateway) being the same as used for the Public Traffic.

#. Pod Name - We'll use ``Pod1`` for our cloud.

#. Reserved system gateway - we'll use ``172.16.10.1`` # (or whatever is your physical gateway e.g. 192.168.1.1)

#. Reserved system netmask - we'll use ``255.255.255.0``

#. Start reserved system IPs - we will use ``172.16.10.21`` # (or e.g. 192.168.1.21)

#. End Reserved system IP - we will use ``172.16.10.30`` # (or e.g. 192.168.1.30)

.. note::
   * The network described above must be a subnet of the management network.

Click "Next" to continue.

Guest Traffic
~~~~~~~~~~~~~

Next we will configure a range of VLAN IDs for our Guest Instances.

A range of ``100`` - ``200`` would suffice.

Click "Next" to continue.

Cluster
~~~~~~~

Multiple clusters can belong to a pod and multiple hosts can belong to a
cluster. We will have one cluster and we have to give our cluster a name.

Enter ``Cluster1``

Click "Next" to continue.

Host
~~~~
This is where we specify the details of our hypervisor host. In our case,
we are running the management server on the same machine that we will be using
as a hypervisor.

#. Hostname - we'll use the IP address ``172.16.10.2`` since we didn't set up a
   DNS server for name resolution. (this is your local server, so swap with the correct IP)

#. Username - we'll use ``root``

#. Password - enter the operating system password for the root user

Click "Next" to continue.

Primary Storage
^^^^^^^^^^^^^^^

With your cluster now setup - you should be prompted for primary storage 
information. Enter the following values in the fields:

#. Name - We'll use ``Primary1``

#. Scope - We'll use ``Cluster`` even though either is fine in this case. With
   "Zone" scope, all hosts in all clusters would have access to this storage
   pool.

#. Protocol - We'll use ``NFS``

#. Server - We'll be using the IP address ``172.16.10.2`` (this is your local server, so swap with the correct IP)

#. Path - Well define ``/export/primary`` as the path we are using

Click "Next" to continue.

Secondary Storage
^^^^^^^^^^^^^^^^^

You'll be prompted for secondary storage information - populate it as follows:

#. Provider - Choose ``NFS``

#. Name - ``Secondary1``

#. NFS server - We'll use the IP address ``172.16.10.2`` (this is your local server, so swap with the correct IP)

#. Path - We'll use ``/export/secondary``

Click "Next" to continue.

Now, click "Launch Zone" and your cloud should begin setup - it may take
several minutes for setup to finalize.

When done, click on "Enable Zone" and your zone will be ready.

That's it, you are done with installation of your Apache CloudStack demo cloud.

To check the health of your CloudStack installation, go to Infrastructure --> System VMs and refresh
the UI from time to time - you should see “S-1-VM” and “V-2-VM” system VMs (SSVM and CPVM) in State=Running and Agent State=Up
After that you can go to Images --> Templates, click on the built-in Template named "CentOS 5.5(64-bit) no GUI (KVM)",
then click on "Zones" tab - and observe how the Status is moving from a few percents downloaded up to fully downloaded,
after which the Status will show as "Download Complete" and "Ready" column will say "Yes".
After this is done, you will be able to deploy an Instance from this Template.

