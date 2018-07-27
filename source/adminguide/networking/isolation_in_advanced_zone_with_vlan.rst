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
   

Isolation in Advanced Zone Using Private VLAN
---------------------------------------------

Isolation of guest traffic in shared networks can be achieved by using
Private VLANs (PVLAN). PVLANs provide Layer 2 isolation between ports
within the same VLAN. In a PVLAN-enabled shared network, a user VM
cannot reach other user VM though they can reach the DHCP server and
gateway, this would in turn allow users to control traffic within a
network and help them deploy multiple applications without communication
between application as well as prevent communication with other users'
VMs.

-  Isolate VMs in a shared networks by using Private VLANs.

-  Supported on KVM, XenServer, and VMware hypervisors

-  PVLAN-enabled shared network can be a part of multiple networks of a
   guest VM.


About Private VLAN
~~~~~~~~~~~~~~~~~~

In an Ethernet switch, a VLAN is a broadcast domain where hosts can
establish direct communication with each another at Layer 2. Private
VLAN is designed as an extension of VLAN standard to add further
segmentation of the logical broadcast domain. A regular VLAN is a single
broadcast domain, whereas a private VLAN partitions a larger VLAN
broadcast domain into smaller sub-domains. A sub-domain is represented
by a pair of VLANs: a Primary VLAN and a Secondary VLAN. The original
VLAN that is being divided into smaller groups is called Primary, which
implies that all VLAN pairs in a private VLAN share the same Primary
VLAN. All the secondary VLANs exist only inside the Primary. Each
Secondary VLAN has a specific VLAN ID associated to it, which
differentiates one sub-domain from another.

Three types of ports exist in a private VLAN domain, which essentially
determine the behaviour of the participating hosts. Each ports will have
its own unique set of rules, which regulate a connected host's ability
to communicate with other connected host within the same private VLAN
domain. Configure each host that is part of a PVLAN pair can be by using
one of these three port designation:

-  **Promiscuous**: A promiscuous port can communicate with all the
   interfaces, including the community and isolated host ports that
   belong to the secondary VLANs. In Promiscuous mode, hosts are
   connected to promiscuous ports and are able to communicate directly
   with resources on both primary and secondary VLAN. Routers, DHCP
   servers, and other trusted devices are typically attached to
   promiscuous ports.

-  **Isolated VLANs**: The ports within an isolated VLAN cannot
   communicate with each other at the layer-2 level. The hosts that are
   connected to Isolated ports can directly communicate only with the
   Promiscuous resources. If your customer device needs to have access
   only to a gateway router, attach it to an isolated port.

-  **Community VLANs**: The ports within a community VLAN can
   communicate with each other and with the promiscuous ports, but they
   cannot communicate with the ports in other communities at the layer-2
   level. In a Community mode, direct communication is permitted only
   with the hosts in the same community and those that are connected to
   the Primary PVLAN in promiscuous mode. If your customer has two
   devices that need to be isolated from other customers' devices, but
   to be able to communicate among themselves, deploy them in community
   ports.

For further reading:

-  `Understanding Private
   VLANs <http://www.cisco.com/en/US/docs/switches/lan/catalyst3750/software/release/12.2_25_see/configuration/guide/swpvlan.html#wp1038379>`_

-  `Cisco Systems' Private VLANs: Scalable Security in a Multi-Client
   Environment <http://tools.ietf.org/html/rfc5517>`_

-  `Private VLAN (PVLAN) on vNetwork Distributed Switch - Concept
   Overview (1010691) <http://kb.vmware.com>`_


Prerequisites
~~~~~~~~~~~~~

-  Use a PVLAN supported switch.

   See `Private VLAN Catalyst Switch Support
   Matrix <http://www.cisco.com/en/US/products/hw/switches/ps708/products_tech_note09186a0080094830.shtml>`_ for
   more information.

-  All the layer 2 switches, which are PVLAN-aware, are connected to
   each other, and one of them is connected to a router. All the ports
   connected to the host would be configured in trunk mode. Open
   Management VLAN, Primary VLAN (public) and Secondary Isolated VLAN
   ports. Configure the switch port connected to the router in PVLAN
   promiscuous trunk mode, which would translate an isolated VLAN to
   primary VLAN for the PVLAN-unaware router.

   Note that only Cisco Catalyst 4500 has the PVLAN promiscuous trunk
   mode to connect both normal VLAN and PVLAN to a PVLAN-unaware switch.
   For the other Catalyst PVLAN support switch, connect the switch to
   upper switch by using cables, one each for a PVLAN pair.

-  Configure private VLAN on your physical switches out-of-band.

-  Before you use PVLAN on XenServer and KVM, enable Open vSwitch (OVS).

   .. note:: 
      OVS on XenServer and KVM does not support PVLAN natively. Therefore,
      CloudStack managed to simulate PVLAN on OVS for XenServer and KVM by
      modifying the flow table.


Creating a PVLAN-Enabled Guest Network
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as administrator.

#. In the left navigation, choose Infrastructure.

#. On Zones, click View More.

#. Click the zone to which you want to add a guest network.

#. Click the Physical Network tab.

#. Click the physical network you want to work with.

#. On the Guest node of the diagram, click Configure.

#. Click the Network tab.

#. Click Add guest network.

   The Add guest network window is displayed.

#. Specify the following:

   -  **Name**: The name of the network. This will be visible to the
      user.

   -  **Description**: The short description of the network that can be
      displayed to users.

   -  **VLAN ID**: The unique ID of the VLAN.

   -  **Secondary Isolated VLAN ID**: The unique ID of the Secondary
      Isolated VLAN.

      For the description on Secondary Isolated VLAN, see
      `About Private VLAN" <#about-private-vlan>`_.

   -  **Scope**: The available scopes are Domain, Account, Project, and
      All.

      -  **Domain**: Selecting Domain limits the scope of this guest
         network to the domain you specify. The network will not be
         available for other domains. If you select Subdomain Access,
         the guest network is available to all the sub domains within
         the selected domain.

      -  **Account**: The account for which the guest network is being
         created for. You must specify the domain the account belongs
         to.

      -  **Project**: The project for which the guest network is being
         created for. You must specify the domain the project belongs
         to.

      -  **All**: The guest network is available for all the domains,
         account, projects within the selected zone.

   -  **Network Offering**: If the administrator has configured multiple
      network offerings, select the one you want to use for this
      network.

   -  **Gateway**: The gateway that the guests should use.

   -  **Netmask**: The netmask in use on the subnet the guests will use.

   -  **IP Range**: A range of IP addresses that are accessible from the
      Internet and are assigned to the guest VMs.

   -  **Network Domain**: A custom DNS suffix at the level of a network.
      If you want to assign a special domain name to the guest VM
      network, specify a DNS suffix.

#. Click OK to confirm.
