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


Networking in a Pod
-------------------

The figure below illustrates network setup within a single pod. The
hosts are connected to a pod-level switch. At a minimum, the hosts
should have one physical uplink to each switch. Bonded NICs are
supported as well. The pod-level switch is a pair of redundant gigabit
switches with 10 G uplinks.

|networksinglepod.png| 

Servers are connected as follows:

-  Storage devices are connected to only the network that carries
   management traffic.

-  Hosts are connected to networks for both management traffic and
   public traffic.

-  Hosts are also connected to one or more networks carrying guest
   traffic.

We recommend the use of multiple physical Ethernet cards to implement
each network interface as well as redundant switch fabric in order to
maximize throughput and improve reliability.


.. |networksinglepod.png| image:: /_static/images/network-singlepod.png
   :alt: diagram showing logical view of network in a pod.