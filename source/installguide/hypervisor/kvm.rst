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


Host KVM Installation
---------------------

System Requirements for KVM Hypervisor Hosts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

KVM is included with a variety of Linux-based operating systems.
Although you are not required to run these distributions, the following
are recommended:

-  CentOS / RHEL: 7.X

-  CentOS / RHEL / Binary-compatible variants: 8.X

-  Ubuntu: 18.04 +

-  openSUSE / SLES: 15.2 +

The main requirement for KVM hypervisors is the libvirt and Qemu
version. No matter what Linux distribution you are using, make sure the
following requirements are met:

-  libvirt: 1.2.0 or higher

-  Qemu/KVM: 1.5 or higher (2.5 or higher recommended)

The default bridge in CloudStack is the Linux native bridge
implementation (bridge module). CloudStack includes an option to work
with OpenVswitch, the requirements are listed below

-  libvirt: 1.2.0 or higher

-  openvswitch: 1.7.1 or higher

Not all versions of Qemu/KVM may support dynamic scaling of Instances. Some combinations may result CPU or memory related failures during Instance deployment.

In addition, the following hardware requirements apply:

-  Within a single cluster, the hosts must be of the same distribution
   version.

-  All hosts within a cluster must be homogenous. The CPUs must be of
   the same type, count, and feature flags.

-  Must support HVM (Intel-VT or AMD-V enabled)

-  64-bit x86 CPU (more cores results in better performance)

-  4 GB of memory

-  At least 1 NIC

-  When you deploy CloudStack, the hypervisor host must not have any Instances
   already running. These will be destroy by CloudStack.


KVM Installation Overview
~~~~~~~~~~~~~~~~~~~~~~~~~

If you want to use the Linux Kernel Virtual Machine (KVM) hypervisor to
run Guest Instances, install KVM on the host(s) in your cloud.
The material in this section doesn't duplicate KVM installation docs. It
provides the CloudStack-specific steps that are needed to prepare a KVM
host to work with CloudStack.

.. warning::
   Before continuing, make sure that you have applied the latest updates to
   your host.

.. warning::
   It is NOT recommended to run services on this host not controlled by
   CloudStack.

.. warning::
   Certain servers such as Dell provide the option to choose the Power Management Profile.
   The Active Power Controller enables Dell System DBPM (Demand Based Power Management)
   which can restrict the visibility of the maximum CPU clock speed availble to the OS,
   which in turn can lead to CloudStack fetching the incorrect CPU speed of the server.
   To ensure that CloudStack can always fetch the maximum cpu speed on the server, ensure
   that "OS Control" is set as the Power Management Profile.

The procedure for installing a KVM Hypervisor Host is:

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

.. warning::
   CloudStack |version| requires Java 17 JRE. Installing CloudStack agent will
   automatically install Java 17, but it's good to explicitly confirm that the Java 17
   is the selected/active one (in case you had a previous Java version already installed)
   with ``alternatives --config java``, after CloudStack agent is installed.

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
Ubuntu 20.04 (focal), Ubuntu 22.04 (jammy), Ubuntu 24.04 (noble).

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

To manage KVM Instances on the host CloudStack uses a Agent. This Agent
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


The host is now ready to be added to a cluster. This is covered in a
later section, see :ref:`adding-a-host`. It is
recommended that you continue to read the documentation before adding
the host!

If you're using a non-root user to add the KVM host, please add the user to
sudoers file:

.. parsed-literal::

   cloudstack ALL=NOPASSWD: /usr/bin/cloudstack-setup-agent
   Defaults:cloudstack !requiretty


Configure CPU model for KVM guest (Optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In additional,the CloudStack Agent allows host administrator to control
the guest CPU model which is exposed to KVM Instances. By default, the
CPU model of KVM Instance is likely QEMU Virtual CPU version x.x.x with
least CPU features exposed. There are a couple of reasons to specify the
CPU model:

-  To maximise performance of Instances by exposing new host CPU
   features to the KVM Instances;

-  To ensure a consistent default CPU across all machines,removing
   reliance of variable QEMU defaults;

For the most part it will be sufficient for the host administrator to
specify the guest CPU config in the per-host configuration file
(/etc/cloudstack/agent/agent.properties). This will be achieved by
introducing following configuration parameters:

.. parsed-literal::

   guest.cpu.mode=custom|host-model|host-passthrough
   guest.cpu.model=from /usr/share/libvirt/cpu_map.xml(only valid when guest.cpu.mode=custom)
   guest.cpu.features=vmx ept aes smx mmx ht (space separated list of cpu flags to apply)

There are three choices to fulfill the cpu model changes:

#. **custom:** you can explicitly specify one of the supported named
   model in /usr/share/libvirt/cpu\_map.xml

#. **host-model:** libvirt will identify the CPU model in
   /usr/share/libvirt/cpu\_map.xml which most closely matches the host,
   and then request additional CPU flags to complete the match. This
   should give close to maximum functionality/performance, which
   maintaining good reliability/compatibility if the guest is migrated
   to another host with slightly different host CPUs.

#. **host-passthrough:** libvirt will tell KVM to passthrough the host
   CPU with no modifications. The difference to host-model, instead of
   just matching feature flags, every last detail of the host CPU is
   matched. This gives absolutely best performance, and can be important
   to some apps which check low level CPU details, but it comes at a
   cost with respect to migration: the guest can only be migrated to an
   exactly matching host CPU.

Here are some examples:

-  custom

   .. parsed-literal::

      guest.cpu.mode=custom
      guest.cpu.model=SandyBridge

-  host-model

   .. parsed-literal::

      guest.cpu.mode=host-model

-  host-passthrough

   .. parsed-literal::

      guest.cpu.mode=host-passthrough
      guest.cpu.features=vmx

.. note::
   host-passthrough may lead to migration failure,if you have this problem,
   you should use host-model or custom. guest.cpu.features will force cpu features
   as a required policy so make sure to put only those features that are provided
   by the host CPU. As your kvm cluster needs to be made up of homogenous nodes anyway
   (see System Requirements), it might make most sense to use guest.cpu.mode=host-model
   or guest.cpu.mode=host-passthrough.

Install and Configure libvirt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack uses libvirt for managing Instances. Therefore it is
vital that libvirt is configured correctly. Libvirt is a dependency of
cloudstack-agent and should already be installed.

.. note::
   Please note that Cloudstack will automatically perform basic configuration of the agent and libvirt when the host is added. This is relevant if you are
   planning to automate the deployment and configuration of your KVM hosts.

#. To avoid potential security attack to Instances, We need to turn
   off libvirt to listen on unsecure TCP port. CloudStack will automatically
   set up cloud keystore and certificates when the host is added to cloudstack.
   We also need to turn off libvirts attempt
   to use Multicast DNS advertising. Both of these settings are in
   ``/etc/libvirt/libvirtd.conf``

   Set the following parameters:

   .. parsed-literal::

      listen_tls = 0

   .. parsed-literal::

      listen_tcp = 0

   .. parsed-literal::

      tls_port = "16514"

   .. parsed-literal::

      tcp_port = "16509"

   .. parsed-literal::

      auth_tcp = "none"

   .. parsed-literal::

      mdns_adv = 0

#. We have to change the parameters as well:

   On RHEL or CentOS or SUSE modify ``/etc/sysconfig/libvirtd``:

   Uncomment the following line:

   .. parsed-literal::

      #LIBVIRTD_ARGS="--listen"

   On RHEL 8 / CentOS 8 / SUSE run the following command :

   .. parsed-literal::

      systemctl mask libvirtd.socket libvirtd-ro.socket libvirtd-admin.socket libvirtd-tls.socket libvirtd-tcp.socket


   On Ubuntu 20.04 or older, modify ``/etc/default/libvirtd``

   Uncomment and change the following line

   .. parsed-literal::

      #libvirtd_opts=""

   so it looks like:

   .. parsed-literal::

      libvirtd_opts="-l"

   On Ubuntu 22.04 or newer version, modify ``/etc/default/libvirtd``:

   Uncomment the following line:

   .. parsed-literal::

      #LIBVIRTD_ARGS="--listen"

#. Restart libvirt

   In RHEL or CentOS or SUSE or Ubuntu:

   .. parsed-literal::

        $ systemctl restart libvirtd


Configure the Security Policies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack does various things which can be blocked by security
mechanisms like AppArmor and SELinux. These have to be disabled to
ensure the Agent has all the required permissions.

#. Configure SELinux (RHEL, CentOS, SUSE)

   #. Check to see whether SELinux is installed on your machine. If not,
      you can skip this section.

      In RHEL or CentOS, SELinux is installed and enabled by default.
      You can verify this with:

      .. parsed-literal::

         $ rpm -qa | grep selinux

   #. Set the SELINUX variable in ``/etc/selinux/config`` to
      "permissive". This ensures that the permissive setting will be
      maintained after a system reboot.

      In RHEL or CentOS:

      .. parsed-literal::

         $ vi /etc/selinux/config

      Change the following line

      .. parsed-literal::

         SELINUX=enforcing

      to this

      .. parsed-literal::

         SELINUX=permissive

   #. Then set SELinux to permissive starting immediately, without
      requiring a system reboot.

      .. parsed-literal::

         $ setenforce permissive

#. Configure Apparmor (Ubuntu)


   #. Check to see whether AppArmor is installed on your machine. If
      not, you can skip this section.

      In Ubuntu AppArmor is installed and enabled by default. You can
      verify this with:

      .. parsed-literal::

         $ dpkg --list 'apparmor'

   #. Disable the AppArmor profiles for libvirt

      .. parsed-literal::

         $ ln -s /etc/apparmor.d/usr.sbin.libvirtd /etc/apparmor.d/disable/

      .. parsed-literal::

         $ ln -s /etc/apparmor.d/usr.lib.libvirt.virt-aa-helper /etc/apparmor.d/disable/

      .. parsed-literal::

         $ apparmor_parser -R /etc/apparmor.d/usr.sbin.libvirtd

      .. parsed-literal::

         $ apparmor_parser -R /etc/apparmor.d/usr.lib.libvirt.virt-aa-helper


Configuring the Networking
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. warning::
   This is a very important section, please make sure you read this thoroughly.

.. note::
   This section details how to configure bridges using the native
   implementation in Linux. Please refer to the next section if you intend to
   use OpenVswitch

CloudStack uses the network bridges in conjunction with KVM to connect the Guest Instances to
each other and the outside world.  They also are used to connect the System VMs to your
infrastructure.

By default these bridges are called *cloudbr0* and *cloudbr1* etc, but this can be
changed to be more descriptive.

.. note::
   Ensure that the interfaces names to be used for configuring the bridges match one of the following patterns:
   **'eth*', 'bond*', 'team*', 'vlan*', 'em*', 'p*p*', 'ens*', 'eno*', 'enp*', 'enx*'**.

   Otherwise, the KVM agent will not be able to configure the bridges properly.

.. warning::
   It is essential that you keep the configuration consistent across all of your hypervisors.

There are many ways to configure your networking. Even within the scope of a given
network mode.  Below are a few simple examples.

.. note::
   Since Ubuntu 20.04 the standard for manging network connections is by
   using NetPlan YAML files. Please refer to the Ubuntu man pages for further
   information and set up network connections figuratively.

Network example for Basic Networks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the Basic networking, all of the guests in a given pod will be on the same VLAN/subnet.
It is common to use the native (untagged) VLAN for the private/management network, so in
this example we will have two VLANs, one (native) for your private/management network and one
for the guest network.

We assume that the hypervisor has one NIC (eth0) with one tagged VLAN trunked from the switch:

#. Native VLAN for Management Network (cloudbr0)
#. VLAN 200 for guest network of the Instances (cloudbr1)

In this the following example we give the Hypervisor the IP-Address 192.168.42.11/24
with the gateway 192.168.42.1

.. note::
   The Hypervisor and Management server don't have to be in the same subnet

Configuring the Network Bridges for Basic Networks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It depends on the distribution you are using how to configure these,
below you'll find examples for RHEL/CentOS, SUSE and Ubuntu.

.. note::
   The goal is to have two bridges called 'cloudbr0' and 'cloudbr1' after this
   section. This should be used as a guideline only. The exact configuration
   will depend on your network layout.

Configure RHEL or CentOS for Basic Networks
'''''''''''''''''''''''''''''''''''''''''''

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
   BRIDGE=cloudbr0

We now have to configure the VLAN interfaces:

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
   BRIDGE=cloudbr1

Now that we have the VLAN interfaces configured we can add the bridges on top
of them.

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-cloudbr0

Now we configure cloudbr0 and include the Management IP of the hypervisor.

.. note::
   The management IP of the hypervisor doesn't have to be in same subnet/VLAN as the
   management network, but its quite common.

.. parsed-literal::

   DEVICE=cloudbr0
   TYPE=Bridge
   ONBOOT=yes
   BOOTPROTO=none
   IPV6INIT=no
   IPV6_AUTOCONF=no
   DELAY=5
   IPADDR=192.168.42.11
   GATEWAY=192.168.42.1
   NETMASK=255.255.255.0
   STP=yes

We configure cloudbr1 as a plain bridge without an IP address

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

Configure SUSE for Basic Networks
'''''''''''''''''''''''''''''''''''''

The required packages were installed when libvirt was installed, we can
proceed to configuring the network.

First we configure eth0

.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-eth0

Make sure it looks similar to:

.. parsed-literal::

   NAME=eth0
   STARTMODE=auto
   BOOTPROTO=none

We now have to configure the VLAN interfaces:

.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-eth0.200

.. parsed-literal::

   NAME=eth0.200
   STARTMODE=auto
   BOOTPROTO=none
   VLAN_ID=200
   ETHERDEVICE=eth0

Now that we have the VLAN interfaces configured we can add the bridges on top
of them.

.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-cloudbr0

Now we configure cloudbr0 and include the Management IP of the hypervisor.

.. note::
   The management IP of the hypervisor doesn't have to be in same subnet/VLAN as the
   management network, but its quite common.

.. parsed-literal::

   NAME=cloudbr0
   STARTMODE=auto
   BOOTPROTO=static
   BRIDGE=yes
   BRIDGE_PORTS=eth0
   BRIDGE_STP=on
   BRIDGE_FORWARDDELAY=5
   IPADDR=192.168.42.11
   NETMASK=255.255.255.0

Add the gateway in ``/etc/sysconfig/network/routes``

.. parsed-literal::

   default 192.168.42.1 - cloudbr0


We configure cloudbr1 as a plain bridge without an IP address

.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-cloudbr1

.. parsed-literal::

   NAME=cloudbr1
   STARTMODE=auto
   BOOTPROTO=none
   BRIDGE=yes
   BRIDGE_PORTS=eth0.200
   BRIDGE_STP=on
   BRIDGE_FORWARDDELAY=5

With this configuration you should be able to restart the network,
although a reboot is recommended to see if everything works properly.

.. warning::
   Make sure you have an alternative way like IPMI or ILO to reach the machine
   in case you made a configuration error and the network stops functioning!


Configure Ubuntu for Basic Networks
'''''''''''''''''''''''''''''''''''

All the required packages were installed when you installed libvirt, so
we only have to configure the network.

.. parsed-literal::

   $ vi /etc/network/interfaces

Modify the interfaces file to look like this:

.. parsed-literal::

   auto lo
   iface lo inet loopback

   # The primary network interface
   auto eth0
   iface eth0 inet manual

   auto eth0.200
   iface eth0 inet manual

   # management network
   auto cloudbr0
   iface cloudbr0 inet static
       bridge_ports eth0
       bridge_fd 0
       bridge_stp off
       bridge_maxwait 1
       address 192.168.42.11
       netmask 255.255.255.240
       gateway 192.168.42.1
       dns-nameservers 8.8.8.8 8.8.4.4
       dns-domain lab.example.org

   # guest network
   auto cloudbr1
   iface cloudbr1 inet manual
       bridge_ports eth0.200
       bridge_fd 0
       bridge_stp off
       bridge_maxwait 1

With this configuration you should be able to restart the network,
although a reboot is recommended to see if everything works properly.

.. warning::
   Make sure you have an alternative way like IPMI or ILO to reach the machine
   in case you made a configuration error and the network stops functioning!



Network Example for Advanced Networks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the Advanced networking mode, it is most common to have (at least) two physical interfaces per hypervior-host.
We will use the interface eth0 linked to the bridge 'cloudbr0' using the untagged (native) VLAN for hypervisor management.
Additionally we configure the second interface for usage with the bridge 'cloudbr1' for public and guest traffic.
This time there are no VLANs applied by us - CloudStack will add the VLANs as required during actual use.

We again give the Hypervisor the IP-Address 192.168.42.11/24 with
the gateway 192.168.42.1

.. note::
   The Hypervisor and Management server don't have to be in the same subnet


Configuring the Network Bridges for Advanced Networks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It depends on the distribution you are using how to configure these,
below you'll find examples for RHEL/CentOS, SUSE and Ubuntu.

.. note::
   The goal is to have two bridges called 'cloudbr0' and 'cloudbr1' after this
   section. This should be used as a guideline only. The exact configuration
   will depend on your network layout.


Configure RHEL/CentOS for Advanced Networks
'''''''''''''''''''''''''''''''''''''''''''

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
   BRIDGE=cloudbr0

We now have to configure the second network-interface for use in guest VLANs:

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-eth1

.. parsed-literal::

   DEVICE=eth1
   HWADDR=00:04:xx:xx:xx:xx
   ONBOOT=yes
   HOTPLUG=no
   BOOTPROTO=none
   TYPE=Ethernet
   BRIDGE=cloudbr1

Now we have the interfaces configured and can add the bridges on top
of them.

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-cloudbr0

Now we configure cloudbr0 and include the Management IP of the hypervisor.

.. note::
   The management IP of the hypervisor doesn't have to be in same subnet/VLAN as the
   management network, but its quite common.

.. parsed-literal::

   DEVICE=cloudbr0
   TYPE=Bridge
   ONBOOT=yes
   BOOTPROTO=none
   IPV6INIT=no
   IPV6_AUTOCONF=no
   DELAY=5
   IPADDR=192.168.42.11
   GATEWAY=192.168.42.1
   NETMASK=255.255.255.0
   STP=yes

We configure 'cloudbr1' as a plain bridge without an IP address or dedicated VLAN configuration.

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

Configure SUSE for Advanced Networks
''''''''''''''''''''''''''''''''''''''''

The required packages were installed when libvirt was installed, we can
proceed to configuring the network.

First we configure eth0

.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-eth0

Make sure it looks similar to:

.. parsed-literal::

   NAME=eth0
   STARTMODE=auto
   BOOTPROTO=none

We now have to configure the VLAN interfaces:

.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-eth1

.. parsed-literal::

   NAME=eth1
   STARTMODE=auto
   BOOTPROTO=none

Now we have the VLAN interfaces configured we can add the bridges on top
of them.

.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-cloudbr0

Now we configure cloudbr0 and include the Management IP of the hypervisor.

.. note::
   The management IP of the hypervisor doesn't have to be in same subnet/VLAN as the
   management network, but its quite common.

.. parsed-literal::

   NAME=cloudbr0
   STARTMODE=auto
   BOOTPROTO=static
   BRIDGE=yes
   BRIDGE_PORTS=eth0
   BRIDGE_STP=on
   BRIDGE_FORWARDDELAY=5
   IPADDR=192.168.42.11
   NETMASK=255.255.255.0

Add the gateway in ``/etc/sysconfig/network/routes``

.. parsed-literal::

   default 192.168.42.1 - cloudbr0

We configure cloudbr1 as a plain bridge without an IP address

.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-cloudbr1

.. parsed-literal::

   NAME=cloudbr1
   STARTMODE=auto
   BOOTPROTO=none
   BRIDGE=yes
   BRIDGE_PORTS=eth1
   BRIDGE_STP=on
   BRIDGE_FORWARDDELAY=5

With this configuration you should be able to restart the network,
although a reboot is recommended to see if everything works properly.

.. warning::
   Make sure you have an alternative way like IPMI or ILO to reach the machine
   in case you made a configuration error and the network stops functioning!


Configure Ubuntu for Advanced Networks
''''''''''''''''''''''''''''''''''''''

All the required packages were installed when you installed libvirt, so
we only have to configure the network.

.. parsed-literal::

   $ vi /etc/network/interfaces

Modify the interfaces file to look like this:

.. parsed-literal::

   auto lo
   iface lo inet loopback

   # The primary network interface
   auto eth0
   iface eth0 inet manual

   # The second network interface
   auto eth1
   iface eth1 inet manual

   # management network
   auto cloudbr0
   iface cloudbr0 inet static
       bridge_ports eth0
       bridge_fd 5
       bridge_stp off
       bridge_maxwait 1
       address 192.168.42.11
       netmask 255.255.255.240
       gateway 192.168.42.1
       dns-nameservers 8.8.8.8 8.8.4.4
       dns-domain lab.example.org

   # guest network
   auto cloudbr1
   iface cloudbr1 inet manual
       bridge_ports eth1
       bridge_fd 5
       bridge_stp off
       bridge_maxwait 1

If you are using *netplan* with Ubuntu, below is a sample configuration.

.. parsed-literal::

   $vi /etc/netplan/01-KVM-config.yaml 

Modify the *YAML* file to look like this:

.. parsed-literal::

   ---
   network:
     version: 2
     ethernets:
       eth0: {}
       eth1: {}
     bridges:
       cloudbr0:
         addresses:
           - 192.168.42.11/24
         dhcp4: false
         routes:
           - to: default
             via: 192.168.42.1
         nameservers:
           addresses:
             - 8.8.8.8
             - 8.8.4.4
           search: []
         interfaces:
           - eth0
         parameters:
           stp: true
       cloudbr1:
         dhcp4: false
         interfaces:
           - eth1
         parameters:
           stp: true

To apply the above configuration:

.. parsed-literal::

   netplan apply

With this configuration you should be able to restart the network,
although a reboot is recommended to see if everything works properly.

.. warning::
   Make sure you have an alternative way like IPMI or ILO to reach the machine
   in case you made a configuration error and the network stops functioning!


Configure the network using OpenVswitch
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. warning::
   This is a very important section, please make sure you read this thoroughly.

In order to forward traffic to your Instances you will need at least two
bridges: *public* and *private*.

By default these bridges are called *cloudbr0* and *cloudbr1*, but you
do have to make sure they are available on each hypervisor.

The most important factor is that you keep the configuration consistent
on all your hypervisors.


Preparing
^^^^^^^^^

To make sure that the native bridge module will not interfere with
openvswitch the bridge module should be added to the denylist (likely named
'denylist') see the modprobe documentation for your distribution on
where to find the denylist. Make sure the module is not loaded either
by rebooting or executing rmmod bridge before executing next steps.

The network configurations below depend on the ifup-ovs and ifdown-ovs
scripts which are part of the openvswitch installation. They should be
installed in /etc/sysconfig/network-scripts/


OpenVswitch Network example
^^^^^^^^^^^^^^^^^^^^^^^^^^^

There are many ways to configure your network. In the Basic networking
mode you should have two VLANs, one for your private network and one
for the public network.

We assume that the hypervisor has one NIC (eth0) with three tagged
VLANs:

#. VLAN 100 for management of the hypervisor

#. VLAN 200 for public network of the Instances (cloudbr0)

#. VLAN 300 for private network of the instances (cloudbr1)

On VLAN 100 we give the Hypervisor the IP-Address 192.168.42.11/24 with
the gateway 192.168.42.1

.. note::
   The Hypervisor and Management server don't have to be in the same subnet


Configuring the network bridges for OpenVswitch
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It depends on the distribution you are using how to configure these,
below you'll find examples for RHEL/CentOS.

.. note::
   The goal is to have three bridges called 'mgmt0', 'cloudbr0' and 'cloudbr1'
   after this section. This should be used as a guideline only. The exact
   configuration will depend on your network layout.


Configure OpenVswitch
'''''''''''''''''''''

The network interfaces using OpenVswitch are created using the ovs-vsctl
command. This command will configure the interfaces and persist them to
the OpenVswitch database.

First we create a main bridge connected to the eth0 interface. Next we
create three fake bridges, each connected to a specific vlan tag.

.. parsed-literal::

   # ovs-vsctl add-br cloudbr
   # ovs-vsctl add-port cloudbr eth0
   # ovs-vsctl set port cloudbr trunks=100,200,300
   # ovs-vsctl add-br mgmt0 cloudbr 100
   # ovs-vsctl add-br cloudbr0 cloudbr 200
   # ovs-vsctl add-br cloudbr1 cloudbr 300


Configure OpenVswitch in RHEL or CentOS
'''''''''''''''''''''''''''''''''''''''

The required packages were installed when openvswitch and libvirt were
installed, we can proceed to configuring the network.

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

We have to configure the base bridge with the trunk.

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-cloudbr

.. parsed-literal::

   DEVICE=cloudbr
   ONBOOT=yes
   HOTPLUG=no
   BOOTPROTO=none
   DEVICETYPE=ovs
   TYPE=OVSBridge

We now have to configure the three VLAN bridges:

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-mgmt0

.. parsed-literal::

   DEVICE=mgmt0
   ONBOOT=yes
   HOTPLUG=no
   BOOTPROTO=static
   DEVICETYPE=ovs
   TYPE=OVSBridge
   IPADDR=192.168.42.11
   GATEWAY=192.168.42.1
   NETMASK=255.255.255.0

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-cloudbr0

.. parsed-literal::

   DEVICE=cloudbr0
   ONBOOT=yes
   HOTPLUG=no
   BOOTPROTO=none
   DEVICETYPE=ovs
   TYPE=OVSBridge

.. parsed-literal::

   $ vi /etc/sysconfig/network-scripts/ifcfg-cloudbr1

.. parsed-literal::

   DEVICE=cloudbr1
   ONBOOT=yes
   HOTPLUG=no
   BOOTPROTO=none
   TYPE=OVSBridge
   DEVICETYPE=ovs

With this configuration you should be able to restart the network,
although a reboot is recommended to see if everything works properly.

.. warning::
   Make sure you have an alternative way like IPMI or ILO to reach the machine
   in case you made a configuration error and the network stops functioning!


Configure OpenVswitch in SUSE
'''''''''''''''''''''''''''''''''

The required packages were installed when openvswitch and libvirt were
installed, we can proceed to configuring the network.

First we configure eth0

.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-eth0

Make sure it looks similar to:

.. parsed-literal::

   NAME=eth0
   STARTMODE=auto
   BOOTPROTO=none


We have to configure the base bridge with the trunk.

.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-cloudbr

.. parsed-literal::

   NAME=cloudbr
   STARTMODE=auto
   BOOTPROTO=none
   OVS_BRIDGE=yes

We now have to configure the three VLAN bridges:

.. parsed-literal::

   $ vi /etc/sysconfig/network/mgmt0

.. parsed-literal::

   NAME=mgmt0
   STARTMODE=auto
   BOOTPROTO=static
   OVS_BRIDGE=yes
   IPADDR=192.168.42.11
   NETMASK=255.255.255.0


Add the gateway in ``/etc/sysconfig/network/routes``

.. parsed-literal::

   default 192.168.42.1 - mgmt0


.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-cloudbr0

.. parsed-literal::

   NAME=cloudbr0
   STARTMODE=auto
   BOOTPROTO=none
   OVS_BRIDGE=yes


.. parsed-literal::

   $ vi /etc/sysconfig/network/ifcfg-cloudbr1

.. parsed-literal::

   NAME=cloudbr1
   STARTMODE=auto
   BOOTPROTO=none
   OVS_BRIDGE=yes

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

#. 16514 (libvirt)

#. 5900 - 6100 (VNC consoles)

#. 49152 - 49216 (libvirt live migration)

It depends on the firewall you are using how to open these ports. Below
you'll find examples how to open these ports in RHEL/CentOS and Ubuntu.


Open ports in RHEL / CentOS / SUSE
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

RHEL and CentOS use iptables for firewalling the system, you can open
extra ports by executing the following iptable commands:

.. parsed-literal::

   $ iptables -I INPUT -p tcp -m tcp --dport 22 -j ACCEPT

.. parsed-literal::

   $ iptables -I INPUT -p tcp -m tcp --dport 1798 -j ACCEPT

.. parsed-literal::

   $ iptables -I INPUT -p tcp -m tcp --dport 16514 -j ACCEPT

.. parsed-literal::

   $ iptables -I INPUT -p tcp -m tcp --dport 5900:6100 -j ACCEPT

.. parsed-literal::

   $ iptables -I INPUT -p tcp -m tcp --dport 49152:49216 -j ACCEPT

These iptable settings are not persistent accross reboots, we have to
save them first.

.. parsed-literal::

   $ iptables-save > /etc/sysconfig/iptables

.. warning::
   On RHEL 8 / CentOS 8 / SUSE, firewalld is the default firewall manager and controls iptables. It is
   recommended that it be disabled ``systemctl stop firewalld ; systemctl disable firewalld``

.. warning::
   On SUSE, iptables are not persisted on reboot, so it is recommended that an iptables and
   ip6tables service be created to ensure that they persist


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

   $ ufw allow proto tcp from any to any port 16514

.. parsed-literal::

   $ ufw allow proto tcp from any to any port 5900:6100

.. parsed-literal::

   $ ufw allow proto tcp from any to any port 49152:49216

.. note::
   By default UFW is not enabled on Ubuntu. Executing these commands with the
   firewall disabled does not enable the firewall.

   If you have an issue with ufw while using a bridged connection,
   add those two lines at the end of the /etc/ufw/before.rules just before COMMIT

.. parsed-literal::
   sudo vi /etc/ufw/before.rules

.. parsed-literal::
   -A FORWARD -d 192.168.42.11 -j ACCEPT
   -A FORWARD -s 192.168.42.11 -j ACCEPT


Additional Packages Required for Features
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Secondary Storage Bypass
^^^^^^^^^^^^^^^^^^^^^^^^

New in 4.11 is the ability to bypass storing a Template on secondary storage, and
instead directly downloading a 'Template' from an alternate remote location.
In order to facilitate this the **Aria2** (https://aria2.github.io/) package must be
installed on all of your KVM hosts.

As this package often is not available in standard distribution repos, you will need
to install the package from your preferred source.


Volume Snapshots
^^^^^^^^^^^^^^^^

CloudStack uses the qemu-img to perform Snapshots.  In CentOS >= 6.5, the qemu-img
supplied by RedHat/CentOS ceased to include a '-s' switch which performs Snapshots. The
'-s' switch has been restored in latest CentOS/RHEL 7.x versions.

In order to be able to perform Volume Snapshots on CentOS 6.x (greater than 6.4) you must
replace your version of qemu-img with one which has been patched to include the '-s'
switch.


Live Migration
^^^^^^^^^^^^^^

For Live Migration of the guests, it is better to configure the guest network bridge on
the same interface in the KVM hosts. In case, the guest network bridge is configured on
different interfaces in the KVM hosts, ensure the destination host doesn't have interface
with the interface name of guest network bridge in the source host.


UEFI legacy / secureboot
^^^^^^^^^^^^^^^^^^^^^^^^

For deploying instances using UEFI legacy / secureboot, there are some further tasks to
perform.

In case of KVM, UEFI enabled hypervisor hosts must have the ``ovmf`` or
``edk2-ovmf`` package installed.

You can find further informations regarding prerequisites at the CloudStack Wiki
(https://cwiki.apache.org/confluence/display/CLOUDSTACK/Enable+UEFI+booting+for+Instance)
as well as limitations for using UEFI in CloudStack.

The options to deploy instances using UEFI can be found in the "Advanced Mode" section
of the instance deployment wizard, where users can specify the boot type and
boot mode for the selected valid template or ISO.

Add the host to CloudStack
~~~~~~~~~~~~~~~~~~~~~~~~~~

The host is now ready to be added to a cluster. This is covered in a
later section, see :ref:`adding-a-host`. It is
recommended that you continue to read the documentation before adding
the host!
