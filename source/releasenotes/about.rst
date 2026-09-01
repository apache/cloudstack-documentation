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

• NetApp ONTAP Primary Storage Support, including volume management and storage pool maintenance
• Key Management Service (KMS) with HSM Integration
• CloudStack DNS Framework, with PowerDNS as the first plugin
• Network Extension: Orchestrate External Network Devices
• API Key Pair Restructure, allowing multiple API key pairs per user
• Keycloak OAuth Provider Support
• KVM Backup on Secondary Storage (KBOSS), a new backup provider
• Veeam Backup and Recovery Integration for KVM
• CLVM (Clustered LVM) Enhancements and Fixes
• Support Firewall Rules on Public IPs in VPC
• Clone Existing Compute/Service Offerings and Update Them
• Incremental NAS Backup Support for KVM
• Support for Dedicating Backup Offerings to Domains
• Per-Domain OAuth Provider Support (Google, GitHub)
• Conserve Mode for VPC Offerings
• Live Scaling for VMs with Fixed Service Offerings on KVM
• Scheduled Min/Max Sizing for VM Autoscaling Groups
• CKS: Affinity Group Selection during Cluster Creation
• Headlamp as the New Kubernetes Dashboard (Legacy Dashboard Deprecated)
• Support for Enabling/Disabling NICs on KVM
• MAC Address Reuse Control for Virtual Router Public NICs
• Several UI fixes and improvements

Known Issues
------------

• Restoring a backed up volume and attaching it to a VM can fail on KVM hosts, across NFS, Linstor and Ceph
  primary storage, due to a regression in the restore-and-attach command handling. See
  https://github.com/apache/cloudstack/pull/14007 for details and status.

The full list of new features can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.23.0.0/releasenotes/changes.html
