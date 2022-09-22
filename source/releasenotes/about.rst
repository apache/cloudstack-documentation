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

Apache CloudStack |release| is a 4.17 LTS minor release with over 150 fixes and
improvements since the 4.17.0.0 release. Highlights include:

• Support for Ubuntu 22.04 LTS as management server and KVM host
• Improvements for System VM storage migration on KVM
• CKS cluster upgrade enhancements
• Several network and VPC related fixes especially related IPv6 and permissions
• KVM libvirt Java library upgrade
• KVM Shared Mount Point fix
• VMware local storage volume migration improvements

The full list of fixes and improvements can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.17.1.0/releasenotes/changes.html

What's New in 4.17.0.0
======================

Apache CloudStack 4.17.0.0 is a 4.17 LTS release with 383 new
features, improvements and bug fixes since 4.16, including 16 major
new features. Some of the highlights include:

• IPv6 with Static Routing
• Zero Downtime Upgrades
• Virtual Router Live Patching
• CloudStack Status & management
• User Shared Networks
• StorPool storage plugin
• Storage-based Snapshots for KVM Instances
• Attach and detach features to UI for ROOT disks
• Enable CloudStack to use multiple LOCAL storage pools
• Multiple SSH Keys support
• Reserve and release Public IPs

The full list of new features can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.17.0.0/releasenotes/changes.html

Apache CloudStack Advisory on KVM Shared Mount Point issues on version 4.17.0.0
===============================================================================

On 14th June 2022, a new issue affecting only KVM users using Shared
Mount Point storage was reported [1]. This issue affects the creation
and the usage of existing Shared Mount Point storage pools on Apache
CloudStack 4.17.0.0.

Apache CloudStack 4.17.0.0 added support for the StorPool storage
based on Shared Mount Point. However, the current version of
CloudStack doesn't allow multiple implementations of Shared Mount
Point storage pool providers, causing the StorPool provider to
override the default implementation. This affected the other storage
pool providers for Shared Mount Point since CloudStack tries to add
them as a StorPool storage pool.

To mitigate the issue, a CloudStack administrator needs to do the
following on version 4.17.0.0:

• On each management server: stop the CloudStack management service, remove the Storpool plugin jar on /usr/share/cloudstack-management/lib/cloud-plugin-storage-volume-storpool-4.17.0.0.jar and restart the Cloudstack management service
• On each KVM host: stop the CloudStack agent service, remove the StorPool plugin jar on /usr/share/cloudstack-agent/lib/cloud-plugin-storage-volume-storpool-4.17.0.0.jar and restart the CloudStack agent service

Note: This workaround removes the StorPool plugin support. StorPool
users should not apply the workaround to continue using their Storpool
storage.

This issue will be fixed in the upcoming CloudStack version 4.17.1.0.

[1] https://github.com/apache/cloudstack/issues/6455


Legacy UI Removal Notice
========================

The legacy UI was deprecated with Apache CloudStack 4.15 release and
with 4.16 release the legacy UI has been removed. Users are encouraged to
implement a migration path in their production environments.
