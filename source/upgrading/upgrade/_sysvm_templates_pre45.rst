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

Update System-VM Templates
--------------------------

.. warning::
   Upgrading from 4.4 or older to 4.6.0 require 2 systemvm Templates to be
   downloaded, for 4.5 and 4.6.

#. While running the existing |version_to_upgrade| system, log in to the UI as 
   root administrator.

#. In the left navigation bar, click Templates.

#. In Select view, click Templates.

#. Register 4.5 systemvm Template:
   
   #. Click Register Template.

      The Register Template dialog box is displayed.

   #. In the Register Template dialog box, specify the following values
      (do not change these):

      .. cssclass:: table-striped table-bordered table-hover
   
      +------------+------------------------------------------------------------+
      | Hypervisor | Description                                                |
      +============+============================================================+
      | XenServer  | Name: systemvm-xenserver-4.5                               |
      |            |                                                            |
      |            | Description: systemvm-xenserver-4.5                        |
      |            |                                                            |
      |            | URL: |acs45-sysvm64-url-xen|                               |
      |            |                                                            |
      |            | Zone: Choose the zone where this hypervisor is used        |
      |            |                                                            |
      |            | Hypervisor: XenServer                                      |
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
      | KVM        | Name: systemvm-kvm-4.5                                     |
      |            |                                                            |
      |            | Description: systemvm-kvm-4.5                              |
      |            |                                                            |
      |            | URL: |acs45-sysvm64-url-kvm|                               |  
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
      | VMware     | Name: systemvm-vmware-4.5                                  |
      |            |                                                            |
      |            | Description: systemvm-vmware-4.5                           |
      |            |                                                            |
      |            | URL: |acs45-sysvm64-url-vmware|                            |
      |            |                                                            |
      |            | Zone: Choose the zone where this hypervisor is used        |
      |            |                                                            |
      |            | Hypervisor: VMware                                         |
      |            |                                                            |
      |            | Format: OVA                                                |
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

#. Register |release| System VM Template:
   
   #. Click Register Template.

      The Register Template dialog box is displayed.

   #. In the Register Template dialog box, specify the following values
      (do not change these):

      .. cssclass:: table-striped table-bordered table-hover
      
      +------------+------------------------------------------------------------+
      | Hypervisor | Description                                                |
      +============+============================================================+
      | XenServer  | Name: systemvm-xenserver-4.6                               |
      |            |                                                            |
      |            | Description: systemvm-xenserver-4.6                        |
      |            |                                                            |
      |            | URL: |sysvm64-url-xen|                                     |
      |            |                                                            |
      |            | Zone: Choose the zone where this hypervisor is used        |
      |            |                                                            |
      |            | Hypervisor: XenServer                                      |
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
      | KVM        | Name: systemvm-kvm-4.6                                     |
      |            |                                                            |
      |            | Description: systemvm-kvm-4.6                              |
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
      | VMware     | Name: systemvm-vmware-4.6                                  |
      |            |                                                            |
      |            | Description: systemvm-vmware-4.6                           |
      |            |                                                            |
      |            | URL: |sysvm64-url-vmware|                                  |
      |            |                                                            |
      |            | Zone: Choose the zone where this hypervisor is used        |
      |            |                                                            |
      |            | Hypervisor: VMware                                         |
      |            |                                                            |
      |            | Format: OVA                                                |
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
