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


The Nicira NVP Plugin
=====================

Introduction to the Nicira NVP Plugin
-------------------------------------

The Nicira NVP plugin adds Nicira NVP as one of the available SDN
implementations in CloudStack. With the plugin an existing Nicira NVP
setup can be used by CloudStack to implement isolated guest Networks and
to provide additional services like routing and NAT.


Features of the Nicira NVP Plugin
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following table lists the CloudStack Network services provided by
the Nicira NVP Plugin.

.. cssclass:: table-striped table-bordered table-hover

+----------------------+----------------------+---------------+
| Network Service      | CloudStack version   | NVP version   |
+======================+======================+===============+
| Virtual Networking   | >= 4.0               | >= 2.2.1      |
+----------------------+----------------------+---------------+
| Source NAT           | >= 4.1               | >= 3.0.1      |
+----------------------+----------------------+---------------+
| Static NAT           | >= 4.1               | >= 3.0.1      |
+----------------------+----------------------+---------------+
| Port Forwarding      | >= 4.1               | >= 3.0.1      |
+----------------------+----------------------+---------------+

Table: Supported Services

.. note::
   The Virtual Networking service was originally called 'Connectivity'
   in CloudStack 4.0

The following hypervisors are supported by the Nicira NVP Plugin.

.. cssclass:: table-striped table-bordered table-hover

+--------------+----------------------+
| Hypervisor   | CloudStack version   |
+==============+======================+
| XenServer    | >= 4.0               |
+--------------+----------------------+
| KVM          | >= 4.1               |
+--------------+----------------------+

Table: Supported Hypervisors

.. note::
   Please refer to the Nicira NVP configuration guide on how to prepare
   the hypervisors for Nicira NVP integration.


Configuring the Nicira NVP Plugin
---------------------------------

Prerequisites
~~~~~~~~~~~~~

Before enabling the Nicira NVP plugin the NVP Controller needs to be
configured. Please review the NVP User Guide on how to do that.

Make sure you have the following information ready:

-  The IP address of the NVP Controller

-  The username to access the API

-  The password to access the API

-  The UUID of the Transport Zone that contains the hypervisors in this
   Zone

-  The UUID of the Gateway Service used to provide router and NAT
   services.


.. note::
   The gateway service uuid is optional and is used for Layer 3
   services only (SourceNat, StaticNat and PortForwarding)


Zone Configuration
~~~~~~~~~~~~~~~~~~

CloudStack needs to have at least one physical Network with the isolation
method set to "STT". This Network should be enabled for the Guest
traffic type.

.. note::
   The Guest traffic type should be configured with the traffic label
   that matches the name of the Integration Bridge on the hypervisor.
   See the Nicira NVP User Guide for more details on how to set this up
   in XenServer or KVM.

.. figure:: /_static/images/nvp-physical-network-stt.png
   :align: center
   :alt: a screenshot of a physical Network with the STT isolation type


Enabling the service provider
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Nicira NVP provider is disabled by default. Navigate to the "Network
Service Providers" configuration of the physical Network with the STT
isolation type. Navigate to the Nicira NVP provider and press the
"Enable Provider" button.

.. note::
   CloudStack 4.0 does not have the UI interface to configure the
   Nicira NVP plugin. Configuration needs to be done using the API
   directly.

.. figure:: /_static/images/nvp-physical-network-stt.png
   :align: center
   :alt: a screenshot of an enabled Nicira NVP provider


Device Management
~~~~~~~~~~~~~~~~~

In CloudStack a Nicira NVP setup is considered a "device" that can be added
and removed from a physical Network. To complete the configuration of
the Nicira NVP plugin a device needs to be added to the physical
Network. Press the "Add NVP Controller" button on the provider panel and
enter the configuration details.

.. figure:: /_static/images/nvp-physical-network-stt.png
   :align: center
   :alt: a screenshot of the device configuration popup.


Network Offerings
~~~~~~~~~~~~~~~~~

Using the Nicira NVP plugin requires a Network offering with Virtual
Networking enabled and configured to use the NiciraNvp element. Typical
use cases combine services from the Virtual Router appliance and the
Nicira NVP plugin.

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
| Load Balancer        | VirtualRouter   |
+----------------------+-----------------+
| User Data            | VirtualRouter   |
+----------------------+-----------------+
| Source NAT           | VirtualRouter   |
+----------------------+-----------------+
| Static NAT           | VirtualRouter   |
+----------------------+-----------------+
| Post Forwarding      | VirtualRouter   |
+----------------------+-----------------+
| Virtual Networking   | NiciraNVP       |
+----------------------+-----------------+

Table: Isolated Network offering with regular services from the Virtual
Router.

.. figure:: /_static/images/nvp-physical-network-stt.png
   :align: center
   :alt: a screenshot of a Network offering.


.. note::
   The tag in the Network offering should be set to the name of the
   physical Network with the NVP provider.

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
| Source NAT           | NiciraNVP       |
+----------------------+-----------------+
| Static NAT           | NiciraNVP       |
+----------------------+-----------------+
| Post Forwarding      | NiciraNVP       |
+----------------------+-----------------+
| Virtual Networking   | NiciraNVP       |
+----------------------+-----------------+

Table: Isolated network offering with network services


Using the Nicira NVP plugin with VPC
------------------------------------

Supported VPC features
~~~~~~~~~~~~~~~~~~~~~~

The Nicira NVP plugin supports CloudStack VPC to a certain extent. Starting
with CloudStack version 4.1 VPCs can be deployed using NVP isolated
networks.

It is not possible to use a Nicira NVP Logical Router for as a VPC
Router

It is not possible to connect a private gateway using a Nicira NVP
Logical Switch


VPC Offering with Nicira NVP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To allow a VPC to use the Nicira NVP plugin to provision Networks, a new
VPC offering needs to be created which allows the Virtual Networking
service to be implemented by NiciraNVP.

This is not currently possible with the UI. The API does provide the
proper calls to create a VPC offering with Virtual Networking enabled.
However due to a limitation in the 4.1 API it is not possible to select
the provider for this Network service. To configure the VPC offering
with the NiciraNVP provider edit the database table
'vpc\_offering\_service\_map' and change the provider to NiciraNvp for
the service 'Connectivity'

It is also possible to update the default VPC offering by adding a row
to the 'vpc\_offering\_service\_map' with service 'Connectivity' and
provider 'NiciraNvp'

.. figure:: /_static/images/nvp-physical-network-stt.png
   :align: center
   :alt: a screenshot of the mysql table.


.. note::
   When creating a new VPC offering please note that the UI does not
   allow you to select a VPC offering yet. The VPC needs to be created
   using the API with the offering UUID.


VPC Network Offerings
~~~~~~~~~~~~~~~~~~~~~

The VPC needs specific Network offerings with the VPC flag enabled.
Otherwise these Network offerings are identical to regular Network
offerings. To allow VPC networks with a Nicira NVP isolated network the
offerings need to support the Virtual Networking service with the
NiciraNVP provider.

In a typical configuration two network offerings need to be created. One
with the loadbalancing service enabled and one without loadbalancing.

.. cssclass:: table-striped table-bordered table-hover

+----------------------+--------------------+
| Service              | Provider           |
+======================+====================+
| VPN                  | VpcVirtualRouter   |
+----------------------+--------------------+
| DHCP                 | VpcVirtualRouter   |
+----------------------+--------------------+
| DNS                  | VpcVirtualRouter   |
+----------------------+--------------------+
| Load Balancer        | VpcVirtualRouter   |
+----------------------+--------------------+
| User Data            | VpcVirtualRouter   |
+----------------------+--------------------+
| Source NAT           | VpcVirtualRouter   |
+----------------------+--------------------+
| Static NAT           | VpcVirtualRouter   |
+----------------------+--------------------+
| Post Forwarding      | VpcVirtualRouter   |
+----------------------+--------------------+
| NetworkACL           | VpcVirtualRouter   |
+----------------------+--------------------+
| Virtual Networking   | NiciraNVP          |
+----------------------+--------------------+

Table: VPC Network Offering with Loadbalancing


Troubleshooting the Nicira NVP Plugin
-------------------------------------

UUID References
~~~~~~~~~~~~~~~

The plugin maintains several references in the CloudStack database to items
created on the NVP Controller.

Every guest network that is created will have its broadcast type set to
Lswitch and if the network is in state "Implemented", the broadcast URI
will have the UUID of the Logical Switch that was created for this
network on the NVP Controller.

The Nics that are connected to one of the Logical Switches will have
their Logical Switch Port UUID listed in the nicira\_nvp\_nic\_map table

.. note::
   All devices created on the NVP Controller will have a tag set to
   domain-account of the owner of the network, this string can be used
   to search for items in the NVP Controller.


Database tables
~~~~~~~~~~~~~~~

The following tables are added to the cloud database for the Nicira NVP
Plugin

.. cssclass:: table-striped table-bordered table-hover

+---------------------+--------------------------------------------------------------+
| id                  | auto incrementing id                                         |
+---------------------+--------------------------------------------------------------+
| logicalswitch       | uuid of the logical switch this port is connected to         |
+---------------------+--------------------------------------------------------------+
| logicalswitchport   | uuid of the logical switch port for this nic                 |
+---------------------+--------------------------------------------------------------+
| nic                 | the CloudStack uuid for this nic, reference to the nics table| 
+---------------------+--------------------------------------------------------------+

Table: nicira\_nvp\_nic\_map

.. cssclass:: table-striped table-bordered table-hover

+-------------------------+-------------------------------------------------------------+
| id                      | auto incrementing id                                        |
+-------------------------+-------------------------------------------------------------+
| uuid                    | UUID identifying this device                                |
+-------------------------+-------------------------------------------------------------+
| physical\_network\_id   | the physical network this device is configured on           |
+-------------------------+-------------------------------------------------------------+
| provider\_name          | NiciraNVP                                                   |
+-------------------------+-------------------------------------------------------------+
| device\_name            | display name for this device                                |
+-------------------------+-------------------------------------------------------------+
| host\_id                | reference to the host table with the device configuration   |
+-------------------------+-------------------------------------------------------------+

Table: external\_nicira\_nvp\_devices

.. cssclass:: table-striped table-bordered table-hover

+-----------------------+----------------------------------------------+
| id                    | auto incrementing id                         |
+-----------------------+----------------------------------------------+
| logicalrouter\_uuid   | uuid of the logical router                   |
+-----------------------+----------------------------------------------+
| network\_id           | id of the network this router is linked to   |
+-----------------------+----------------------------------------------+

Table: nicira\_nvp\_router\_map

.. note::
   nicira\_nvp\_router\_map is only available in CloudStack 4.1 and above


Revision History
----------------

0-0 Wed Oct 03 2012 Hugo Trippaers hugo@apache.org Documentation created
for 4.0.0-incubating version of the NVP Plugin 1-0 Wed May 22 2013 Hugo
Trippaers hugo@apache.org Documentation updated for CloudStack 4.1.0


.. | nvp-physical-network-stt.png: a screenshot of a physical network with the STT isolation type | image:: ./images/nvp-physical-network-stt.png
.. | nvp-physical-network-stt.png: a screenshot of an enabled Nicira NVP provider | image:: ./images/nvp-enable-provider.png
.. | nvp-physical-network-stt.png: a screenshot of the device configuration popup. | image:: ./images/nvp-add-controller.png
.. | nvp-physical-network-stt.png: a screenshot of a network offering. | image:: ./images/nvp-network-offering.png
.. | nvp-physical-network-stt.png: a screenshot of the mysql table. | image:: ./images/nvp-vpc-offering-edit.png
