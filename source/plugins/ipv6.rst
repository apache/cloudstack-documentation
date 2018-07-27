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


IPv6 Support in CloudStack
===========================

CloudStack supports Internet Protocol version 6 (IPv6), the recent
version of the Internet Protocol (IP) that defines routing the network
traffic. IPv6 uses a 128-bit address that exponentially expands the
current address space that is available to the users. IPv6 addresses
consist of eight groups of four hexadecimal digits separated by colons,
for example, 5001:0dt8:83a3:1012:1000:8s2e:0870:7454. CloudStack
supports IPv6 for public IPs in shared networks. With IPv6 support, VMs
in shared networks can obtain both IPv4 and IPv6 addresses from the DHCP
server. You can deploy VMs either in a IPv6 or IPv4 network, or in a
dual network environment. If IPv6 network is used, the VM generates a
link-local IPv6 address by itself, and receives a stateful IPv6 address
from the DHCPv6 server.

IPv6 is supported only on KVM and XenServer hypervisors. The IPv6
support is only an experimental feature.

Here's the sequence of events when IPv6 is used:

#. The administrator creates an IPv6 shared network in an advanced zone.

#. The user deploys a VM in an IPv6 shared network.

#. The user VM generates an IPv6 link local address by itself, and gets
   an IPv6 global or site local address through DHCPv6.


Prerequisites and Guidelines
----------------------------

Consider the following:

-  CIDR size must be 64 for IPv6 networks.

-  The DHCP client of the guest VMs should support generating DUID based
   on Link-layer Address (DUID- LL). DUID-LL derives from the MAC
   address of guest VMs, and therefore the user VM can be identified by
   using DUID. See `Dynamic Host Configuration Protocol for
   IPv6 <http://tools.ietf.org/html/rfc3315>`__\ for more information.

-  The gateway of the guest network generates Router Advisement and
   Response messages to Router Solicitation. The M (Managed Address
   Configuration) flag of Router Advisement should enable stateful IP
   address configuration. Set the M flag to where the end nodes receive
   their IPv6 addresses from the DHCPv6 server as opposed to the router
   or switch.

   .. note:: 
      The M flag is the 1-bit Managed Address Configuration flag for Router
      Advisement. When set, Dynamic Host Configuration Protocol (DHCPv6) is
      available for address configuration in addition to any IPs set by
      using stateless address auto-configuration.

-  Use the System VM template exclusively designed to support IPv6.
   Download the System VM template from
   `http://download.cloudstack.org/systemvm/ 
   <http://download.cloudstack.org/systemvm/>`__.

-  The concept of Default Network applies to IPv6 networks. However,
   unlike IPv4 CloudStack does not control the routing information of
   IPv6 in shared network; the choice of Default Network will not affect
   the routing in the user VM.

-  In a multiple shared network, the default route is set by the rack
   router, rather than the DHCP server, which is out of CloudStack
   control. Therefore, in order for the user VM to get only the default
   route from the default NIC, modify the configuration of the user VM,
   and set non-default NIC's ``accept_ra`` to 0 explicitly. The
   ``accept_ra`` parameter accepts Router Advertisements and
   auto-configure ``/proc/sys/net/ipv6/conf/interface`` with received
   data.


Limitations of IPv6 in CloudStack
---------------------------------

The following are not yet supported:

#. Security groups

#. Userdata and metadata

#. Passwords


Guest VM Configuration for DHCPv6
---------------------------------

For the guest VMs to get IPv6 address, run dhclient command manually on
each of the VMs. Use DUID-LL to set up dhclient.

.. note:: 
   The IPv6 address is lost when a VM is stopped and started. Therefore,
   use the same procedure to get an IPv6 address when a VM is stopped and
   started.

#. Set up dhclient by using DUID-LL.

   Perform the following for DHCP Client 4.2 and above:

   #. Run the following command on the selected VM to get the dhcpv6
      offer from VR:

      .. parsed-literal::

         dhclient -6 -D LL <dev>

   Perform the following for DHCP Client 4.1:

   #. Open the following to the dhclient configuration file:

      .. parsed-literal::

         vi /etc/dhcp/dhclient.conf

   #. Add the following to the dhclient configuration file:

      .. parsed-literal::

         send dhcp6.client-id = concat(00:03:00, hardware);

#. Get IPv6 address from DHCP server as part of the system or network
   restart.

   Based on the operating systems, perform the following:

   On CentOS 6.2:

   #. Open the Ethernet interface configuration file:

      .. parsed-literal::

         vi /etc/sysconfig/network-scripts/ifcfg-eth0

      The ``ifcfg-eth0`` file controls the first NIC in a system.

   #. Make the necessary configuration changes, as given below:

      .. parsed-literal::

         DEVICE=eth0
         HWADDR=06:A0:F0:00:00:38
         NM_CONTROLLED=no
         ONBOOT=yes
         BOOTPROTO=dhcp6
         TYPE=Ethernet
         USERCTL=no
         PEERDNS=yes
         IPV6INIT=yes
         DHCPV6C=yes

   #. Open the following:

      .. parsed-literal::

         vi /etc/sysconfig/network

   #. Make the necessary configuration changes, as given below:

      .. parsed-literal::

         NETWORKING=yes
         HOSTNAME=centos62mgmt.lab.vmops.com
         NETWORKING_IPV6=yes
         IPV6_AUTOCONF=no

   On Ubuntu 12.10

   #. Open the following:

      .. parsed-literal::

         etc/network/interfaces:

   #. Make the necessary configuration changes, as given below:

      .. parsed-literal::

         iface eth0 inet6 dhcp
         autoconf 0
         accept_ra 1
