.. Licensed to the Apache Software Foundation (ASF) under one
   or more contributor license agreements.  See the NOTICE file
   distributed with this work for additional information#
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


Host LXC Installation
---------------------

System Requirements for LXC Hosts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

LXC requires the Linux kernel cgroups functionality which is available
starting 2.6.24. Although you are not required to run these
distributions, the following are recommended:

-  CentOS / RHEL: 6.3

-  Ubuntu: 12.04(.1)

The main requirement for LXC hypervisors is the libvirt and Qemu
version. No matter what Linux distribution you are using, make sure the
following requirements are met:

-  libvirt: 1.0.0 or higher

-  Qemu/KVM: 1.0 or higher

The default bridge in CloudStack is the Linux native bridge
implementation (bridge module). CloudStack includes an option to work
with OpenVswitch, the requirements are listed below

-  libvirt: 1.0.0 or higher

-  openvswitch: 1.7.1 or higher

In addition, the following hardware requirements apply:

-  Within a single cluster, the hosts must be of the same distribution
   version.

-  All hosts within a cluster must be homogeneous. The CPUs must be of
   the same type, count, and feature flags.

-  Must support HVM (Intel-VT or AMD-V enabled)

-  64-bit x86 CPU (more cores results in better performance)

-  4 GB of memory

-  At least 1 NIC

-  When you deploy CloudStack, the hypervisor host must not have any Instances
   already running


LXC Installation Overview
~~~~~~~~~~~~~~~~~~~~~~~~~

LXC does not have any native system VMs, instead KVM will be used to run
system VMs. This means that your host will need to support both LXC and
KVM, thus most of the installation and configuration will be identical
to the KVM installation. The material in this section doesn't duplicate
information, so perform the steps in the Host KVM Installation section first
:ref:`host-kvm-installation`.

.. warning:: 
   Before continuing, make sure that you have applied the latest updates to 
   your host.

.. warning::
   It is NOT recommended to run services on this host not controlled by 
   CloudStack.

The procedure for installing an LXC Host is:

#. Prepare the Operating System

#. Install and configure libvirt

#. Configure Security Policies (AppArmor and SELinux)

#. Install and configure the Agent


Prepare the Operating System
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The OS of the Host must be prepared to host the CloudStack Agent and run
KVM Instances.

#. Log in to your OS as root.

#. Check for a fully qualified hostname.

   .. parsed-literal::

      $ hostname --fqdn

   This should return a fully qualified hostname such as
   "kvm1.lab.example.org". If it does not, edit /etc/hosts so that it
   does.

#. Make sure that the machine can reach the Internet.

   .. parsed-literal::

      $ ping www.cloudstack.org

#. Turn on NTP for time synchronization.

   .. note:: 
      NTP is required to synchronize the clocks of the servers in your
      cloud. Unsynchronized clocks can cause unexpected problems.

#. Install NTP

   In RHEL or CentOS:

      .. parsed-literal::

         $ yum install chrony

   In Ubuntu:

      .. parsed-literal::

         $ apt install chrony

   In SUSE:

      .. parsed-literal::

         $ zypper install chrony

#. Repeat all of these steps on every hypervisor host.


Configure package repository
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

CloudStack is only distributed from source from the official mirrors.
However, members of the CloudStack community may build convenience
binaries so that users can install Apache CloudStack without needing to
build from source.

If you didn't follow the steps to build your own packages from source in
the sections for `“Building RPMs from Source”
<../building_from_source.html#building-rpms-from-source>`__ or
`“Building DEB packages” <../building_from_source.html#building-deb-packages>`__
you may find pre-built DEB and RPM packages for your convenience linked from
the `downloads <http://cloudstack.apache.org/downloads.html>`_ page.

.. note::
   These repositories contain both the Management Server and KVM Hypervisor
   packages.

RPM package repository
~~~~~~~~~~~~~~~~~~~~~~

There is a RPM package repository for CloudStack so you can easily
install on RHEL and SUSE based platforms.

If you're using an RPM-based system, you'll want to add the Yum
repository so that you can install CloudStack with Yum.

In RHEL or CentOS:

Yum repository information is found under ``/etc/yum.repos.d``. You'll
see several ``.repo`` files in this directory, each one denoting a
specific repository.

To add the CloudStack repository, create
``/etc/yum.repos.d/cloudstack.repo`` and insert the following
information.

In the case of RHEL being used, you can replace 'centos' by 'rhel' in the value of baseurl

.. parsed-literal::

   [cloudstack]
   name=cloudstack
   baseurl=http://download.cloudstack.org/centos/$releasever/|version|/
   enabled=1
   gpgcheck=0

Now you should now be able to install CloudStack using Yum.

In SUSE:

Zypper repository information is found under ``/etc/zypp/repos.d/``. You'll
see several ``.repo`` files in this directory, each one denoting a
specific repository.

To add the CloudStack repository, create
``/etc/zypp/repos.d/cloudstack.repo`` and insert the following
information.

.. parsed-literal::

   [cloudstack]
   name=cloudstack
   baseurl=http://download.cloudstack.org/suse/|version|/
   enabled=1
   gpgcheck=0


Now you should now be able to install CloudStack using zypper.


DEB package repository
~~~~~~~~~~~~~~~~~~~~~~

You can add a DEB package repository to your apt sources with the
following commands. Replace the code name with your Ubuntu LTS version :
Ubuntu 22.04 (jammy), Ubuntu 24.04 (noble).

Use your preferred editor and open (or create)
``/etc/apt/sources.list.d/cloudstack.list``. Add the community provided
repository to the file (replace "trusty" with "xenial" or "bionic" if it is the case):

.. parsed-literal::

   deb https://download.cloudstack.org/ubuntu focal |version|

We now have to add the public key to the trusted keys.

.. parsed-literal::

   wget -O - https://download.cloudstack.org/release.asc |sudo tee /etc/apt/trusted.gpg.d/cloudstack.asc

Now update your local apt cache.

.. parsed-literal::

   sudo apt update

Your DEB package repository should now be configured and ready for use.

Install and configure the Agent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To manage LXC Instances on the host CloudStack uses a Agent. This Agent
communicates with the Management server and controls all the Instances
on the host.

.. note::
   Depending on your distribution you might need to add the corresponding package repository
   for CloudStack.

First we start by installing the agent:

In RHEL or CentOS:

.. parsed-literal::

   $ yum install -y epel-release
   $ yum install cloudstack-agent

In Ubuntu:

.. parsed-literal::

   $ apt install cloudstack-agent

In SUSE:

.. parsed-literal::

   $ zypper install cloudstack-agent


If you're using a non-root user to add the LXC host, please add the user to
sudoers file:

.. parsed-literal::

   cloudstack ALL=NOPASSWD: /usr/bin/cloudstack-setup-agent
   Defaults:cloudstack !requiretty

Next step is to update the Agent configuration settings. The settings
are in ``/etc/cloudstack/agent/agent.properties``

#. Set the Agent to run in LXC mode:

   .. parsed-literal::

      hypervisor.type=lxc

#. Optional: If you would like to use direct networking (instead of the
   default bridge networking), configure these lines:

   .. parsed-literal::

      libvirt.vif.driver=com.cloud.hypervisor.kvm.resource.DirectVifDriver

   .. parsed-literal::

      network.direct.source.mode=private

   .. parsed-literal::

      network.direct.device=eth0

The host is now ready to be added to a cluster. This is covered in a
later section, see :ref:`adding-a-host`. It is
recommended that you continue to read the documentation before adding
the host!


Install and Configure libvirt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack uses libvirt for managing System VM Instances, even in a LXC host. Therefore it is
vital that libvirt is configured correctly. Libvirt is a dependency of
cloudstack-agent and should already be installed.

Please refer to :ref:`install-and-configure-libvirt` for the steps to install and configure
libvirt. Only the, perform the next steps.

In Ubuntu:

.. parsed-literal::

   apt install libvirt-daemon-driver-lxc -y


Configure the Security Policies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack does various things which can be blocked by security
mechanisms like AppArmor and SELinux. These have to be disabled to
ensure the Agent has all the required permissions.

Please refer to :ref:`configure-the-security-policies` for the steps to install and configure libvirt.


Configure the network bridges
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. warning:: 
   This is a very important section, please make sure you read this thoroughly.

.. note:: 
   This section details how to configure bridges using the native 
   implementation in Linux. Please refer to the next section if you intend to 
   use OpenVswitch

In order to forward traffic to your Instances you will need at least two
bridges: *public* and *private*.

By default these bridges are called *cloudbr0* and *cloudbr1*, but you
do have to make sure they are available on each hypervisor.

The most important factor is that you keep the configuration consistent
on all your hypervisors.


Network example
^^^^^^^^^^^^^^^

There are many ways to configure your network. In the Basic networking
mode you should have two (V)LAN's, one for your private network and one
for the public network.

We assume that the hypervisor has one NIC (eth0) with three tagged
VLAN's:

#. VLAN 100 for management of the hypervisor

#. VLAN 200 for public network of the Instances (cloudbr0)

#. VLAN 300 for private network of the Instances (cloudbr1)

On VLAN 100 we give the Hypervisor the IP-Address 192.168.42.11/24 with
the gateway 192.168.42.1

.. note::
   The Hypervisor and Management server don't have to be in the same subnet!

Configuring the network bridges
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It depends on the distribution you are using how to configure these,
below you'll find examples for RHEL/CentOS and Ubuntu.

.. note:: 
   The goal is to have two bridges called 'cloudbr0' and 'cloudbr1' after this 
   section. This should be used as a guideline only. The exact configuration 
   will depend on your network layout.


Configure in RHEL or CentOS
'''''''''''''''''''''''''''

The required packages were installed when libvirt was installed, we can
proceed to configuring the network.

First we configure eth0

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-eth0

Make sure it looks similar to:

.. parsed-literal::

   DEVICE=eth0
   HWADDR=00:04:xx:xx:xx:xx
   ONBOOT=yes
   HOTPLUG=no
   BOOTPROTO=none
   TYPE=Ethernet

We now have to configure the three VLAN interfaces:

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-eth0.100

.. parsed-literal::

   DEVICE=eth0.100
   HWADDR=00:04:xx:xx:xx:xx
   ONBOOT=yes
   HOTPLUG=no
   BOOTPROTO=none
   TYPE=Ethernet
   VLAN=yes
   IPADDR=192.168.42.11
   GATEWAY=192.168.42.1
   NETMASK=255.255.255.0

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-eth0.200

.. parsed-literal::

   DEVICE=eth0.200
   HWADDR=00:04:xx:xx:xx:xx
   ONBOOT=yes
   HOTPLUG=no
   BOOTPROTO=none
   TYPE=Ethernet
   VLAN=yes
   BRIDGE=cloudbr0

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-eth0.300

.. parsed-literal::

   DEVICE=eth0.300
   HWADDR=00:04:xx:xx:xx:xx
   ONBOOT=yes
   HOTPLUG=no
   BOOTPROTO=none
   TYPE=Ethernet
   VLAN=yes
   BRIDGE=cloudbr1

Now we have the VLAN interfaces configured we can add the bridges on top
of them.

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-cloudbr0

Now we just configure it is a plain bridge without an IP-Address

.. parsed-literal::

   DEVICE=cloudbr0
   TYPE=Bridge
   ONBOOT=yes
   BOOTPROTO=none
   IPV6INIT=no
   IPV6_AUTOCONF=no
   DELAY=5
   STP=yes

We do the same for cloudbr1

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-cloudbr1

.. parsed-literal::

   DEVICE=cloudbr1
   TYPE=Bridge
   ONBOOT=yes
   BOOTPROTO=none
   IPV6INIT=no
   IPV6_AUTOCONF=no
   DELAY=5
   STP=yes

With this configuration you should be able to restart the network,
although a reboot is recommended to see if everything works properly.

.. warning:: 
   Make sure you have an alternative way like IPMI or ILO to reach the machine 
   in case you made a configuration error and the network stops functioning!


Configure in Ubuntu
'''''''''''''''''''

All the required packages were installed when you installed libvirt, so
we only have to configure the network.

.. parsed-literal::

   $ vi /etc/network/interfaces

Modify the interfaces file to look like this:

.. parsed-literal::

   auto lo
   iface lo inet loopback

   # The primary network interface
   auto eth0.100
   iface eth0.100 inet static
       address 192.168.42.11
       netmask 255.255.255.240
       gateway 192.168.42.1
       dns-nameservers 8.8.8.8 8.8.4.4
       dns-domain lab.example.org

   # Public network
   auto cloudbr0
   iface cloudbr0 inet manual
       bridge_ports eth0.200
       bridge_fd 5
       bridge_stp off
       bridge_maxwait 1

   # Private network
   auto cloudbr1
   iface cloudbr1 inet manual
       bridge_ports eth0.300
       bridge_fd 5
       bridge_stp off
       bridge_maxwait 1

With this configuration you should be able to restart the network,
although a reboot is recommended to see if everything works properly.

.. warning:: 
   Make sure you have an alternative way like IPMI or ILO to reach the machine 
   in case you made a configuration error and the network stops functioning!


Configuring the firewall
~~~~~~~~~~~~~~~~~~~~~~~~

The hypervisor needs to be able to communicate with other hypervisors
and the management server needs to be able to reach the hypervisor.

In order to do so we have to open the following TCP ports (if you are
using a firewall):

#. 22 (SSH)

#. 1798

#. 16509 (libvirt)

#. 5900 - 6100 (VNC consoles)

#. 49152 - 49216 (libvirt live migration)

It depends on the firewall you are using how to open these ports. Below
you'll find examples how to open these ports in RHEL/CentOS and Ubuntu.


Open ports in RHEL/CentOS
^^^^^^^^^^^^^^^^^^^^^^^^^

RHEL and CentOS use iptables for firewalling the system, you can open
extra ports by executing the following iptable commands:

.. parsed-literal::

   $ iptables -I INPUT -p tcp -m tcp --dport 22 -j ACCEPT

.. parsed-literal::

   $ iptables -I INPUT -p tcp -m tcp --dport 1798 -j ACCEPT

.. parsed-literal::

   $ iptables -I INPUT -p tcp -m tcp --dport 16509 -j ACCEPT

.. parsed-literal::

   $ iptables -I INPUT -p tcp -m tcp --dport 5900:6100 -j ACCEPT

.. parsed-literal::

   $ iptables -I INPUT -p tcp -m tcp --dport 49152:49216 -j ACCEPT

These iptable settings are not persistent across reboots, we have to
save them first.

.. parsed-literal::

   $ iptables-save > /etc/sysconfig/iptables


Open ports in Ubuntu
^^^^^^^^^^^^^^^^^^^^

The default firewall under Ubuntu is UFW (Uncomplicated FireWall), which
is a Python wrapper around iptables.

To open the required ports, execute the following commands:

.. parsed-literal::

   $ ufw allow proto tcp from any to any port 22

.. parsed-literal::

   $ ufw allow proto tcp from any to any port 1798

.. parsed-literal::

   $ ufw allow proto tcp from any to any port 16509

.. parsed-literal::

   $ ufw allow proto tcp from any to any port 5900:6100

.. parsed-literal::

   $ ufw allow proto tcp from any to any port 49152:49216

.. note:: 
   By default UFW is not enabled on Ubuntu. Executing these commands with the 
   firewall disabled does not enable the firewall.


Add the host to CloudStack
~~~~~~~~~~~~~~~~~~~~~~~~~~

The host is now ready to be added to a cluster. This is covered in a
later section, see :ref:`adding-a-host`. It is
recommended that you continue to read the documentation before adding
the host!
