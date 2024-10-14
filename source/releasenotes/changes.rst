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

Changes in |release| since 4.19.1.0
===================================

Apache CloudStack uses GitHub https://github.com/apache/cloudstack/milestone/30?closed=1
to track its issues.


.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+------------------------------------------------------------+
| Version                 | Github   | Description                                                |
+=========================+==========+============================================================+
| 4.20.0.0                | `#8911`_ | Linked clone migration between file-based storages on KVM  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9751`_ | API: Fix listing Userdata by keyword or name               |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9731`_ | Hide UserData field from the EditVM view for VMs that do   |
|                         |          | not offer it                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9195`_ | cleanup validations for VPN connection creation            |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9738`_ | debian12: update debian/control                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9723`_ | Shutdown expunged resources cleanup executor properly, and |
|                         |          | allow other components to configure/start/stop on error    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9739`_ | Fix ISO url in test_usage.py                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#7650`_ | CKS: add ConfigDrive to cloud-init datasource_list in      |
|                         |          | systemvm template                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8588`_ | CKS: fix creation on shared network if HA is enabled       |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9664`_ | PowerFlex on demand disable config key                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9559`_ | server: fix nfs version option during mounts               |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9374`_ | server: apply network ACL even if there is no network ACLs |
|                         |          | rules in the ACL list                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9720`_ | Revert "list VMs by displayname instead of name"           |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9596`_ | Fix: Filter out networks without access while getting      |
|                         |          | networks with SG with free IPs                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9711`_ | ui: load project list with minimum details                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9006`_ | build/packaging: build tungsten plugin only if noredist is |
|                         |          | passed                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9637`_ | Fixed Unable to create a domain when networkdomain is      |
|                         |          | mentioned and cleared                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8846`_ | Removed deprecated instruction MAINTAINER                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9714`_ | Fix main build errors                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9636`_ | [VMware] Make disk controller selection on volume          |
|                         |          | attachment consistent with VM creation and start           |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9699`_ | VR: fix password server exception when no password is      |
|                         |          | found                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9698`_ | lb: fix haproxy cannot start if algorithm is not lowercase |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9700`_ | UI: enable project menu on mobile devices                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9563`_ | Fix resource count discrepancy while associating IP        |
|                         |          | address to a network                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9676`_ | Enable Backup and Recovery for Shared Filesystems          |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9200`_ | refactor: cloud-sysvmadm script                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9557`_ | UI: Fix VPC network offerings listing on VPC tier creation |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8503`_ | list VMs by displayname instead of name                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9696`_ | pre-commit run --all-files; fix end of file                |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9680`_ | Update of the schema 41910to42000.sql for compatibility    |
|                         |          | with MariaDB version 10.3.38.                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9655`_ | Fix toc generation for api docs                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9681`_ | Implemented the lateral expansion of the area-box in the   |
|                         |          | forms (creat…                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9669`_ | CPVM: move focus on input area after clearing clipboard    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9661`_ | List Events returns intermittent SQL exception.Fixed       |
|                         |          | listEvents intermittent exception.                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9675`_ | Minor naming changes in Shared FileSystems 4.20 Feature    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9663`_ | Provide encryption key for DATA volume type (in addition   |
|                         |          | to ROOT) to copy volume.                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9585`_ | allow domain suffix update in shared networks              |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9662`_ | Host capacity calculation: use VM creation time if update  |
|                         |          | time is null.                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9509`_ | Feature: Forgot password                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9656`_ | Fix the Cloudian Integration SSO Redirect link             |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9188`_ | Enhance the `listAffinityGroups` API by adding the         |
|                         |          | dedicated resources related to an affinity group           |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9566`_ | Allow more generic searches of ACLs                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8924`_ | Add logs to CPVM connection process                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9461`_ | Restore listNetworks behavior & clean up the code          |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9633`_ | Feature: Allow adding delete protection for VMs & volumes  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9652`_ | UI: Fix starting VMs through group action by               |
|                         |          | non-root-admin users                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9528`_ | Linstor: Fix migrate primary storage                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8906`_ | NSX Integration fixes                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9107`_ | Refactor type and range validation in configuration update |
|                         |          | process                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8511`_ | Add logs to `LibvirtComputingResource`'s metrics           |
|                         |          | collection process                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9639`_ | ui: refactor config update/reset notification              |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9619`_ | New Feature: Multi-arch Zones                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9647`_ | engine/schema: update url links to match new               |
|                         |          | systemvmtemplate names                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9428`_ | Fix root disk resize issue when service offering has no    |
|                         |          | root disk size specified                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9470`_ | New feature: Dynamic and Static Routing                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9451`_ | backup: simple NAS backup plugin for KVM                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8389`_ | Add support for Ceph RGW Object Store                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9208`_ | Shared Filesystem as a First Class Feature                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9415`_ | Shared Network Firewall (Security groups) in Advanced zone |
|                         |          | without security groups                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9624`_ | propagate sort order through retrieval sequence            |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8925`_ | Go back to previous timestamp on logging                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9543`_ | Added update, enable, disable events to the                |
|                         |          | updateStoragePool API                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9569`_ | Global setting to allow/disallow users to force stop a vm  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9449`_ | Display associated resource name on storage pools objects  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9518`_ | framework/db: use HikariCP as default and improvements     |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9628`_ | framework/config,server: configkey caching                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9591`_ | [VMware] Add support for VMware 8.0u2 (8.0.2.x) and 8.0u3  |
|                         |          | (8.0.3.x)                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9634`_ | UI: list vms with details=min when attach a volume to vm   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8683`_ | Bump org.apache.commons:commons-compress from 1.21 to      |
|                         |          | 1.26.0                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9632`_ | linstor: update java-linstor dependency to 0.5.2           |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9631`_ | Fix PR lint error caused by deps/install-non-oss.sh        |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#7610`_ | Notify users when upgrades are available or restart is     |
|                         |          | required for network or VPC                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9239`_ | Fix snapshot deletion on template creation failure         |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9236`_ | kvm: Present the UUID of the VM as serial through smbios   |
|                         |          | information                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9205`_ | updated install-non-oss with vmware v7.0 and v8.0          |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9116`_ | Testcases Added                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8958`_ | Update en.json                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9629`_ | Add FelipeM525 to .asf.yaml as a collaborator              |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9206`_ | storage: fix private templates are not copied to new image |
|                         |          | store                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9567`_ | Add validation for secstorage.allowed.internal.sites       |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9568`_ | VR: remove vpn user info when apply vpn users list         |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9578`_ | server: fix stopped vm volume migration check on local     |
|                         |          | volume attach                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9588`_ | Updated listStoragePools response - added new managed      |
|                         |          | parameter                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9616`_ | Add minimum details parameter to Search View's listDomains |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9625`_ | SystemVM template changes - updated debian version & other |
|                         |          | changes                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9610`_ | engine-orchestration: fix issue for empty product in vm    |
|                         |          | metadata                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9560`_ | linstor: set/unset allow-two-primaries and protocol on rc  |
|                         |          | level                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9627`_ | Update Debian version to 12 in systemvm welcome message    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9573`_ | Fix VGPU available devices listing                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9617`_ | Fixed incorrect label in VRs and  SVMs                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9554`_ | ui: show guest networks for guest vlans list               |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9575`_ | Fix userdata append header restrictions                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8755`_ | Added support for storpool_qos service                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8649`_ | Improve logs in primary storage removal process            |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9600`_ | systemvm: have flags to check x86_64 to install specifics  |
|                         |          | for amd64 arch                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9125`_ | Fix NPE when sending copy command to least busy SSVM       |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9255`_ | Add certificate validation to check headers                |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9455`_ | Updated invalid parameter/value error with proper          |
|                         |          | exception                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8743`_ | Fix `deleteAccount` API to prevent deletion of the caller  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8751`_ | Configuration to disable URL validation when registering   |
|                         |          | templates/ISOs                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9549`_ | New Feature: Enable/Disable Roles                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8609`_ | Build: drop EL7 support, support JRE17 for packages and    |
|                         |          | sonar check                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9572`_ | Update project account for all the events with project     |
|                         |          | account owner, except for create project event             |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9468`_ | [VMware] Disconnect/Detach config drive ISO (if exists) on |
|                         |          | stop VM                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9433`_ | [VMware] Update data disk controller same as the root disk |
|                         |          | controller type when it is not set in the VM detail        |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9589`_ | [UI] Add project toggle for buckets                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9459`_ | Fix usage volume size after resizing                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9540`_ | Added domain path to all entities                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9329`_ | Add support for network data in Config Drive               |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9571`_ | test: fix component tests test_acl_isolatednetwork and     |
|                         |          | test_acl_isolatednetwork_delete                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8832`_ | Fix snapshot scheduling with expired jobs                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9163`_ | orchestration,hypervisor: allow custom manufacturer,       |
|                         |          | product for vm metadata                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9422`_ | allow users to apply extraconfig on updating VMs           |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9542`_ | server: do not check affinity groups if no vm group        |
|                         |          | mappings                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8878`_ | Download Volume Snapshots                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9550`_ | Fix to allow actions on the network if it belongs to a     |
|                         |          | project                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9548`_ | UI: Add filter to list encrypted volumes                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9545`_ | Fix Template and ISO upload events                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9553`_ | Fix main branch issues                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9551`_ | UI: Improve router listing page                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8689`_ | Fix being able to expunge a VM through                     |
|                         |          | destroyVirtualMachine even when role rule does not allow   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9417`_ | linstor: Improve copyPhysicalDisk performance              |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9264`_ | fix removeSecondaryStorageSelector response for docs       |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8556`_ | Allow deletion of system VM templates                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9225`_ | Improvements to quota tariffs APIs and UI                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9435`_ | NSX: add back removed code for NSX                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8812`_ | Fix column from op_dc_ip_address_alloc not being           |
|                         |          | referenced correctly by its ORM class                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9396`_ | created VPC message a little less misleading               |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9385`_ | add procedures procedure                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9201`_ | Ensure affinity groups are honored when VMs are deployed   |
|                         |          | in parallel                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9487`_ | ui: rename autoscale instance group to simply autoscaling  |
|                         |          | group                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9499`_ | test: fix component test                                   |
|                         |          | test_acl_sharednetwork_deployVM-impersonation.py           |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9340`_ | Support user resource name / displaytext with emoji,       |
|                         |          | unicode chars, and some sql exception msg improvements     |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9390`_ | libvirtstorageadaptor: better handle failed libvirt        |
|                         |          | storagepool destroy                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#22`_   | Vpc refactor clean for pr                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9447`_ | Fix snapshot chain being deleted on XenServer              |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8615`_ | Add UI to view and download usage records                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9450`_ | packaging: bundle latest cmk x86 build with deb and rpm    |
|                         |          | packages                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9426`_ | test: improve purge expunged resources b/g task testcase   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9419`_ | API: Fix missing keys in listZonesMetrics response         |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9399`_ | ui: vm metrics note about behaviour across hypervisors     |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9434`_ | Fixup CKS UI for external managed clusters                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9458`_ | UI: Display Firewall, LB and Port Forwading rules tab for  |
|                         |          | CKS clusters deployed on isolated networks                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9442`_ | Fix removal of usage records                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9437`_ | Add systemvmtemplate arm64 build support                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8739`_ | [4.20] VR: fix issue if userdata is binary data            |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9043`_ | Enhancement in the accuracy of the logs regarding the      |
|                         |          | capacity, usage, and threshold of secondary storages       |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9062`_ | Change exception when orchestrating VM start               |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#8833`_ | Fix link to removed volumes being shown in info card and   |
|                         |          | list view                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9409`_ | ui: add new API docs tab                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.20.0.0                | `#9402`_ | Icon changed for control-outlined                          |
+-------------------------+----------+------------------------------------------------------------+

151 Issues listed

.. _`#8911`: https://github.com/apache/cloudstack/pull/8911 
.. _`#9751`: https://github.com/apache/cloudstack/pull/9751 
.. _`#9731`: https://github.com/apache/cloudstack/pull/9731 
.. _`#9195`: https://github.com/apache/cloudstack/pull/9195 
.. _`#9738`: https://github.com/apache/cloudstack/pull/9738 
.. _`#9723`: https://github.com/apache/cloudstack/pull/9723 
.. _`#9739`: https://github.com/apache/cloudstack/pull/9739 
.. _`#7650`: https://github.com/apache/cloudstack/pull/7650 
.. _`#8588`: https://github.com/apache/cloudstack/pull/8588 
.. _`#9664`: https://github.com/apache/cloudstack/pull/9664 
.. _`#9559`: https://github.com/apache/cloudstack/pull/9559 
.. _`#9374`: https://github.com/apache/cloudstack/pull/9374 
.. _`#9720`: https://github.com/apache/cloudstack/pull/9720 
.. _`#9596`: https://github.com/apache/cloudstack/pull/9596 
.. _`#9711`: https://github.com/apache/cloudstack/pull/9711 
.. _`#9006`: https://github.com/apache/cloudstack/pull/9006 
.. _`#9637`: https://github.com/apache/cloudstack/pull/9637 
.. _`#8846`: https://github.com/apache/cloudstack/pull/8846 
.. _`#9714`: https://github.com/apache/cloudstack/pull/9714 
.. _`#9636`: https://github.com/apache/cloudstack/pull/9636 
.. _`#9699`: https://github.com/apache/cloudstack/pull/9699 
.. _`#9698`: https://github.com/apache/cloudstack/pull/9698 
.. _`#9700`: https://github.com/apache/cloudstack/pull/9700 
.. _`#9563`: https://github.com/apache/cloudstack/pull/9563 
.. _`#9676`: https://github.com/apache/cloudstack/pull/9676 
.. _`#9200`: https://github.com/apache/cloudstack/pull/9200 
.. _`#9557`: https://github.com/apache/cloudstack/pull/9557 
.. _`#8503`: https://github.com/apache/cloudstack/pull/8503 
.. _`#9696`: https://github.com/apache/cloudstack/pull/9696 
.. _`#9680`: https://github.com/apache/cloudstack/pull/9680 
.. _`#9655`: https://github.com/apache/cloudstack/pull/9655 
.. _`#9681`: https://github.com/apache/cloudstack/pull/9681 
.. _`#9669`: https://github.com/apache/cloudstack/pull/9669 
.. _`#9661`: https://github.com/apache/cloudstack/pull/9661 
.. _`#9675`: https://github.com/apache/cloudstack/pull/9675 
.. _`#9663`: https://github.com/apache/cloudstack/pull/9663 
.. _`#9585`: https://github.com/apache/cloudstack/pull/9585 
.. _`#9662`: https://github.com/apache/cloudstack/pull/9662 
.. _`#9509`: https://github.com/apache/cloudstack/pull/9509 
.. _`#9656`: https://github.com/apache/cloudstack/pull/9656 
.. _`#9188`: https://github.com/apache/cloudstack/pull/9188 
.. _`#9566`: https://github.com/apache/cloudstack/pull/9566 
.. _`#8924`: https://github.com/apache/cloudstack/pull/8924 
.. _`#9461`: https://github.com/apache/cloudstack/pull/9461 
.. _`#9633`: https://github.com/apache/cloudstack/pull/9633 
.. _`#9652`: https://github.com/apache/cloudstack/pull/9652 
.. _`#9528`: https://github.com/apache/cloudstack/pull/9528 
.. _`#8906`: https://github.com/apache/cloudstack/pull/8906 
.. _`#9107`: https://github.com/apache/cloudstack/pull/9107 
.. _`#8511`: https://github.com/apache/cloudstack/pull/8511 
.. _`#9639`: https://github.com/apache/cloudstack/pull/9639 
.. _`#9619`: https://github.com/apache/cloudstack/pull/9619 
.. _`#9647`: https://github.com/apache/cloudstack/pull/9647 
.. _`#9428`: https://github.com/apache/cloudstack/pull/9428 
.. _`#9470`: https://github.com/apache/cloudstack/pull/9470 
.. _`#9451`: https://github.com/apache/cloudstack/pull/9451 
.. _`#8389`: https://github.com/apache/cloudstack/pull/8389 
.. _`#9208`: https://github.com/apache/cloudstack/pull/9208 
.. _`#9415`: https://github.com/apache/cloudstack/pull/9415 
.. _`#9624`: https://github.com/apache/cloudstack/pull/9624 
.. _`#8925`: https://github.com/apache/cloudstack/pull/8925 
.. _`#9543`: https://github.com/apache/cloudstack/pull/9543 
.. _`#9569`: https://github.com/apache/cloudstack/pull/9569 
.. _`#9449`: https://github.com/apache/cloudstack/pull/9449 
.. _`#9518`: https://github.com/apache/cloudstack/pull/9518 
.. _`#9628`: https://github.com/apache/cloudstack/pull/9628 
.. _`#9591`: https://github.com/apache/cloudstack/pull/9591 
.. _`#9634`: https://github.com/apache/cloudstack/pull/9634 
.. _`#8683`: https://github.com/apache/cloudstack/pull/8683 
.. _`#9632`: https://github.com/apache/cloudstack/pull/9632 
.. _`#9631`: https://github.com/apache/cloudstack/pull/9631 
.. _`#7610`: https://github.com/apache/cloudstack/pull/7610 
.. _`#9239`: https://github.com/apache/cloudstack/pull/9239 
.. _`#9236`: https://github.com/apache/cloudstack/pull/9236 
.. _`#9205`: https://github.com/apache/cloudstack/pull/9205 
.. _`#9116`: https://github.com/apache/cloudstack/pull/9116 
.. _`#8958`: https://github.com/apache/cloudstack/pull/8958 
.. _`#9629`: https://github.com/apache/cloudstack/pull/9629 
.. _`#9206`: https://github.com/apache/cloudstack/pull/9206 
.. _`#9567`: https://github.com/apache/cloudstack/pull/9567 
.. _`#9568`: https://github.com/apache/cloudstack/pull/9568 
.. _`#9578`: https://github.com/apache/cloudstack/pull/9578 
.. _`#9588`: https://github.com/apache/cloudstack/pull/9588 
.. _`#9616`: https://github.com/apache/cloudstack/pull/9616 
.. _`#9625`: https://github.com/apache/cloudstack/pull/9625 
.. _`#9610`: https://github.com/apache/cloudstack/pull/9610 
.. _`#9560`: https://github.com/apache/cloudstack/pull/9560 
.. _`#9627`: https://github.com/apache/cloudstack/pull/9627 
.. _`#9573`: https://github.com/apache/cloudstack/pull/9573 
.. _`#9617`: https://github.com/apache/cloudstack/pull/9617 
.. _`#9554`: https://github.com/apache/cloudstack/pull/9554 
.. _`#9575`: https://github.com/apache/cloudstack/pull/9575 
.. _`#8755`: https://github.com/apache/cloudstack/pull/8755 
.. _`#8649`: https://github.com/apache/cloudstack/pull/8649 
.. _`#9600`: https://github.com/apache/cloudstack/pull/9600 
.. _`#9125`: https://github.com/apache/cloudstack/pull/9125 
.. _`#9255`: https://github.com/apache/cloudstack/pull/9255 
.. _`#9455`: https://github.com/apache/cloudstack/pull/9455 
.. _`#8743`: https://github.com/apache/cloudstack/pull/8743 
.. _`#8751`: https://github.com/apache/cloudstack/pull/8751 
.. _`#9549`: https://github.com/apache/cloudstack/pull/9549 
.. _`#8609`: https://github.com/apache/cloudstack/pull/8609 
.. _`#9572`: https://github.com/apache/cloudstack/pull/9572 
.. _`#9468`: https://github.com/apache/cloudstack/pull/9468 
.. _`#9433`: https://github.com/apache/cloudstack/pull/9433 
.. _`#9589`: https://github.com/apache/cloudstack/pull/9589 
.. _`#9459`: https://github.com/apache/cloudstack/pull/9459 
.. _`#9540`: https://github.com/apache/cloudstack/pull/9540 
.. _`#9329`: https://github.com/apache/cloudstack/pull/9329 
.. _`#9571`: https://github.com/apache/cloudstack/pull/9571 
.. _`#8832`: https://github.com/apache/cloudstack/pull/8832 
.. _`#9163`: https://github.com/apache/cloudstack/pull/9163 
.. _`#9422`: https://github.com/apache/cloudstack/pull/9422 
.. _`#9542`: https://github.com/apache/cloudstack/pull/9542 
.. _`#8878`: https://github.com/apache/cloudstack/pull/8878 
.. _`#9550`: https://github.com/apache/cloudstack/pull/9550 
.. _`#9548`: https://github.com/apache/cloudstack/pull/9548 
.. _`#9545`: https://github.com/apache/cloudstack/pull/9545 
.. _`#9553`: https://github.com/apache/cloudstack/pull/9553 
.. _`#9551`: https://github.com/apache/cloudstack/pull/9551 
.. _`#8689`: https://github.com/apache/cloudstack/pull/8689 
.. _`#9417`: https://github.com/apache/cloudstack/pull/9417 
.. _`#9264`: https://github.com/apache/cloudstack/pull/9264 
.. _`#8556`: https://github.com/apache/cloudstack/pull/8556 
.. _`#9225`: https://github.com/apache/cloudstack/pull/9225 
.. _`#9435`: https://github.com/apache/cloudstack/pull/9435 
.. _`#8812`: https://github.com/apache/cloudstack/pull/8812 
.. _`#9396`: https://github.com/apache/cloudstack/pull/9396 
.. _`#9385`: https://github.com/apache/cloudstack/pull/9385 
.. _`#9201`: https://github.com/apache/cloudstack/pull/9201 
.. _`#9487`: https://github.com/apache/cloudstack/pull/9487 
.. _`#9499`: https://github.com/apache/cloudstack/pull/9499 
.. _`#9340`: https://github.com/apache/cloudstack/pull/9340 
.. _`#9390`: https://github.com/apache/cloudstack/pull/9390 
.. _`#9447`: https://github.com/apache/cloudstack/pull/9447 
.. _`#8615`: https://github.com/apache/cloudstack/pull/8615 
.. _`#9450`: https://github.com/apache/cloudstack/pull/9450 
.. _`#9426`: https://github.com/apache/cloudstack/pull/9426 
.. _`#9419`: https://github.com/apache/cloudstack/pull/9419 
.. _`#9399`: https://github.com/apache/cloudstack/pull/9399 
.. _`#9434`: https://github.com/apache/cloudstack/pull/9434 
.. _`#9458`: https://github.com/apache/cloudstack/pull/9458 
.. _`#9442`: https://github.com/apache/cloudstack/pull/9442 
.. _`#9437`: https://github.com/apache/cloudstack/pull/9437 
.. _`#8739`: https://github.com/apache/cloudstack/pull/8739 
.. _`#9043`: https://github.com/apache/cloudstack/pull/9043 
.. _`#9062`: https://github.com/apache/cloudstack/pull/9062 
.. _`#8833`: https://github.com/apache/cloudstack/pull/8833 
.. _`#9409`: https://github.com/apache/cloudstack/pull/9409 
.. _`#9402`: https://github.com/apache/cloudstack/pull/9402 
