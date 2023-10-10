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


VNF Templates and Appliances
=======================

Virtualized Network Functions (VNFs) refers to virtualized software applications
which offers network services, for example routers, firewalls, load balancers.


Adding VNF templates from URL
-------

To create a VNF appliance, user needs to register a VNF template and add VNF settings.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Images -> Templates

#. Click the "Register template from URL" button.

#. Specify the "Template type" to "VNF"

#. Click OK button.

When the VNF template is registered successfully, you will see the template on
the same page or under Network -> VNF templates.

   For more information, see `“Uploading Templates from a remote HTTP server”
   <templates.html#uploading-templates-from-a-remote-http-server>`_.


Updating a VM template to VNF template
-------

Users are able to update an existing VM template, which is uploaded from
HTTP server or local, or created from volume, to a VNF template.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Images -> Templates

#. Select the VM template you want to work with.

#. Into System Preferences -> Network 

#. Change the "Template type" to "VNF"

#. Click OK button.


Update VNF settings of VNF template
-------------------

Users need to add VNF nics and VNF details of the VNF templates.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Images -> Templates

#. Select the VNF template you want to work with.

#. Click "VNF settings" tab of the VNF template

|vnf-template-vnf-settings.png|

#. To add VNF nics, click "Add VNF nic"

|vnf-add-nic.png|

The following parameters are supported.

- deviceid: The device ID of the VNF nic. The device id must be consecutive and start from 0.

- name: The name of the VNF nic.

- required: True if the VNF nic is required. Otherwise it is optional. It cannot be true if a precedent nic is optional.

- management: True if the VNF nic is a management interface. False otherwise

- description: The description of the VNF nic.

When VNF nics are added, user will see the list of VNF nics.

|vnf-nics-list.png|

#. To add VNF details, click click "Add VNF detail"

|vnf-add-detail.png|

The following parameters are supported.

- name: The name of the VNF detail. The valid values are: ACCESS_METHODS,
  USERNAME, PASSWORD, SSH_USER, SSH_PASSWORD, SSH_PORT, WEB_USER, WEB_PASSWORD,
  HTTP_PATH, HTTP_PORT, HTTPS_PATH, HTTPS_PORT and ICON, VERSION, VENDOR, MAINTAINER

- value: The value of the VNF detail. If the name is access_methods, the valid values are: console, http, https, ssh-key, ssh-password

Users are also able to edit or remove the existing VNF details.

|vnf-details-list.png|


Deploy VNF appliances
-------------------

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network -> VNF appliances

#. Click the "Add VNF Appliance" button.

   For more information, see `“Creating VMs”
   <virtual_machines.html#creating-vms>`_.

#. Choose the networks you want to add to the VNF appliance

|vnf-appliance-networks-selection.png|

#. In the "VNF nics" step, choose the network each VNF nic will use

|vnf-appliance-vnf-nics.png|

#. Click "Launch VNF appliance" button

When the VNF appliance is deployed successfully, you will see the VNF appliance on
the same page.


.. |vnf-template-vnf-settings.png| image:: /_static/images/vnf-template-vnf-settings.png
   :alt: VNF settings of VM template
.. |vnf-add-nic.png| image:: /_static/images/vnf-add-nic.png
   :alt: Add VNF nic
.. |vnf-nics-list.png| image:: /_static/images/vnf-nics-list.png
   :alt: List of VNF nics
.. |vnf-add-detail.png| image:: /_static/images/vnf-add-detail.png
   :alt: Add VNF detail
.. |vnf-details-list.png| image:: /_static/images/vnf-details-list.png
   :alt: List of VNF details
.. |vnf-appliance-networks-selection.png| image:: /_static/images/vnf-appliance-networks-selection.png
   :alt: Select networks for VNF appliance
.. |vnf-appliance-vnf-nics.png| image:: /_static/images/vnf-appliance-vnf-nics.png
   :alt: Specify VNF nics of VNF appliance

