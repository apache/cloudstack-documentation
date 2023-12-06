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

.. sub-section included in upgrade notes.

Update System VM Templates
--------------------------

.. note::
   From ACS 4.16 onwards, CloudStack will support automatic registration of System VM
   Templates (when using noredist packages), if not done prior initiating upgrade. However, the usual upgrade process
   continues to be supported. 

#. While running the existing |version_to_upgrade| system, log in to the UI as 
   the root administrator.

#. In the left navigation bar, click Templates.

#. In Select view, click Templates.

#. Click Register Template.
   The Register Template dialog box is displayed.

#. To register the System VM Template do the following:

   In the Register Template dialog box, specify the following values
   (do not change these):

   .. cssclass:: table-striped table-bordered table-hover

   +------------+------------------------------------------------------------+
   | Hypervisor | Description                                                |
   +============+============================================================+
   | XenServer  | Name: |sysvm64-name-xen|                                   |
   |            |                                                            |
   |            | Description: |sysvm64-name-xen|                            |
   |            |                                                            |
   |            | URL: |sysvm64-url-xen|                                     |
   |            |                                                            |
   |            | Zone: Choose the zone where this hypervisor is used        |
   |            |                                                            |
   |            | Hypervisor: XenServer                                      |
   |            |                                                            |
   |            | Format: VHD                                                |
   |            |                                                            |
   |            | OS Type: Other Linux (64-bit)                              |
   |            |                                                            |
   |            | Extractable: no                                            |
   |            |                                                            |
   |            | Password Enabled: no                                       |
   |            |                                                            |
   |            | Public: no                                                 |
   |            |                                                            |
   |            | Featured: no                                               |
   |            |                                                            |
   |            | Routing: no                                                |
   +------------+------------------------------------------------------------+
   | KVM        | Name: |sysvm64-name-kvm|                                   |
   |            |                                                            |
   |            | Description: |sysvm64-name-kvm|                            |
   |            |                                                            |
   |            | URL: |sysvm64-url-kvm|                                     |  
   |            |                                                            |
   |            | Zone: Choose the zone where this hypervisor is used        |
   |            |                                                            |
   |            | Hypervisor: KVM                                            |
   |            |                                                            |
   |            | Format: QCOW2                                              |
   |            |                                                            |
   |            | OS Type: Debian GNU/Linux 7.0 (64-bit) (or the             |
   |            | highest Debian release number available in the             |
   |            | dropdown)                                                  |
   |            |                                                            |
   |            | Extractable: no                                            |
   |            |                                                            |
   |            | Password Enabled: no                                       |
   |            |                                                            |
   |            | Public: no                                                 |
   |            |                                                            |
   |            | Featured: no                                               |
   |            |                                                            |
   |            | Routing: no                                                |
   +------------+------------------------------------------------------------+
   | VMware     | Name: |sysvm64-name-vmware|                                |
   |            |                                                            |
   |            | Description: |sysvm64-name-vmware|                         |
   |            |                                                            |
   |            | URL: |sysvm64-url-vmware|                                  |
   |            |                                                            |
   |            | Zone: Choose the zone where this hypervisor is used        |
   |            |                                                            |
   |            | Hypervisor: VMware                                         |
   |            |                                                            |
   |            | Format: OVA                                                |
   |            |                                                            |
   |            | OS Type: Other Linux (64-bit)                              |
   |            |                                                            |
   |            | Extractable: no                                            |
   |            |                                                            |
   |            | Password Enabled: no                                       |
   |            |                                                            |
   |            | Public: no                                                 |
   |            |                                                            |
   |            | Featured: no                                               |
   |            |                                                            |
   |            | Routing: no                                                |
   +------------+------------------------------------------------------------+
   | HyperV     | Name: |sysvm64-name-hyperv|                                |
   |            |                                                            |
   |            | Description: |sysvm64-name-hyperv|                         |
   |            |                                                            |
   |            | URL: |sysvm64-url-hyperv|                                  |
   |            |                                                            |
   |            | Zone: Choose the zone where this hypervisor is used        |
   |            |                                                            |
   |            | Hypervisor: Hyper-V                                        |
   |            |                                                            |
   |            | Format: VHD                                                |
   |            |                                                            |
   |            | OS Type: Debian GNU/Linux 7.0 (64-bit) (or the             |
   |            | highest Debian release number available in the             |
   |            | dropdown)                                                  |
   |            |                                                            |
   |            | Extractable: no                                            |
   |            |                                                            |
   |            | Password Enabled: no                                       |
   |            |                                                            |
   |            | Public: no                                                 |
   |            |                                                            |
   |            | Featured: no                                               |
   |            |                                                            |
   |            | Routing: no                                                |
   +------------+------------------------------------------------------------+

#. Watch the screen to be sure that the Template downloads successfully and
   enters the **READY** state. Do not proceed until this is successful.

