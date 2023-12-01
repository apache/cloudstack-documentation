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


.. _remote-access-vpn:

Remote Access VPN
-----------------

CloudStack Account owners can create virtual private networks (VPN) to
access their Instances. If the guest network is instantiated from
a network offering that offers the Remote Access VPN service, the
virtual router (based on the System VM) is used to provide the service.
CloudStack provides a L2TP-over-IPsec-based remote access VPN service to
guest virtual networks. Since each network gets its own virtual router,
VPNs are not shared across the networks. VPN clients native to `Windows,
Mac OS X <networking/using_remote_access.html>`_ and iOS can be used to connect to the guest networks. The
account owner can create and manage users for their VPN. CloudStack does
not use its account database for this purpose but uses a separate table.
The VPN user database is shared across all the VPNs created by the
account owner. All VPN users get access to all VPNs created by the
account owner.

.. note::
   Make sure that not all traffic goes through the VPN. That is, the route
   installed by the VPN should be only for the guest network and not for
   all traffic.

-  **Road Warrior / Remote Access**. Users want to be able to connect
   securely from a home or office to a private network in the cloud.
   Typically, the IP address of the connecting client is dynamic and
   cannot be preconfigured on the VPN server.

-  **Site to Site**. In this scenario, two private subnets are connected
   over the public Internet with a secure VPN tunnel. The cloud user's
   subnet (for example, an office network) is connected through a
   gateway to the network in the cloud. The address of the user's
   gateway must be preconfigured on the VPN server in the cloud. Note
   that although L2TP-over-IPsec can be used to set up Site-to-Site
   VPNs, this is not the primary intent of this feature. For more
   information, see ":ref:`setting-s2s-vpn-conn`".


Configuring Remote Access VPN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To set up VPN for the cloud:

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, click Global Settings.

#. Set the following global configuration parameters.

   -  remote.access.vpn.client.ip.range - The range of IP addresses to
      be allocated to remote access VPN clients. The first IP in the
      range is used by the VPN server.

   -  remote.access.vpn.psk.length - Length of the IPSec key.

   -  remote.access.vpn.user.limit - Maximum number of VPN users per
      account.

To enable VPN for a particular network:

#. Log in as a user or administrator to the CloudStack UI.

#. In the left navigation, click Network.

#. Click the name of the network you want to work with.

#. Click Public IP Addresses.

#. Click one of the displayed IP address names.

#. Click the VPN Tab

#. Click the Enable Remote Access VPN. |vpn-icon.png|

   The IPsec key is displayed in a popup window.


Configuring Remote Access VPN in VPC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

On enabling Remote Access VPN on a VPC, any VPN client present outside
the VPC can access instances present in the VPC by using the Remote VPN
connection. The VPN client can be present anywhere except inside the VPC
on which the user enabled the Remote Access VPN service.

To enable VPN for a VPC:

#. Log in as a user or administrator to the CloudStack UI.

#. In the left navigation, click Network.

#. In the Select view, select VPC.

   All the VPCs that you have created for the account is listed in the
   page.

#. Click the Configure button of the VPC.

   For each Network Tier, the following options are displayed:

   -  Internal LB

   -  Public LB IP

   -  Static NAT

   -  Instances

   -  CIDR

   The following router information is displayed:

   -  Private Gateways

   -  Public IP Addresses

   -  Site-to-Site VPNs

   -  Network ACL Lists

#. In the Router node, select Public IP Addresses.

   The IP Addresses page is displayed.

#. Click Source NAT IP address.

#. Click the Enable VPN button. |vpn-icon.png|

   Click OK to confirm. The IPsec key is displayed in a pop-up window.

Now, you need to add the VPN users.

#. Click the Source NAT IP.

#. Select the VPN tab.

#. Add the username and the corresponding password of the user you
   wanted to add.

#. Click Add.

#. Repeat the same steps to add the VPN users.