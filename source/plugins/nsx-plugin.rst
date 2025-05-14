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
- Password injection, User Data and SSH Keys
- External, Internal DNS
- DHCP
- Kubernetes host orchestration, supporting CKS on VPCs

Supported Versions
------------------

.. cssclass:: table-striped table-bordered table-hover

+--------------+----------------------+--------------------+
| Hypervisor   | CloudStack Version   | VMware NSX Version |
+==============+======================+====================+
| VMware       | >= 4.20              | 4.1                |
+--------------+----------------------+--------------------+

Table: Supported Versions

Configuration
-------------

Prerequisites
~~~~~~~~~~~~~

The VMware NSX plugin is enabled by the 'nsx.plugin.enable' setting, false by default. It enables the NSX Plugin on CloudStack when it is set to true. The global setting is non-dynamic, that is, the management server would need to be restarted after being modified.

Prior to creating the zone, ensure that the global setting: 'vmware.management.portgroup' is set to the correct management network for ESXi hosts. 

Zone creation
~~~~~~~~~~~~~

For an NSX-based zone, the administrator will have to create atleast 2 physical networks, one for Public and Guest networks with **NSX** isolation method and one for Management (and / or storage networks),
which uses VLAN isolation method.

**Physical network for Public and Guest traffic:**
   Isolation method: NSX
   VLAN ID must be empty 
   vSwitch type: distributed virtual switch (dvSwitch)
   vSwitch name: name of the dvSwitch to handle NSX traffic 

**Phsyical network for Management traffic:**
   Isolation method: VLAN
   VLAN ID: ID for Management traffic
   vSwitch type: distributed virtual switch (dvSwitch)
   vSwitch name: name of the dvSwitch to handle Management traffic.


An example of physical networks setup: 

.. |nsx-phy-networks.png| image:: /_static/images/nsx-phy-networks.png
   :alt: Physical Networks with NSX

The next stage of zone creation would be to link the NSX controller to the CloudStack. 

.. |nsx-provider.png| image:: /_static/images/nsx-provider.png
   :alt: NSX Provider details

The administrator then needs to setup the IP ranges for Public and NSX Public traffic.
   - Public Traffic: IP range for non-NSX public traffic used by system VMs 
   - NSX Public Traffic: IP range to use for Public IP Addresses on NSX-based VPCs or Isolated Networks.

.. |nsx-public-traffic.png| image:: /_static/images/nsx-public-traffic.png
   :alt: NSX Traffic

The subsequent steps of zone creation remain unchanged and once the zone is successfully created and enabled, the system VMs come up with IPs from the Public IP Range (not the NSX public IP range).

VPC creation on NSX
~~~~~~~~~~~~~~~~~~~~

When a VPC is created in CloudStack, the following operations occur on NSX end:
   - CloudStack creates a Tier1 Gateway with the following: 

      - ID and name on NSX: D<d_id>-A<a_id>-Z<z_id>-V<v_id> 
      - Linked Tier0 Gateway: the Tier0 Gateway provided on the NSX Controller creation in CloudStack
      - For NAT mode VPCs, the following Route Advertisement settings are enabled: 
            - All IPSec Local Endpoints 
            - All NAT IPs 
            - All LB VIP Routes 
      - For ROUTED mode VPCs, the following Route Advertisement settings are enabled: 
            - All IPSec Local Endpoints 
            - All NAT IPs 
            - All LB VIP Routes  
            - All Connected Segments & Service Ports 

      - The VPC Virtual Router acquires a free IP address on from the NSX Public Range and sets it as the Source NAT IP of the VPC.
      - A new NAT Rule is created on NSX: 
         - ID and Name: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-NAT 
         - Action: SNAT 
         - Source IP: Any 
         - Destination IP: Any 
         - Translated IP: The Source NAT IP of the VPC (selected from the NSX Public Range) 
      

VPC Tier creation on NSX
~~~~~~~~~~~~~~~~~~~~~~~~~

On VPC network tier creation, CloudStack creates the following NSX elements: 
   - A Segment is linked to the VPC Tier1 Gateway with the following: 
      - ID and name on NSX: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-S<s_id> 
      - Linked Tier1 Gateway: The VPC Tier1 Gateway with name: D<d_id>-A<a_id>-Z<z_id>-V<v_id> 
      - Linked Transport Zone: The Transport Zone provided on NSX Controller creation in CloudStack 
      - Subnets: The VPC network tier CIDR provided on CloudStack 
   
   - A Group under Inventory with the following: 
      - ID and name on NSX: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-S<s_id> (same as the segment) 
      - Group members: The created NSX segment    

VPC network ACL creation
~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack allows creating ACL rules for NSX based network tiers. The supported protocols for creating NSX based ACL rules are:are TCP, UDP and ICMP. 
Network ACLs can be assigned to any network tier in the VPC during network tier creation or an existing ACL on the network tier can be replaced. 

VPC tier Implementation
~~~~~~~~~~~~~~~~~~~~~~~~

When the first VM is created on the network tier, CloudStack creates the following NSX elements:

   - A DHCP Relay Networking Profile is created; associated to the segment: 
      - ID and name: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-S<s_id>-Relay 
      - Server IP address: A free IP on the network tier CIDR is selected.  

   - A Distributed Firewall policy:
      - ID and name: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-S<s_id> (same as the segment) 
      - Applied to the Group: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-S<s_id> 

   - Distributed Firewall policy rules under the created policy:
      - ID and name: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-S<s_id>-R<r_id> where r_id is the 'id' column on the 'network_acl_items' table for all the rules on the selected Network ACL 
      - Action: Allow or Drop depending on the CloudStack ALC rule action (Allow or Deny) 
      - Service: 
         - Any: for the default 'Allow all' and 'Deny all' CloudStack ACLs  
         - In case there is a default service for the selected protocol and port then CloudStack uses the pre-existing one. In case it does not exist, then a new service is created, matching the protocol

   - After acquiring a new Public IP Address on a VPC, users can:    
      - Make the acquired IP address the Source NAT IP: This will replace the current NAT rule associated with the VPC Tier 1 Gateway, replacing the Translated IP for the new one. 
      - Enable Static NAT: a new NAT rule is created on NSX with: 
         - ID and name: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-STATICNAT 
         - Action: DNAT
         - Destination IP: The acquired NSX Public IP address
         - Translated IP: The Guest VM IP address

      - Create Port Forwarding rules: For each CloudStack Port Forwarding rule, a new NAT rule is created on NSX, with:
         - ID and name: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-PF<pf_id> where pf_id is the 'id' column on the 'port_forwarding_rules' table, for the created rule
         - Gateway: The VPC Tier 1 Gateway (with name D<d_id>-A<a_id>-Z<z_id>-V<v_id>)
         - Action: DNAT 
         - Source IP: Any 
         - Destination IP: The acquired NSX Public IP address 
         - Destination Port: The start-end port range 
         - Translated IP: The guest IP of the VM 
         - Translated Port: The start-end port range  

      - Create Load Balancing rules: There will be one load balancer created per VPC if load balancer rules are created for a specific VPC. For every subsequent load balancer rule created, additional virtual servers and server pools are added to the load balancer:
         - ID and name: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-LB<lb_id> where lb_id is the 'id' column on the 'load_balancing_rules' table, for the created rule 
         - Attachment: Tier 1 Gateway with ID and name: D<d_id>-A<a_id>-Z<z_id>-V<v_id> 
         - Virtual Server: a new Virtual Server is created, with:
            - ID and name: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-LB<lb_id>-VS 
            - IP address: The acquired NSX Public IP address 
            - Port: The public port 
            - Type: TCP or UDP depending on the selected protocol 
         - Server Pool: a new Server Pool is created, with:
            - ID and name: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-LB<lb_id>-SP
            - Algorithm: Supported values: Round-robin, least connection
            - Members: All the selected VMs are added as server pool members, with:
               - ID and name: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-VM<vm_id> 
               - IP address: The VM Guest IP address 
               - Port: The private port 
            - Active Monitor: a new Active Monitor is created, with: 
               - ID and name: D<d_id>-A<a_id>-Z<z_id>-V<v_id>-LB<lb_id>-SP-<PROTO>-<PORT>-AM, where PROTO is the selected Protocol, and PORT is the selected Private Port
            - Passive Monitor: default passive monitor

.. note::

The following notations were used in the above section: 

   - d_id: the 'id' column on the 'domain' table for the caller domain 
   - a_id: the 'id' column of the 'accounts' table for the owner account 
   - z_id: the 'id' column of the 'datacenter' table for the zone 
   - v_id: the 'id' column of the 'vpcs' table for the new VPC being created 
   - s_id: the 'id' column of the 'networks' table for the network tier being created 


CKS on NSX
~~~~~~~~~~~

To enable CKS clusters on NSX networks respective default network offerings have been created for isolated and VPC tiers. 

**DefaultNSXNetworkOfferingforKubernetesService** - is the default pre-created NSX-based network offering for enabling deployment of CKS clusters on isolated networks. 
**DefaultNSXVPCNetworkOfferingforKubernetesService** - is the default pre-created NSX-based network offering to enable CKS cluster deployment on VPC tiers. 
 

When deploying CKS clusters, it is possible to either select a pre-existing network or allow CloudStack create a new network for the cluster during the deployment. If one chooses the latter means of cluster deployment on a NSX-based environment, it would be needed that the 'cloud.kubernetes.cluster.network.offering' global setting be updated to point to either the default offerings or the appropriate NSX-based offering created. 

All the network resources required by the CKS cluster such as load balancer, firewall rules, port forwarding rules, etc., will be created on and provided by NSX. 

Additional Notes 
~~~~~~~~~~~~~~~~~

- Ports 67-68 need to be manually opened for network tiers of VPCs created in NSX based zones with default_deny ACL for DHCP to work as expected. 
- When creating routed VPC networks in NSX-enabled zones, ensure that no 2 VPCs use the same CIDR, to prevent IP conflicts upstream (BGP). 