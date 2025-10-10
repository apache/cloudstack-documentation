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

Currently, only backup of VMs from the NFS-based Primary Storage are tested to work.
You can also make backups of CEPH-based VMs, but restoring is not possible yet.

The NAS B&R plugin requires admin to first add backup repositories which are
network-attached storage (shared storage). It supports NFS, CIFS/Samba and CephFS.

When initiating B&R operations on KVM instance, the assigned backup offering
is used to infer backup repository (NAS) details which are then used to mount
the shared storage temporarily on the KVM host to perform instance backup/restore
disks operations. This also requires that admin installs NAS-storage specific
utilities on the KVM hosts such as nfs-utils/nfs-common, ceph-common and cifs-utils.

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

Using the NAS Backup and Recovery Plugin
----------------------------------------
To use the NAS Backup and Recovery Plugin, the Backup and Recovery framework needs to be enabled first. Then the backup plugin 'nas' needs to be enabled on either the global or zone settings. 

================================= ========================
Configuration                     Value
================================= ========================
backup.framework.enabled          true
backup.framework.provider.plugin  nas
================================= ========================

Once the above two configurations are set, restart the cloudstack-management service. After restart check the Settings of the Zone where you want to enable NAS backups - make sure that the "backup.framework.enabled"="true" on the Setting tab of the Zone. Once this is done, we can add the backup repository for the 'nas' Backup and Recovery plugin.
Navigate to the Infrastructure -> Backup Repository. Click on 'Add Backup Repository' and fill the form.

=================== ========================
Field               Value
=================== ========================
Name                A suitable name to represent the Backup Repository
Address             URL, in case of NFS <server IP>:/path
Type                NFS / CIFS / CEPH
Mount options       Any mount point options to be passed while mounting this storage on the hypervisor.
Zone                The zone in CloudStack with which this Backup Repository must be associated.
=================== ========================

.. image:: /_static/images/B&R-Backup-Repository.png
   :align: center
   :alt: NAS Backup repository

Pay attention to the "Name" given to this repository, as you will have to specify this in the "External ID" field when creating Backup Offerings (Importing backup offering)

Once the Backup Repository is created, we need to add a Backup Offering, in this plugin the Backup offering is a placeholder to associate an instance to a Backup Repository. While creating the Backup Offering, select the desired Backup Repository. Associate the Backup Offering on an instance to create an Adhoc or scheduled backup.

For the "External ID", please specify the name of the previously created backup repository.

.. image:: /_static/images/B&R-Backup-Offerings.png
   :align: center
   :alt: NAS Backup offerings

After this has been done, you can go to any Instance view and there will be buttons available for either ad-hoc backup or a scheduled backup of the VM

Quiesce (Filesystem Freeze and Thaw)
------------------------------------

Users can set quiesce to true while creating a backup or a backup schedule.
When a backup is initiated with quiesce enabled, CloudStack uses QEMU guest agent
to freeze the filesystem before starting backup. This operation flushes all dirty
filesystem buffers to disk and quiesces new writes. The filesystem is then thawed
immediately after the backup process starts, keeping the freezing window very short.

|NASB&R-quiesceInstance.png|

This enhancement brings the NAS backup plugin from crash-consistent backups closer to
application-consistent backups.

Points to note:

#. The feature requires qemu-guest-agent to be installed and running on the guest instance.
#. This method does not capture the memory state of the guest. Any data held in application memory
   that hasn’t been flushed to disk prior to the filesystem freeze will not be captured.
#. For fully application-consistent backups, guest applications must implement pre-freeze hooks
   to flush their internal state to disk before the filesystem is frozen.

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
based primary storage pools, and restored volumes are fully backed disks (i.e.
not using any backing template file).

Backup and restore operations are not fully supported for CKS cluster instances and should
be avoided.

.. |NASB&R-quiesceInstance.png| image:: /_static/images/NASB&R-quiesceInstance.png
   :alt: Quiesce option while creating backups.
   :width: 400 px
