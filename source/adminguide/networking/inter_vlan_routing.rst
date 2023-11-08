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
   

About Inter-VLAN Routing (nTier Apps)
-------------------------------------

Inter-VLAN Routing (nTier Apps) is the capability to route network
traffic between VLANs. This feature enables you to build Virtual Private
Clouds (VPC), an isolated segment of your cloud, that can hold
multi-tier applications. These tiers are deployed on different VLANs
that can communicate with each other. You provision VLANs to the tiers
your create, and instances can be deployed on different tiers. The VLANs are
connected to a virtual router, which facilitates communication between
the instances. In effect, you can segment instances by means of VLANs into different
networks that can host multi-tier applications, such as Web,
Application, or Database. Such segmentation by means of VLANs logically
separate application instances for higher security and lower broadcasts, while
remaining physically connected to the same device.

This feature is supported on XenServer, KVM, and VMware hypervisors.

The major advantages are:

-  The administrator can deploy a set of VLANs and allow users to deploy
   instances on these VLANs. A guest VLAN is randomly allotted to an account
   from a pre-specified set of guest VLANs. All the instances of a certain
   tier of an account reside on the guest VLAN allotted to that account.

   .. note:: 
      A VLAN allocated for an account cannot be shared between multiple accounts.

-  The administrator can allow users create their own VPC and deploy the
   application. In this scenario, the instances that belong to the account are
   deployed on the VLANs allotted to that account.

-  Both administrators and users can create multiple VPCs. The guest
   network NIC is plugged to the VPC virtual router when the first instance is
   deployed in a tier.

-  The administrator can create the following gateways to send to or
   receive traffic from the instances:

   -  **VPN Gateway**: For more information, see `"Creating a VPN gateway for the
      VPC" <#creating-a-vpn-gateway-for-the-vpc>`_.

   -  **Public Gateway**: The public gateway for a VPC is added to the
      virtual router when the virtual router is created for VPC. The
      public gateway is not exposed to the end users. You are not
      allowed to list it, nor allowed to create any static routes.

   -  **Private Gateway**: For more information, see ":ref:`adding-priv-gw-vpc`".

-  Both administrators and users can create various possible
   destinations-gateway combinations. However, only one gateway of each
   type can be used in a deployment.

   For example:

   -  **VLANs and Public Gateway**: For example, an application is
      deployed in the cloud, and the Web application instances communicate
      with the Internet.

   -  **VLANs, VPN Gateway, and Public Gateway**: For example, an
      application is deployed in the cloud; the Web application instances
      communicate with the Internet; and the database instances communicate
      with the on-premise devices.

-  The administrator can define Network Access Control List (ACL) on the
   virtual router to filter the traffic among the VLANs or between the
   Internet and a VLAN. You can define ACL based on CIDR, port range,
   protocol, type code (if ICMP protocol is selected) and Ingress/Egress
   type.

The following figure shows the possible deployment scenarios of a
Inter-VLAN setup:

|mutltier.png|

To set up a multi-tier Inter-VLAN deployment, see ":ref:`configuring-vpc`".


.. |mutltier.png| image:: /_static/images/multi-tier-app.png
   :alt: a multi-tier setup.
