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


Create Network and VPC Offering with ROUTED mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For more information, see `“Creating a New Network Offering” <networking.html#creating-a-new-network-offering>`_.

TODO


Create Network with Static Routing for IPv4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO


Create Network with Static Routing for IPv6
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The IPv6 static routing has been introduced in Apache CloudStack 4.17.0.0.
For more information, see `“IPv6 support for isolated networks and VPC Network Tiers” <../plugins/ipv6.html#isolated-network-and-vpc-network-tier>`_.

Manage IPv4 Routing Firewall
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO

Manage AS number
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO

Manage BPG peers for Dynamic Routing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO

Create Network with Dynamic Routing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO

