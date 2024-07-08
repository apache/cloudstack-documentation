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

Compatibility Matrix
====================

Supported OS Versions for Management Server
-------------------------------------------

This section lists the operating systems that are supported for running
CloudStack Management Server.

-  Ubuntu 20.04 LTS, 22.04 LTS, 24.04 LTS
-  Oracle Linux 8, 9
-  Alma Linux 8, 9
-  Rocky Linux 8, 9
-  RHEL versions 8, 9
-  openSUSE Leap 15
-  SUSE Linux Enterprise Server 15 (not tested, but expected to work same as with openSUSE 15)
-  Debian 12 (not tested, but expected to work same as Ubuntu)

   .. note:: There is a known issue with ipmitool with EL8 / EL9 / SUSE, so certain functionality such as out of band management might not work

Software Requirements
~~~~~~~~~~~~~~~~~~~~~

-  Java JRE 11 or Java JRE 17
-  MySQL 8.0 (or equivalent compatible DBMS)

Supported Hypervisor Versions
-----------------------------

CloudStack supports three hypervisor families, KVM, XenServer/XCP-ng with XAPI,
and VMware with vSphere.

-  Ubuntu 20.04 LTS, 22.04 LTS, 24.04 LTS with KVM
-  Oracle Linux 8, 9 with KVM
-  Alma Linux 8, 9 with KVM
-  Rocky Linux 8, 9 with KVM
-  Red Hat Enterprise Linux 8, 9 with KVM
-  openSUSE Leap 15 with KVM
-  SUSE Linux Enterprise Server 15 with KVM
-  XCP-ng 8.2.0
-  Citrix Hypervisor/XenServer version 8.2 (not tested, but expected to work. For 8.2 please check the note below) with latest hotfixes
-  Debian 12 with KVM (not tested, but expected to work same as Ubuntu)

   .. note:: It is now required to enable HA on the XenServer pool in order to recover from a pool-master failure. Please refer to the `XenServer documentation <https://docs.citrix.com/en-us/xencenter/7-1/pools-ha-enable.html>`_.

   .. note:: For XenServer version 8.2 to work it might be necessary to manually add a custom storage repository with name "XenServer Tools" containing the systemvm.iso file.

-  VMware versions 7.0 and 8.0.0

   .. note:: The following VMware minor versions are supported and tested: 7.0, 7.0.1.0, 7.0.2.0, 7.0.3.0, 8.0, 8.0a (8.0.0.1), 8.0b (8.0.0.2), 8.0c (8.0.0.3).
    For any minor versions without hypervisor mappings, all Instances have guest OS identifier "otherGuest64" (x86-64 architecture) or "otherGuest" (other architectures).

   .. note:: There are some known issues with 8.0 U1 (https://github.com/apache/cloudstack/issues/7572). VMware 8.0 U1 (8.0.1.0) is not supported yet.

-  LXC Host Containers on RHEL 8, 9 (not tested to work fine for last many CloudStack releases)
-  Windows Server 2012 R2 with Hyper-V Role enabled (not tested to work fine for last many CloudStack releases)
-  Hyper-V 2012 R2 (not tested to work fine for last many CloudStack releases)
-  Oracle VM 3.0+ (not tested to work fine for last many CloudStack releases)
-  Bare metal hosts are supported, which have no hypervisor. These hosts
   can run the following operating systems:

   -  Fedora 17
   -  Ubuntu 12.04

(not tested to work for last many CloudStack releases)

Supported External Devices
--------------------------

-  Netscaler VPX and MPX versions 9.3, 10.1e and 10.5 (not tested to work fine for last many CloudStack releases)
-  Netscaler SDX version 9.3, 10.1e and 10.5 (not tested to work fine for last many CloudStack releases)
-  SRX (Model srx100b) versions 10.3 to 10.4 R7.5 (not tested to work fine for last many CloudStack releases)
-  F5 11.X (not tested to work fine for last many CloudStack releases)
-  Force 10 Switch version S4810 for Baremetal Advanced Networks (not tested to work fine for last many CloudStack releases)

Supported Browsers
------------------

The CloudStack Web-based UI should be compatible with any modern
browser, but it's possible that some browsers will not render portions
of the UI reliably, depending on their support of Web standards. For
best results, one of the following browsers recommended:

-  Firefox version 75 or later

-  Google Chrome version 85 or later

-  Safari 12+

Notice Of Management OSes and Hypervisors to be Deprecated
----------------------------------------------------------

The following hypervisors are no longer be supported in this release due to vendor EOL:

-  KVM with CentOS/RHEL 6.x, 7.x
-  KVM with CentOS 8.x
-  KVM with Ubuntu 14.04, 16.04, 18.04
-  XCP-ng 7.4.0, 7.6.0, 8.0.0, 8.1.0
-  XenServer 6.2, 6.5, 7.0, 7.1, 7.2, 7.4, 7.5, 8.0, 8.1
-  vSphere 5.0, 5.1, 5.5, 6.0, 6.5, 6.7

The following Management Server Operating Systems are no longer supported in this release due to vendor EOL:

-  CentOS/RHEL 6.x, 7.x
-  CentOS 8.x [1]_
-  Ubuntu 14.04, 16.04, 18.04

.. [1] in spite of mostly being phased out some support is remaining in for now. See the section :ref:`Possible Issue with Guest OS IDs` for details.

Please see `CloudStack Wiki <https://cwiki.apache.org/confluence/display/CLOUDSTACK/Hypervisor+and+Management+Server+OS+EOL+Dates>`_
for details.
