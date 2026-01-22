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

   

All Object Types in Apache CloudStack
-------------------------------------

.. cssclass:: table-striped table-bordered table-hover

=========================  ===================================
Object Name                    Description                    
=========================  ===================================
 Account                   A CloudStack account is a group of users. An account is used to manage users and resources. Each resource is owned by an account. Resources can be shared between accounts within the same domain.   
 Affinity Group            An affinity group is a way to group instances together on the same host or to keep them apart. Affinity groups are defined at the account level and can be applied to instances at the time of deployment.
 Alert                     Alerts are used to notify administrators of system events. Alerts can be generated for various events
 Cluster                   A cluster is a collection of hosts. A cluster contains hosts that are managed by the same hypervisor. A cluster is contained within a zone and can contain primary storage.
 Disk Offering             A disk offering defines the characteristics of a disk volume. A disk offering specifies the size of the disk volume and whether it is local or shared storage.
 Domain                    A domain is a hierarchical administrative unit within CloudStack. Domains are used to partition the CloudStack environment into separate sections. Each domain can have its own administrators, users, and resources. Domains can be nested to create a hierarchy.
 Event                     Events are used to track system activity. Events are generated for various actions taken by users and administrators.
 Global Settings           Global settings are configuration parameters that apply to the entire CloudStack environment.
 Host                      A host is a physical server that runs the hypervisor software. Hosts are grouped into clusters and are contained within a zone.
 Hypervisor                A hypervisor is the software that enables virtualization. CloudStack supports several hypervisors, including KVM, XenServer, VMware, and Hyper-V.
 Instance                  An Instance is a virtual machine that runs on a host. Historically they were called Virtual Machines, so CloudStack APIs are named after that. Instances are created from templates and can be managed by users and administrators.
 IP Address                An IP address is a unique identifier assigned to an instance or a network interface. IP addresses can be either public or private.
 ISO Image                 An ISO image is a disk image that contains an operating system or other software. ISO images can be used to create instances or to install software on existing instances.
 Load Balancer             A load balancer is a device that distributes network traffic across multiple instances. Load balancers can be used to improve performance and availability.
 Network                   A Network is a virtual network that connects instances and other resources. Networks can be either isolated or shared.
 Network Offering          A network offering defines the characteristics of a network. A network offering specifies the type of network, the services it provides, and the traffic types it supports.
 Physical Network          A physical network is a representation of the underlying physical network infrastructure. Physical networks can be used to define how virtual networks are mapped to physical networks.
 Pod                       A pod is a collection of hosts within a zone. Pods are used to group hosts that are in the same physical location.
 Primary Storage           Primary storage is the storage that is used to store virtual machine disk volumes. Primary storage can be either local or shared storage.
 Project                   A project is a way to group resources together for a specific purpose. Projects can be used to manage resources for a specific team or application.
 Resource Tag              Resource tags are labels that can be applied to resources to help organize and manage them.
 Secondary Storage         Secondary storage is the storage that is used to store templates, ISO images, and snapshots. Secondary storage is typically shared storage.
 Security Group            A security group is a virtual firewall that controls inbound and outbound traffic to instances. Security groups can be used to restrict access to instances based on IP address, port, and protocol.
 Service Offering          A service offering defines the characteristics of an instance. A service offering specifies the CPU, memory, and other resources that are allocated to an instance.
 Snapshot                  A snapshot is a point-in-time copy of a disk volume. Snapshots can be used to back up data or to create new disk volumes.
 SSH Key Pair              An SSH key pair is a pair of cryptographic keys that are used to authenticate users when they connect to instances via SSH.
 Storage Pool              A storage pool is a collection of storage resources that can be used to store virtual machine disk volumes. Storage pools can be either local or shared storage.
 Template                  A Template is a pre-configured disk image that contains an operating system and other software. Templates can be used to create instances.    
 User                      A User is an individual who has access to the CloudStack environment. Users can be assigned to accounts and can have different roles and permissions.   
 VLAN                      A VLAN (Virtual Local Area Network) is a logical partition of a physical network. VLANs can be used to isolate network traffic and improve security.
 VPC                       A VPC (Virtual Private Cloud) is a virtual network that is isolated from other networks. VPCs can be used to create a private cloud environment within CloudStack.
 Volume                    A volume is a virtual disk that can be attached to an instance. Volumes can be created from templates, snapshots, or other volumes.
 Zone                      A zone is a top-level container for resources. A zone contains clusters, pods, and primary storage. Zones can be used to represent different geographical locations or different environments (e.g., production, development).                                
=========================  ===================================
