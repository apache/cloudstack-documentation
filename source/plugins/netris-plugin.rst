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

The Netris Plugin
=================

Introduction
------------

The Netris Plugin introduces Netris as a network service provider in CloudStack to be able to create and manage Virtual Private Clouds (VPCs) in CloudStack, being able to orchestrate the following network functionalities:

- Network segmentation with Netris-VXLAN isolation method
- Routing between “public” IP and network segments with an ACS ROUTED mode offering
- SourceNAT, DNAT, 1:1 NAT between “public” IP and network segments with an ACS NATTED mode offering
- Routing between VPC network segments (tiers in ACS nomenclature)
- Access Lists (ACLs) between VPC tiers and "public" network (TCP, UDP, ICMP) both as global egress rules and “public” IP specific ingress rules.
- ACLs between VPC network tiers (TCP, UDP, ICMP)
- External load balancing – between VPC network tiers and “public” IP
- Internal load balancing – between VPC network tiers
- CloudStack Virtual Router services (DHCP, DNS, UserData, Password Injection, etc…)


Supported Versions
------------------

.. cssclass:: table-striped table-bordered table-hover

+--------------+----------------------+----------------+
| Hypervisor   | CloudStack Version   | Netris Version |
+==============+======================+================+
| KVM          | >= 4.20              | 4.4.0          |
+--------------+----------------------+----------------+

Table: Supported Versions