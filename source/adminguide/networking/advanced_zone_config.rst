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



Advanced Zone Physical Network Configuration
--------------------------------------------

Within a zone that uses advanced networking, you need to tell the
Management Server how the physical Network is set up to carry different
kinds of traffic in isolation.


Configure Guest Traffic in an Advanced Zone
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These steps assume you have already logged in to the CloudStack UI. To
configure the base guest Network:

#. In the left navigation, choose Network.

#. Click Add Network.

   The Add guest Network window is displayed:

   |addguestnetwork.png|

#. Provide the following information for creating an isolated Network:

   -  **Name**: The name of the Network. This will be User-visible
 
   -  **Description**: The description of the Network. This will be
      User-visible

   -  **Zone**: The zone in which you are configuring the guest Network.

   -  **Network offering**: If the administrator has configured multiple
      Network offerings, select the one you want to use for this Network

   - **Public MTU**: The MTU that will be configured on the public interfaces
      of the Network's VR.
      **NOTE:** This will not be considered for VPC Network Tiers, as the
      public MTU defined at the VPC Network creation level will be considered

   - **Private MTU**: The MTU that will configured on the private interface(s)
      of the Network's VR

   -  **External Id**: ID of the Network in an external system.
 
   -  **Gateway**: The gateway that the guests Instances will use.
 
   -  **Netmask**: The netmask in use on the subnet the Guest Instances
      will use.

   -  **DNS**: A set of custom DNS that will be used by the guest Network. If not provided then DNS specified for the zone will be used. Available only when the selected Network offering supports DNS service.

   -  **IPv6 DNS**: A set of custom IPv6 DNS that will be used by the guest Network. If not provided then IPv6 DNS specified for the zone will be used. Available only when the selected Network offering is IPv6 enabled and supports DNS service.

   -  **IPv4 address for the VR in this Network**: The source NAT address or primary public Network address to use by the guest Network. If not provided then a random address from the available pool of addresses wil be used.

   -  **Network Domain**: A custom DNS suffix at the level of a Network. If you
      want to assign a special domain name to the Guest Instance Network, specify a
      DNS suffix.


#. Click OK.

.. note:: 
   * In security groups-enabled Advanced zones and Basic zones, creation of VPC and isolated Networks are not supported.
   * MTU options will be shown in the UI and considered only when zone configuration - `allow.end.users.to.specify.vr.mtu` is set to true. Maximum allowed values for public and private MTU can be controlled by zone-level configurations, `vr.public.interface.max.mtu` and `vr.private.interface.max.mtu` respectively.

Configure Public Traffic in an Advanced Zone
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In a zone that uses advanced networking, you need to configure at least
one range of IP addresses for Internet traffic.


Configuring a Shared Guest Network
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as administrator or an end User.

#. In the left navigation, choose Network.

#. Click the Guest Networks tab

#. Click the Add Network icon.

#. Click the Shared tab.

   The Add guest Network window is displayed.

   |addsharednetwork.png|

#. Specify the following:

   -  **Name**: The name of the Network. This will be visible to the User.

   -  **Description**: The short description of the Network that can be
      displayed to Users.

   -  **Zone**: The zone for the Network.

   -  **Physical Network**: The physical Network ID the Network belongs to.

   -  **VLAN ID**: (Administrators only) The unique ID of the VLAN.

   -  **Secondary VLAN Type**: (Administrators only) The isolation private
      VLAN type for this Network

   -  **Secondary VLAN ID**: (Administrators only) The unique ID of the
      Secondary Isolated VLAN.

   -  **Bypass VLAN id/range overlap**: (Administrators only) When true
      bypasses VLAN id/range overlap check during Network creation for
      shared and L2 Networks

   -  **Scope**: The available scopes are Domain, Account, Project, and
      All.

      -  **Domain**: Selecting Domain limits the scope of this guest
         Network to the domain you specify. The Network will not be
         available for other domains. If you select Subdomain Access,
         the guest Network is available to all the sub domains within
         the selected domain.

      -  **Account**: The Account for which the guest Network is being
         created for. You must specify the domain the Account belongs
         to.

      -  **Project**: The project for which the guest Network is being
         created for. You must specify the domain the project belongs
         to.

      -  **All**: (Administrators only) The guest Network is available
         for all the domains, Account, projects within the selected zone.

   -  **Network Offering**: If the administrator has configured multiple
      Network offerings, select the one you want to use for this
      Network.
   
   - **Public MTU**: The MTU that will be configured on the public interfaces
      of the Network's VR. This MTU will considered for redundant VRs

   - **Private MTU**: The MTU that will configured on the private interface(s)
      of the Network's VR

   -  **Associated Network**: The L2 or Isolated Network this Network is
      associated to. This Network will use same VLAN as associated Network.
      This will be visible if Network offering has specifyvlan is false.

   -  **Gateway**: The gateway that the guests should use.

   -  **Netmask**: The netmask in use on the subnet the guests will use.

   -  **IP Range**: A range of IP addresses that are accessible from the
      Internet and are assigned to the Guest Instances.

   -  **DNS**: A set of custom DNS that will be used by the Network. If not provided then DNS specified for the zone will be used. Available only when the selected Network offering supports DNS service.

      If one NIC is used, these IPs should be in the same CIDR in the
      case of IPv6.

   -  **IPv6 CIDR**: The Network prefix that defines the guest Network
      subnet. This is the CIDR that describes the IPv6 addresses in use
      in the guest Networks in this zone. To allot IP addresses from
      within a particular address block, enter a CIDR.

   -  **IPv6 DNS**: A set of custom IPv6 DNS that will be used by the Network. If not provided then IPv6 DNS specified for the zone will be used. Available only when the selected Network offering supports DNS service.

   -  **Network Domain**: A custom DNS suffix at the level of a Network.
      If you want to assign a special domain name to the Guest Instance
      Network, specify a DNS suffix.

#. Click OK to confirm.

   .. note::
      * End users (not administrator) can only use the Network
        offerings with specifyvlan is false. Please create a Network offering
        with specifyvlan is false to enable this for end users. See
        `“Creating a New Network Offering”
        <networking.html#creating-a-new-network-offering>`_.
      * MTU options will be shown in the UI and considered only when zone configuration - `allow.end.users.to.specify.vr.mtu` is set to true. Maximum allowed values for public and private MTU can be controlled by zone-level configurations, `vr.public.interface.max.mtu` and `vr.private.interface.max.mtu` respectively.


.. |addguestnetwork.png| image:: /_static/images/add-guest-network.png
   :alt: Add Guest network setup in a single zone.

.. |addsharednetwork.png| image:: /_static/images/add-shared-network.png
   :alt: Add Shared Guest Network.
