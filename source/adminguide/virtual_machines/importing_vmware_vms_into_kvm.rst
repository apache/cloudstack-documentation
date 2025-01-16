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

.. note:: This functionality requires **virt-v2v** (https://www.libguestfs.org/virt-v2v.1.html) binary installed on destination cluster hosts (needs to be installed manually as it's not a dependency of the CloudStack agent during the agent installation).

Requirements on the KVM hosts
-----------------------------

The CloudStack agent does not install the virt-v2v binary as a dependency. The virt-v2v binary must be installed manually on KVM hosts, or the migration will fail.

The virt-v2v output (progress) is logged in the CloudStack agent logs, to help administrators track the progress on the Instance conversion processes. The verbose mode for virt-v2v can be enabled by adding the following line to /etc/cloudstack/agent/agent.properties and restart cloudstack-agent:

    ::

        virtv2v.verbose.enabled=true


Installing virt-v2v on Ubuntu KVM hosts does not install nbdkit which is required in the conversion of VMware VCenter guests. To install it, please execute:

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
Ubuntu                      22.04 LTS, 24.04 LTS
========================    ========================


Importing Windows VMs from VMware requires installing the virtio drivers for Windows on the hypervisor hosts for the virt-v2v conversion.

On (RH)EL hosts:

    ::

        yum install virtio-win

You can also install the RPM manually from https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.noarch.rpm


For Debian-based distributions:

    ::

        apt install virtio-win (if the package is not available, then manual steps will be required to install the virtio drivers for windows)

The OVF tool (ovftool) must be installed on the destination KVM hosts if the hosts should export VM files (OVF) from vCenter. If not, the management server exports them (the management server doesn't require ovftool installed).

Usage
-----

In the UI, Virtual Machines to import from VMware are listed in *Tools > Import-Export Instances* section, selecting:

.. cssclass:: table-striped table-bordered table-hover

==================================================== =================================
Select Import-Export Source Hypervisor               Action  
==================================================== =================================
VMware                                               Migrate existing instances to KVM
==================================================== =================================

|import-vm-from-vmware-to-kvm.png|

Selecting the Destination cluster
---------------------------------

CloudStack administrators must select a KVM cluster to import the VMware Virtual Machines (right side of the image above). Once a KVM cluster is selected, the VMware Datacenter selection part is displayed.

Selecting the VM from a VMware Datacenter
-----------------------------------------

CloudStack administrators must select the Source VMware Datacenter:

    - Existing: The existing zones are listed, and for each zone, CloudStack will list if there is any VMware Datacenter associated with it. In case it is, it can be selected.
    - External: CloudStack allows listing Virtual Machines from a VMware Datacenter that is not associated with any CloudStack zone. To do so, the vCenter IP address, the datacenter name, and username and password credentials are needed to log in to the vCenter. To import from a standalone VMware host, you can use the default datacenter name (ha-datacenter or other) along with the host credentials (Only stopped VMs are supported).

Once the VMware Datacenter is selected, click on List VMware Instances to display the list of Virtual Machines in the Datacenter. You must then choose the VMware Instance for import and click on Import Instance.

Converting and importing a VMware VM
------------------------------------

.. note:: CloudStack allows importing Running Linux Virtual Machines, but it is generally recommended that the Virtual Machine to import is powered off and has been gracefully shut down before the process starts. In case a Linux VM is imported while running, it will be converted in a "crash consistent" state. For Windows Virtual Machines, it is not possible to import them while running, they must be shut down gracefully so the filesystem is in a clean state.

.. note:: You can configure the parallel import of VM disk files on KVM host and management server, using the global settings: threads.on.kvm.host.to.import.vmware.vm.files and threads.on.ms.to.import.vmware.vm.files respectively.

In the UI import wizard, you can optionally select a KVM host and temporary destination storage (default is Secondary Storage, but if using Primary Storage - only NFS pools are supported) for the conversion, where VM files (OVF) will be copied to. This can be done by a random (or explicitly chosen) KVM host (if the ovftools are installed), otherwise, the management server will export/copy the VM files (optionally, you can force this action to be done by the management server even the KVM hosts have the ovftools installed in it). Irrelevant if the KVM host or the management server performs the copy of the VM files (OVF), you can further either let CloudStack choose which KVM host should do the conversion of the VM files using virt-v2v and which host will import the files to the destination Primary Storage Pool, or you can explicitly choose these KVM hosts for each of the 2 mentioned operations.

|import-vm-from-vmware-to-kvm-options.png|

When importing an instance from VMware to KVM, CloudStack performs the following actions:

    - Export the VM files (OVF) of the instance to a temporary storage location
      (which can be selected by the administrator). The export is performed by a
      KVM host if ovftool is installed or management server (can be forced by the 
      administrator, doesn't need ovftool installed on the management server).
      The existence of ovftool on KVM host is checked using 
      ``ovftool --version`` command.

      - If the instance on VMware is in **running** state, we clone the instance on
        VMware and use the new cloned instance to export OVF files.
        The cloning process may take some time to complete and is used to ensure data consistency,
        disk consolidation, etc.
      - If the instance on VMware is in **stopped** state, we directly use the
        instance to export its OVF files.
    - Converts the OVF on the temporary storage location to KVM using
      **virt-v2v**. CloudStack (or the administrator) selects a running and
      enabled KVM host to perform the conversion (of the previously exported OVF files) from VMware to KVM using
      **virt-v2v**. If the binary is not installed, then the host will fail to convert the Instance.
      In case it is installed, it will perform the conversion into
      the temporary location to store the converted QCOW2 disks of the instance.
      The virt-v2v conversion is a long-lasting process which can be set to
      time out by the global setting ``convert.vmware.instance.to.kvm.timeout``.
      The conversion process takes a long time because virt-v2v creates a
      temporary instance to inspect the source VM and generate the converted
      disks with the correct drivers. Additionally, it needs to copy the
      converted disks into the temporary location.
    - The converted instance (i.e. QCOW2 files) is then imported into the chosen KVM cluster.
      Administrator can choose the KVM host to perform the import or let CloudStack choose it. Only enabled 
      cluster and enabled hosts are considered.

.. note:: Please do not restart the management servers while migration is in progress as it will lead to the interruption of the process and you will need to start again.

.. note:: As mentioned above, the migration/conversion process uses an external tool, virt-v2v, which supports most but not all the operating systems out there (this is true for both the host on which the virt-v2v tool is running as well as the guest OS of the instances being migrated by the tool). Thus, the success of the import process will, almost exclusively, depend on the success of the virt-v2v conversion. In other words, the success will vary based on factors such as the current OS version, installed packages, guest OS setup, file systems, and others. Success is not guaranteed. We strongly recommend testing the migration process before proceeding with production deployments.

.. note:: The resulting imported VM uses the default Guest OS type: **CentOS 4.5 (32-bit)**. After importing the VM, please Edit the Instance to change the Guest OS Type accordingly.

.. |import-vm-from-vmware-to-kvm.png| image:: /_static/images/import-vm-from-vmware-to-kvm.png
   :alt: Import VMware Virtual Machines into KVM.
   :width: 800 px

.. |import-vm-from-vmware-to-kvm-options.png| image:: /_static/images/import-vm-from-vmware-to-kvm-options.png
   :alt: Import VMware Virtual Machines into KVM Options.
   :width: 800 px
