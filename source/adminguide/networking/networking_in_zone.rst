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


Networking in a Zone
--------------------

The following figure illustrates the network setup within a single zone.

|networksetupzone.png|

A firewall for management traffic operates in the NAT mode. The network
typically is assigned IP addresses in the 192.168.0.0/16 Class B private
address space. Each pod is assigned IP addresses in the 192.168.\*.0/24
Class C private address space.

Each zone has its own set of public IP addresses. Public IP addresses
from different zones do not overlap.


.. |networksetupzone.png| image:: /_static/images/network-setup-zone.png
   :alt: Depicts network setup in a single zone.