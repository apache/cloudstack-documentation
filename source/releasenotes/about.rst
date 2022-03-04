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

Apache CloudStack |release| is a 4.16 LTS minor release with over 150 fixes and
improvements since the 4.16.0.0 release. Highlights include:

• System VM Template improvements
• CKS enhancements
• Support for VMware 7.0u2, 7.0u3
• Several Hypervisor (VMware, KVM, XenServer) fixes and improvements 
• Several UI fixes and improvements
• First Install and Onboarding Message improvements
• Log4j v1.x migration to reload4j v1.2.18.0
• Several security fixes addressing multiple CVEs and improvements

The full list of fixes and improvements can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.16.1.0/releasenotes/changes.html

What's New in 4.16.0.0
=======================

Apache CloudStack 4.16.0.0 is a 4.16 LTS release with over 22 major new
features, and over 244 enhancements and fixes since 4.15. Highlights include:

• System VM Template improvements
• CKS Support for Cluster Autoscaling
• Dell EMC VxFlex integration
• Linstor Volume Plugin integration
• Support for OpenSuse
• Support for Rocky Linux
• Granular control of dynamic scaling of VM's CPU/RAM
• Comments in the UI
• Resource Icons
• Bulk actions through the UI
• UI for VM Ingestion
• L2 Networks Persistent modern
• Script cloudstack-setup-databases improvement
• Add mac learning mode in network offering
• API-call to declare host as Degraded
• New API endpoint to update pod management network IP range
• Add New API endpoint: UpdateVlanIpRange

The full list of new features can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.16.0.0/releasenotes/changes.html

Legacy UI Removal Notice
========================

The legacy UI was deprecated with Apache CloudStack 4.15 release and
with 4.16 release the legacy UI has been removed. Users are encouraged to
implement a migration path in their production environments.
