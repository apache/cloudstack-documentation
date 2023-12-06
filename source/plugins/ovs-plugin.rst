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

.. warning::
   The OVS Plugin was not maintained in some CloudStack versions. Please use CloudStack
   4.16.0.0 and later. If you wish to use OVS as the default networking backend on Linux,
   only follow the Agent Configuration part of this guide.
   CloudStack will automatically detect it up based on the configuration in the
   agent.properties file. This in spite of the OVS Plugin not being shown in the
   Network Service Providers.


Introduction to the OVS Plugin
------------------------------

The OVS plugin is the native SDN
implementations in CloudStack, using GRE isolation method. The plugin can be
used by CloudStack to implement isolated guest Networks and to provide
additional services like NAT, port forwarding and load balancing.


Features of the OVS Plugin
~~~~~~~~~~~~~~~~~~~~~~~~~~

The following table lists the CloudStack Network services provided by
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

CloudStack needs to have at least one physical Network with the isolation
method set to “GRE”. This Network should be enabled for the Guest
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
   :alt: a screenshot of a physical Network with the GRE isolation type


Agent Configuration
~~~~~~~~~~~~~~~~~~~

.. note::
   Only for KVM hypervisor

-  Configure Network interfaces:

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
Service Providers" configuration of the physical Network with the GRE
isolation type. Navigate to the OVS provider and press the
"Enable Provider" button.

.. figure:: /_static/images/ovs-physical-network-gre-enable.png
   :align: center
   :alt: a screenshot of an enabled OVS provider


Network Offerings
~~~~~~~~~~~~~~~~~

Using the OVS plugin requires a Network offering with Virtual
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

Table: Isolated Network offering with regular services from the Virtual
Router.

.. figure:: /_static/images/ovs-network-offering.png
   :align: center
   :alt: a screenshot of a Network offering.


.. note::
   The tag in the Network offering should be set to the name of the
   physical Network with the OVS provider.

Isolated Network with Network services. The virtual router is still
required to provide Network services like dns and dhcp.

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

Table: Isolated Network offering with Network services


Using the OVS plugin with VPC
-----------------------------

OVS plugin does not work with VPC at that time


DPDK Support
------------------------------

Since version 4.12 it is possible to enable DPDK support on CloudStack along with the OVS plugin.

.. _Agent configuration for DPDK support:

Agent configuration
~~~~~~~~~~~~~~~~~~~

-  Edit /etc/cloudstack/agent/agent.properties to enable DPDK support on the agent and on ovs-vstcl commands for port creations as well as the path to OVS ports (usually: /var/run/openvswitch)

   ::

      openvswitch.dpdk.enabled=true
      openvswitch.dpdk.ovs.path=OVS_PATH

Agent should be restarted for actions to take effect.

When the host agent connects to the management server, it sends the list of hosts capabilities. When DPDK support is enabled on the host, the capability with name 'dpdk' is sent to the management server. The list of host capabilities are persisted on the 'capabilities' column on 'hosts' table, and can be retrieved by the 'listHosts' API method:

::

      list hosts id=HOST_ID filter=capabilities

Additional Instance configurations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In order to enable DPDK on Instance deployments, users should pass addition configuration to Instances. The required configurations are listed on the next section. Administrators can allow users to pass additional configurations to their Instances by the Account scoped setting:

::

      enable.additional.vm.configuration

Users are able to pass extra configurations as part of the 'deployVirtualMachine' or 'updateVirtualMachine' API methods.
These extra configurations are included on the resulting XML domain of the Instance and are also persisted on CloudStack database as details on the 'user_vm_details' table.

The 'deployVirtualMachine' and 'updateVirtualMachine' API methods accept a URL UTF-8 string encoded parameter 'extraconfig'.

Parameter is decoded following these rules:

- There could be multiple XML sections, separated by a new line
- Each section can be named, setting a title ending on ':' at the first line
- Double quotes instead of single quotes should be used
- Configurations are persisted as Instance details, with the key: 'extraconfig-TITLE' or 'extraconfig-N' where N is a number.

Example:

In order to pass the below extra configuration to the Instance, named 'config-1'

::

      config-1:
      <tag>
         <inner-tag>VALUE</inner-tag>
      </tag>

The 'extraconfig' parameter should receive the UTF-8 URL encoded string:

::

      config-1%3A%0A%3Ctag%3E%0A%20%20%20%3Cinner-tag%3EVALUE%3C%2Finner-tag%3E%0A%3C%2Ftag%3E

On 'user_vm_details' table the additional configuration is persisted with key: 'extraconfig-config-1'


Additional configurations to enable DPDK on Instances
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To enable DPDK on Instance deployments:

-  Set the global configuration to 'true' (as global setting or Account setting)

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

- Pass the 'extraconfig' parameter to 'deployVirtualMachine' or 'updateVirtualMachine' API methods as a single UTF-8 URL encoded string containing multiple extra configurations (as shown above). Note: if multiple extra configurations are needed, follow the example above and add new sections separated by an empty line, encode the whole string and pass it as a single string to the APIs as 'extraconfig' parameter.

   ::

      deployVirtualMachine extraconfig=dpdk-hugepages%3A%0A%3CmemoryBacking%3E%0A%20%20%20%3Chugepages%3E%0A%20%20%20%20%3C%2Fhugepages%3E%0A%3C%2FmemoryBacking%3E%0A%0Adpdk-numa%3A%0A%3Ccpu%20mode%3D%22host-passthrough%22%3E%0A%20%20%20%3Cnuma%3E%0A%20%20%20%20%20%20%20%3Ccell%20id%3D%220%22%20cpus%3D%220%22%20memory%3D%229437184%22%20unit%3D%22KiB%22%20memAccess%3D%22shared%22%2F%3E%0A%20%20%20%3C%2Fnuma%3E%0A%3C%2Fcpu%3E%0A

- Additionally, users can pass extra configuration named 'dpdk-interface-TAG' to be included on Instances interfaces definition. Example below:

   ::

      dpdk-interface-model:
      <model type='virtio'/>

DPDK vHost User mode selection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The vHost user mode describes a client/server model between Openvswitch along with DPDK and QEMU, in which one acts as client while the other as server. The server creates and manages the vHost user sockets and the client connects to the sockets created by the server:

- DPDK vHost user server mode:
   - Is the default configuration.
   - OVS with DPDK acts as the server, while QEMU acts as the client.
   - The port types used are: dpdkvhostuser

- DPDK vHost user client mode:
   - OVS with DPDK acts as the client and QEMU acts as the server.
   - If Openvswitch is restarted then the sockets can reconnect to the existing sockets on the server, and normal connectivity can be resumed.
   - The port types used are: dpdkvhostuserclient

Applying additional configurations via service offerings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is possible to avoid passing additional configuration on each Instance deployment, but setting these configurations on a service offering, and those are passed to the Instance.

- To create a service offering with additional configurations, pass each key/value pair as service offering details on service offering creation, with keys starting with the "extraconfig" keyword, and each value an URL UTF-8 encoded string.
- Additional configurations are stored as service offering details

For example, applying DPDK additional configurations via service offering:

::

   create serviceoffering name=<NAME> displaytext=<NAME> serviceofferingdetails[0].key=extraconfig-dpdk-hugepages serviceofferingdetails[0].value=%3CmemoryBacking%3E%20%3Chugepages%2F%3E%20%3C%2FmemoryBacking%3E serviceofferingdetails[1].key=extraconfig-dpdk-numa serviceofferingdetails[1].value=%3Ccpu%20mode%3D%22host-passthrough%22%3E%20%3Cnuma%3E%20%3Ccell%20id%3D%220%22%20cpus%3D%220%22%20memory%3D%229437184%22%20unit%3D%22KiB%22%20memAccess%3D%22shared%22%2F%3E%20%3C%2Fnuma%3E%20%3C%2Fcpu%3E

The preferred DPDK vHost User Mode must be passed as a service offering detail, with special key name: "DPDK-VHOSTUSER". Possible values are: "client" or "server". The following table illustrates the expected behaviour on DPDK ports and Instance guest interfaces.

By default, the server mode is assumed if it is not passed as a service offering detail.

+----------------------+------------------------+-------------------------------+
| DPDK vHost User Mode | OVS port creation type | Instance guest interface mode |
+======================+========================+===============================+
| server               | dpdkvhostuser          |           client              |
+----------------------+------------------------+-------------------------------+
| client               | dpdkvhostuserclient    |           server              |
+----------------------+------------------------+-------------------------------+

::

   create serviceoffering name=<NAME> displaytext=<NAME> serviceofferingdetails[0].key=DPDK-VHOSTUSER serviceofferingdetails[0].value=client serviceofferingdetails[1].key=extraconfig-dpdk-hugepages serviceofferingdetails[1].value=%3CmemoryBacking%3E%20%3Chugepages%2F%3E%20%3C%2FmemoryBacking%3E serviceofferingdetails[2].key=extraconfig-dpdk-numa serviceofferingdetails[2].value=%3Ccpu%20mode%3D%22host-passthrough%22%3E%20%3Cnuma%3E%20%3Ccell%20id%3D%220%22%20cpus%3D%220%22%20memory%3D%229437184%22%20unit%3D%22KiB%22%20memAccess%3D%22shared%22%2F%3E%20%3C%2Fnuma%3E%20%3C%2Fcpu%3E

DPDK Instances live migrations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
It is possible to perform live migrations of DPDK enabled Instances since CloudStack version 4.13. DPDK enabled Instances can be migrated between hosts in the same cluster which are both DPDK enabled.

CloudStack determines that an Instance is a DPDK enabled VM when the following conditions are met:

- The Instance is a user Instance
- The Instance state is Running
- The host in which the Instance is running is a DPDK enabled host (i.e. host contains the 'dpdk' capability as part of its capabilities. Check `Agent configuration for DPDK support`_.)
- The Instance acquires the DPDK required configurations via Instance details or service offering details. DPDK required additional configurations are additional configurations with name:
   - 'extraconfig-dpdk-numa'
   - 'extraconfig-dpdk-hugepages'

DPDK enabled Instances can only be migrated between DPDK enabled hosts. Therefore the 'findHostsForMigration' API method excludes non-DPDK enabled hosts from the list of suitable hosts to migrate DPDK enabled Instances.

DPDK ports
~~~~~~~~~~
When an Instance is created or started, CloudStack creates ports with DPDK support with format: "csdpdk-N" where N is a number, incremented on new ports creation. This port is set into the 'source' property of the 'interface' tag on the XML domain of the Instance, prepended by the value of the OVS path set on the property:

::

      openvswitch.dpdk.ovs.path=OVS_PATH

That would set interfaces to type 'vhostuser' and reference the ports created in the XML domain of the Instances as:

::

      <interface type='vhostuser'>
         <source type="unix" path="<OVS_PATH>/<port_name>" .../>
         ...
      </interface>

Note that the OVS_PATH property is required, as explained on `Agent configuration for DPDK support`_. For example, when OVS_PATH is set to the default path for Openvswitch (/var/run/openvswitch), interfaces will reference created ports on: /var/run/openvswitch/<port_name>

Revision History
----------------

0-0 Mon Dec 2 2013 Nguyen Anh Tu tuna@apache.org Documentation
created for 4.3.0 version of the OVS Plugin
