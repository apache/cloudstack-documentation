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
To access the VMs from the Internet, users need to create Load balancing rules,
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
- ROUTED. For isolated networks in ROUTED mode, the VR no longer supports Source NAT, Static NAT, Load Balancer, Port Forwarding and Vpn. The supported services are Dns, Dhcp, User data, Firewall (for isolated networks) and Network ACL (for vpc and vpc networks).


About Routing mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Routing mode indicates how routing will operate with the isolated networks with ROUTED network mode.
There are two valid options

- Static. The operators need to add the static routes to the isolated networks or VPCs in the upstream router manually.
- Dynamic. The AS number will be automatically allocated, and BGP peer sessions will be set up automatically in the VR of the isolated networks or VPCs. The operators need to add the AS number ranges and BGP peers for each zone before creating network with Dynamic routing mode.


Manage IPv4 Subnets for Zone
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Like IPv6 prefixes, operators need to configure the IPv4 subnets for zone, which will be eventually used by guest networks.

Supported CloudStack APIs for operators to manage the IPv4 subnets for zone are:

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

There are some global settings which can be set for each account. See below

.. cssclass:: table-striped table-bordered table-hover

================================================= ========================
Configuration                                       Description
================================================= ========================
routed.ipv4.network.cidr.auto.allocation.enabled    Whether the auto-allocation of network CIDR for routed network is enabled or not. True by default.
routed.ipv4.network.max.cidr.size                   The maximum value of the cidr size for isolated networks in ROUTED mode	
routed.ipv4.network.min.cidr.size                   The minimum value of the cidr size for isolated networks in ROUTED mode	
routed.ipv4.vpc.max.cidr.size                       The maximum value of the cidr size for VPC in ROUTED mode	
routed.ipv4.vpc.min.cidr.size                       The minimum value of the cidr size for VPC in ROUTED mode	
================================================= ========================

Supported CloudStack APIs for operators to manage the IPv4 subnets for guest networks are:

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

To create a network with static routing, users need to navigate to Network -> Add Network -> Isolated, and

- Choose a network offering with ROUTED mode and routing mode is Static
- Specify the gateway and netmask (available for ROOT admin only)
- OR, specify the cidrsize (available for all users)

|routed-add-network-cidrsize.png|

If cidrsize is specified, CloudStack will allocate an IPv4 subnet for guest network to the net network

- Check if there is an IPv4 subnet with same CIDR size available,
- If not, and setting "routed.ipv4.network.cidr.auto.allocation.enabled" is true for account, allocate an IPv4 subnet for the new network, from the IPv4 subnet for zone which the account can access.
- Otherwise, the network creation fails.

When the network is implemented, the Ipv4 routes are displayed in the network details page.

|routed-ipv4-routes.png|

.. note::
   For networks or VPCs with ipv4 static routing, the administrator needs to add upstream IPv4 routes once a network or VPC is successfully deployed.


Create Network with Static Routing for IPv6
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The IPv6 static routing has been introduced in Apache CloudStack 4.17.0.0.
For more information, see `“IPv6 support for isolated networks and VPC Network Tiers” <../plugins/ipv6.html#isolated-network-and-vpc-network-tier>`_.

Users can create network with static routing for both IPv4 and IPv6, if the network offering supports DualStack.


Manage IPv4 Routing Firewall
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Users can manage the IPv4 Routing firewalls by navigating to Network -> Guest Networks -> choose a network -> IPv4 Routing Firewall

|routed-ipv4-routing-firewall.png|

Supported CloudStack APIs for operators to manage the IPv4 Routing firewall rules are:

- **createRoutingFirewallRule** : create an IPv4 routing firewall rule
- **updateRoutingFirewallRule** : update an IPv4 routing firewall rule
- **deleteRoutingFirewallRule** : delete an IPv4 routing firewall rule
- **listRoutingFirewallRules** : list IPv4 routing firewall rules


Manage AS number for Dynamic Routing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create network with dynamic routing, operators must add AS number ranges in advance by navigating to Infrastructure -> Zones -> choose a zone -> AS Number.

|dynamic-routing-as-number-ranges.png|

Supported CloudStack APIs for operators to manage the AS number ranges and AS numbers are:

- **createASNRange** : Creates a range of Autonomous Systems for BGP Dynamic Routing
- **listASNRanges** : List Autonomous Systems Number Ranges
- **deleteASNRange** : deletes a range of Autonomous Systems for BGP Dynamic Routing
- **listASNumbers** : List Autonomous Systems Numbers
- **releaseASNumber** : Releases an AS Number back to the pool

Operators can list the AS numbers by navigating to Network -> AS Numbers

|dynamic-routing-as-numbers.png|


Manage BPG peers for Dynamic Routing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create network with dynamic routing, operators must add BGP peers in advance. Guest networks with Dynamic Routing will connect to all BGP peers the account can access.

|dynamic-routing-bgp-peers.png|

Supported CloudStack APIs for operators to manage the BGP peers are:

- **createBgpPeer** : create a BGP peer
- **dedicateBgpPeer** : dedicate a BGP peer to a domain or an account
- **deleteBgpPeer** : delete a BGP peer
- **listBgpPeers** : list BGP peers
- **releaseBgpPeer** : release a dedicated BGP peer from a domain or an account
- **updateBgpPeer** : update a BGP peer


Create Network with Dynamic Routing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The steps to create a network with dynamic routing is almost same as the network with static routing. The only difference is that, users need to choose a network offering with routing mode is Dynamic.

During the network creation, CloudStack will

- Allocate an AS number to the network
- If the network owner does not have dedicated BGP peers, or account setting "use.system.bgp.peers" is set to true, configure BGP sessions in the network VR to connect to all BGP peers the network owner can access.
- If the network owner has dedicated BGP peers, and account setting "use.system.bgp.peers" is set to false, configure BGP sessions in the network VR to connect to all dedicated BGP peers of the domain and the network owner.

ROOT admin can change BGP peers of an existing network with Dynamic routing. After that, the network VR will only connect to selected BGP peers.

|dynamic-routing-change-network-bgp-peers.png|


Create VPC with Dynamic Routing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The creation of VPC with Dynamic routing is almost as VPC with static routing. CloudStack will allocate an AS number to the VPC, and 
- If the VPC owner does not have dedicated BGP peers, or account setting "use.system.bgp.peers" is set to true, configure BGP sessions in the VPC VR to connect to all BGP peers the VPC owner can access.
- If the VPC owner has dedicated BGP peers, and account setting "use.system.bgp.peers" is set to false, configure BGP sessions in the VPC VR to connect to all dedicated BGP peers of the domain and the VPC owner.

ROOT admin can change BGP peers of an existing VPC with Dynamic routing. After that, the VPC VR will only connect to selected BGP peers.

|dynamic-routing-change-vpc-bgp-peers.png|

.. note::
   If a BGP peer is added, removed or updated, the existing network VRs and VPC VRs will not be automatically reconfigured. Please restart the network or VPC to reconfigure the VRs.


CloudStack Kubernetes Service support on ROUTED networks and VPCs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To support CloudStack Kubernetes Service on ROUTED networks and VPCs, operators have to configure the networks.

- The management server must be able to connect to the VMs on ROUTED networks or VPCs
- Some routing firewall Ingress rules (for ROUTED networks) or Network ACL Ingress rules (for ROUTED VPCs) must be configured to open the following ports.

.. cssclass:: table-striped table-bordered table-hover

================= ========================
Ports              Description
================= ========================
22                 The management server configures the CKS nodes via port 22.
6443               The port of Kubernetes API server.
8080               The port of Kubernetes Dashboard.
================= ========================

For more information, see `“CloudStack Kubernetes Service” <../plugins/cloudstack-kubernetes-service.html>`_.


.. |manage-ipv4-subnets-for-zone.png| image:: /_static/images/manage-ipv4-subnets-for-zone.png
   :alt: Manage IPv4 subnets for zoone

.. |manage-ipv4-subnets-for-networks.png| image:: /_static/images/manage-ipv4-subnets-for-networks.png
   :alt: Manage IPv4 subnets for guest networks

.. |routed-add-network-offering.png| image:: /_static/images/routed-add-network-offering.png
   :alt: Add network offering with ROUTED mode

.. |routed-add-vpc-offering.png| image:: /_static/images/routed-add-vpc-offering.png
   :alt: Add vpc offering with ROUTED mode

.. |routed-add-network-cidrsize.png| image:: /_static/images/routed-add-network-cidrsize.png
   :alt: Add ROUTED network with specified cidr size

.. |routed-ipv4-routes.png| image:: /_static/images/routed-ipv4-routes.png
   :alt: IPv4 static routes

.. |routed-ipv4-routing-firewall.png| image:: /_static/images/routed-ipv4-routing-firewall.png
   :alt: IPv4 routing firewall rules

.. |dynamic-routing-as-number-ranges.png| image:: /_static/images/dynamic-routing-as-number-ranges.png
   :alt: AS number ranges for Dynamic Routing

.. |dynamic-routing-as-numbers.png| image:: /_static/images/dynamic-routing-as-numbers.png
   :alt: AS numbers for Dynamic Routing

.. |dynamic-routing-bgp-peers.png| image:: /_static/images/dynamic-routing-bgp-peers.png
   :alt: BGP peers for Dynamic Routing

.. |dynamic-routing-change-network-bgp-peers.png| image:: /_static/images/dynamic-routing-change-network-bgp-peers.png
   :alt: Change BGP peers for network with Dynamic Routing

.. |dynamic-routing-change-vpc-bgp-peers.png| image:: /_static/images/dynamic-routing-change-vpc-bgp-peers.png
   :alt: Change BGP peers for VPC with Dynamic Routing

