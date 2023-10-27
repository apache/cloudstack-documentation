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


Supported Distributions for KVM Hypervisor:


.. cssclass:: table-striped table-bordered table-hover

========================    ========================
Linux Distribution          Supported Versions
========================    ========================
Alma Linux                  8, 9
Red Hat Enterprise Linux    8, 9
Rocky Linux                 8, 9
Ubuntu                      22.04 LTS
========================    ========================


Importing Windows guest VMs from VMware requires installing the virtio drivers on the hypervisor hosts for the virt-v2v conversion.

On (RH)EL hosts:

    ::

        yum install virtio-win

You can also install the RPM manually from https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.noarch.rpm


For Debian-based distributions:

    ::

        apt install virtio-win

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


Converting and importing a VMware VM
------------------------------------

.. note:: CloudStack allows importing Running Linux Virtual Machines, but it is recommended that the Virtual Machine to import is powered off and has been gracefully shutdown before the process starts. For Windows Virtual Machines, it is not possible to import them while running.

When importing a Virtual Machine from VMware to KVM, CloudStack performs the following actions:

    - Cloning the Source Virtual Machine on the selected VMware Datacenter: The source Virtual Machine will be cloned in the original state (running or stopped for Linux VMs, or stopped for Windows VMs). The recommended state is the stopped state to prevent data inconsistencies or loss when cloning the virtual machine.
    - Converting the Cloned Virtual Machine to KVM using virt-v2v: CloudStack (or the administrator) selects a running and Enabled KVM host to perform the conversion from VMware to KVM using virt-v2v. If the binary is not installed, then the host will fail the migration. In case it is installed it will perform the conversion into a temporary location (which can be selected by the administrator) to store the converted QCOW2 disks of the virtual machine. The disks are then moved into the destination storage pools for the virtual machine. The conversion process is a long-lasting process which can be set to timeout by the global setting 'convert.vmware.instance.to.kvm.timeout'. The conversion processes are long-lasting processes since virt-v2v creates a virtual machine to inspect the source VM and generate the converted disks with the correct drivers. Also, it needs to copy the converted disks into the temporary location.

.. note:: Please consider not restarting the management servers during the imports since this action can cause failures on the on-going importing processes.

.. |import-vm-from-vmware-to-kvm.png| image:: /_static/images/import-vm-from-vmware-to-kvm.png
   :alt: Import VMware Virtual Machines into KVM.
   :width: 800 px
