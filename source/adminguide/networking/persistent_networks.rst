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


Persistent Networks
-------------------

The network that you can provision without having to deploy any instances on
it is called a persistent network. A persistent network can be part of a
VPC or a non-VPC environment.

When you create other types of network, a network is only a database
entry until the first instance is created on that network. When the first instance
is created, a VLAN ID is assigned and the network is provisioned. Also,
when the last instance is destroyed, the VLAN ID is released and the network
is no longer available. With the addition of persistent network, you
will have the ability to create a network in CloudStack in which
physical devices can be deployed without having to run any instances.
Additionally, you can deploy physical devices on that network.

One of the advantages of having a persistent network is that you can
create a VPC with a Network Tier consisting of only physical devices. For
example, you might create a VPC for a three-tier application, deploy instances
for Web and Application tier, and use physical machines for the Database
tier. Another use case is that if you are providing services by using
physical hardware, you can define the network as persistent and
therefore even if all its instances are destroyed the services will not be
discontinued.


Persistent Network Considerations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Persistent network is designed for isolated and L2 networks.

-  All default network offerings are non-persistent.

-  A network offering cannot be editable because changing it affects the
   behavior of the existing networks that were created using this
   network offering.

-  When you create a guest network, the network offering that you select
   defines the network persistence. This in turn depends on whether
   persistent network is enabled in the selected network offering.

-  Creation of an Isolated Persistent network will deploy a Virtual Router
   when the network is created.

-  Creation of an L2 Persistent network setups up the network devices namely,
   bridges, VLANs or port-groups across all hosts in a zone.

-  An existing network can be made persistent by changing its network
   offering to an offering that has the Persistent option enabled. While
   setting this property, even if the network has no running instances, the
   network is provisioned.

-  An existing network can be made non-persistent by changing its
   network offering to an offering that has the Persistent option
   disabled. If the network has no running instances, during the next network
   garbage collection run the network is shut down.

-  When the last instance on a network is destroyed, the network garbage
   collector checks if the network offering associated with the network
   is persistent, and shuts down the network only if it is
   non-persistent.


Creating a Persistent Guest Network
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a persistent network, perform the following:

#. Create a network offering with the Persistent option enabled.

   See `"Creating a New Network Offering"
   <networking.html#creating-a-new-network-offering>`_.

#. Select Network from the left navigation pane.

#. Select the guest network that you want to offer this network service
   to.

#. Click the Edit button.

#. From the Network Offering drop-down, select the persistent network
   offering you have just created.

#. Click OK.
