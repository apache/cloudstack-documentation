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

Refer to the advisory blog at
https://cloudstack.apache.org/blog/security-release-advisory-4.19.0.2-4.18.2.1

What's in 4.19.0.1
==================

Refer to the advisory blog at
https://cloudstack.apache.org/blog/security-release-advisory-4.19.0.1-4.18.1.1

What's in since 4.19.0.0
========================

Apache CloudStack 4.19.0.0 is the initial 4.19 LTS release. It has over 300 fixes
and features since the 4.18.1.0 release.

The full list of fixes and improvements can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.19.0.0/releasenotes/changes.html

Apache CloudStack 4.19.0.0 is the initial 4.19 LTS release with 300+ new
features, improvements and bug fixes since 4.18, including 26 major
new features. Some of the highlights include:

• CloudStack Object Storage Feature
• VMware to KVM Migration
• KVM Import
• CloudStack DRS
• OAuth2 Authentication
• VNF Appliances Support
• CloudStack DRS
• CloudStack Snapshot Copy
• Scheduled Instance Lifecycle Operations
• Guest OS Management
• Pure Flash Array and HPE-Primera Support
• User-specified source NAT
• Storage Browser
• Safe CloudStack Shutdown
• New CloudStack Dashboard
• Domain migration
• Flexible tags for hosts and storage pools
• Support for Userdata in Autoscale Groups
• KVM Host HA for StorPool storage
• Dynamic secondary storage selection
• Domain VPCs
• Global ACL for VPCs

The full list of new features can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.19.0.0/releasenotes/changes.html

.. _guestosids

Possible Issue with volume snapshot revert with KVM
===================================================

Between versions 4.17.x, 4.18.0 and 4.18.1, KVM volume snapshot backups were
not full snapshots and they rely on the primary storage as a backing store.
To prevent any loss of data, care must be taken during revert operation and
it must be ensured that the source primary storage snapshot file is present
if the snapshot is created with any of these CloudStack versions.

Users will have a backing store in their volume snapshots in the following cases:

- the snapshots are from a ROOT volume created from template;

Users will not have a backing store in their volume snapshots in the following cases:

- the snapshots are from ROOT volumes created with ISO;
- the snapshots are from DATADISK volumes;

Following there are two queries to help users identify snapshots with a backing store:

Identify snapshots that were not removed yet and were created from a volume that was created from a template:

.. parsed-literal::
   SELECT  s.uuid AS "Snapshot ID",
           s.name AS "Snapshot Name",
           s.created AS "Snapshot creation datetime",
           img_s.uuid AS "Sec Storage ID",
           img_s.name AS "Sec Storage Name",
           ssr.install_path AS "Snapshot path on Sec Storage",
           v.uuid AS "Volume ID",
           v.name AS "Volume Name"
   FROM    cloud.snapshots s
   INNER   JOIN cloud.volumes v ON (v.id = s.volume_id)
   INNER   JOIN cloud.snapshot_store_ref ssr ON (ssr.snapshot_id = s.id
                                             AND ssr.store_role = 'Image')
   INNER   JOIN cloud.image_store img_s  ON (img_s.id = ssr.store_id)
   WHERE   s.removed IS NULL
   AND   v.template_id IS NOT NULL;

With that, one can use qemu-img info in the snapshot file to check if they have a backing store.

For those snapshots that have a backing store, one can use the following query to check which template is it and in which storage pool it is:

.. parsed-literal::
   SELECT  vt.uuid AS "Template ID",
         vt.name AS "Template Name",
         tsr.install_path AS "Template file on Pri Storage",
         sp.uuid AS "Pri Storage ID",
         sp.name AS "Pri Storage Name",
         sp.`path` AS "Pri Storage Path",
         sp.pool_type as "Pri Storage type"
   FROM    cloud.template_spool_ref tsr
   INNER   JOIN cloud.storage_pool sp ON (sp.id = tsr.pool_id AND sp.removed IS NULL)
   INNER   JOIN cloud.vm_template vt ON (vt.id = tsr.template_id)
   WHERE   tsr.install_path = "<template file in the snapshot backing store>";

After identifying the snapshots with a backing store and the related templates, one can mount the secondary storage on a host that has access to the template and use qemu-img convert on the snapshot to consolidate it:

.. parsed-literal::
   qemu-img convert -O qcow2 -U --image-opts driver=qcow2,file.filename=<path to snapshot on secondary storage> <path to snapshot on secondary storage>-converted
