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


Guest Traffic
-------------

A network can carry guest traffic only between Instances within one zone.
Instances in different zones cannot communicate with each other
using their IP addresses; they must communicate with each other by
routing through a public IP address.

See a typical guest traffic setup given below:

|guest-traffic-setup.png| 

Typically, the Management Server automatically creates a virtual router
for each network. A virtual router is a special Instance that
runs on the hosts. Each virtual router in an isolated network has three
network interfaces. If multiple public VLAN is used, the router will
have multiple public interfaces. Its eth0 interface serves as the
gateway for the guest traffic and has the IP address of 10.1.1.1. Its
eth1 interface is used by the system to configure the virtual router.
Its eth2 interface is assigned a public IP address for public traffic.
If multiple public VLAN is used, the router will have multiple public
interfaces.

The virtual router provides DHCP and will automatically assign an IP
address for each Guest Instance within the IP range assigned for the network.
The user can manually reconfigure Guest Instances to assume different IP
addresses.

Source NAT is automatically configured in the virtual router to forward
outbound traffic for all Guest Instances


.. |guest-traffic-setup.png| image:: /_static/images/guest-traffic-setup.png
   :alt: Depicts a guest traffic setup
