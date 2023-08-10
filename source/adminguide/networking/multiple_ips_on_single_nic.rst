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


Configuring Multiple IP Addresses on a Single NIC
-------------------------------------------------

CloudStack provides you the ability to associate multiple private IP
addresses per Guest Instance NIC. In addition to the primary IP, you can
assign additional IPs to the Guest Instance NIC. This feature is supported on
all the network configurations: Basic, Advanced, and VPC. Security
Groups, Static NAT and Port forwarding services are supported on these
additional IPs.

As always, you can specify an IP from the guest subnet; if not
specified, an IP is automatically picked up from the Guest Instance subnet.
You can view the IPs associated with for each Guest Instance NICs on the UI.
You can apply NAT on these additional guest IPs by using network
configuration option in the CloudStack UI. You must specify the NIC to
which the IP should be associated.

This feature is supported on XenServer, KVM, and VMware hypervisors.
Note that Basic zone security groups are not supported on VMware.


Use Cases
~~~~~~~~~

Some of the use cases are described below:

-  Network devices, such as firewalls and load balancers, generally work
   best when they have access to multiple IP addresses on the network
   interface.

-  Moving private IP addresses between interfaces or instances.
   Applications that are bound to specific IP addresses can be moved
   between instances.

-  Hosting multiple SSL Websites on a single instance. You can install
   multiple SSL certificates on a single instance, each associated with
   a distinct IP address.


Guidelines
~~~~~~~~~~

To prevent IP conflict, configure different subnets when multiple
networks are connected to the same instance.


Assigning Additional IPs to an instance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI.

#. In the left navigation bar, click Instances.

#. Click the name of the instance you want to work with.

#. Click the NICs tab.

#. Click View Secondary IPs.

#. Click Acquire New Secondary IP, and click Yes in the confirmation
   dialog.

   You need to configure the IP on the Guest Instance NIC manually. CloudStack
   will not automatically configure the acquired IP address on the instance.
   Ensure that the IP address configuration persist on instance reboot.

   Within a few moments, the new IP address should appear with the state
   Allocated. You can now use the IP address in Port Forwarding or
   StaticNAT rules.


Port Forwarding and StaticNAT Services Changes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Because multiple IPs can be associated per NIC, you are allowed to
select a desired IP for the Port Forwarding and StaticNAT services. The
default is the primary IP. To enable this functionality, an extra
optional parameter 'vmguestip' is added to the Port forwarding and
StaticNAT APIs (enableStaticNat, createIpForwardingRule) to indicate on
what IP address NAT need to be configured. If vmguestip is passed, NAT
is configured on the specified private IP of the instance. if not passed, NAT
is configured on the primary IP of the instance.
