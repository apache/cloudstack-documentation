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

Apache CloudStack |release| is the initial 4.19 LTS release. It has over 300 fixes
and features since the 4.18.1.0 release.

The full list of fixes and improvements can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.19.0.0/releasenotes/changes.html

What's in since 4.19.0.0
========================

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
not full snapshots and they rely on the snapshots on the primary storage.
To prevent any loss of data, care must be taken during revert operation and
it must be ensured that the source primary storage snapshot file is present.
