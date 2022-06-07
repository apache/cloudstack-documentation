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

Apache CloudStack 4.17.0.0 is a 4.17 LTS release with 16 major new
features, and over 210 enhancements and fixes since 4.16. Highlights include:

• IPv6 with Static Routing
• Deprecate systemvm.iso & Live Patch (Zero Downtime Upgrades)
• CloudStack Status & management (API & UI)
• User-Shared Networks
• StorPool storage plugin
• Storage-based Snapshots for KVM VMs
• UI: Added attach and detach features to UI for ROOT disks
• KVM: Enable CloudStack to use multiple LOCAL storage pools
• Multiple SSH Keys support
• Reserve and release Public Ips

The full list of new features can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.17.0.0/releasenotes/changes.html

Legacy UI Removal Notice
========================

The legacy UI was deprecated with Apache CloudStack 4.15 release and
with 4.16 release the legacy UI has been removed. Users are encouraged to
implement a migration path in their production environments.
