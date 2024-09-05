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

.. _NAS Backup and Recovery Plugin:

NAS Backup and Recovery Plugin
==============================

About the NAS Backup and Recovery Plugin
----------------------------------------

The NAS Backup and Recovery Plugin provider simple B&R operations for KVM
instances to any shared storage (NAS). It is based on `libvirt push backup mode
<https://libvirt.org/kbase/live_full_disk_backup.html>`_
to take full instance backups (qcow2) and requires libvirt-7.2.0 and QEMU-4.2,
or high versions on the KVM hosts.

The NAS B&R plugin requires admin to first add backup repositories which are
network-attached storage (shared storage). Currently it supports NFS, and may
support other shared storage such as CephFS and CIFS/Samba in future.

When initiating B&R operations on KVM instance, the assigned backup offering
is used to infer backup repository (NAS) details which are then used to mount
the shared storage temporarily on the KVM host to peform instance backup/restore
disks operations. This also requires that admin installs NAS-storage specific
utilities on the KVM hosts such as nfs-utils/nfs-common (ceph-common, cifs-utils).

Consider the following mount, typically performed on a KVM/Linux host to mount storage:

    mount -t <nas/storage type> -o <mount options> <address> <mount point>

Some examples for variety of shared storage can be:

    mount -t nfs 10.10.1.10:/export /target -o vers=4.2,defaults

    mount -t ceph 10.10.1.10,10.10.1.11,10.10.1.12:/ /target -o name=user,secret=xyz,defaults

The backup repository is designed to accept these parameters (type, address and
mount options) as configurations to be used to execute mount operations such as
illustrated above.

With 'nas' B&R plugin enabled, after a backup repositories are added, root
admins can create new backup offerings by selecting the zone and the backup
repository. These backup offerings are then assigned and used with KVM instances
to perform support B&R actions and operations.

Support Information and Limitation
----------------------------------

The NAS B&R plugin has been tested with EL8, EL9, Ubuntu 22.04 and 24.04. Older
KVM distros such as EL7, Ubuntu 20.04 etc may not work due to libvirt/qemu
version requirements. Other supported KVM-distros are not tested but may work
such as OpenSUSE 15, Debian 11 and Debian 12.

Instance backups are full disk backups and limited by libvirt's ability to
initiate and handle backup. All such backups are exported and stored in qcow2
format. Due to this, restore operation are supported for volumes of type qcow2
and limited to NFS and local storage based primary storage pools.

For running instances, their disks (of any format/storage type) are backed up by
libvirtd's push based efficient-backup mechanism exported as qcow2 disks on the
backup repository.

For stopped instances, `qemu-img` is used to convert and export full-disk backup
in qcow2 format to the backup repository.

For restore operations, the KVM instance must be stopped in CloudStack.
Currently, only volume(s) restoration is supported only to NFS and local storage
based primary storage pools, and restored volumes are fully baked disks (i.e.
not using any backing template file).

Restoring fully expunged and unmanaged instances are not supported. Backup and
restore operations are not fully supported for CKS cluster instances and should
be avoided.
