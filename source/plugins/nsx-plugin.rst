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


The VMware NSX Plugin
=====================

Introduction
------------

The VMware NSX Plugin introduces VMware NSX 4 as a network service provider in CloudStack to be able to create and manage Virtual Private Clouds (VPCs) in CloudStack, being able to orchestrate the following network functionalities:

- Routing between VPC network tiers (NSX segments)
- Access Lists (ACLs) between VPC tiers and "public" network (TCP, UDP, ICMP) both as global egress rules and “public” IP specific ingress rules.
- ACLs between VPC network tiers (TCP, UDP, ICMP)
- Port Forwarding between “public” networks and VPC network tier
- External load balancing – between VPCs network tiers and “public” networks (runs on Edge Cluster)
- Internal load balancing – between VPC network tiers
- Password injection, UserData and SSH Keys
- External, Internal DNS
- DHCP
- Kubernetes host orchestration, supporting CKS on VPCs

Supported versions
------------------

- VMware NSX 4.1, since CloudStack 4.20


 