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


Dynamic and Static Routing
-----------------------------

For VMs on Isolated networks, the IP of VMs are not publicly accessible.
To access the VMs from the Internet, Users need to create Load balanceing rules,
Port Forwarding rules, enable Static NAT, or enable VPN.

The IPv6 static routing feature has been introduced in Apache CloudStack 4.17.0.0, so that
users are able to access the IPv6 address of guest VMs on Isolated networks from the Internet or public network.
For more information, see `“IPv6 support for isolated networks and VPC Network Tiers” <../plugins/ipv6.html#isolated-network-and-vpc-network-tier>`_.

From Apache CloudStack 4.20.0.0, users are able to create isolated networks and VPCs with ROUTED mode.

- Manage IPv4 subnets for Zones (ROOT admin/operator only)
- Create Networks with Static Routing for IPv4
- Manage IPv4 Routing Firewall for Networks
- Manage AS number and BPG peers for Dynamic Routing (ROOT admin only)
- Create Networks with Dynamic Routing for IPv4 and IPv6


About Network Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Network mode indicates the mode with which the isolated network or VPC will operate.
There are two valid options

- NATTED. This is the default network mode of isolated networks. The VR of isolated networks and VPCs provides Source NAT services, as well as Static NAT, Load Balancer, Port Forwarding, Vpn if the network offering supports.
- ROUTED. For isolated networks in ROUTED mode, the VR no longer supports Source NAT, Static NAT, Load Balancer, Port Forwarding and Vpn. The supported services are Dns, Dhcp, Userdata, Firewall (for isolated networks) and Network ACL (for vpc and vpc networks).


About Routing mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Routing mode indicates how routing will operate with the isolated networks with ROUTED network mode.
There are two valid options

- Static. The operators need to add the static routes to the isolated networks or VPCs in the upstream router manually.
- Dynamic. The AS number will be automatically allocated, and BGP peer sessions will be set up automatically in the VR of the isolated networks or VPCs. The operators need to add the AS number ranges and BGP peers for each zone before creating network with Dynamic routing mode.


Manage IPv4 Subnets for Zone
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Like IPv6 prefixes, operators need to configure the IPv4 subnets for zone, which will be eventually used by guest networks.

Supported CloudStack API for operators to manage the IPv4 subnets for zone are:

- **createIpv4SubnetForZone** : create an IPv4 subnet for zone
- **dedicateIpv4SubnetForZone** : dedicate an IPv4 subnet for zone to a domain or an account
- **deleteIpv4SubnetForZone** : delete an IPv4 subnet for zone
- **listIpv4SubnetsForZone** : list IPv4 subnets for zone
- **releaseIpv4SubnetForZone** : release a dedicated IPv4 subnet for zone from a domain or an account
- **updateIpv4SubnetForZone** : update an IPv4 subnet for zone

Operators (root admins) can manage the IPv4 subnets for zone by navigating to Infrastructure -> Zones -> IPv4 Subnets
|manage-ipv4-subnets-for-zone.png|


Manage IPv4 Subnets for Guest Networks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Unlike IPv6 (each isolated network with IPv6 support gets a /64 IPv6 network), operators need to manage IPv4 subnets for guest networks.
An IPv4 subnet for guest networks is created from its parent which is a IPv4 subnet for zone.

.. cssclass:: table-striped table-bordered table-hover

======================================= ========================
Configuration                            Description
======================================= ========================
routed.ipv4.network.cidr.auto.allocation.enabled    whether the auto-allocation of network CIDR for routed network is enabled or not. True by default.
routed.ipv4.network.max.cidr.size       The maximum value of the cidr size for isolated networks in ROUTED mode	
routed.ipv4.network.min.cidr.size       The minimum value of the cidr size for isolated networks in ROUTED mode	
routed.ipv4.vpc.max.cidr.size           The maximum value of the cidr size for VPC in ROUTED mode	
routed.ipv4.vpc.min.cidr.size           The minimum value of the cidr size for VPC in ROUTED mode	
======================================= ========================

Supported CloudStack API for operators to manage the IPv4 subnets for guest networks are:

- **createIpv4SubnetForGuestNetwork** : create an IPv4 subnet for guest networks
- **deleteIpv4SubnetForGuestNetwork** : delete an IPv4 subnet for guest networks
- **listIpv4SubnetsForGuestNetwork** : list IPv4 subnets for guest networks
 
Operators (root admins) can manage the IPv4 subnet by navigating to Network -> IPv4 Subnets
|manage-ipv4-subnets-for-networks.png|


Create Network and VPC Offering with ROUTED mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create network offering with ROUTED mode, see `“Creating a New Network Offering” <networking.html#creating-a-new-network-offering>`_.

|routed-add-network-offering.png|

To create VPC offering with ROUTED mode, see below

|routed-add-vpc-offering.png|


Create Network with Static Routing for IPv4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



Create Network with Static Routing for IPv6
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The IPv6 static routing has been introduced in Apache CloudStack 4.17.0.0.
For more information, see `“IPv6 support for isolated networks and VPC Network Tiers” <../plugins/ipv6.html#isolated-network-and-vpc-network-tier>`_.

Manage IPv4 Routing Firewall
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO

Manage AS number for Dynamic Routing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO

Manage BPG peers for Dynamic Routing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO

Create Network with Dynamic Routing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO


.. |manage-ipv4-subnets-for-zone.png| image:: /_static/images/manage-ipv4-subnets-for-zone.png
   :alt: Manage IPv4 subnets for zoone

.. |manage-ipv4-subnets-for-networks.png| image:: /_static/images/manage-ipv4-subnets-for-networks.png
   :alt: Manage IPv4 subnets for guest networks

.. |routed-add-network-offering.png| image:: /_static/images/routed-add-network-offering.png
   :alt: Add network offering with ROUTED mode

.. |routed-add-vpc-offering.png| image:: /_static/images/routed-add-vpc-offering.png
   :alt: Add vpc offering with ROUTED mode

