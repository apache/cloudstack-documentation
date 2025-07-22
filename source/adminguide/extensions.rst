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
   

Extensions
==========

Extensions are a new mechanism introduced in Apache CloudStack to allow administrators to extend the platform's functionality by integrating external systems or custom workflows. Currently, CloudStack supports a single extension type called Orchestrator.

In the UI, extensions can be managed under *Extensions* menu.

   |extensions.png|

Overview
^^^^^^^^

An extension in CloudStack is defined as an external binary (written in any programming language) that implements specific actions CloudStack can invoke. This allows operators to manage resource lifecycle operations outside CloudStack, such as provisioning VMs in third-party systems or triggering external automation pipelines.

Extensions are managed through the API and UI, with support for configuration, resource mappings, and action execution.

   |create-extension.png|

Configuration
^^^^^^^^^^^^^

Administrators can define and manage the following components of an extension:

   - Path: A path to a file or script that will be executed during extension operations.

   - Configuration Details: Key-value properties used by the extension at runtime.

   - Resource Mappings: Association between extensions and CloudStack resources such as clusters, etc.

Path and Availabilty
^^^^^^^^^^^^^^^^^^^^

The path for an extension can point to any binary or executable script. If no explicit path is provided, CloudStack uses a default base Bash script. The state of the path is validated across all management servers. In the UI, the Availabilty is displayed as Not Ready if the file is missing, inaccessible, or differs across management servers.

All extension files are stored under a directory named after the extension within `/usr/share/cloudstack-management/extensions`.

Payload
^^^^^^^

CloudStack sends structured JSON payloads to the extension binary during each operation. These payloads are written to .json files stored under `/var/lib/cloudstack/management/extensions`. The extension binary is expected to read the file and return an appropriate result. CloudStack automatically attempts to clean up payload files older than one day.

Orchestrator Extension
^^^^^^^^^^^^^^^^^^^^^^

An Orchestrator extension enables CloudStack to delegate VM orchestration to an external system. Key features include:

   - Cluster Mapping: Orchestrator extensions can be associated with one or more CloudStack clusters.

   - Hosts: Multiple hosts can be added to such clusters, ideally pointing to different physical or external hosts.

   - Instance Lifecycle Support: Extensions can handle basic VM actions like prepare, deploy, start, stop, reboot, status and delete.

   - Configuration Details: Key-value configuration details can be specified at different levels - extension, cluster mapping, host, template, service offering, instance.

   - Custom Actions: Admins can define custom actions beyond the standard VM operations.

   - Instance Preparation: Orchestrator extensions can optionally perform a preparation step during instance deployment. This step is executed before the instance is started on the external system. It allows the extension to update certain instance details in CloudStack. CloudStack sends a structured JSON containing the instance configuration, and the extension can respond with the values it wishes to modify. Currently, only a limited set of fields can be updated: the instance’s VNC password, MAC address, and the IPv4/IPv6 addresses of its NICs.

   - Networking: If networking is setup properly on the external system (See :ref:`built-in extensions networking <proxmox-networking>` for more details.), the Virtual Router in CloudStack can connect to the external VMs and provide DHCP, DNS, and routing services.

     **Note**: User data and ssh-key injection from within CloudStack is not supported for the external VMs in this release. The External systems should handle user-data and ssh-key injections natively using other mechanisms.

   |extension.png|


CloudStack provides sample built-in orchestrator extensions for demonstration and testing purposes.

.. note:: When a CloudStack host linked to an orchestrator extension is placed into Maintenance mode, all running VMs on the host will be stopped.

.. include:: extensions/custom_actions.rst

.. include:: extensions/builtin_extensions.rst

.. include:: extensions/troubleshooting.rst

.. include:: extensions/developer.rst

.. Images


.. |extensions.png| image:: /_static/images/extensions.png
.. |create-extension.png| image:: /_static/images/create-extension.png
.. |extension.png| image:: /_static/images/extension.png
