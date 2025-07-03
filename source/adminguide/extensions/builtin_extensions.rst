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


Built-in Orchestator Extensions
===============================

CloudStack provides sample built-in orchestrator extensions for Proxmox and Hyper-V. These extensions are intended for demonstration and testing purposes.
The extension files are located at `/usr/share/cloudstack-management/extensions/Promox` and `/usr/share/cloudstack-management/extensions/HyperV` respectively.
The Proxmox extension is written in shell script, while the Hyper-V extension is written in python.
Both of these extensions support some custom actions in addition to the standard VM actions like deploy, start, stop, reboot, status and delete.
After installing or upgrading Cloudstack, these extensions will show up as disabled on the Extensions page in the UI.

   |built-in-extensions.png|

**Note**: These extension may undergo changes with different CloudStack releases and backwards compatibility is not guaranteed.

Proxmox
^^^^^^^^

The Proxmox Cloudstack extension is written in shell script and communicates with a Proxmox cluster using the `Proxmox VE API`_.

Before using the Proxmox extension, ensure that the Proxmox cluster is configured correctly and accessible to CloudStack.

Get the Api Token-Secret from Proxmox
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If not already set up, create a new API Token in the Proxmox UI by navigating to `Datacenter > Permissions > API Tokens`.
Uncheck the `Privilege Separation` checkbox in the `Add: Token` dialog or give permission to the API Token
by navigating to `Datacenter > Permissions > Add > API Tokens Permission` and setting Role = `PVEAdmin` and Path = `/vms`.
Note down the **user**, **token**, and **secret**.

   |proxmox-add-token.png|
   |proxmox-api-token-permission.png|

Adding Proxmox to CloudStack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To set up the Proxmox extension, follow these steps in CloudStack:

#. **Enable extension.** Enable the extension by clicking the `Enable` button on the `Extensions` page in the UI.
#. **Create Cluster**. Create a Cluster with hypervisor type `External` and extension type `Proxmox`.

   |proxmox-add-cluster.png|

#. **Add Host.** Add a host to the newly created cluster with the following details:

   |proxmox-add-host.png|

   If the Proxmox nodes use a shared API endpoint or credentials, the `url`, `user`, `token`, and `secret` can be set in the Extension's `Configuration Details` instead of per host. However, `node` and `network_bridge` must still be specified individually for each host.

#. **Create Template.** A Template in CloudStack can map to either a `Template` or an `ISO` in Proxmox.
   Provide a dummy `url` and template name. Select `External` as the hypervisor and `Proxmox` as the extension. Under `External Details`, specify:

   * **template_type**: `template` or `iso`
   * **template_id**: ID of the template in Proxmox (if `template_type` is `template`)

   |proxmox-add-template.png|

   * **iso_path**: full path to the ISO in Proxmox (if `template_type` is `iso`)
   |proxmox-add-iso.png|

   Note: Templates and ISOs should be stored on shared storage when using multiple Proxmox nodes. Or copy the template/iso to each host's local storage at the same location.

#. **Deploy Instance.** Deploy an instance using the template created above. Optionally, provide the detail `vm_name` to specify the name of the VM in Proxmox.
   Otherwise, the CloudStack instance's internal name is used. The VM Id in Proxmox is mapped to the CloudStack instance and stored as a detail in CloudStack DB.
   The instance will be provisioned on a randomly selected Proxmox host. The VM will be configured with the MAC address and VLAN ID as defined in CloudStack.

   |proxmox-deploy-instance.png|

#. **Lifecycle operations.** Operations **Start**, **Stop**, **Reboot**, and **Delete** can be performed on the instance from CloudStack.

#. **Custom actions.** Custom actions **Create Snapshot**, **Restore Snapshot**, and **Delete Snapshot** are also supported for instances.

Configuring Networking
~~~~~~~~~~~~~~~~~~~~~~

Proxmox nodes and CloudStack hypervisor hosts must be connected via a VLAN trunked network. On each Proxmox node,
a bridge interface should be created and connected to the network interface that carries the VLAN-tagged traffic.
This bridge must be specified under Configuration Details (`network_bridge`) when registering the Proxmox node as a host in CloudStack.

When a VM is deployed, CloudStack includes the assigned MAC address and VLAN ID in the extension payload.
The VM created on the Proxmox node is configured with this MAC and connected to the corresponding VLAN via the specified bridge.

Upon boot, the VM broadcasts a VLAN-tagged DHCP request, which reaches the CloudStack Virtual Router (VR) handling that VLAN.
The VR responds with the appropriate IP address as configured in CloudStack. Once the VM receives the lease, it becomes fully integrated into the CloudStack-managed network.

Users can then manage the Hyper-V VM like any other CloudStack guest instance. Users can apply egress policies,
firewall rules, port forwarding, and other networking features seamlessly through the CloudStack UI or API.

Hyper-V
^^^^^^

The Hyper-V CloudStack extension is a python script connects to the Hyper-V server using SSH and executes powershell commands to manage the VMs.
Each Hyper-V host maps to a CloudStack host.
Before using the Proxmox extension, ensure that the Proxmox cluster is configured correctly and accessible to CloudStack.

Host Details
~~~~~~~~~~~~

Apart from the `url`, `username` and `password`, the following details are required when adding a Hyper-V host in CloudStack:

* **network_bridge**: Name of the network bridge to use for VM networking. This bridge must be configured on the Hyper-V host and connected to the appropriate network interface as explained in the `Configuring Networking` section below.
* **vhd_path**: Path to the storage location where VM disks will be created.
* **vm_path**: Path to the storage location where VM configuration files and metadata will be stored.


Adding Hyper-V to CloudStack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. **Enable extension.** Enable the extension by clicking the `Enable` button on the `Extensions` page in the UI.
#. **Create Cluster**. Create a Cluster with hypervisor type `External` and extension type `HyperV`.

   |hyperv-add-cluster.png|

#. **Add Host.** Add a host to the newly created cluster with the following details:

   |hyperv-add-host.png|

#. **Create Template.** A Template in CloudStack can map to either a `Template` or an `ISO` in Hyper-V.
   Provide a dummy `url` and template name. Select `External` as the hypervisor and `HyperV` as the extension. Under `External Details`, specify:

   * **template_type**: `template` or `iso`
   * **generation**: VM generation (1 or 2)
   * **template_path**: Full path to the template .vhdx file in Proxmox (if `template_type` is `template`)

   |hyperv-add-template.png|

   * **iso_path**: full path to the ISO in HyperV (if `template_type` is `iso`)
   * **vhd_size_gb**: Size of the VHD disk to create (in GB) (if `template_type` is `iso`)

   |hyperv-add-iso.png|

   Note: Templates and ISOs should be stored on shared storage when using multiple HyperV nodes. Or copy the template/iso to each host's local storage at the same location.

#. **Deploy Instance.** Deploy an instance using the template created above. The instance will be provisioned on a randomly selected Hyper-V host.
   The VM will be configured with the MAC address and VLAN ID as defined in CloudStack.
   The VM in Hyper-V is created with the name `'CloudStack instance's internal name' + '-' + 'CloudStack instance's UUID'` to keep it unique.

#. **Lifecycle operations.** Operations **Start**, **Stop**, **Reboot**, and **Delete** can be performed on the instance from CloudStack.

#. **Custom actions.** Custom actions **Suspend**, **Resume**, **Create Snapshot**, **Restore Snapshot**, and **Delete Snapshot** are also supported for instances.

Configuring Networking
~~~~~~~~~~~~~~~~~~~~~~

Hyper-V hosts and CloudStack hypervisor hosts must be connected via a VLAN trunked network.
On each Hyper-V host, an external virtual switch should be created and bound to the physical network interface that carries VLAN-tagged traffic.
This switch must be specified in the Configuration Details (network_bridge) when adding the Hyper-V host to CloudStack.

When a VM is deployed, CloudStack includes the assigned MAC address and VLAN ID in the extension payload.
The VM is then created on the Hyper-V host with this MAC address and attached to the specified external switch with the corresponding VLAN configured.

Upon boot, the VM sends a VLAN-tagged DHCP request, which reaches the CloudStack Virtual Router (VR) responsible for that VLAN.
The VR responds with the correct IP address as configured in CloudStack. Once the VM receives the lease, it becomes fully integrated into the CloudStack-managed network.

Users can then manage the Hyper-V VM like any other CloudStack guest instance. Users can apply egress policies,
firewall rules, port forwarding, and other networking features seamlessly through the CloudStack UI or API.


.. _Proxmox VE API: https://pve.proxmox.com/pve-docs/api-viewer/index.html

.. Images


.. |built-in-extensions.png| image:: /_static/images/built-in-extensions.png
.. |proxmox-add-cluster.png| image:: /_static/images/proxmox-add-cluster.png
.. |proxmox-add-host.png| image:: /_static/images/proxmox-add-host.png
.. |proxmox-add-token.png| image:: /_static/images/proxmox-add-token.png
.. |proxmox-api-token-permission.png| image:: /_static/images/proxmox-api-token-permission.png
.. |proxmox-add-template.png| image:: /_static/images/proxmox-add-template.png
.. |proxmox-add-iso.png| image:: /_static/images/proxmox-add-iso.png
.. |proxmox-deploy-instance.png| image:: /_static/images/proxmox-deploy-instance.png
.. |hyperv-add-cluster.png| image:: /_static/images/hyperv-add-cluster.png
.. |hyperv-add-host.png| image:: /_static/images/hyperv-add-host.png
.. |hyperv-add-template.png| image:: /_static/images/hyperv-add-template.png
.. |hyperv-add-iso.png| image:: /_static/images/hyperv-add-iso.png
