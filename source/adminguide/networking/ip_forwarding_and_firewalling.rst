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


IP Forwarding and Firewalling
-----------------------------

By default, all incoming traffic to the public IP address is rejected.
All outgoing traffic from the guests is also blocked by default.

To allow outgoing traffic, follow the procedure in :ref:`egress-fw-rules`.

To allow incoming traffic, users may set up firewall rules and/or port
forwarding rules. For example, you can use a firewall rule to open a
range of ports on the public IP address, such as 33 through 44. Then use
port forwarding rules to direct traffic from individual ports within
that range to specific ports on user instances. For example, one port
forwarding rule could route incoming traffic on the public IP's port 33
to port 100 on one user instance's private IP.


Firewall Rules
~~~~~~~~~~~~~~

By default, all incoming traffic to the public IP address is rejected by
the firewall. To allow external traffic, you can open firewall ports by
specifying firewall rules. You can optionally specify one or more CIDRs
to filter the source IPs. This is useful when you want to allow only
incoming requests from certain IP addresses.

You cannot use firewall rules to open ports for an elastic IP address.
When elastic IP is used, outside access is instead controlled through
the use of security groups. See `"Adding a Security
Group" <#adding-a-security-group>`_.

In an advanced zone, you can also create egress firewall rules by using
the virtual router. For more information, see ":ref:`egress-fw-rules`".

Firewall rules can be created using the Firewall tab in the Management
Server UI. This tab is not displayed by default when CloudStack is
installed. To display the Firewall tab, the CloudStack administrator
must set the global configuration parameter firewall.rule.ui.enabled to
"true."

To create a firewall rule:

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. Click the name of the network where you want to work with.

#. Click Public IP Addresses tab.

#. Click the IP address you want to work with.

#. Click the Firewall tab and fill in the following values.

   -  **Source CIDR**: (Optional) To accept only traffic from IP
      addresses within a particular address block, enter a CIDR or a
      comma-separated list of CIDRs. Example: 192.168.0.0/22. Leave
      empty to allow all CIDRs.

   -  **Protocol**: The communication protocol in use on the opened
      port(s).

   -  **Start Port and End Port**: The port(s) you want to open on the
      firewall. If you are opening a single port, use the same number in
      both fields

   -  **ICMP Type and ICMP Code**: Used only if Protocol is set to ICMP.
      Provide the type and code required by the ICMP protocol to fill
      out the ICMP header. Refer to ICMP documentation for more details
      if you are not sure what to enter

#. Click Add.


.. _egress-fw-rules:

Egress Firewall Rules in an Advanced Zone
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The egress traffic originates from a private network to a public
network, such as the Internet. By default, the egress traffic is blocked
in default network offerings, so no outgoing traffic is allowed from a
guest network to the Internet. However, you can control the egress
traffic in an Advanced zone by creating egress firewall rules. When an
egress firewall rule is applied, the traffic specific to the rule is
allowed and the remaining traffic is blocked. When all the firewall
rules are removed the default policy, Block, is applied.


Prerequisites and Guidelines
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Consider the following scenarios to apply egress firewall rules:

-  The egress firewall rules are not supported on shared networks.

-  Allow the egress traffic from specified source CIDR. The Source CIDR
   is part of guest network CIDR.

-  Allow the egress traffic with protocol TCP,UDP,ICMP, or ALL.

-  Allow the egress traffic with protocol and destination port range.
   The port range is specified for TCP, UDP or for ICMP type and code.

-  The default policy is Allow for the new network offerings, whereas on
   upgrade existing network offerings with firewall service providers
   will have the default egress policy Deny.


Configuring an Egress Firewall Rule
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In Select view, choose Guest networks, then click the Guest network
   you want.

#. To add an egress rule, click the Egress rules tab and fill out the
   following fields to specify what type of traffic is allowed to be
   sent out of instances in this guest network:

   |egress-firewall-rule.png|

   -  **CIDR**: (Add by CIDR only) To send traffic only to the IP
      addresses within a particular address block, enter a CIDR or a
      comma-separated list of CIDRs. The CIDR is the base IP address of
      the destination. For example, 192.168.0.0/22. To allow all CIDRs,
      set to 0.0.0.0/0.

   -  **Protocol**: The networking protocol that instances uses to send
      outgoing traffic. The TCP and UDP protocols are typically used for
      data exchange and end-user communications. The ICMP protocol is
      typically used to send error messages or network monitoring data.

   -  **Start Port, End Port**: (TCP, UDP only) A range of listening
      ports that are the destination for the outgoing traffic. If you
      are opening a single port, use the same number in both fields.

   -  **ICMP Type, ICMP Code**: (ICMP only) The type of message and
      error code that are sent.

#. Click Add.


Configuring the Default Egress Policy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The default egress policy for Isolated guest network is configured by
using Network offering. Use the create network offering option to
determine whether the default policy should be block or allow all the
traffic to the public network from a guest network. Use this network
offering to create the network. If no policy is specified, by default
all the traffic is allowed from the guest network that you create by
using this network offering.

You have two options: Allow and Deny.

Allow
'''''

If you select Allow for a network offering, by default egress traffic is
allowed. However, when an egress rule is configured for a guest network,
rules are applied to block the specified traffic and rest are allowed.
If no egress rules are configured for the network, egress traffic is
accepted.

Deny
''''

If you select Deny for a network offering, by default egress traffic for
the guest network is blocked. However, when an egress rules is
configured for a guest network, rules are applied to allow the specified
traffic. While implementing a guest network, CloudStack adds the
firewall egress rule specific to the default egress policy for the guest
network.

This feature is supported only on the virtual router.

#. Create a network offering with your desirable default egress policy:

   #. Log in with admin privileges to the CloudStack UI.

   #. In the left navigation bar, click Service Offerings.

   #. In the left navigation bar, click Service Offerings and choose Network Offering.

   #. Click Add Network Offering.

   #. In the dialog, make necessary choices, including firewall
      provider.

   #. In the Default egress policy field, specify the behaviour.

   #. Click OK.

#. Create an isolated network by using this network offering.

   Based on your selection, the network will have the egress public
   traffic blocked or allowed.


Port Forwarding
~~~~~~~~~~~~~~~

A port forward service is a set of port forwarding rules that define a
policy. A port forward service is then applied to one or more Guest Instances.
The Guest Instance then has its inbound network access managed according to
the policy defined by the port forwarding service. You can optionally
specify one or more CIDRs to filter the source IPs. This is useful when
you want to allow only incoming requests from certain IP addresses to be
forwarded.

A Guest Instance can be in any number of port forward services. Port forward
services can be defined but have no members. If a Guest Instance is part of
more than one network, port forwarding rules will function only if they
are defined on the default network

You cannot use port forwarding to open ports for an elastic IP address.
When elastic IP is used, outside access is instead controlled through
the use of security groups. See Security Groups.

To set up port forwarding:

#. Log in to the CloudStack UI as an administrator or end user.

#. If you have not already done so, add a public IP address range to a
   zone in CloudStack. See Adding a Zone and Pod in the Installation
   Guide.

#. Add one or more instances to CloudStack.

#. In the left navigation bar, click Network.

#. Click the name of the guest network where the instances are running.

#. Choose an existing IP address or acquire a new IP address. See
   `"Acquiring a New IP Address" <#acquiring-a-new-ip-address>`_.
   Click the name of the IP address in the list.

#. Click the Port Forwarding tab.

#. Fill in the following:

   -  **Public Port**: The port to which public traffic will be
      addressed on the IP address you acquired in the previous step.

   -  **Private Port**: The port on which the instance is listening for
      forwarded public traffic.

   -  **Protocol**: The communication protocol in use between the two
      ports

#. Click Add.


.. |egress-firewall-rule.png| image:: /_static/images/egress-firewall-rule.png
   :alt: adding an egress firewall rule.
