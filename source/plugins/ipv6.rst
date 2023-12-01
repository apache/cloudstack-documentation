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
supports IPv6 for shared and isolated networks. It also supports IPv6 for VPC Network Tiers.

Shared network
--------------
With IPv6 support, Instances in shared networks can obtain both IPv4 and IPv6 addresses from the DHCP
server. You can deploy Instances either in a IPv6 or IPv4 network, or in a
dual network environment. If IPv6 network is used, the Instance generates a
link-local IPv6 address by itself, and receives a stateful IPv6 address
from the DHCPv6 server.

IPv6 is supported only on KVM and XenServer hypervisors. The IPv6
support is only an experimental feature.

Here's the sequence of events when IPv6 is used:

#. The administrator creates an IPv6 shared network in an advanced zone.

#. The user deploys an Instance in an IPv6 shared network.

#. The user Instance generates an IPv6 link local address by itself, and gets
   an IPv6 global or site local address through DHCPv6.


Prerequisites and Guidelines
############################

Consider the following:

-  CIDR size must be 64 for IPv6 networks.

-  The DHCP client of the Guest Instances should support generating DUID based
   on Link-layer Address (DUID- LL). DUID-LL derives from the MAC
   address of Guest Instances, and therefore the user Instance can be identified by
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

-  Use the System VM Template exclusively designed to support IPv6.
   Download the System VM Template from
   `http://download.cloudstack.org/systemvm/ 
   <http://download.cloudstack.org/systemvm/>`__.

-  The concept of Default Network applies to IPv6 networks. However,
   unlike IPv4 CloudStack does not control the routing information of
   IPv6 in shared network; the choice of Default Network will not affect
   the routing in the user Instance.

-  A shared network cannot be IPv6 only. Therefore, it is necessary to configure the IPv4 address range for the shared network with IPv6 addresses. The IPv4 range can be of a public or internal IPv4 network.

-  In a multiple shared network, the default route is set by the rack
   router, rather than the DHCP server, which is out of CloudStack
   control. Therefore, in order for the user Instance to get only the default
   route from the default NIC, modify the configuration of the user Instance,
   and set non-default NIC's ``accept_ra`` to 0 explicitly. The
   ``accept_ra`` parameter accepts Router Advertisements and
   auto-configure ``/proc/sys/net/ipv6/conf/interface`` with received
   data.


Limitations
###########

The following are not yet supported:

#. Security groups

#. Userdata and metadata

#. Passwords


Guest Instance Configuration for DHCPv6
#######################################

For the Guest Instances to get IPv6 address, run dhclient command manually on
each of the Instances. Use DUID-LL to set up dhclient.

.. note:: 
   The IPv6 address is lost when an Instance is stopped and started. Therefore,
   use the same procedure to get an IPv6 address when an Instance is stopped and
   started.

#. Set up dhclient by using DUID-LL.

   Perform the following for DHCP Client 4.2 and above:

   #. Run the following command on the selected Instance to get the dhcpv6
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


Isolated network and VPC Network Tier
-------------------------------------

.. note::
   - The IPv6 support for isolated networks and VPC Network Tiers is available from version 4.17.0.

   - The IPv6 isolated networks and VPC Network Tiers only supports **Static routing**, i.e, the administrator will need to add upstream routes for routing to work inside the networks.

   - IPv6 only isolated networks and VPC Network Tiers are not supported currently. Public network for IPv6 supported isolated networks and VPC Network Tiers must be on the same VLAN for both IPv4 and IPv6.

Guest Instances in an isolated network or VPC Network Tier can obtain both IPv4 and IPv6 IP addresses by using a supported network offering and appropriate configurations for IPv6 support by the administrator.
Both VR for such networks and the Guest Instances using these networks obtain a SLAAC based IPv6 address. While VR is assigned an IPv6 address from the public IPv6 range, Guest Instances get their IPv6 addresses from the IPv6 subnet assigned to the network.

Here's the sequence of events when IPv6 is used:

#. The administrator sets global configuration - ``ipv6.offering.enabled`` to **true**.

#. The administrator adds a public IPv6 range in an advanced zone.

#. The administrator adds an IPv6 prefix for guest traffic type for the zone.

#. The administrator creates a network or VPC offering with IPv4 + IPv6 (Dual stack) support.

#. The user deploys an isolated network with the IPv6 supported network offering. For VPC, user creates a VPC with IPv6 supported VPC offering and then deploys a Network Tier with IPv6 supported network offering.

#. CloudStack assigns a SLAAC based public IPv6 address to the network from the public IPv6 range of the zone. It also assigns an IPv6 subnet to the network from the guest IPv6 prefix for the zone. See `SLAAC <https://datatracker.ietf.org/doc/html/rfc4862>`__\ for more information.

#. The user deploys a Guest Instance in the network. The Instance is assigned a SLAAC based IPv6 address from the guest IPv6 subnet of the network.


Prerequisites and Guidelines
############################

Consider the following:

-  CIDR size for the public IPv6 range for a zone must be 64.

-  CIDR size for the guest IPv6 prefix for the zone must be lesser than 64. Each guest network is assigned a subnet from this prefix with CIDR size 64 therefore only as many IPv6 supporting guest networks can be deployed from the guest prefix as the number of subnets with CIDR size 64.

-  Currently, a guest network cannot be IPv6 only and it can only be either IPv4 only or Dual Stack (both IPv4 + IPv6).

-  Once a public IPv6 address and guest subnet are assigned to the network or the network is successfully, the operator must update routing in the upstream router. For this, CloudStack returns the gateway and subnet for the network with listNetworks API response.


Adding a Public IPv6 Range
##########################

The administrator can use both UI and API to add a public IPv6 range. UI is the preferable option.
Option to add a new public IPv6 range in the UI can be found in Infrastructure > Zones > Zone details > Physical Network tab > Physical network details > Traffic Types tab > Public > *Add IP range*.
In the Add IP range form, IPv6 can be selected as the IP Range Type. IPv6 Gateway and CIDR must be provided and optionally a VLAN/VNI can be provided.

Alternatively, ``createVlanIpRange`` API can be used to add a new public IPv6 range.

|add-public-ipv6-range-form.png|



   .. note::
      - The public IPv6 address range or CIDR must be added with same VLAN as that of public IPv4 address range.

      - As SLAAC based public IPv6 addresses will be assigned to the networks therefore public IPv6 range must be added without specifying start and end IP addresses.


Adding Guest IPv6 Prefix
########################

Again, both UI and API to add a guest IPv6 prefix. UI is the preferable option.
Option to add a new public Ipv6 range in the UI can be found in Infrastructure > Zones > Zone details > Physical Network tab > Physical network details > Traffic Types tab > Guest > *Add IPv6 prefix*.
In the Add IPv6 prefix form, an IPv6 prefix with CIDR size lesser than 64 must be provided.

Alternatively, ``createGuestNetworkIpv6Prefix`` API can be used to add a new guest IPv6 prefix.

|add-guest-ipv6-prefix-form.png|


Adding Network or VPC Offering with IPv6 Support
################################################

To create an IPv6 suported network or VPC offering, global configuration - ``ipv6.offering.enabled`` must be set to **true**.

With 4.17.0, a new paramter - ``internetprotocol`` has been added to:
 - the ``createNetworkOffering`` API which can be used to create a network offering with IPv6 support by using the value dualstack.
 - the ``createVPCOffering`` API which can be used to create a VPC offering with IPv6 support by using the value dualstack.
Corresponding option has also been provided in the UI form creating network/VPC offering:

|add-ipv6-network-offering-form.png|

|add-ipv6-vpc-offering-form.png|


Adding Upstream Route
#####################

Currently, CloudStack supports IPv6 isolated networks and VPC Network Tiers only with **static** routes and therefore the administrator needs to add upstream IPv6 routes once a network is successfully deployed.
To facilitate the automation, *CloudStack Event Notification* can be used. CloudStack will generate appropriate events on network creation or deletion and while assigning or releasing a public IPv6 address for a network. Based on the events the corresponding network can be queried for the IPv6 routes that it needs configured in upstream network.
Upstream IPv6 routes required by an IPv6 supported isolated network or VPC Network Tier are also shown in the UI in the network details.

|network-details-upstream-ipv6-routes.png|


IPv6 Firewall
#############

For using and managing firewall rules with an IPv6 supported isolated network, CloudStack provides following APIs:

-  ``listIpv6FirewallRules`` - To list existing IPv6 firewall rules for a network.
-  ``createIpv6FirewallRule`` - To create a new IPv6 firewall rules for a network.
-  ``updateIpv6FirewallRule`` - To update an exisitng IPv6 firewall rules for a network.
-  ``deleteIpv6FirewallRule`` - To delete an exisitng IPv6 firewall rules for a network.

These operations are also available using UI in the network details view of an IPv6 supported network.

|network-details-ipv6-firewall.png|


IPv6 ACL
########

IPv6 ACL rules for an IPv6 supported VPC Network Tier can be managed using Network ACL lists for the VPC. IPv6 CIDRs can be specified while adding or updating an ACL rule.

|add-ipv6-acl-rule-form.png|
|ipv6-acl-list.png|


.. |add-public-ipv6-range-form.png| image:: /_static/images/add-public-ipv6-range-form.png
   :alt: Add Public IPv6 Range form.
.. |add-guest-ipv6-prefix-form.png| image:: /_static/images/add-guest-ipv6-prefix-form.png
   :alt: Add Guest IPv6 Prefix form.
.. |add-ipv6-network-offering-form.png| image:: /_static/images/add-ipv6-network-offering-form.png
   :alt: Add IPv6 supported Network Offering form.
.. |add-ipv6-vpc-offering-form.png| image:: /_static/images/add-ipv6-vpc-offering-form.png
   :alt: Add IPv6 supported VPC Offering form.
.. |network-details-upstream-ipv6-routes.png| image:: /_static/images/network-details-upstream-ipv6-routes.png
   :alt: Upstream IPv6 routes in network details.
.. |network-details-ipv6-firewall.png| image:: /_static/images/network-details-ipv6-firewall.png
   :alt: IPv6 Firewall management in network details.
.. |add-ipv6-acl-rule-form.png| image:: /_static/images/add-ipv6-acl-rule-form.png
   :alt: Add IPv6 ACL rule.
.. |ipv6-acl-list.png| image:: /_static/images/ipv6-acl-list.png
   :alt: IPv6 ACL rule in Network ACL list.
