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


What's New in |release|
=======================

Apache CloudStack |release| is a 4.22 LTS release with 10 new features,
around 15 improvements and more than 140 bug fixes since the 4.21.0.0 release.
Some of the highlights include:

Support for NAS Backup & Restore with Ceph and Shared MountPoint
Configurable backup and backup-schedule during instance deployment
Instance creation from backup in another zone (DRaaS use-case)
SSL offloading support in VR-based load balancers
Baremetal support with built-in Canonical/MaaS extension
Support for noVNC and External Console within the Extensions Framework, including built-in Proxmox extension
VMware-to-KVM migration improvements
Overview UI page and related APIs for scheduled snapshots
Allow per-zone Console Proxy configuration
Bypass secondary storage during the volume migration from one primary storage pool to another in the same cluster
Make KVM domains persistent upon unmanaging them
Support for userdata on System VMs - use case: rsyslog-based centralized logging for System VMs and VRs
Support for EL10 (Oracle Linux, AlmaLinux, Rocky Linux, RHEL) and openSUSE 15.6 as Management Server and KVM host distributions
Replace md5sum with sha512sum for improved security
Support for CloudStack CSI driver to dynamically provision and manage the volumes and snapshots
Enable KVM volume and VM snapshot by default
Support xz format for template registration
Support for shared Filesystem on Config Drive Networks

Known Issues
------------

• Starting 4.21 VM snapshots are supported for instances on KVM hosts. However, volume snapshots and VM snapshots cannot coexist.
  Restoring a volume snapshot will remove any existing VM snapshots and may lead to data loss.
  There is a UI issue where error messages in such scenarios may not clearly indicate the problem.

• When managing and unmanaging UEFI-based VMs on KVM hosts, migration of such VMs may fail in certain scenarios.
  This typically occurs when a VM that was unmanaged and later re-imported is started on a different host and then
  migrated back to its original host. The migration fails because the VM domain still exists on the original host,
  resulting in a conflict. As a workaround, manually remove the old domain from the original host before attempting the migration again.

The full list of new features can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.22.0.0/releasenotes/changes.html
