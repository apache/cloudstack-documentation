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


The VXLAN Plugin
================

System Requirements for VXLAN
-----------------------------

In CloudStack 4.X.0, this plugin only supports the KVM hypervisor with the
standard linux bridge.

The following table lists the requirements for the hypervisor.

.. cssclass:: table-striped table-bordered table-hover

+----------------+-----------------------------------------------+----------------------------------------------------------------------------------------------------------------+
| Item           | Requirement                                   | Note                                                                                                           |
+================+===============================================+================================================================================================================+
| Hypervisor     | KVM                                           | OvsVifDriver is not supported by this plugin in CloudStack 4.X, use BridgeVifDriver (default).                    |
+----------------+-----------------------------------------------+----------------------------------------------------------------------------------------------------------------+
| Linux kernel   | version >= 3.7, VXLAN kernel module enabled   | It is recommended to use kernel >=3.9, since Linux kernel categorizes the VXLAN driver as experimental <3.9.   |
+----------------+-----------------------------------------------+----------------------------------------------------------------------------------------------------------------+
| iproute2       | matches kernel version                        |                                                                                                                |
+----------------+-----------------------------------------------+----------------------------------------------------------------------------------------------------------------+

Table: Hypervisor Requirement for VXLAN


Linux Distributions that meet the requirements
----------------------------------------------

The following table lists distributions which meet requirements.

.. cssclass:: table-striped table-bordered table-hover

+----------------+-------------------+-------------------------------------------+----------------------------------------------------------------+
| Distribution   | Release Version   | Kernel Version (Date confirmed)           | Note                                                           |
+================+===================+===========================================+================================================================+
| Ubuntu         | 13.04             | 3.8.0 (2013/07/23)                        |                                                                |
+----------------+-------------------+-------------------------------------------+----------------------------------------------------------------+
| Fedora         | >= 17             | 3.9.10 (2013/07/23)                       | Latest kernel packages are available in "update" repository.   |
+----------------+-------------------+-------------------------------------------+----------------------------------------------------------------+
| CentOS         | >= 6.5            | 2.6.32-431.3.1.el6.x86\_64 (2014/01/21)   |                                                                |
+----------------+-------------------+-------------------------------------------+----------------------------------------------------------------+

Table: List of Linux distributions which meet the hypervisor
requirements


Check the capability of your system
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To check the capability of your system, execute the following commands.

::

   $ sudo modprobe vxlan && echo $?
   # Confirm the output is "0".
   # If it's non-0 value or error message, your kernel doesn't have VXLAN kernel module.

   $ ip link add type vxlan help
   # Confirm the output is usage of the command and that it's for VXLAN.
   # If it's not, your iproute2 utility doesn't support VXLAN.


Important note on MTU size
~~~~~~~~~~~~~~~~~~~~~~~~~~

When new VXLAN interfaces are created, kernel will obtain current MTU size of the physical interface (ethX or the bridge)
and then create VXLAN interface/bridge that are exactly 50 bytes smaller than the MTU on physical interface/bridge.
This means that in order to support default MTU size of 1500 bytes inside Instance, your VXLAN interface/bridge must also
have MTU of 1500 bytes, meaning that your physical interface/bridge must have MTU of at least 1550 bytes.
In order to configure "jumbo frames" you can i.e. make physical interface/bridge with 9000 bytes MTU, then all the VXLAN
interfaces will be created with MTU of 8950 bytes, and then MTU size inside Instance can be set to 8950 bytes.

Important note on max number of multicast groups (and thus VXLAN interfaces)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Default value of "net.ipv4.igmp_max_memberships" (cat /proc/sys/net/ipv4/igmp_max_memberships) is "20", which means that host can be joined to max 20 multicast groups (attach max 20 multicast IPs on the host).
Since all VXLAN (VTEP) interfaces provisioned on host are multicast-based (belong to certain multicast group, and thus has it's own multicast IP that is used as VTEP), this means that you can not provision more than 20 (working) VXLAN interfaces per host.
On Linux kernel 3.x you actually can provision more than 20, but ARP request will silently fail and cause client's networking problems
On Linux kernel 4.x you can NOT provision (start) more than 20 VXLAN interfaces and error message "No buffer space available" can be observed in Cloudstack Agent logs after provisioning required bridges and VXLAN interfaces.
Increase needed parameter to sane value (i.e. 100 or 200) as required.
If you need to operate more than 20 Instances from different client's Network, this change above is required.

Advanced: Build kernel and iproute2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Even if your system doesn't support VXLAN, you can compile the kernel
and iproute2 by yourself. The following procedure is an example for
CentOS 6.4.


Build kernel
^^^^^^^^^^^^

::

   $ sudo yum groupinstall "Development Tools"
   $ sudo yum install ncurses-devel hmaccalc zlib-devel binutils-devel elfutils-libelf-devel bc

   $ KERNEL_VERSION=3.10.4
   # Declare the kernel version you want to build.

   $ wget https://www.kernel.org/pub/linux/kernel/v3.x/linux-${KERNEL_VERSION}.tar.xz
   $ tar xvf linux-${KERNEL_VERSION}.tar.xz
   $ cd linux-${KERNEL_VERSION}
   $ cp /boot/config-`uname -r` .config
   $ make oldconfig
   # You may keep hitting enter and choose the default.

   $ make menuconfig
   # Dig into "Device Drivers" -> "Network device support",
   # then select "Virtual eXtensible Local Area Network (VXLAN)" and hit space.
   # Make sure it indicates "<M>" (build as module), then Save and Exit.

   # You may also want to check "IPv4 NAT" and its child nodes in "IP: Netfilter Configuration"
   # and "IPv6 NAT" and its child nodes in "IPv6: Netfilter Configuration".
   # In 3.10.4, you can find the options in
   # "Networking support" -> "Networking options"
   #   -> "Network packet filtering framework (Netfilter)".

   $ make # -j N
   # You may use -j N option to make the build process parallel and faster,
   # generally N = 1 + (cores your machine have).

   $ sudo make modules_install
   $ sudo make install
   # You would get an error like "ERROR: modinfo: could not find module XXXX" here.
   # This happens mainly due to config structure changes between kernel versions.
   # You can ignore this error, until you find you need the kernel module.
   # If you feel uneasy, you can go back to make menuconfig,
   # find module XXXX by using '/' key, enable the module, build and install the kernel again.

   $ sudo vi /etc/grub.conf
   # Make sure the new kernel isn't set as the default and the timeout is long enough,
   # so you can select the new kernel during boot process.
   # It's not a good idea to set the new kernel as the default until you confirm the kernel works fine.

   $ sudo reboot
   # Select the new kernel during the boot process.


Build iproute2
^^^^^^^^^^^^^^

::

   $ sudo yum install db4-devel

   $ git clone git://git.kernel.org/pub/scm/linux/kernel/git/shemminger/iproute2.git
   $ cd iproute2
   $ git tag
   # Find the version that matches the kernel.
   # If you built kernel 3.10.4 as above, it would be v3.10.0.

   $ git checkout v3.10.0
   $ ./configure
   $ make # -j N
   $ sudo make install


.. note:: Please use rebuild kernel and tools at your own risk.


Configure CloudStack to use VXLAN Plugin
-------------------------------------

Configure hypervisor
~~~~~~~~~~~~~~~~~~~~

Configure hypervisor: KVM
^^^^^^^^^^^^^^^^^^^^^^^^^

In addition to "KVM Hypervisor Host Installation" in "CloudStack
Installation Guide", you have to configure the following item on the
host.


Create bridge interface with IPv4 address
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This plugin requires an IPv4 address on the KVM host to terminate and
originate VXLAN traffic. The address should be assinged to a physical
interface or a bridge interface bound to a physical interface. Both a
private address or a public address are fine for the purpose. It is not
required to be in the same subnet for all hypervisors in a zone, but
they should be able to reach each other via IP multicast with UDP/8472
port. A name of a physical interface or a name of a bridge interface
bound to a physical interface can be used as a traffic label. Physical
interface name fits for almost all cases, but if physical interface name
differs per host, you may use a bridge to set a same name. If you would
like to use a bridge name as a traffic label, you may create a bridge in
this way.

Let ``cloudbr1`` be the bridge interface for the Instances' private
Network.


Configure in RHEL or CentOS
'''''''''''''''''''''''''''

When you configured the ``cloudbr1`` interface as below,

::

   $ sudo vi /etc/sysconfig/network-scripts/ifcfg-cloudbr1

::

   DEVICE=cloudbr1
   TYPE=Bridge
   ONBOOT=yes
   BOOTPROTO=none
   IPV6INIT=no
   IPV6_AUTOCONF=no
   DELAY=5
   STP=yes

you would change the configuration similar to below.

::

   DEVICE=cloudbr1
   TYPE=Bridge
   ONBOOT=yes
   BOOTPROTO=static
   IPADDR=192.0.2.X
   NETMASK=255.255.255.0
   IPV6INIT=no
   IPV6_AUTOCONF=no
   DELAY=5
   STP=yes


Configure in Ubuntu
'''''''''''''''''''

When you configured ``cloudbr1`` as below,

::

   $ sudo vi /etc/network/interfaces

::

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

you would change the configuration similar to below.

::

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
   iface cloudbr1 inet static
       addres 192.0.2.X
       netmask 255.255.255.0
       bridge_ports eth0.300
       bridge_fd 5
       bridge_stp off
       bridge_maxwait 1


Configure iptables to pass XVLAN packets
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Since VXLAN uses UDP packet to forward encapsulated the L2 frames,
UDP/8472 port must be opened.


Configure in RHEL or CentOS
'''''''''''''''''''''''''''

RHEL and CentOS use iptables for firewalling the system, you can open
extra ports by executing the following iptable commands:

::

   $ sudo iptables -I INPUT -p udp -m udp --dport 8472 -j ACCEPT


These iptable settings are not persistent accross reboots, we have to
save them first.

::

   $ sudo iptables-save > /etc/sysconfig/iptables


With this configuration you should be able to restart the Network,
although a reboot is recommended to see if everything works properly.

::

   $ sudo service network restart
   $ sudo reboot


.. warning::
   Make sure you have an alternative way like IPMI or ILO to reach the machine
   in case you made a configuration error and the Network stops functioning!


Configure in Ubuntu
'''''''''''''''''''

The default firewall under Ubuntu is UFW (Uncomplicated FireWall), which
is a Python wrapper around iptables.

To open the required ports, execute the following commands:

::

   $ sudo ufw allow proto udp from any to any port 8472

.. note::
   By default UFW is not enabled on Ubuntu. Executing these commands with the
   firewall disabled does not enable the firewall.

With this configuration you should be able to restart the Network,
although a reboot is recommended to see if everything works properly.

::

   $ sudo service networking restart
   $ sudo reboot

.. warning::
   Make sure you have an alternative way like IPMI or ILO to reach the machine
   in case you made a configuration error and the Network stops functioning!


Setup zone using VXLAN
~~~~~~~~~~~~~~~~~~~~~~

In almost all parts of zone setup, you can just follow the advanced zone
setup instruction in "CloudStack Installation Guide" to use this plugin. It
is not required to add a Network element nor to reconfigure the Network
offering. The only thing you have to do is configure the physical
Network to use VXLAN as the isolation method for Guest Network.


Configure the physical Network
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. figure:: /_static/images/vxlan-physicalnetwork.png

CloudStack needs to have one physical Network for Guest Traffic with the
isolation method set to "VXLAN".

.. figure:: /_static/images/vxlan-trafficlabel.png

Guest Network traffic label should be the name of the physical interface
or the name of the bridge interface and the bridge interface and they
should have an IPv4 address. See ? for details.


Configure the guest traffic
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. figure:: /_static/images/vxlan-vniconfig.png

Specify a range of VNIs you would like to use for carrying guest Network
traffic.

.. warning::
   VNI must be unique per zone and no duplicate VNIs can exist in the zone.
   Exercise care when designing your VNI allocation policy.
