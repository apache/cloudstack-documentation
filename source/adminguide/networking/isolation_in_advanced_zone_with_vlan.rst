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


Isolation in Advanced Zone Using Private VLANs
-----------------------------------------------

About PVLANs (Secondary VLANs)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The clasic use-case for PVLANs is a shared backup network, where you wish all users'
hosts to be able to communicate with a backup host, but not with each other.

   |pvlans.png|

For further reading:

-  `Understanding Private
   VLANs <http://www.cisco.com/en/US/docs/switches/lan/catalyst3750/software/release/12.2_25_see/configuration/guide/swpvlan.html#wp1038379>`_

-  `Cisco Systems' Private VLANs: Scalable Security in a Multi-Client
   Environment <http://tools.ietf.org/html/rfc5517>`_

-  `Private VLAN (PVLAN) on vNetwork Distributed Switch - Concept
   Overview (1010691) <http://kb.vmware.com>`_

Supported Secondary VLAN types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Of the three types of Private VLAN (promiscuous, community and isolated),
CloudStack supports **one promiscuous** PVLAN, **one isolated** PVLAN and **multiple community** PVLANs **per
primary VLAN**.
PVLANs are currently supported on shared and layer 2 networks.
The PVLAN concept is supported on KVM (when using OVS), XenServer (when using OVS), and VMware hypervisors

   .. note::
      OVS on XenServer and KVM does not support PVLAN natively. Therefore,
      CloudStack managed to simulate PVLAN on OVS for XenServer and KVM by
      modifying the flow table.

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


Creating a PVLAN-Enabled Network
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

   .. note::
      If you are facing issues with connectivity in PVLANS, especially community and promiscuous PVLANS
      in a multi hypervisor environment, this could be caused by the way PVLANs were implemented
      in 4.14.0, which was later fixed in 4.15.0. To resolve this, delete the PVLAN network and recreate it.

PVLAN-enabled networks can be either shared or layer 2 networks.

For a general description of how to create a shared network see `"configuring a shared guest network" <#configuring-a-shared-guest-network>`_.

On top of the parameters required to create a *normal* shared or layer 2 network, the following
parameters must be set:

-  **VLAN ID**: The unique ID of the primary VLAN that you want to use.

-  **Secondary Isolated VLAN ID**: The PVLAN ID to use within the primary VLAN.

-  **PVLAN Type**: The PVLAN type corresponding to the PVLAN ID to use within the primary VLAN.

Creating a PVLAN-enabled network can be done in multiple ways depending on the PVLAN type:

   - For a **promiscuous** PVLAN:
      - Set the secondary VLAN ID to the same VLAN ID as the primary VLAN that the promiscuous PVLAN will be inside (available only via API, not UI), or
      - Set the PVLAN type to "Promiscuous" and do not set the secondary VLAN ID.

   - For an **isolated** PVLAN:
      - Set the secondary VLAN ID to the PVLAN ID which you wish to use inside the primary VLAN (available only via API, not UI), or
      - Set the PVLAN type to "Isolated" and set the secondary VLAN ID to the PVLAN ID which you wish to use inside the primary VLAN.

   - For a **community** PVLAN:
      - Set the PVLAN type to "Community" and set the secondary VLAN ID to the PVLAN ID which you wish to use inside the primary VLAN.

.. |pvlans.png| image:: /_static/images/pvlans.png
   :alt: Diagram of PVLAN communications
