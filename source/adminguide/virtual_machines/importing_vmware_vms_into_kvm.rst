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

The OVF tool (ovftool) must be installed on the destination KVM hosts if the hosts should import VM files (OVF) from vCenter directly, if not management server imports them.

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
    - External: CloudStack allows listing Virtual Machines from a VMware Datacenter that is not associated to any CloudStack zone. To do so, it needs the vCenter IP address, the datacenter name, and username and password credentials to log in the vCenter. You can use default datacenter name (ha-datacenter or other) along with host credentials to import from standalone VMware hosts (Only stopped VMs are supported).

Once the VMware Datacenter is selected, click on List VMware Instances to display the list of Virtual Machines on the Datacenter. You must then select the VMware Instance for import and click on Import Instance.

Converting and importing a VMware VM
------------------------------------

.. note:: CloudStack allows importing Running Linux Virtual Machines, but it is generally recommended that the Virtual Machine to import is powered off and has been gracefully shutdown before the process starts. In case a Linux VM is imported while running, it will be converted in "crash consistent" state. For Windows Virtual Machines, it is not possible to import them while running, it is mandatory they are shut down gracefully so the filesystem is in a clean state.

.. note:: You can configure the parallel import of VM disk files on KVM host and management server, using the global settings: threads.on.kvm.host.to.import.vmware.vm.files and threads.on.ms.to.import.vmware.vm.files respectively.

In the UI to import instance, you can optionally select a KVM host and temporary destination storage (Default is Secondary Storage, Only NFS pools are supported) for the conversion. The conversion needs VM files (OVF) to be imported to temporary destination storage, the KVM host used for conversion can import them if the ovftool is installed in it, otherwise the management server imports them. You can force the management server to import them by enabling Force MS to import VM file(s), even the KVM host has ovftool installed in it.

|import-vm-from-vmware-to-kvm-options.png|

When importing a Virtual Machine from VMware to KVM, CloudStack performs the following actions:

    - Clones the Source Virtual Machine on the selected VMware Datacenter for running VMs: The source Virtual Machine will be cloned in the original state for running VMs. The recommended state is the stopped state to prevent data inconsistencies or loss when cloning the virtual machine.
    - Imports the VM files (OVF) of the Cloned Virtual Machine for running VMs, Source Virtual Machine for stopped VMs to a temporary storage location (which can be selected by the administrator) from KVM host if ovftool installed or management server (can be forced by the administrator).
    - Converts the OVF on the temporary storage location to KVM using virt-v2v: CloudStack (or the administrator) selects a running and enabled KVM host to perform the conversion from VMware to KVM using **virt-v2v**. If the binary is not installed, then the host will fail the migration. In case it is installed, it will perform the conversion into the temporary location to store the converted QCOW2 disks of the virtual machine. The disks are then moved into the destination storage pools for the virtual machine. The conversion is a long-lasting process which can be set to time out by the global setting 'convert.vmware.instance.to.kvm.timeout'. The conversion processes takes a long time because virt-v2v creates a temporary virtual machine to inspect the source VM and generate the converted disks with the correct drivers. Additionally, it needs to copy the converted disks into the temporary location.

.. note:: Please consider not restarting the management servers while importing as it will lead to the interruption of the process and you will need to start again.

.. note:: As mentioned above, the migration/conversion process uses an external tool, virt-v2v, which supports most but not all the operating systems out there (this is true for both the host on which the virt-v2v tool is running as well as the guest OS of the instances being migrated by the tool). Thus, the success of the import process will, almost exclusively, depend on the success of the virt-v2v conversion. In other words, the success will vary based on factors such as the current OS version, installed packages, guest OS setup, file systems, and others. Success is not guaranteed. We strongly recommend testing the migration process before proceeding with production deployments.

.. note:: The resulting imported VM uses the default Guest OS: CentOS 4.5 (32-bit). After importing the VM, please Edit the Instance to change the Guest OS Type accordingly.

.. |import-vm-from-vmware-to-kvm.png| image:: /_static/images/import-vm-from-vmware-to-kvm.png
   :alt: Import VMware Virtual Machines into KVM.
   :width: 800 px

.. |import-vm-from-vmware-to-kvm-options.png| image:: /_static/images/import-vm-from-vmware-to-kvm-options.png
   :alt: Import VMware Virtual Machines into KVM Options.
   :width: 800 px
