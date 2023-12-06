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


Portable IPs
------------

About Portable IP
~~~~~~~~~~~~~~~~~

Portable IPs in CloudStack are region-level pool of IPs, which are
elastic in nature, that can be transferred across geographically
separated zones. As an administrator, you can provision a pool of
portable public IPs at region level and are available for user
consumption. The users can acquire portable IPs if admin has provisioned
portable IPs at the region level they are part of. These IPs can be use
for any service within an advanced zone. You can also use portable IPs
for EIP services in basic zones.

The salient features of Portable IP are as follows:

-  IP is statically allocated

-  IP need not be associated with a network

-  IP association is transferable across networks

-  IP is transferable across both Basic and Advanced zones

-  IP is transferable across VPC, non-VPC isolated and shared networks

-  Portable IP transfer is available only for static NAT.

.. note::
   Portable IPs is currently not supported in the new UI.
   To manage Portable IPs, please directly invoke the
   respective APIs or use `cloudmonkey <https://github.com/apache/cloudstack-cloudmonkey>`_,
   the CLI tool for cloudstack


Guidelines
^^^^^^^^^^

Before transferring to another network, ensure that no network rules
(Firewall, Static NAT, Port Forwarding, and so on) exist on that
portable IP.


Configuring Portable IPs
~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, click Regions.

#. Choose the Regions that you want to work with.

#. Click View Portable IP.

#. Click Portable IP Range.

   The Add Portable IP Range window is displayed.

#. Specify the following:

   -  **Start IP/ End IP**: A range of IP addresses that are accessible
      from the Internet and will be allocated to Guest Instances. Enter the
      first and last IP addresses that define a range that CloudStack
      can assign to Guest Instances.

   -  **Gateway**: The gateway in use for the Portable IP addresses you
      are configuring.

   -  **Netmask**: The netmask associated with the Portable IP range.

   -  **VLAN**: The VLAN that will be used for public traffic.

#. Click OK.


Acquiring a Portable IP
~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. Click the name of the network where you want to work with.

#. Click Public IP Addresses.

#. Click Acquire New IP.

   The Acquire New IP window is displayed.

#. Specify whether you want cross-zone IP or not.

#. Click Yes in the confirmation dialog.

   Within a few moments, the new IP address should appear with the state
   Allocated. You can now use the IP address in port forwarding or
   static NAT rules.


Transferring Portable IP
~~~~~~~~~~~~~~~~~~~~~~~~

An IP can be transferred from one network to another only if Static NAT
is enabled. However, when a portable IP is associated with a network,
you can use it for any service in the network.

To transfer a portable IP across the networks, execute the following
API:

.. code:: bash

   http://localhost:8096/client/api?command=enableStaticNat&response=json&ipaddressid=a4bc37b2-4b4e-461d-9a62-b66414618e36&virtualmachineid=a242c476-ef37-441e-9c7b-b303e2a9cb4f&networkid=6e7cd8d1-d1ba-4c35-bdaf-333354cbd49810

Replace the UUID with appropriate UUID. For example, if you want to
transfer a portable IP to network X and instance Y in a network, execute the
following:

.. code:: bash

   http://localhost:8096/client/api?command=enableStaticNat&response=json&ipaddressid=a4bc37b2-4b4e-461d-9a62-b66414618e36&virtualmachineid=Y&networkid=X
