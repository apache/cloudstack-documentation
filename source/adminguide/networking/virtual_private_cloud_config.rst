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
   

.. _configuring-vpc:

Configuring a Virtual Private Cloud
-----------------------------------

.. _about-vpc:

About Virtual Private Clouds
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack Virtual Private Cloud is a private, isolated part of
CloudStack. A VPC can have its own virtual network topology that
resembles a traditional physical network. You can launch VMs in the
virtual network that can have private addresses in the range of your
choice, for example: 10.0.0.0/16. You can define network tiers within
your VPC network range, which in turn enables you to group similar kinds
of instances based on IP address range.

For example, if a VPC has the private range 10.0.0.0/16, its guest
networks can have the network ranges 10.0.1.0/24, 10.0.2.0/24,
10.0.3.0/24, and so on.


Major Components of a VPC
^^^^^^^^^^^^^^^^^^^^^^^^^

A VPC is comprised of the following network components:

-  **VPC**: A VPC acts as a container for multiple isolated networks
   that can communicate with each other via its virtual router.

-  **Network Tiers**: Each tier acts as an isolated network with its own
   VLANs and CIDR list, where you can place groups of resources, such as
   VMs. The tiers are segmented by means of VLANs. The NIC of each tier
   acts as its gateway.

-  **Virtual Router**: A virtual router is automatically created and
   started when you create a VPC. The virtual router connect the tiers
   and direct traffic among the public gateway, the VPN gateways, and
   the NAT instances. For each tier, a corresponding NIC and IP exist in
   the virtual router. The virtual router provides DNS and DHCP services
   through its IP.

-  **Public Gateway**: The traffic to and from the Internet routed to
   the VPC through the public gateway. In a VPC, the public gateway is
   not exposed to the end user; therefore, static routes are not support
   for the public gateway.

-  **Private Gateway**: All the traffic to and from a private network
   routed to the VPC through the private gateway. For more information,
   see ":ref:`adding-priv-gw-vpc`".

-  **VPN Gateway**: The VPC side of a VPN connection.

-  **Site-to-Site VPN Connection**: A hardware-based VPN connection
   between your VPC and your datacenter, home network, or co-location
   facility. For more information, see ":ref:`setting-s2s-vpn-conn`".

-  **Customer Gateway**: The customer side of a VPN Connection. For more
   information, see `"Creating and Updating a VPN
   Customer Gateway" <#creating-and-updating-a-vpn-customer-gateway>`_.

-  **NAT Instance**: An instance that provides Port Address Translation
   for instances to access the Internet via the public gateway. For more
   information, see ":ref:`enabling-disabling-static-nat-on-vpc`".

-  **Network ACL**: Network ACL is a group of Network ACL items. Network
   ACL items are nothing but numbered rules that are evaluated in order,
   starting with the lowest numbered rule. These rules determine whether
   traffic is allowed in or out of any tier associated with the network
   ACL. For more information, see ":ref:`conf-net-acl`".


Network Architecture in a VPC
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In a VPC, the following four basic options of network architectures are
present:

-  VPC with a public gateway only

-  VPC with public and private gateways

-  VPC with public and private gateways and site-to-site VPN access

-  VPC with a private gateway only and site-to-site VPN access


Connectivity Options for a VPC
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can connect your VPC to:

-  The Internet through the public gateway.

-  The corporate datacenter by using a site-to-site VPN connection
   through the VPN gateway.

-  Both the Internet and your corporate datacenter by using both the
   public gateway and a VPN gateway.


VPC Network Considerations
^^^^^^^^^^^^^^^^^^^^^^^^^^

Consider the following before you create a VPC:

-  A VPC, by default, is created in the enabled state.

-  A VPC can be created in Advance zone only, and can't belong to more
   than one zone at a time.

-  The default number of VPCs an account can create is 20. However, you
   can change it by using the max.account.vpcs global parameter, which
   controls the maximum number of VPCs an account is allowed to create.

-  The default number of tiers an account can create within a VPC is 3.
   You can configure this number by using the vpc.max.networks
   parameter.

-  Each tier should have an unique CIDR in the VPC. Ensure that the
   tier's CIDR should be within the VPC CIDR range.

-  A tier belongs to only one VPC.

-  All network tiers inside the VPC should belong to the same account.

-  When a VPC is created, by default, a SourceNAT IP is allocated to it.
   The Source NAT IP is released only when the VPC is removed.

-  A public IP can be used for only one purpose at a time. If the IP is
   a sourceNAT, it cannot be used for StaticNAT or port forwarding.

-  The instances can only have a private IP address that you provision.
   To communicate with the Internet, enable NAT to an instance that you
   launch in your VPC.

-  Only new networks can be added to a VPC. The maximum number of
   networks per VPC is limited by the value you specify in the
   vpc.max.networks parameter. The default value is three.

-  The load balancing service can be supported by only one tier inside
   the VPC.

-  If an IP address is assigned to a tier:

   -  That IP can't be used by more than one tier at a time in the VPC.
      For example, if you have tiers A and B, and a public IP1, you can
      create a port forwarding rule by using the IP either for A or B,
      but not for both.

   -  That IP can't be used for StaticNAT, load balancing, or port
      forwarding rules for another guest network inside the VPC.

-  Remote access VPN is not supported in VPC networks.


Adding a Virtual Private Cloud
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When creating the VPC, you simply provide the zone and a set of IP
addresses for the VPC network address space. You specify this set of
addresses in the form of a Classless Inter-Domain Routing (CIDR) block.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

#. Click Add VPC. The Add VPC page is displayed as follows:

   |add-vpc.png|

   Provide the following information:

   -  **Name**: A short name for the VPC that you are creating.

   -  **Description**: A brief description of the VPC.

   -  **Zone**: Choose the zone where you want the VPC to be available.

   -  **Super CIDR for Guest Networks**: Defines the CIDR range for all
      the tiers (guest networks) within a VPC. When you create a tier,
      ensure that its CIDR is within the Super CIDR value you enter. The
      CIDR must be RFC1918 compliant.

   -  **DNS domain for Guest Networks**: If you want to assign a special
      domain name, specify the DNS suffix. This parameter is applied to
      all the tiers within the VPC. That implies, all the tiers you
      create in the VPC belong to the same DNS domain. If the parameter
      is not specified, a DNS domain name is generated automatically.

   -  **Public Load Balancer Provider**: You have two options: VPC
      Virtual Router and Netscaler.

#. Click OK.


Adding Tiers
~~~~~~~~~~~~

Tiers are distinct locations within a VPC that act as isolated networks,
which do not have access to other tiers by default. Tiers are set up on
different VLANs that can communicate with each other by using a virtual
router. Tiers provide inexpensive, low latency network connectivity to
other tiers within the VPC.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPC that you have created for the account is listed in the
   page.

   .. note:: 
      The end users can see their own VPCs, while root and domain admin can
      see any VPC they are authorized to see.

#. Click the Configure button of the VPC for which you want to set up
   tiers.

#. Click Create network.

   The Add new tier dialog is displayed, as follows:

   |add-tier.png|

   If you have already created tiers, the VPC diagram is displayed.
   Click Create Tier to add a new tier.

#. Specify the following:

   All the fields are mandatory.

   -  **Name**: A unique name for the tier you create.

   -  **Network Offering**: The following default network offerings are
      listed: Internal LB,
      DefaultIsolatedNetworkOfferingForVpcNetworksNoLB,
      DefaultIsolatedNetworkOfferingForVpcNetworks

      In a VPC, only one tier can be created by using LB-enabled network
      offering.

   -  **Gateway**: The gateway for the tier you create. Ensure that the
      gateway is within the Super CIDR range that you specified while
      creating the VPC, and is not overlapped with the CIDR of any
      existing tier within the VPC.

   -  **VLAN**: The VLAN ID for the tier that the root admin creates.

      This option is only visible if the network offering you selected
      is VLAN-enabled.

      For more information, see `"Assigning VLANs to
      Isolated Networks" <hosts.html#assigning-vlans-to-isolated-networks>`_.

   -  **Netmask**: The netmask for the tier you create.

      For example, if the VPC CIDR is 10.0.0.0/16 and the network tier
      CIDR is 10.0.1.0/24, the gateway of the tier is 10.0.1.1, and the
      netmask of the tier is 255.255.255.0.

#. Click OK.

#. Continue with configuring access control list for the tier.


.. _conf-net-acl:

Configuring Network Access Control List
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Define Network Access Control List (ACL) on the VPC virtual router to
control incoming (ingress) and outgoing (egress) traffic between the VPC
tiers, and the tiers and Internet. By default, all incoming traffic to
the guest networks is blocked and all outgoing traffic from guest
networks is allowed, once you add an ACL rule for outgoing traffic, then
only outgoing traffic specified in this ACL rule is allowed, the rest is
blocked. To open the ports, you must create a new network ACL. The
network ACLs can be created for the tiers only if the NetworkACL service
is supported.


About Network ACL Lists
^^^^^^^^^^^^^^^^^^^^^^^

In CloudStack terminology, Network ACL is a group of Network ACL items.
Network ACL items are nothing but numbered rules that are evaluated in
order, starting with the lowest numbered rule. These rules determine
whether traffic is allowed in or out of any tier associated with the
network ACL. You need to add the Network ACL items to the Network ACL,
then associate the Network ACL with a tier. Network ACL is associated
with a VPC and can be assigned to multiple VPC tiers within a VPC. A
Tier is associated with a Network ACL at all the times. Each tier can be
associated with only one ACL.

The default Network ACL is used when no ACL is associated. Default
behavior is all the incoming traffic is blocked and outgoing traffic is
allowed from the tiers. Default network ACL cannot be removed or
modified. Contents of the default Network ACL is:

.. cssclass:: table-striped table-bordered table-hover

===== ======== ============ ====== =========
Rule  Protocol Traffic type Action CIDR
===== ======== ============ ====== =========
1     All      Ingress      Deny   0.0.0.0/0
2     All      Egress       Deny   0.0.0.0/0
===== ======== ============ ====== =========


Creating ACL Lists
^^^^^^^^^^^^^^^^^^

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Click the Configure button of the VPC.

   For each tier, the following options are displayed:

   -  Internal LB

   -  Public LB IP

   -  Static NAT

   -  Virtual Machines

   -  CIDR

   The following router information is displayed:

   -  Private Gateways

   -  Public IP Addresses

   -  Site-to-Site VPNs

   -  Network ACL Lists

#. Select Network ACL Lists.

   The following default rules are displayed in the Network ACLs page:
   default\_allow, default\_deny.

#. Click Add ACL Lists, and specify the following:

   -  **ACL List Name**: A name for the ACL list.

   -  **Description**: A short description of the ACL list that can be
      displayed to users.


Creating an ACL Rule
^^^^^^^^^^^^^^^^^^^^

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Click the Configure button of the VPC.

#. Select Network ACL Lists.

   In addition to the custom ACL lists you have created, the following
   default rules are displayed in the Network ACLs page: default\_allow,
   default\_deny.

#. Select the desired ACL list.

#. Select the ACL List Rules tab.

   To add an ACL rule, fill in the following fields to specify what kind
   of network traffic is allowed in the VPC.

   -  **Rule Number**: The order in which the rules are evaluated.

   -  **CIDR**: The CIDR acts as the Source CIDR for the Ingress rules,
      and Destination CIDR for the Egress rules. To accept traffic only
      from or to the IP addresses within a particular address block,
      enter a CIDR or a comma-separated list of CIDRs. The CIDR is the
      base IP address of the incoming traffic. For example,
      192.168.0.0/22. To allow all CIDRs, set to 0.0.0.0/0.

   -  **Action**: What action to be taken. Allow traffic or block.

   -  **Protocol**: The networking protocol that sources use to send
      traffic to the tier. The TCP and UDP protocols are typically used
      for data exchange and end-user communications. The ICMP protocol
      is typically used to send error messages or network monitoring
      data. All supports all the traffic. Other option is Protocol
      Number.

   -  **Start Port**, **End Port** (TCP, UDP only): A range of listening
      ports that are the destination for the incoming traffic. If you
      are opening a single port, use the same number in both fields.

   -  **Protocol Number**: The protocol number associated with IPv4 or
      IPv6. For more information, see `Protocol Numbers 
      <http://www.iana.org/assignments/protocol-numbers/protocol-numbers.xml>`_.

   -  **ICMP Type**, **ICMP Code** (ICMP only): The type of message and
      error code that will be sent.

   -  **Traffic Type**: The type of traffic: Incoming or outgoing.

#. Click Add. The ACL rule is added.

   You can edit the tags assigned to the ACL rules and delete the ACL
   rules you have created. Click the appropriate button in the Details
   tab.


Creating a Tier with Custom ACL List
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Create a VPC.

#. Create a custom ACL list.

#. Add ACL rules to the ACL list.

#. Create a tier in the VPC.

   Select the desired ACL list while creating a tier.

#. Click OK.


Assigning a Custom ACL List to a Tier
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Create a VPC.

#. Create a tier in the VPC.

#. Associate the tier with the default ACL rule.

#. Create a custom ACL list.

#. Add ACL rules to the ACL list.

#. Select the tier for which you want to assign the custom ACL.

#. Click the Replace ACL List icon. |replace-acl-icon.png|

   The Replace ACL List dialog is displayed.

#. Select the desired ACL list.

#. Click OK.


.. _adding-priv-gw-vpc:

Adding a Private Gateway to a VPC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A private gateway can be added by the root admin only. The VPC private
network has 1:1 relationship with the NIC of the physical network. You
can configure multiple private gateways to a single VPC. No gateways
with duplicated VLAN and IP are allowed in the same data center.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Click the Configure button of the VPC to which you want to configure
   load balancing rules.

   The VPC page is displayed where all the tiers you created are listed
   in a diagram.

#. Click the Settings icon.

   The following options are displayed.

   -  Internal LB

   -  Public LB IP

   -  Static NAT

   -  Virtual Machines

   -  CIDR

   The following router information is displayed:

   -  Private Gateways

   -  Public IP Addresses

   -  Site-to-Site VPNs

   -  Network ACL Lists

#. Select Private Gateways.

   The Gateways page is displayed.

#. Click Add new gateway:

   |add-new-gateway-vpc.png|

#. Specify the following:

   -  **Physical Network**: The physical network you have created in the
      zone.

   -  **IP Address**: The IP address associated with the VPC gateway.

   -  **Gateway**: The gateway through which the traffic is routed to
      and from the VPC.

   -  **Netmask**: The netmask associated with the VPC gateway.

   -  **VLAN**: The VLAN associated with the VPC gateway.

   -  **Source NAT**: Select this option to enable the source NAT
      service on the VPC private gateway.

      See ":ref:`source-nat-priv-gw`".

   -  **ACL**: Controls both ingress and egress traffic on a VPC private
      gateway. By default, all the traffic is blocked.

      See ":ref:`acl-priv-gw`".

   The new gateway appears in the list. You can repeat these steps to
   add more gateway for this VPC.


.. _source-nat-priv-gw:

Source NAT on Private Gateway
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You might want to deploy multiple VPCs with the same super CIDR and
guest tier CIDR. Therefore, multiple guest VMs from different VPCs can
have the same IPs to reach a enterprise data center through the private
gateway. In such cases, a NAT service need to be configured on the
private gateway to avoid IP conflicts. If Source NAT is enabled, the
guest VMs in VPC reaches the enterprise network via private gateway IP
address by using the NAT service.

The Source NAT service on a private gateway can be enabled while adding
the private gateway. On deletion of a private gateway, source NAT rules
specific to the private gateway are deleted.

To enable source NAT on existing private gateways, delete them and
create afresh with source NAT.


.. _acl-priv-gw:

ACL on Private Gateway
^^^^^^^^^^^^^^^^^^^^^^

The traffic on the VPC private gateway is controlled by creating both
ingress and egress network ACL rules. The ACLs contains both allow and
deny rules. As per the rule, all the ingress traffic to the private
gateway interface and all the egress traffic out from the private
gateway interface are blocked.

You can change this default behaviour while creating a private gateway.
Alternatively, you can do the following:

#. In a VPC, identify the Private Gateway you want to work with.

#. In the Private Gateway page, do either of the following:

   -  Use the Quickview. See 3.

   -  Use the Details tab. See 4 through .

#. In the Quickview of the selected Private Gateway, click Replace ACL,
   select the ACL rule, then click OK

#. Click the IP address of the Private Gateway you want to work with.

#. In the Detail tab, click the Replace ACL button.
   |replace-acl-icon.png|

   The Replace ACL dialog is displayed.

#. select the ACL rule, then click OK.

   Wait for few seconds. You can see that the new ACL rule is displayed
   in the Details page.


Creating a Static Route
^^^^^^^^^^^^^^^^^^^^^^^

CloudStack enables you to specify routing for the VPN connection you
create. You can enter one or CIDR addresses to indicate which traffic is
to be routed back to the gateway.

#. In a VPC, identify the Private Gateway you want to work with.

#. In the Private Gateway page, click the IP address of the Private
   Gateway you want to work with.

#. Select the Static Routes tab.

#. Specify the CIDR of destination network.

#. Click Add.

   Wait for few seconds until the new route is created.


Blacklisting Routes
^^^^^^^^^^^^^^^^^^^

CloudStack enables you to block a list of routes so that they are not
assigned to any of the VPC private gateways. Specify the list of routes
that you want to blacklist in the ``blacklisted.routes`` global
parameter. Note that the parameter update affects only new static route
creations. If you block an existing static route, it remains intact and
continue functioning. You cannot add a static route if the route is
blacklisted for the zone.


Deploying VMs to the Tier
~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Click the Configure button of the VPC to which you want to deploy the
   VMs.

   The VPC page is displayed where all the tiers you have created are
   listed.

#. Click Virtual Machines tab of the tier to which you want to add a VM.

   |add-vm-vpc.png|

   The Add Instance page is displayed.

   Follow the on-screen instruction to add an instance. For information
   on adding an instance, see the Installation Guide.


Deploying VMs to VPC Tier and Shared Networks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack allows you deploy VMs on a VPC tier and one or more shared
networks. With this feature, VMs deployed in a multi-tier application
can receive monitoring services via a shared network provided by a
service provider.

#. Log in to the CloudStack UI as an administrator.

#. In the left navigation, choose Instances.

#. Click Add Instance.

#. Select a zone.

#. Select a template or ISO, then follow the steps in the wizard.

#. Ensure that the hardware you have allows starting the selected
   service offering.

#. Under Networks, select the desired networks for the VM you are
   launching.

   You can deploy a VM to a VPC tier and multiple shared networks.

   |addvm-tier-sharednw.png|

#. Click Next, review the configuration and click Launch.

   Your VM will be deployed to the selected VPC tier and shared network.


Acquiring a New IP Address for a VPC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When you acquire an IP address, all IP addresses are allocated to VPC,
not to the guest networks within the VPC. The IPs are associated to the
guest network only when the first port-forwarding, load balancing, or
Static NAT rule is created for the IP or the network. IP can't be
associated to more than one network at a time.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Click the Configure button of the VPC to which you want to deploy the
   VMs.

   The VPC page is displayed where all the tiers you created are listed
   in a diagram.

   The following options are displayed.

   -  Internal LB

   -  Public LB IP

   -  Static NAT

   -  Virtual Machines

   -  CIDR

   The following router information is displayed:

   -  Private Gateways

   -  Public IP Addresses

   -  Site-to-Site VPNs

   -  Network ACL Lists

#. Select IP Addresses.

   The Public IP Addresses page is displayed.

#. Click Acquire New IP, and click Yes in the confirmation dialog.

   You are prompted for confirmation because, typically, IP addresses
   are a limited resource. Within a few moments, the new IP address
   should appear with the state Allocated. You can now use the IP
   address in port forwarding, load balancing, and static NAT rules.


Releasing an IP Address Alloted to a VPC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The IP address is a limited resource. If you no longer need a particular
IP, you can disassociate it from its VPC and return it to the pool of
available addresses. An IP address can be released from its tier, only
when all the networking ( port forwarding, load balancing, or StaticNAT
) rules are removed for this IP address. The released IP address will
still belongs to the same VPC.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Click the Configure button of the VPC whose IP you want to release.

   The VPC page is displayed where all the tiers you created are listed
   in a diagram.

   The following options are displayed.

   -  Internal LB

   -  Public LB IP

   -  Static NAT

   -  Virtual Machines

   -  CIDR

   The following router information is displayed:

   -  Private Gateways

   -  Public IP Addresses

   -  Site-to-Site VPNs

   -  Network ACL Lists

#. Select Public IP Addresses.

   The IP Addresses page is displayed.

#. Click the IP you want to release.

#. In the Details tab, click the Release IP button |release-ip-icon.png|


.. _enabling-disabling-static-nat-on-vpc:

Enabling or Disabling Static NAT on a VPC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A static NAT rule maps a public IP address to the private IP address of
a VM in a VPC to allow Internet traffic to it. This section tells how to
enable or disable static NAT for a particular IP address in a VPC.

If port forwarding rules are already in effect for an IP address, you
cannot enable static NAT to that IP.

If a guest VM is part of more than one network, static NAT rules will
function only if they are defined on the default network.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Click the Configure button of the VPC to which you want to deploy the
   VMs.

   The VPC page is displayed where all the tiers you created are listed
   in a diagram.

   For each tier, the following options are displayed.

   -  Internal LB

   -  Public LB IP

   -  Static NAT

   -  Virtual Machines

   -  CIDR

   The following router information is displayed:

   -  Private Gateways

   -  Public IP Addresses

   -  Site-to-Site VPNs

   -  Network ACL Lists

#. In the Router node, select Public IP Addresses.

   The IP Addresses page is displayed.

#. Click the IP you want to work with.

#. In the Details tab,click the Static NAT button. |enable-disable.png| 
   The button toggles between Enable and
   Disable, depending on whether static NAT is currently enabled for the
   IP address.

#. If you are enabling static NAT, a dialog appears as follows:

   |select-vmstatic-nat.png|

#. Select the tier and the destination VM, then click Apply.


Adding Load Balancing Rules on a VPC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In a VPC, you can configure two types of load balancing: external LB and
internal LB. External LB is nothing but a LB rule created to redirect
the traffic received at a public IP of the VPC virtual router. The
traffic is load balanced within a tier based on your configuration.
Citrix NetScaler and VPC virtual router are supported for external LB.
When you use internal LB service, traffic received at a tier is load
balanced across different VMs within that tier. For example, traffic
reached at Web tier is redirected to another VM in that tier. External
load balancing devices are not supported for internal LB. The service is
provided by a internal LB VM configured on the target tier.


Load Balancing Within a Tier (External LB)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A CloudStack user or administrator may create load balancing rules that
balance traffic received at a public IP to one or more VMs that belong
to a network tier that provides load balancing service in a VPC. A user
creates a rule, specifies an algorithm, and assigns the rule to a set of
VMs within a tier.


Enabling NetScaler as the LB Provider on a VPC Tier
'''''''''''''''''''''''''''''''''''''''''''''''''''

#. Add and enable Netscaler VPX in dedicated mode.

   Netscaler can be used in a VPC environment only if it is in dedicated
   mode.

#. Create a network offering, as given in ":ref:`create-net-offering-ext-lb`".

#. Create a VPC with Netscaler as the Public LB provider.

   For more information, see `"Adding a Virtual Private
   Cloud" <#adding-a-virtual-private-cloud>`_.

#. For the VPC, acquire an IP.

#. Create an external load balancing rule and apply, as given in
   :ref:`create-ext-lb-rule`.


.. _create-net-offering-ext-lb:

Creating a Network Offering for External LB
'''''''''''''''''''''''''''''''''''''''''''

To have external LB support on VPC, create a network offering as
follows:

#. Log in to the CloudStack UI as a user or admin.

#. From the Select Offering drop-down, choose Network Offering.

#. Click Add Network Offering.

#. In the dialog, make the following choices:

   -  **Name**: Any desired name for the network offering.

   -  **Description**: A short description of the offering that can be
      displayed to users.

   -  **Network Rate**: Allowed data transfer rate in MB per second.

   -  **Traffic Type**: The type of network traffic that will be carried
      on the network.

   -  **Guest Type**: Choose whether the guest network is isolated or
      shared.

   -  **Persistent**: Indicate whether the guest network is persistent
      or not. The network that you can provision without having to
      deploy a VM on it is termed persistent network.

   -  **VPC**: This option indicate whether the guest network is Virtual
      Private Cloud-enabled. A Virtual Private Cloud (VPC) is a private,
      isolated part of CloudStack. A VPC can have its own virtual
      network topology that resembles a traditional physical network.
      For more information on VPCs, see :ref: `about-vpc`.

   -  **Specify VLAN**: (Isolated guest networks only) Indicate whether
      a VLAN should be specified when this offering is used.

   -  **Supported Services**: Select Load Balancer. Use Netscaler or
      VpcVirtualRouter.

   -  **Load Balancer Type**: Select Public LB from the drop-down.

   -  **LB Isolation**: Select Dedicated if Netscaler is used as the
      external LB provider.

   -  **System Offering**: Choose the system service offering that you
      want virtual routers to use in this network.

   -  **Conserve mode**: Indicate whether to use conserve mode. In this
      mode, network resources are allocated only when the first virtual
      machine starts in the network.

#. Click OK and the network offering is created.


.. _create-ext-lb-rule:

Creating an External LB Rule
''''''''''''''''''''''''''''

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Click the Configure button of the VPC, for which you want to
   configure load balancing rules.

   The VPC page is displayed where all the tiers you created listed in a
   diagram.

   For each tier, the following options are displayed:

   -  Internal LB

   -  Public LB IP

   -  Static NAT

   -  Virtual Machines

   -  CIDR

   The following router information is displayed:

   -  Private Gateways

   -  Public IP Addresses

   -  Site-to-Site VPNs

   -  Network ACL Lists

#. In the Router node, select Public IP Addresses.

   The IP Addresses page is displayed.

#. Click the IP address for which you want to create the rule, then
   click the Configuration tab.

#. In the Load Balancing node of the diagram, click View All.

#. Select the tier to which you want to apply the rule.

#. Specify the following:

   -  **Name**: A name for the load balancer rule.

   -  **Public Port**: The port that receives the incoming traffic to be
      balanced.

   -  **Private Port**: The port that the VMs will use to receive the
      traffic.

   -  **Algorithm**. Choose the load balancing algorithm you want
      CloudStack to use. CloudStack supports the following well-known
      algorithms:

      -  Round-robin

      -  Least connections

      -  Source

   -  **Stickiness**. (Optional) Click Configure and choose the
      algorithm for the stickiness policy. See Sticky Session Policies
      for Load Balancer Rules.

   -  **Add VMs**: Click Add VMs, then select two or more VMs that will
      divide the load of incoming traffic, and click Apply.

The new load balancing rule appears in the list. You can repeat these
steps to add more load balancing rules for this IP address.


Load Balancing Across Tiers
^^^^^^^^^^^^^^^^^^^^^^^^^^^

CloudStack supports sharing workload across different tiers within your
VPC. Assume that multiple tiers are set up in your environment, such as
Web tier and Application tier. Traffic to each tier is balanced on the
VPC virtual router on the public side, as explained in
`"Adding Load Balancing Rules on a VPC" <#adding-load-balancing-rules-on-a-vpc>`_. 
If you want the traffic coming
from the Web tier to the Application tier to be balanced, use the
internal load balancing feature offered by CloudStack.


How Does Internal LB Work in VPC?
'''''''''''''''''''''''''''''''''

In this figure, a public LB rule is created for the public IP
72.52.125.10 with public port 80 and private port 81. The LB rule,
created on the VPC virtual router, is applied on the traffic coming from
the Internet to the VMs on the Web tier. On the Application tier two
internal load balancing rules are created. An internal LB rule for the
guest IP 10.10.10.4 with load balancer port 23 and instance port 25 is
configured on the VM, InternalLBVM1. Another internal LB rule for the
guest IP 10.10.10.4 with load balancer port 45 and instance port 46 is
configured on the VM, InternalLBVM1. Another internal LB rule for the
guest IP 10.10.10.6, with load balancer port 23 and instance port 25 is
configured on the VM, InternalLBVM2.

|vpc-lb.png|


Guidelines
''''''''''

-  Internal LB and Public LB are mutually exclusive on a tier. If the
   tier has LB on the public side, then it can't have the Internal LB.

-  Internal LB is supported just on VPC networks in CloudStack 4.2
   release.

-  Only Internal LB VM can act as the Internal LB provider in CloudStack
   4.2 release.

-  Network upgrade is not supported from the network offering with
   Internal LB to the network offering with Public LB.

-  Multiple tiers can have internal LB support in a VPC.

-  Only one tier can have Public LB support in a VPC.


Enabling Internal LB on a VPC Tier
''''''''''''''''''''''''''''''''''

#. Create a network offering, as given in 
   :ref:`creating-net-offering-internal-lb`.

#. Create an internal load balancing rule and apply, as given in 
   :ref:`create-int-lb-rule`.


.. _creating-net-offering-internal-lb:

Creating a Network Offering for Internal LB
'''''''''''''''''''''''''''''''''''''''''''

To have internal LB support on VPC, either use the default offering,
DefaultIsolatedNetworkOfferingForVpcNetworksWithInternalLB, or create a
network offering as follows:

#. Log in to the CloudStack UI as a user or admin.

#. From the Select Offering drop-down, choose Network Offering.

#. Click Add Network Offering.

#. In the dialog, make the following choices:

   -  **Name**: Any desired name for the network offering.

   -  **Description**: A short description of the offering that can be
      displayed to users.

   -  **Network Rate**: Allowed data transfer rate in MB per second.

   -  **Traffic Type**: The type of network traffic that will be carried
      on the network.

   -  **Guest Type**: Choose whether the guest network is isolated or
      shared.

   -  **Persistent**: Indicate whether the guest network is persistent
      or not. The network that you can provision without having to
      deploy a VM on it is termed persistent network.

   -  **VPC**: This option indicate whether the guest network is Virtual
      Private Cloud-enabled. A Virtual Private Cloud (VPC) is a private,
      isolated part of CloudStack. A VPC can have its own virtual
      network topology that resembles a traditional physical network.
      For more information on VPCs, see `"About Virtual
      Private Clouds" <#about-virtual-private-clouds>`_.

   -  **Specify VLAN**: (Isolated guest networks only) Indicate whether
      a VLAN should be specified when this offering is used.

   -  **Supported Services**: Select Load Balancer. Select
      ``InternalLbVM`` from the provider list.

   -  **Load Balancer Type**: Select Internal LB from the drop-down.

   -  **System Offering**: Choose the system service offering that you
      want virtual routers to use in this network.

   -  **Conserve mode**: Indicate whether to use conserve mode. In this
      mode, network resources are allocated only when the first virtual
      machine starts in the network.

#. Click OK and the network offering is created.


.. _create-int-lb-rule:

Creating an Internal LB Rule
''''''''''''''''''''''''''''

When you create the Internal LB rule and applies to a VM, an Internal LB
VM, which is responsible for load balancing, is created.

You can view the created Internal LB VM in the Instances page if you
navigate to **Infrastructure** > **Zones** > <zone\_ name> >
<physical\_network\_name> > **Network Service Providers** > **Internal
LB VM**. You can manage the Internal LB VMs as and when required from
the location.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Locate the VPC for which you want to configure internal LB, then
   click Configure.

   The VPC page is displayed where all the tiers you created listed in a
   diagram.

#. Locate the Tier for which you want to configure an internal LB rule,
   click Internal LB.

   In the Internal LB page, click Add Internal LB.

#. In the dialog, specify the following:

   -  **Name**: A name for the load balancer rule.

   -  **Description**: A short description of the rule that can be
      displayed to users.

   -  **Source IP Address**: (Optional) The source IP from which traffic
      originates. The IP is acquired from the CIDR of that particular
      tier on which you want to create the Internal LB rule. If not
      specified, the IP address is automatically allocated from the
      network CIDR.

      For every Source IP, a new Internal LB VM is created for load
      balancing.

   -  **Source Port**: The port associated with the source IP. Traffic
      on this port is load balanced.

   -  **Instance Port**: The port of the internal LB VM.

   -  **Algorithm**. Choose the load balancing algorithm you want
      CloudStack to use. CloudStack supports the following well-known
      algorithms:

      -  Round-robin

      -  Least connections

      -  Source


Adding a Port Forwarding Rule on a VPC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Click the Configure button of the VPC to which you want to deploy the
   VMs.

   The VPC page is displayed where all the tiers you created are listed
   in a diagram.

   For each tier, the following options are displayed:

   -  Internal LB

   -  Public LB IP

   -  Static NAT

   -  Virtual Machines

   -  CIDR

   The following router information is displayed:

   -  Private Gateways

   -  Public IP Addresses

   -  Site-to-Site VPNs

   -  Network ACL Lists

#. In the Router node, select Public IP Addresses.

   The IP Addresses page is displayed.

#. Click the IP address for which you want to create the rule, then
   click the Configuration tab.

#. In the Port Forwarding node of the diagram, click View All.

#. Select the tier to which you want to apply the rule.

#. Specify the following:

   -  **Public Port**: The port to which public traffic will be
      addressed on the IP address you acquired in the previous step.

   -  **Private Port**: The port on which the instance is listening for
      forwarded public traffic.

   -  **Protocol**: The communication protocol in use between the two
      ports.

      -  TCP

      -  UDP

   -  **Add VM**: Click Add VM. Select the name of the instance to which
      this rule applies, and click Apply.

      You can test the rule by opening an SSH session to the instance.


Removing Tiers
~~~~~~~~~~~~~~

You can remove a tier from a VPC. A removed tier cannot be revoked. When
a tier is removed, only the resources of the tier are expunged. All the
network rules (port forwarding, load balancing and staticNAT) and the IP
addresses associated to the tier are removed. The IP address still be
belonging to the same VPC.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPC that you have created for the account is listed in the
   page.

#. Click the Configure button of the VPC for which you want to set up
   tiers.

   The Configure VPC page is displayed. Locate the tier you want to work
   with.

#. Select the tier you want to remove.

#. In the Network Details tab, click the Delete Network button.
   |del-tier.png|

   Click Yes to confirm. Wait for some time for the tier to be removed.


Editing, Restarting, and Removing a Virtual Private Cloud
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note:: Ensure that all the tiers are removed before you remove a VPC.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Select the VPC you want to work with.

#. In the Details tab, click the Remove VPC button |remove-vpc.png|

   You can remove the VPC by also using the remove button in the Quick
   View.

   You can edit the name and description of a VPC. To do that, select
   the VPC, then click the Edit button. |vpc-edit-icon.png|

   To restart a VPC, select the VPC, then click the Restart button.
   |restart-vpc.png|


.. |add-vpc.png| image:: /_static/images/add-vpc.png
   :alt: adding a vpc.
.. |add-tier.png| image:: /_static/images/add-tier.png
   :alt: adding a tier to a vpc.
.. |replace-acl-icon.png| image:: /_static/images/replace-acl-icon.png
   :alt: button to replace an ACL list
.. |add-new-gateway-vpc.png| image:: /_static/images/add-new-gateway-vpc.png
   :alt: adding a private gateway for the VPC.
.. |add-vm-vpc.png| image:: /_static/images/add-vm-vpc.png
   :alt: adding a VM to a vpc.
.. |addvm-tier-sharednw.png| image:: /_static/images/addvm-tier-sharednw.png
   :alt: adding a VM to a VPC tier and shared network.
.. |release-ip-icon.png| image:: /_static/images/release-ip-icon.png
   :alt: button to release an IP.
.. |enable-disable.png| image:: /_static/images/enable-disable.png
   :alt: button to enable Static NAT.
.. |select-vmstatic-nat.png| image:: /_static/images/select-vm-staticnat-vpc.png
   :alt: selecting a tier to apply staticNAT.
.. |vpc-lb.png| image:: /_static/images/vpc-lb.png
   :alt: Configuring internal LB for VPC
.. |del-tier.png| image:: /_static/images/del-tier.png
   :alt: button to remove a tier
.. |vpc-edit-icon.png| image:: /_static/images/edit-icon.png
   :alt: button to edit.
.. |remove-vpc.png| image:: /_static/images/remove-vpc.png
   :alt: button to remove a VPC
.. |restart-vpc.png| image:: /_static/images/restart-vpc.png
   :alt: button to restart a VPC
