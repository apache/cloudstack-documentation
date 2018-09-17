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


The OVS Plugin
==============

Introduction to the OVS Plugin
------------------------------

The OVS plugin is the native SDN
implementations in CloudStack, using GRE isolation method. The plugin can be 
used by CloudStack to implement isolated guest networks and to provide 
additional services like NAT, port forwarding and load balancing.


Features of the OVS Plugin
~~~~~~~~~~~~~~~~~~~~~~~~~~

The following table lists the CloudStack network services provided by
the OVS Plugin.

.. cssclass:: table-striped table-bordered table-hover

+----------------------+----------------------+
| Network Service      | CloudStack version   |
+======================+======================+
| Virtual Networking   | >= 4.0               |
+----------------------+----------------------+
| Static NAT           | >= 4.3               |
+----------------------+----------------------+
| Port Forwarding      | >= 4.3               |
+----------------------+----------------------+
| Load Balancing       | >= 4.3               |
+----------------------+----------------------+

Table: Supported Services

.. note::
   The Virtual Networking service was originally called 'Connectivity'
   in CloudStack 4.0

The following hypervisors are supported by the OVS Plugin.

.. cssclass:: table-striped table-bordered table-hover

+--------------+----------------------+
| Hypervisor   | CloudStack version   |
+==============+======================+
| XenServer    | >= 4.0               |
+--------------+----------------------+
| KVM          | >= 4.3               |
+--------------+----------------------+

Table: Supported Hypervisors


Configuring the OVS Plugin
--------------------------

Prerequisites
~~~~~~~~~~~~~

Before enabling the OVS plugin the hypervisor needs to be install OpenvSwitch. 
Default, XenServer has already installed OpenvSwitch. However, you must 
install OpenvSwitch manually on KVM. CentOS 6.4 and OpenvSwitch 1.10 are 
recommended.

KVM hypervisor:

-  CentOS 6.4 is recommended.

-  To make sure that the native bridge module will not interfere with 
   openvSwitch the bridge module should be added to the blacklist. See the 
   modprobe documentation for your distribution on where to find the blacklist. 
   Make sure the module is not loaded either by rebooting or executing rmmod 
   bridge before executing next steps.


Zone Configuration
~~~~~~~~~~~~~~~~~~

CloudStack needs to have at least one physical network with the isolation
method set to “GRE”. This network should be enabled for the Guest
traffic type.

.. note::
   With KVM, the traffic type should be configured with the traffic label
   that matches the name of the Integration Bridge on the hypervisor. For 
   example, you should set the traffic label as following:

   -  Management & Storage traffic: cloudbr0

   -  Guest & Public traffic: cloudbr1
      See KVM networking configuration guide for more detail.


.. figure:: /_static/images/ovs-physical-network-gre.png
   :align: center
   :alt: a screenshot of a physical network with the GRE isolation type


Agent Configuration
~~~~~~~~~~~~~~~~~~~

.. note::
   Only for KVM hypervisor

-  Configure network interfaces:

   ::
      
      /etc/sysconfig/network-scripts/ifcfg-eth0
      DEVICE=eth0
      BOOTPROTO=none
      IPV6INIT=no
      NM_CONTROLLED=no
      ONBOOT=yes
      TYPE=OVSPort
      DEVICETYPE=ovs
      OVS_BRIDGE=cloudbr0
    
      /etc/sysconfig/network-scripts/ifcfg-eth1
      DEVICE=eth1
      BOOTPROTO=none
      IPV6INIT=no
      NM_CONTROLLED=no
      ONBOOT=yes
      TYPE=OVSPort
      DEVICETYPE=ovs
      OVS_BRIDGE=cloudbr1
    
      /etc/sysconfig/network-scripts/ifcfg-cloudbr0
      DEVICE=cloudbr0
      ONBOOT=yes
      DEVICETYPE=ovs
      TYPE=OVSBridge
      BOOTPROTO=static
      IPADDR=172.16.10.10
      GATEWAY=172.16.10.1
      NETMASK=255.255.255.0
      HOTPLUG=no
    
      /etc/sysconfig/network-scripts/ifcfg-cloudbr1
      DEVICE=cloudbr1
      ONBOOT=yes
      DEVICETYPE=ovs
      TYPE=OVSBridge
      BOOTPROTO=none
      HOTPLUG=no
    
      /etc/sysconfig/network
      NETWORKING=yes
      HOSTNAME=testkvm1
      GATEWAY=172.10.10.1

-  Edit /etc/cloudstack/agent/agent.properties

   ::
      
      network.bridge.type=openvswitch
      libvirt.vif.driver=com.cloud.hypervisor.kvm.resource.OvsVifDriver


Enabling the service provider
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The OVS provider is disabled by default. Navigate to the "Network
Service Providers" configuration of the physical network with the GRE
isolation type. Navigate to the OVS provider and press the
"Enable Provider" button.

.. figure:: /_static/images/ovs-physical-network-gre-enable.png
   :align: center
   :alt: a screenshot of an enabled OVS provider


Network Offerings
~~~~~~~~~~~~~~~~~

Using the OVS plugin requires a network offering with Virtual
Networking enabled and configured to use the OVS element. Typical
use cases combine services from the Virtual Router appliance and the
OVS plugin.

.. cssclass:: table-striped table-bordered table-hover

+----------------------+-----------------+
| Service              | Provider        |
+======================+=================+
| VPN                  | VirtualRouter   |
+----------------------+-----------------+
| DHCP                 | VirtualRouter   |
+----------------------+-----------------+
| DNS                  | VirtualRouter   |
+----------------------+-----------------+
| Firewall             | VirtualRouter   |
+----------------------+-----------------+
| Load Balancer        | OVS             |
+----------------------+-----------------+
| User Data            | VirtualRouter   |
+----------------------+-----------------+
| Source NAT           | VirtualRouter   |
+----------------------+-----------------+
| Static NAT           | OVS             |
+----------------------+-----------------+
| Post Forwarding      | OVS             |
+----------------------+-----------------+
| Virtual Networking   | OVS             |
+----------------------+-----------------+

Table: Isolated network offering with regular services from the Virtual
Router.

.. figure:: /_static/images/ovs-network-offering.png
   :align: center
   :alt: a screenshot of a network offering.


.. note::
   The tag in the network offering should be set to the name of the
   physical network with the OVS provider.

Isolated network with network services. The virtual router is still
required to provide network services like dns and dhcp.

.. cssclass:: table-striped table-bordered table-hover

+----------------------+-----------------+
| Service              | Provider        |
+======================+=================+
| DHCP                 | VirtualRouter   |
+----------------------+-----------------+
| DNS                  | VirtualRouter   |
+----------------------+-----------------+
| User Data            | VirtualRouter   |
+----------------------+-----------------+
| Source NAT           | VirtualRouter   |
+----------------------+-----------------+
| Static NAT           | OVS             |
+----------------------+-----------------+
| Post Forwarding      | OVS             |
+----------------------+-----------------+
| Load Balancing       | OVS             |
+----------------------+-----------------+
| Virtual Networking   | OVS             |
+----------------------+-----------------+

Table: Isolated network offering with network services


Using the OVS plugin with VPC
-----------------------------

OVS plugin does not work with VPC at that time


DPDK Support
------------------------------

Since version 4.12 it is possible to enable DPDK support on CloudStack along with the OVS plugin.

Agent configuration
~~~~~~~~~~~~~~~~~~~

-  Edit /etc/cloudstack/agent/agent.properties to append DPDK support on ovs-vstcl commands for port creations

   ::
      
      openvswitch.dpdk.enable=true

Use DPDK on VM deployments
~~~~~~~~~~~~~~~~~~~~~~~~~~
Users are able to pass extra configurations as part of the 'deployVirtualMachine' API method.
These extra configurations are included on the resulting XML domain of the virtual machine.

Additional VM configuration
"""""""""""""""""""""""""""
The 'deployVirtualMachine' API method accepts a URL UTF-8 string encoded parameter 'extraconfig'.

Parameter is decoded following these rules:

- There could be multiple XML sections, separated by a new line
- Each section can be named, setting a title ending on ':' at the first line
- Double quotes instead of single quotes should be used
- Configurations are persisted as VM details, with the key: 'extraconfig-TITLE' or 'extraconfig-N' where N is a number.

-  Example:

   - In order to pass the below extra configuration to the VM, named 'config-1'

   ::
      
      config-1:
      <tag>
         <inner-tag>VALUE</inner-tag>
      </tag>

   - The 'extraconfig' parameter should receive the UTF-8 URL encoded string:

   ::
      
      config-1%3A%0A%3Ctag%3E%0A%20%20%20%3Cinner-tag%3EVALUE%3C%2Finner-tag%3E%0A%3C%2Ftag%3E

DPDK required configuration
"""""""""""""""""""""""""""

-  Set the global configuration to 'true' (as global setting or account setting)

   ::
      
      enable.additional.vm.configuration

-  Generate the UTF-8 URL encoded additional configuration to enable huge pages and NUMA, examples below:

   ::
      
      dpdk-hugepages:
      <memoryBacking>
         <hugepages>
         </hugepages>
      </memoryBacking>

      dpdk-numa:
      <cpu mode="host-passthrough">
         <numa>
            <cell id="0" cpus="0" memory="9437184" unit="KiB" memAccess="shared"/>
         </numa>
      </cpu>

- Pass the 'extraconfig' parameter to 'deployVirtualMachine' or 'updateVirtualMachine' API methods

   ::
      
      dpdk-hugepages%3A%0A%3CmemoryBacking%3E%0A%20%20%20%3Chugepages%3E%0A%20%20%20%20%3C%2Fhugepages%3E%0A%3C%2FmemoryBacking%3E%0A%0Adpdk-numa%3A%0A%3Ccpu%20mode%3D%22host-passthrough%22%3E%0A%20%20%20%3Cnuma%3E%0A%20%20%20%20%20%20%20%3Ccell%20id%3D%220%22%20cpus%3D%220%22%20memory%3D%229437184%22%20unit%3D%22KiB%22%20memAccess%3D%22shared%22%2F%3E%0A%20%20%20%3C%2Fnuma%3E%0A%3C%2Fcpu%3E%0A

- Additionally, users can pass extra configuration named 'dpdk-interface-source' as a special case to reference the dpdkvhostuser port. Example below:

   ::
      
      dpdk-interface-source:
      <source type="unix" path="/var/run/openvswitch/vhost-user-1" mode="client"/>


Revision History
----------------

0-0 Mon Dec 2 2013 Nguyen Anh Tu tuna@apache.org Documentation
created for 4.3.0 version of the OVS Plugin
