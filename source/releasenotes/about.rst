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

Apache CloudStack |release| is a 4.23 Regular release with 9 new features,
around 20 improvements and more than 120 bug fixes since the 4.22.0.0 release.
Some of the highlights include:

• CLVM (Clustered LVM) Enhancements for KVM
• Key Management Service (KMS) with HSM Integration
• NetApp ONTAP Primary Storage Support
• KVM Backup on Secondary Storage (KBOSS), a new provider with support for incremental backups, compression, and validation
• Incremental Backup Support for the NAS Backup and Recovery Provider
• Support for Dedicating Backup Offerings to Domains
• Veeam Backup and Recovery Integration for KVM
• Conserve Mode for VPC Offerings
• DNS Framework, with PowerDNS as the first plugin
• DHCP Lease Timeout Support
• MAC Address Reuse Control for Virtual Router Public NICs
• Network Extension: Orchestrate External Network Devices
• Support Firewall Rules on Public IPs in VPC
• Support for Enabling/Disabling NICs on KVM
• API Key Pairs with Limited Permissions and Expiry Dates
• Keycloak OAuth Provider Support
• Per-Domain OAuth Provider Support
• Affinity Group Selection during Kubernetes Cluster Creation
• Headlamp as the New Kubernetes Dashboard (Legacy Dashboard Deprecated)
• Clone Existing Compute/Service Offerings and Update Them
• Flexible JavaScript Rules for Guest OS Allocation
• Quota Plugin Improvements and UI Rework
• Scheduled Min/Max Sizing for VM Autoscaling Groups
• Live Scaling for VMs with Fixed Service Offerings on KVM
• XenServer/XCP-ng 8.3/8.4 vTPM Support
• Several UI fixes and improvements

Known Issues
------------

• Restoring a backed up volume and attaching it to a VM can fail on KVM hosts, across NFS, Linstor and Ceph
  primary storage, due to a regression in the restore-and-attach command handling. See
  https://github.com/apache/cloudstack/pull/14007 for details and status.

The full list of new features can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.23.0.0/releasenotes/changes.html
