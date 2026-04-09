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

        dnf install virt-v2v

        echo "virtv2v.verbose.enabled=true" >> /etc/cloudstack/agent/agent.properties  
    
        systemctl restart cloudstack-agent


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

Ubuntu don’t seem to ship the virtio-win package with drivers, which causes virt-v2v not to convert the VMWare Windows guests to virtio profiles. This could result in slow IDE drives and Intel E1000 NICs. As a workaround, we can follow the below steps to install the package from the RPM on all KVM hosts running the virt-v2v:

    ::

        apt install virtio-win (if the package is not available, then manual steps will be required to install the virtio drivers for windows)
        
        wget https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.noarch.rpm

        # install “alien” which can convert rpms to debs
        apt -y install alien

        # the conversion, can take a while
        alien -d virtio-win.noarch.rpm

        # install the resulting deb
        dpkg -i virtio-win*.deb

In addition to this, we need to install the below package as well to avoid the error “virt-v2v: error: One of rhsrvany.exe or pvvxsvc.exe is missing in /usr/share/virt-tools“.

    :: 
     
        wget -nd -O srvany.rpm https://kojipkgs.fedoraproject.org//packages/mingw-srvany/1.1/4.fc38/noarch/mingw32-srvany-1.1-4.fc38.noarch.rpm

        alien -d srvany.rpm

        dpkg -i *srvany*.deb


The OVF tool (ovftool) must be installed on the destination KVM hosts if the hosts should export VM files (OVF) from vCenter. If not, the management server exports them (the management server doesn't require ovftool installed).

Steps to install ovftool

Download the ovftool from https://developer.broadcom.com/tools/open-virtualization-format-ovf-tool/latest

    ::
       
       unzip VMware-ovftool-4.6.3-24031167-lin.x86_64.zip -d /usr/local/
       
       #create a soft link 

       ln -s /usr/local/ovftool/ovftool /usr/local/bin/ovftool

If you are hitting the following error when running ovftool, install the dependecy

./ovftool.bin: error while loading shared libraries: libnsl.so.1: cannot open shared object file: No such file or directory

     ::
     
        dnf install libnsl


VDDK-based Optimized Conversion
-------------------------------

CloudStack supports an optimized VMware-to-KVM migration path using virt-v2v in vpx input mode combined with
VMware's Virtual Disk Development Kit (VDDK). This method eliminates the OVF export phase entirely and streams
disk blocks directly from the source hypervisor into the conversion pipeline, resulting in significantly faster
migration times.

The traditional OVF-based workflow operates in two sequential phases:

1. Export the entire VM as OVF/VMDK files to temporary storage (full disk copy).
2. Convert the local VMDK files using virt-v2v (second full disk read and write).

The VDDK-based workflow replaces both phases with a single streaming pipeline:

- virt-v2v connects directly to vCenter via ``vpx://``
- Disk blocks are read on demand via VDDK (using nbdkit internally as the translation layer between the
  VDDK API and virt-v2v's NBD block device interface)
- Conversion and disk transfer happen concurrently
- Only allocated blocks are transferred; zero-filled and sparse extents are skipped
- No intermediate OVF or VMDK files are created

This reduces disk I/O amplification, eliminates temporary staging storage, and shortens end-to-end migration time.

.. note:: CloudStack does not distribute VDDK, operators must download it separately.
Along with the new VDDK-based conversion method the traditional OVF-based method remains supported for environments.
Operators can choose the conversion method on a per-migration basis in the UI import wizard.

Host Prerequisites for VDDK-based Conversion
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To use VDDK-based migration, operators must prepare each KVM host that will run the conversion: install the conversion
tools, install VDDK manually, configure libguestfs, and verify host connectivity to vCenter/ESXi.

Example: prepare one KVM conversion host

**Step 1: Install the conversion stack (RHEL / Rocky / Alma Linux)**

::

    dnf install -y epel-release
    dnf config-manager --set-enabled crb
    dnf install -y virt-v2v libguestfs-tools libguestfs-xfs qemu-img nbdkit

**Step 2: Configure libguestfs backend as** ``direct``

VDDK does not work with the default sandbox backend. Configure ``direct``:

::

    cat <<EOF > /etc/profile.d/libguestfs.sh
    export LIBGUESTFS_BACKEND=direct
    EOF

    source /etc/profile.d/libguestfs.sh

This can also be configured persistently with ``libguestfs.backend`` in ``/etc/cloudstack/agent/agent.properties`` (see `Agent Properties for VDDK-based Conversion`_ below).

**Step 3: Download and install VDDK**

Download the VDDK tarball and extract it to a known location on the KVM host, for example, ``/opt/vmware-vddk``.
The resulting directory must contain the VDDK libraries under a ``lib64`` subdirectory.

::

    mkdir -p /opt/vmware-vddk
    tar -xf VMware-vix-disklib-9*.tar.gz -C /opt/vmware-vddk

Expected layout after extraction::

    /opt/vmware-vddk/vmware-vix-disklib-distrib/
      lib64/
      include/
      bin64/

**Step 4: Add EL9 compatibility symlink (when using VDDK 9)**

On EL9 distributions, virt-v2v may expect ``libvixDiskLib.so.8``. Create this compatibility symlink:

::

    cd /opt/vmware-vddk/vmware-vix-disklib-distrib/lib64
    ln -s libvixDiskLib.so.9 libvixDiskLib.so.8

.. note:: This compatibility symlink is commonly required on RHEL 9, Rocky Linux 9, and Alma Linux 9.

**Step 5: Verify host setup**

::

    ls /opt/vmware-vddk/vmware-vix-disklib-distrib/lib64/libvixDiskLib.so.8
    virt-v2v --version
    nbdkit --version

**Step 6: Verify required network access**

The KVM conversion host must be able to reach:

.. cssclass:: table-striped table-bordered table-hover

==============================  ======  ==============================
Target                          Port    Purpose
==============================  ======  ==============================
vCenter                         443     API / authentication
ESXi hosts                      902     VDDK NFC disk transfer
ESXi hosts                      443     VM metadata
==============================  ======  ==============================

Agent Properties for VDDK-based Conversion
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following properties can be configured in ``/etc/cloudstack/agent/agent.properties`` on each KVM host to enable and tune the VDDK-based conversion.
After editing this file, restart the CloudStack agent (``systemctl restart cloudstack-agent``).
These values can also be passed in details parameters in importVm API as key-value pairs.

.. cssclass:: table-striped table-bordered table-hover

+------------------------+----------------------------------------------------------------------+-------------------------------------------------------+
| Property               | Description                                                          | Default / Example                                     |
+========================+======================================================================+=======================================================+
| ``libguestfs.backend`` | The libguestfs backend for VDDK-based conversion.                    | ``direct``                                            |
|                        | Must be set to ``direct`` for VDDK to work correctly.                |                                                       |
+------------------------+----------------------------------------------------------------------+-------------------------------------------------------+
| ``vddk.lib.dir``       | Path to the VDDK library directory on the KVM host.                  | ``/opt/vmware-vddk/vmware-vix-disklib-distrib``       |
|                        | Passed to virt-v2v as ``-io vddk-libdir=<path>``.                    |                                                       |
+------------------------+----------------------------------------------------------------------+-------------------------------------------------------+
| ``vddk.transports``    | Ordered VDDK transport preference.                                   | Example: ``nbd:nbdssl``                               |
|                        | Passed as ``-io vddk-transports=<value>`` to virt-v2v.               |                                                       |
+------------------------+----------------------------------------------------------------------+-------------------------------------------------------+
| ``vddk.thumbprint``    | Optional vCenter SHA1 thumbprint.                                    | If unset, CloudStack computes it automatically on     |
|                        | Passed as ``-io vddk-thumbprint=<value>`` to virt-v2v.               | the KVM host via ``openssl``.                         |
+------------------------+----------------------------------------------------------------------+-------------------------------------------------------+

Example configuration in ``/etc/cloudstack/agent/agent.properties``:

::

    # LIBGUESTFS backend to use for VMware to KVM conversion via VDDK (default: direct)
    libguestfs.backend=direct

    # Path to the VDDK library directory for VMware to KVM conversion via VDDK,
    # passed to virt-v2v as -io vddk-libdir=<path>
    vddk.lib.dir=/opt/vmware-vddk/vmware-vix-disklib-distrib

    # Ordered VDDK transport preference for VMware to KVM conversion via VDDK, passed as
    # -io vddk-transports=<value> to virt-v2v. Example: nbd:nbdssl
    # vddk.transports=nbd:nbdssl

    # Optional vCenter SHA1 thumbprint for VMware to KVM conversion via VDDK, passed as
    # -io vddk-thumbprint=<value>. If unset, CloudStack computes it on the KVM host via openssl.
    # vddk.thumbprint=


Recommendations for Using VDDK-based Conversion
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Use a single primary storage pool for direct conversion**

When VDDK-based conversion is enabled, it is strongly recommended to configure the conversion to write directly
to the destination primary storage pool (i.e., set *Convert to storage pool directly* to ``true`` in the import wizard).
This eliminates the two-step process of the traditional OVF method, conversion to temporary storage followed by
an import step, replacing it with a single streaming pipeline that writes converted QCOW2 disks directly to the
destination primary storage.

**Network placement for optimal disk transfer throughput**

For best performance, place the KVM conversion host on the same high-bandwidth network as the source ESXi hosts.
VDDK disk transfer uses VMware's NFC protocol on TCP port 902. ESXi routes NFC traffic to the conversion host based
on standard IP routing, if the conversion host is reachable over a dedicated storage or migration network,
ESXi will naturally select that VMkernel interface for disk transfer, keeping bulk data off the management network
without requiring any special configuration in virt-v2v or CloudStack.

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

|import-vm-from-vmware-to-kvm-options.png|

In the UI import wizard, administrators can select:

    - (Optional) A KVM host to perform the conversion (must have virt-v2v installed). In case it is not set, then a KVM host is randomly selected.
    - (Optional) A KVM host to import the converted files into CloudStack (this host must have access to the temporary conversion storage in order to move the converted files to the destination storage). In case it is not set, then a KVM host is randomly selected.
    - (Optional) Extra parameters: in case the global setting **convert.vmware.instance.to.kvm.extra.params.allowed** (disabled by default) is enabled, then administrators are allowed to pass extra parameters for the virt-v2v conversion command. This setting must be set along with the setting **convert.vmware.instance.to.kvm.extra.params.allowed.list** (empty by default) which indicates the list of parameters that CloudStack will accept for passing to the virt-v2v conversion command on the KVM hosts.
    
Since version 4.22 it is possible to indicate converting to storage pool directly (not using temporary storage for conversion). This is set to false by default, in which case a temporary conversion storage is used.

    - When set to false (temporary storage used), then administrators must select a Temporary destination storage. The default is Secondary Storage, but if using Primary Storage - only NFS pools are supported.
    - When set to true (not using temporary storage), then administrators must select the destination storage pool. The supported storage pools are: NFS, Local Storage and SharedMountPoint storage pools, under the following assumptions:
     - The KVM host for conversion must be selected and must have access to the destination storage
     - The KVM host for importing must be selected and must have access to the destination storage
     - In case of Local storage, the selected KVM host for conversion must be the same as the KVM host for importing

Since version 4.22.1 it is possible to select the Guest OS for the VM to be imported, based on the source VMware VM Guest OS.

    - When CloudStack has Guest OS mappings for the source VMware Guest OS VM, then the list of supported Guest OS is displayed and administratos can select one of them.
    - In case there are no Guest OS mappings for the source VMware Guest OS VM, then the default import template Guest OS will be used.

The conversion is performed on a random (or explicitly chosen) KVM host (if the ovftools are installed), otherwise, the management server will export/copy the VM files (optionally, you can force this action to be done by the management server even the KVM hosts have the ovftools installed in it). Irrelevant if the KVM host or the management server performs the copy of the VM files (OVF), you can further either let CloudStack choose which KVM host should do the conversion of the VM files using virt-v2v and which host will import the files to the destination Primary Storage Pool, or you can explicitly choose these KVM hosts for each of the 2 mentioned operations.

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

VM Import Tasks
---------------

Since version 4.22 administrators can monitor the VMware to KVM migration jobs. The new section is displayed on *Tools > Import-Export Instances > Migrate existing instances to KVM > VM Import Tasks*:

|import-vm-from-vmware-to-kvm-tasks.png|

The tasks can be filtered by state: Completed, Running or Failed, or listing all the tasks.

.. |import-vm-from-vmware-to-kvm.png| image:: /_static/images/import-vm-from-vmware-to-kvm.png
   :alt: Import VMware Virtual Machines into KVM.
   :width: 800 px

.. |import-vm-from-vmware-to-kvm-options.png| image:: /_static/images/import-vm-from-vmware-to-kvm-options.png
   :alt: Import VMware Virtual Machines into KVM Options.
   :width: 800 px

.. |import-vm-from-vmware-to-kvm-tasks.png| image:: /_static/images/import-vm-from-vmware-to-kvm-tasks.png
   :alt: Listing Importing Tasks to Migrate VMware Virtual Machines into KVM.
   :width: 800 px
