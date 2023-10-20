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

.. note:: This functionality requires to install the **virt-v2v** (https://www.libguestfs.org/virt-v2v.1.html) binary installed on destination cluster hosts, as it is not a dependency of the CloudStack agent installed on the hosts.

As of CS 4.19, it is possible to select a VMware VM from an external or existing VMware datacenter, convert it to a KVM Virtual Machine and importing it into an existing KVM cluster.

Requirements on the KVM hosts
-----------------------------

The CloudStack agent does not install the virt-v2v binary as a dependency, for which this functionality is not supported by default. To enable this functionality, the virt-v2v binary must be installed on the destination KVM hosts where to import the Virtual Machines.

In case virt-v2v is not installed on a KVM host attempting a Virtual Machine conversion from VMware, the process fails.

The virt-v2v output is logged on the CloudStack agent logs to help administrators tracking the progress on the Virtual Machines conversion processes. The verbose mode for virt-v2v can be enabled by adding the following line to /etc/cloudstack/agent/agent.properties and restart cloudstack-agent:

    ::

        virtv2v.verbose.enabled=true


Installing virt-v2v on Ubuntu KVM hosts does not install nbdkit which is required in the conversion of VMWare VCenter guests. To install it, please execute:

    ::

        apt install nbdkit



Usage
-----

In the UI, Virtual Machines to import from VMware are listed in *Tools > Import-Export Instances* section, selecting:

.. cssclass:: table-striped table-bordered table-hover

==================== ========================
Source               Destination Hypervisor  
==================== ========================
Migrate From VMware  KVM
==================== ========================

|import-vm-from-vmware-to-kvm.png|

Selecting the Destination cluster
---------------------------------

CloudStack administrators must select a KVM cluster to import the VMware Virtual Machines (left side of the image above). Once a KVM cluster is selected, the VMware Datacenter selection part is displayed (right side of the image above).

Selecting the VM from a VMware Datacenter
-----------------------------------------

CloudStack administrators must select the Source VMware Datacenter:

    - Existing: The existing zones are listed, and for each zone CloudStack will list if there is any VMware Datacenter associated to it. In case it is, it can be selected
    - External: CloudStack allows listing Virtual Machines from a VMware Datacenter that is not associated to any CloudStack zone. To do so, it needs the vCenter IP address, the datacenter name, and username and password credentials to log in the vCenter.

Once the VMware Datacenter is selected, click on List VMware Instances to display the list of Virtual Machines on the Datacenter


Importing a Virtual Machine from VMware into KVM
------------------------------------------------

.. note:: CloudStack allows importing Running Linux Virtual Machines, but it is recommended that the Virtual Machine to import is powered off and has been gracefully shutdown before the process starts. For Windows Virtual Machines, it is not possible to import them while running.



.. |import-vm-from-vmware-to-kvm.png| image:: /_static/images/import-vm-from-vmware-to-kvm.png
   :alt: Import VMware Virtual Machines into KVM.
   :width: 800 px
