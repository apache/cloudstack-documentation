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


.. |guest-os-categories.png| image:: /_static/images/guest-os-categories.png
   :alt: Guest OS Categories

.. |add-guest-os-category.png| image:: /_static/images/add-guest-os-category.png
   :alt: Add Guest OS Category form

.. |guest-os-button.png| image:: /_static/images/guest-os-button.png
   :alt: Guest OS section

.. |add-guest-os-button.png| image:: /_static/images/add-guest-os-button.png
   :alt: Add guest OS button

.. |view-guest-os-mappings-button.png| image:: /_static/images/view-guest-os-mappings-button.png
   :alt: View guest OS mappings button

.. |guest-os-mapping-button.png| image:: /_static/images/guest-os-mapping-button.png
   :alt: Guest OS mapping button

.. |add-guest-os-mapping-button.png| image:: /_static/images/add-guest-os-mapping-button.png
   :alt: Add guest OS mapping button

CloudStack provides administrators a good control to manage the guest operating systems for the
Instances. CloudStack maintains the list of guest operating systems that are supported
by the hypervisors and also provides a way for operators or admins to add new guest OSs based on the need.
For an operating system to be supported to CloudStack for the Instances, it has to be added in CloudStack
and also need to have a mapping with the actual operating system name supported by hypervisor.

Under "Configuration" section there are sub-sections for guest operating system.

Guest OS Categories
-------------------

A list of existing categories for the guest operating systems are shown as
"Guest OS Categories" section. Operators can also add new guest operating
system categories from the view.

|guest-os-categories.png|

Guest operating system categories are useful for categorizing images, i.e.,
templates and ISOs, in several UI forms such as deploying an instance,
reinstalling an instance, etc., when the modern image selection is used in the
UI configuration.

To allow a guest operating system category to be displayed in the UI forms, it
must be marked as featured. The order of the categories can also be controlled
using the Order option in the categories view.

Like other resources, a custom resource icon can be set for a particular guest
operating system category for further control. If no resource icon is set for
a category, the UI will display default icons based on the category
name.

An existing guest OS category can be deleted if it does not have any
associated guest operating systems.

The "Add guest OS category" option allows operators to create new categories,
which can be marked as featured if they are meant to be displayed in the UI
forms.

|add-guest-os-category.png|

Guest OS
--------

A list of supported guest operating systems are shown under |guest-os-button.png| and also one can add new operating systems.

To add a new guest OS, click on the button |add-guest-os-button.png| and following details needs to be provided:

- **OS name** : Name of the operating system which will be displayed to the users.

- **OS category** : Category of the operating system to which it belongs, eg. Windows, CentOS, Debian, etc.

.. image:: /_static/images/add-guest-os-form.png
   :width: 400px
   :align: center
   :alt: Guest OS dialog box

Operator also need to add mapping with the actual operating system name supported by hypervisor as below.

Guest OS hypervisor mapping
----------------------------
Existing mappings are shown here and also one can add new mapping to an operating system.
To view the mappings of an existing guest OS click on |view-guest-os-mappings-button.png| under guest OS details.

.. image:: /_static/images/guest-os-details-form.png
   :width: 400px
   :align: center
   :alt: Guest OS details form

To a new mapping, inside the sub-section |guest-os-mapping-button.png| click on |add-guest-os-mapping-button.png|
and following details needs to be provided.

- **OS type** : Select the operating system type to which mapping needs to be created.

- **Hypervisor** : Name of the hypervisor.

- **Hypervisor version** : Specific version of the hypervisor. The exact version number found from hypervisor capabilities list.

- **Hypervisor mapping name** : Name of the operating system specific to the hypervisor. Eg. For CentOS 5.0 (64-bit) in VMware
                                the specific name is "centos64Guest".

- **Check OS name with hypervisor** : A toggle button to specify whether to verify the hypervisor mapping name with available
                                      hypervisor.

- **Force** : A toggle button to force add a user defined guest os mapping, overrides any existing user defined mapping.

.. image:: /_static/images/guest-os-mapping-form.png
   :width: 400px
   :align: center
   :alt: Guest OS mapping form

Operator can also do operations like edit and delete guest OS and its hypervisor mappings.
