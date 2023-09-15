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

Apache CloudStack |release| is a 4.18 LTS minor release with 196 fixes
since the 4.18.0.0 release. Some of the highlights include:

• Support Managed User Data in AutoScale VM groups
• Support CKS (CloudStack Kubernetes Cluster) in VPC tiers
• Support for VMware 8.0.0.x
• Several Hypervisor (VMware, KVM, XenServer) fixes and improvements
• Several UI fixes and improvements
• Several Network (L2, VXLAN, etc) fixes and improvements
• Several System VM (CPVM, SSVM) fixes and improvements
• Improve Solidfire storage plugin integration on VMware
• Support volume migration in ScaleIO/PowerFlex within and across ScaleIO/PowerFlex storage clusters
• Volume encryption support for StorPool
• Fix CloudStack upgrade with some MySQL versions
• Fix guest OSes and guest OS mappings in CloudStack database

The full list of fixes and improvements can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.18.1.0/releasenotes/changes.html

What's in since 4.18.0.0
======================

Apache CloudStack 4.18.0.0 is the initial 4.18 LTS release with 300+ new
features, improvements and bug fixes since 4.17, including 19 major
new features. Some of the highlights include:

• Edge Zones
• Autoscaling
• Managed User Data
• Two-Factor Authentication Framework
• Support for Time-based OTP (TOTP) Authenticator
• Volume Encryption
• SDN Integration – Tungsten Fabric
• Ceph Multi Monitor Support
• API-Driven Console Access
• Console Access Security Improvements
• New Global settings UI
• Configurable MTU for VR
• Adaptative Affinity Groups
• Custom DNS Servers for Networks
• Improved Guest OS Support Framework
• Support for Enterprise Linux 9
• Networker Backup Plugin for KVM Hypervisor
• Custom Quota Tariffs
• Secure VNC for KVM

The full list of new features can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.18.0.0/releasenotes/changes.html

.. _guestosids

Possible Issue with Guest OS IDs
================================

It has been noticed during upgrade testing that some environment, where
custom guest OSses where added and mapping for those OSses where added,
problems may occur during upgrade. Part of the mitigation is to make sure
OSses that are newly mapped but should have already been in the guest_os
table are there. Make sure you apply those before you start the new 4.18
management server.

first check which of the guest_os entries you miss:

.. parsed-literal::

  SELECT * FROM cloud.guest_os WHERE display_name IN (´CentOS 8´, ´Debian GNU/Linux 10 (32-bit)´, ´Debian GNU/Linux 10 (64-bit)´, ´SUSE Linux Enterprise Server 15 (64-bit)´, ´Windows Server 2019 (64-bit)´)

Then apply any of the following lines that you might need.

.. parsed-literal::

  INSERT INTO cloud.guest_os (uuid, category_id, display_name, created, is_user_defined) VALUES (UUID(), '1', 'CentOS 8', now(), '0');
  INSERT INTO cloud.guest_os (uuid, category_id, display_name, created, is_user_defined) VALUES (UUID(), '2', 'Debian GNU/Linux 10 (32-bit)', now(), '0');
  INSERT INTO cloud.guest_os (uuid, category_id, display_name, created, is_user_defined) VALUES (UUID(), '2', 'Debian GNU/Linux 10 (64-bit)', now(), '0');
  INSERT INTO cloud.guest_os (uuid, category_id, display_name, created, is_user_defined) VALUES (UUID(), '5', 'SUSE Linux Enterprise Server 15 (64-bit)', now(), '0');
  INSERT INTO cloud.guest_os (uuid, category_id, display_name, created, is_user_defined) VALUES (UUID(), '6', 'Windows Server 2019 (64-bit)', now(), '0');
