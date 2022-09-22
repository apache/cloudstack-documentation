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

Changes in |release| since 4.17.0.0
===================================

Apache CloudStack uses GitHub https://github.com/apache/cloudstack/milestone/25?closed=1
to track its issues.

.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+------------------------------------------------------------+
| Version                 | Github   | Description                                                |
+=========================+==========+============================================================+
| 4.17.1.0                | `#6721`_ | UI fix Theme text color not bind navTextColorPick and      |
|                         |          | reset button                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6725`_ | Reset unusable db connections                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6729`_ | server: fix network upgrade for IPv6                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6728`_ | upgrade a backported patch                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6730`_ | Jacoco: fix no coverage result in server and some other    |
|                         |          | modules                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6706`_ | systemvm,vr: disable radvd for non-applicable VRs          |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6711`_ | ui: Fix netowrkid not passed in deployvm                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6708`_ | UI: fix bulk delete project with cleanup                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6696`_ | kvm: add libvirt host capabilities method for cpu speed    |
|                         |          | retrieval                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6705`_ | server: fix check for ipv6 range overlap                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6707`_ | ui: fix set reservation toggle in add public ip range      |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6693`_ | Ignore opensaml's slf4j dependencies                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6688`_ | server: fix scale vm with compute offering having same     |
|                         |          | disk offering                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6643`_ | vmware: fix vm snapshot with datastore cluster, drs        |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6687`_ | UI: Remove incorrect API calls when initializing the       |
|                         |          | deploy VM page                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6675`_ | ui: fix update network updateinsequence param              |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6655`_ | server: fix error when dedicatingguestvlanrange for        |
|                         |          | physical nw without vlan range                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6671`_ | UI: Fixes suffix icon on project selector not work         |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6664`_ | vpc: prevent sourcenat ip disassociation for an active vpc |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6658`_ | cks: fix k8s cluster deployment with host tagged offering  |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6276`_ | api, vmware: Allow VM setting/detail for disk controller   |
|                         |          | (root/data) to override template details                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6642`_ | server: remove resource tags for disassociated public ip   |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6654`_ | Fix SQL query for uuid wrong format                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6588`_ | server: fix ipv6 network deployment with separate guest nw |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6650`_ | ui: fix resource tags visibility in infocard               |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6634`_ | server: fix delete resource tag permission                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6646`_ | ui: fix gputype in add compute offering                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6645`_ | UI - Fixes the warning in detail tab                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6625`_ | vmware,cks: fix attachiso failure with vmware drs          |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6636`_ | ui: reset disksize param on offering change in scale vm    |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6080`_ | Increase size of column 'value' at table 'account_details' |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6622`_ | Fixes #6621 - Update host memory stats                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6552`_ | removed the use of SharedMountPoint storage type for the   |
|                         |          | StorPool plugin                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6591`_ | vpc,network: fix createLoadBalancer access on user network |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6616`_ | ui: use ssh keypair uuid for listing                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6549`_ | test,xcp-ng: fix tests for VM PV driver issue              |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6341`_ | Enable system VM volume migration for KVM                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6612`_ | ui: fix hypervisortrafficlabel for phy nw traffic          |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6598`_ | UI: Fix delete ISO navigation after job is finished        |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6605`_ | Shows quotaSummary in API documentation                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6607`_ | UI: Fixes notification error can't close when exit config  |
|                         |          | limit tab                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6600`_ | ui: fix icon for vr migrate storage                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6592`_ | ui: fix vpc loadbalancer listing for admins                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6579`_ | api: fix ipv6 firewall apis default role permissions       |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6546`_ | Fixed list networks in projects after setting network      |
|                         |          | permissions                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6586`_ | ui: fix deploy vm override custom disk offering            |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6583`_ | UI: Fix new network service provider dialog                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6578`_ | UI: Fix account limits values reset after focus is lost on |
|                         |          | fields                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6564`_ | Remove psudo jobs from listAsyncJobs API                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6562`_ | utils: use safer parsing utility across codebase           |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6527`_ | [KVM] Fix for Revert volume snapshot                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6547`_ | UI: Fix can't select schedule interval type                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6462`_ | UI: Fixes UI break with SAML authentication                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6338`_ | test: add, refactor ipv6 network, vpc tests                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6430`_ | Filter removed nics while listing LB vm instances          |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6542`_ | Updated log message and throw error when unable to update  |
|                         |          | the secret in key file                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6543`_ | ui: fix zone icon in vm deploy zone selection              |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6480`_ | UI: Fixes some issues from zone wizard with VMWare         |
|                         |          | hypervisor                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6536`_ | kvm: add support nicAdapter detail for vm and template     |
|                         |          | settings for KVM                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6537`_ | kvm: skip test that can't run and pass on M1 mac           |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6513`_ | cks: fix k8s version upgrade                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6525`_ | UI: Add authmethod field allowing to choose password or    |
|                         |          | ssh key when adding host                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6457`_ | Fix SAML SSO plugin redirect URL                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6495`_ | ui: allow instances to be filtered by group                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6530`_ | Excluded fe80 or link local address in keystore setup      |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6529`_ | refactor: new line, lint error fix                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6272`_ | Fix spelling                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6503`_ | UI: Clear all filter values after the reset button clicked |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6414`_ | Fix VMware memory retrieval                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6483`_ | Fix for VMware VM migration with volume in local storage   |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6518`_ | Added information about device id 0 for root volume while  |
|                         |          | attaching to VM                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6142`_ | UI: Remove unused dependencies and fix travis build        |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6446`_ | CKS: add created to k8s cluster and k8s version            |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6476`_ | server: update lb rule with new protocol                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6496`_ | Fix global setting reference for max secondary storage     |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6493`_ | UI fix message.add.vpn.customer.gateway.failed when        |
|                         |          | catched error                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6502`_ | UI: Change notification title when resizing volume         |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6475`_ | UI: fix create tags for LB rules                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6367`_ | Updated PowerFlex/ScaleIO storage plugin to support        |
|                         |          | separate (storage) network for Hosts(KVM)/Storage          |
|                         |          | connection.                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6477`_ | Fix rpfilter config values from integer to boolean on      |
|                         |          | upgrade path                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6484`_ | ui: fix ui hang on offering creation with no zone          |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6481`_ | UI primarystorage linstor fixes                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6472`_ | kvm: upgrade libvirt-java to v0.5.3                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6468`_ | UI: Fixes ui error when upgrade virtual routers from       |
|                         |          | virtual router list                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6462`_ | UI: Fixes UI break with SAML authentication                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6461`_ | api: Add vpc name and uuid to VMs list response (nics) and |
|                         |          | nics response                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#5442`_ | some  component tests fixes                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6307`_ | fix pseudo random behaviour in pool selection              |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6449`_ | Specify vm snapshot uuid in response over db id in the     |
|                         |          | async job response                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6449`_ | Specify vm snapshot uuid in response over db id in the     |
|                         |          | async job response                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6436`_ | UI: Fix hypervisor not selected by default when deploying  |
|                         |          | VM from ISO                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6445`_ | UI: fix create vpc private gw by regular users             |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6439`_ | UI: Hide project delete button while in this project view  |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6438`_ | UI: Fixes the added storage tags issues on adding primary  |
|                         |          | storage                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6443`_ | UI: Fixes error when creating volume from the snapshot     |
+-------------------------+----------+------------------------------------------------------------+
| 4.17.1.0                | `#6441`_ | Fix deploy from ISO with custom disk offering              |
+-------------------------+----------+------------------------------------------------------------+

96 Issues listed

.. _`#6721`: https://github.com/apache/cloudstack/pull/6721 
.. _`#6725`: https://github.com/apache/cloudstack/pull/6725 
.. _`#6729`: https://github.com/apache/cloudstack/pull/6729 
.. _`#6728`: https://github.com/apache/cloudstack/pull/6728 
.. _`#6730`: https://github.com/apache/cloudstack/pull/6730 
.. _`#6706`: https://github.com/apache/cloudstack/pull/6706 
.. _`#6711`: https://github.com/apache/cloudstack/pull/6711 
.. _`#6708`: https://github.com/apache/cloudstack/pull/6708 
.. _`#6696`: https://github.com/apache/cloudstack/pull/6696 
.. _`#6705`: https://github.com/apache/cloudstack/pull/6705 
.. _`#6707`: https://github.com/apache/cloudstack/pull/6707 
.. _`#6693`: https://github.com/apache/cloudstack/pull/6693 
.. _`#6688`: https://github.com/apache/cloudstack/pull/6688 
.. _`#6643`: https://github.com/apache/cloudstack/pull/6643 
.. _`#6687`: https://github.com/apache/cloudstack/pull/6687 
.. _`#6675`: https://github.com/apache/cloudstack/pull/6675 
.. _`#6655`: https://github.com/apache/cloudstack/pull/6655 
.. _`#6671`: https://github.com/apache/cloudstack/pull/6671 
.. _`#6664`: https://github.com/apache/cloudstack/pull/6664 
.. _`#6658`: https://github.com/apache/cloudstack/pull/6658 
.. _`#6276`: https://github.com/apache/cloudstack/pull/6276 
.. _`#6642`: https://github.com/apache/cloudstack/pull/6642 
.. _`#6654`: https://github.com/apache/cloudstack/pull/6654 
.. _`#6588`: https://github.com/apache/cloudstack/pull/6588 
.. _`#6650`: https://github.com/apache/cloudstack/pull/6650 
.. _`#6634`: https://github.com/apache/cloudstack/pull/6634 
.. _`#6646`: https://github.com/apache/cloudstack/pull/6646 
.. _`#6645`: https://github.com/apache/cloudstack/pull/6645 
.. _`#6625`: https://github.com/apache/cloudstack/pull/6625 
.. _`#6636`: https://github.com/apache/cloudstack/pull/6636 
.. _`#6080`: https://github.com/apache/cloudstack/pull/6080 
.. _`#6622`: https://github.com/apache/cloudstack/pull/6622 
.. _`#6552`: https://github.com/apache/cloudstack/pull/6552 
.. _`#6591`: https://github.com/apache/cloudstack/pull/6591 
.. _`#6616`: https://github.com/apache/cloudstack/pull/6616 
.. _`#6549`: https://github.com/apache/cloudstack/pull/6549 
.. _`#6341`: https://github.com/apache/cloudstack/pull/6341 
.. _`#6612`: https://github.com/apache/cloudstack/pull/6612 
.. _`#6598`: https://github.com/apache/cloudstack/pull/6598 
.. _`#6605`: https://github.com/apache/cloudstack/pull/6605 
.. _`#6607`: https://github.com/apache/cloudstack/pull/6607 
.. _`#6600`: https://github.com/apache/cloudstack/pull/6600 
.. _`#6592`: https://github.com/apache/cloudstack/pull/6592 
.. _`#6579`: https://github.com/apache/cloudstack/pull/6579 
.. _`#6546`: https://github.com/apache/cloudstack/pull/6546 
.. _`#6586`: https://github.com/apache/cloudstack/pull/6586 
.. _`#6583`: https://github.com/apache/cloudstack/pull/6583 
.. _`#6578`: https://github.com/apache/cloudstack/pull/6578 
.. _`#6564`: https://github.com/apache/cloudstack/pull/6564 
.. _`#6562`: https://github.com/apache/cloudstack/pull/6562 
.. _`#6527`: https://github.com/apache/cloudstack/pull/6527 
.. _`#6547`: https://github.com/apache/cloudstack/pull/6547 
.. _`#6462`: https://github.com/apache/cloudstack/pull/6462 
.. _`#6338`: https://github.com/apache/cloudstack/pull/6338 
.. _`#6430`: https://github.com/apache/cloudstack/pull/6430 
.. _`#6542`: https://github.com/apache/cloudstack/pull/6542 
.. _`#6543`: https://github.com/apache/cloudstack/pull/6543 
.. _`#6480`: https://github.com/apache/cloudstack/pull/6480 
.. _`#6536`: https://github.com/apache/cloudstack/pull/6536 
.. _`#6537`: https://github.com/apache/cloudstack/pull/6537 
.. _`#6513`: https://github.com/apache/cloudstack/pull/6513 
.. _`#6525`: https://github.com/apache/cloudstack/pull/6525 
.. _`#6457`: https://github.com/apache/cloudstack/pull/6457 
.. _`#6495`: https://github.com/apache/cloudstack/pull/6495 
.. _`#6530`: https://github.com/apache/cloudstack/pull/6530 
.. _`#6529`: https://github.com/apache/cloudstack/pull/6529 
.. _`#6272`: https://github.com/apache/cloudstack/pull/6272 
.. _`#6503`: https://github.com/apache/cloudstack/pull/6503 
.. _`#6414`: https://github.com/apache/cloudstack/pull/6414 
.. _`#6483`: https://github.com/apache/cloudstack/pull/6483 
.. _`#6518`: https://github.com/apache/cloudstack/pull/6518 
.. _`#6142`: https://github.com/apache/cloudstack/pull/6142 
.. _`#6446`: https://github.com/apache/cloudstack/pull/6446 
.. _`#6476`: https://github.com/apache/cloudstack/pull/6476 
.. _`#6496`: https://github.com/apache/cloudstack/pull/6496 
.. _`#6493`: https://github.com/apache/cloudstack/pull/6493 
.. _`#6502`: https://github.com/apache/cloudstack/pull/6502 
.. _`#6475`: https://github.com/apache/cloudstack/pull/6475 
.. _`#6367`: https://github.com/apache/cloudstack/pull/6367 
.. _`#6477`: https://github.com/apache/cloudstack/pull/6477 
.. _`#6484`: https://github.com/apache/cloudstack/pull/6484 
.. _`#6481`: https://github.com/apache/cloudstack/pull/6481 
.. _`#6472`: https://github.com/apache/cloudstack/pull/6472 
.. _`#6468`: https://github.com/apache/cloudstack/pull/6468 
.. _`#6462`: https://github.com/apache/cloudstack/pull/6462 
.. _`#6461`: https://github.com/apache/cloudstack/pull/6461 
.. _`#5442`: https://github.com/apache/cloudstack/pull/5442 
.. _`#6307`: https://github.com/apache/cloudstack/pull/6307 
.. _`#6449`: https://github.com/apache/cloudstack/pull/6449 
.. _`#6449`: https://github.com/apache/cloudstack/pull/6449 
.. _`#6436`: https://github.com/apache/cloudstack/pull/6436 
.. _`#6445`: https://github.com/apache/cloudstack/pull/6445 
.. _`#6439`: https://github.com/apache/cloudstack/pull/6439 
.. _`#6438`: https://github.com/apache/cloudstack/pull/6438 
.. _`#6443`: https://github.com/apache/cloudstack/pull/6443 
.. _`#6441`: https://github.com/apache/cloudstack/pull/6441 


Changes in |release| since 4.16
===============================

Apache CloudStack uses GitHub https://github.com/apache/cloudstack/milestone/21?closed=1
to track its issues.

.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| Version                 | Github   | Type          | Priority | Description                                                |
+=========================+==========+===============+==========+============================================================+
| 4.17.0.0                | `#6418`_ |               |          | cks: Fix when deployed on a nw without internet access     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6423`_ |               |          | Fix UEFI detection on KVM and prevent deployments on non   |
|                         |          |               |          | UEFI enabled hosts                                         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6422`_ |               |          | Fix extract snapshot from vm snapshot on kvm               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6415`_ |               |          | UI: Fix template is deselected if other zone is selected   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6421`_ |               |          | ui: Display associated VPC network name against vpc tiers  |
|                         |          |               |          | - deploy VM form                                           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6416`_ |               |          | ui: Fix create kubernetes cluster with ha enabled          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6417`_ |               |          | UI: Fix Upgrade kubernetes form                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6405`_ |               |          | Fix logic check error for update GPU groupDetails          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6393`_ |               |          | remove request listener to prevent untimely session        |
|                         |          |               |          | invalidation                                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6404`_ |               |          | [KVM] Fix VM migration error due to VNC password on        |
|                         |          |               |          | libvirt limiting versions                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6399`_ |               |          | [KVM] Enable IOURING only when it is available on the host |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6400`_ |               |          | UI: fix create vpc private gateway for regular user        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6407`_ |               |          | [UI] Zone Wizard - fix secret property when setting RBD    |
|                         |          |               |          | primary storage                                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6402`_ |               |          | Backport: kvm: truncate vnc password to 8 chars (#6244)    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6397`_ |               |          | Prevent NPE on reboot stopped VM and startVM output with   |
|                         |          |               |          | null displayname                                           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6356`_ |               |          | Log load bean exception                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6392`_ |               |          | cks: Get caller user keys if cluster belongs to project    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6394`_ |               |          | Log exception on keystore build for custom certificate     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6332`_ |               |          | [UI] update ja locale translation                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6388`_ |               |          | cks: upgrade k8s to 1.23.3/1.24.0 in smoke test            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6385`_ |               |          | test: add test for importUnmanagedInstance                 |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6389`_ |               |          | server: publish ip6 assign event with route, always for    |
|                         |          |               |          | vpc                                                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6380`_ |               |          | Fix, change network.disable.rpfilter type from integer to  |
|                         |          |               |          | boolean.                                                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6377`_ |               |          | Fix changeOfferingForVolume API to consider storage type   |
|                         |          |               |          | in the disk offering                                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6387`_ |               |          | Reword KVM VM snapshot without memory error message        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6384`_ |               |          | Fix: Cannot import Vmware instances                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6378`_ |               |          | Editing two labels for the Portuguese translation          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6383`_ |               |          | remove unused UI field                                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6376`_ |               |          | UI: Add missing tooltips on service offering creation      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6382`_ |               |          | UI: Fix hypervisor list after zone validation when         |
|                         |          |               |          | registering a template                                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6379`_ |               |          | Update VM name, when the new name provided in              |
|                         |          |               |          | updateVirtualMachine API is in different case.             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6371`_ |               |          | agent: enable ssl only for kvm agent (not in system vms)   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6375`_ |               |          | ui: Allow editing host and storage tags in updateHost &    |
|                         |          |               |          | updateStoragePool forms                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6368`_ |               |          | CKS: fix error with pulling weaveworks images when create  |
|                         |          |               |          | k8s ISO                                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6370`_ |               |          | UI: Fix refresh button on Metrics                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6364`_ |               |          | ipv6: set default_egress_policy for ingress rules          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6361`_ |               |          | test_network_ipv6.py : remove wrong icmp type              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6362`_ |               |          | Bugfix: no support for XCPng 8.2.1                         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6363`_ |               |          | schema,upgrade: fix wrong comment for new columns of       |
|                         |          |               |          | cloud.event                                                |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6360`_ |               |          | ui: Fix adding tags to compute and disk offering           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6355`_ |               |          | Gateways after Nic update on Shared Network tests          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6354`_ |               |          | ui: Network offerings not listed if listVPCs not available |
|                         |          |               |          | in the account Role                                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6347`_ |               |          | Move apache DS dependencies to test scope                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6353`_ |               |          | ui: Fix live patch of routers                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6343`_ |               |          | systemvm: setup radvd correctly                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6345`_ |               |          | UI: Fix navigation after delete template job is finished   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6340`_ |               |          | ui: Fix template delete issue                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6336`_ |               |          | UI: show startip and endip if network offering support     |
|                         |          |               |          | specified ip ranges                                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6337`_ |               |          | ui: Fix migrate systemVM icon when stopped                 |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6328`_ |               |          | Change patch path during live patching of systemVMs        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6335`_ |               |          | UI: Fix detail settings                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6329`_ |               |          | test: fix ipv6 network test for xenserver                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6324`_ |               |          | Improve log when live patching fails                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6323`_ |               |          | Added allowuserdrivenbackups toggle to the edit backup     |
|                         |          |               |          | offering button                                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6333`_ |               |          | ui: Fix groupaction for nw cleanup and Notify when         |
|                         |          |               |          | groupaction fails                                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6325`_ |               |          | UI: Fix filter width to display options                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6281`_ |               |          | Fix grammatical errors on en.json                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6322`_ |               |          | ui: add route for network acl event resource               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6319`_ |               |          | Move user shared networks tests to component tests         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6317`_ |               |          | Disable creating StorPool logs when there isn't StorPool   |
|                         |          |               |          | primary storage                                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6315`_ |               |          | ui,api: fix api resourcename and user/project event        |
|                         |          |               |          | resource                                                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6314`_ |               |          | network: fix event, acl, firewall for ipv6 nw              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6283`_ |               |          | [VMWare] error when detaching volume                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5786`_ |               |          | network: ipv6 static routes                                |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6313`_ |               |          | remove superfluent counter and fix log message             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6311`_ |               |          | UI: Fixes the warning display when building UI             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6312`_ |               |          | UI: Fixes InfraMammary screen not display                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5997`_ |               |          | schema,server,api: events improvement                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6309`_ |               |          | UI: Fix upload resource icon button                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6308`_ |               |          | UI: Fix Usage Server stats date display                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6301`_ |               |          | server: do not display 'Default Egress Policy' for vpc     |
|                         |          |               |          | tiers                                                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6297`_ |               |          | Fix upload volume format                                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6296`_ |               |          | xen: Fix volume snapshot deletion when it has child        |
|                         |          |               |          | snapshots                                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6303`_ |               |          | server: fix NPE in travis and merge #6305                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6200`_ |               |          | KVM: Enable SSL if keystore exists                         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6306`_ |               |          | DB: fix duplicated changes in schema-41610to41700.sql      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6245`_ |               |          | Fix VM stats inconsistencies                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5588`_ |               |          | Mshost stats                                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6300`_ |               |          | UI: fix netmask is not passed to api when create share     |
|                         |          |               |          | network                                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6299`_ |               |          | ui: Toggle Theme to default(light) on login                |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6201`_ |               |          | [UI] Added attach and detach features to UI for ROOT disks |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#4774`_ |               |          | Added configuration and Integration test to restrict       |
|                         |          |               |          | public template …                                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5831`_ |               |          | SystemVM optimizations                                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5382`_ |               |          | fix mismatching between db uuids and custom attributes     |
|                         |          |               |          | uuids                                                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6287`_ |               |          | Fix: Prevent NPE on disk offering search while listing VMs |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6289`_ |               |          | UI: hide Virtual Routers tab for domain admins             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6288`_ |               |          | ui: Fix Internal LB LB rule column and missing translation |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6290`_ |               |          | UI: checksum field is optional for direct-download         |
|                         |          |               |          | templates on kvm                                           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5848`_ |               |          | Feat/add vdisk UUID to list volume                         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6286`_ |               |          | ui: Fix bulk deletion of ssh key pairs                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5902`_ |               |          | Allow users to view reserved System VM IPs, if they're     |
|                         |          |               |          | already allocated to user                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6284`_ |               |          | Fixed reset configuration response, to return the updated  |
|                         |          |               |          | config value.                                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5769`_ |               |          | New feature: give access permission of networks to other   |
|                         |          |               |          | accounts in same domain                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6285`_ |               |          | UI: Fix custom unconstrained for a zone does not show CPU  |
|                         |          |               |          | speed                                                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6279`_ |               |          | ui: remove mandatory rule on root disk controller field    |
|                         |          |               |          | while registering / updating a template                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6149`_ |               |          | Update SAML2 auth sessionkey cookie path                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6275`_ |               |          | ui: Incorrect column key specified in secondary store      |
|                         |          |               |          | column filter                                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6185`_ |               |          | Fix spelling                                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6265`_ |               |          | .github: run coverage on pull request                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6268`_ |               |          | Enable flake8 W293 blank line contains whitespace          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6267`_ |               |          | Fix #6263 Cannot scale VM with custom offering             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6261`_ |               |          | UI: Fixes UI bug                                           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6244`_ |               |          | kvm: truncate vnc password to 8 chars                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6007`_ |               |          | StorPool storage plugin                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6238`_ |               |          | .github: improve coverage run                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6262`_ |               |          | ui: Allow editing VM and template settings                 |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6260`_ |               |          | ui: Add project switch to the Kubernetes tab               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6257`_ |               |          | ui: Display action buttons in Project Accounts Tab view if |
|                         |          |               |          | project Admin                                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6258`_ |               |          | UI: fix dedicate public ip range to domain                 |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#4739`_ |               |          | Allow creating snapshot from VM snapshot                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6254`_ |               |          | Fix: Allow disabling the login attempts mechanism for      |
|                         |          |               |          | disabling users                                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6250`_ |               |          | maven: upgrade to latest spring-framework release          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6256`_ |               |          | local versions of .env ignored                             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6253`_ |               |          | Extract the IO_URING configuration into the                |
|                         |          |               |          | agent.properties                                           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6160`_ |               |          | server: honor global setting system.vm.default.hypervisor  |
|                         |          |               |          | as first option when deploy VRs                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6255`_ |               |          | UI: fix icon user-delete-outlined for release dedicated    |
|                         |          |               |          | public ip range                                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6153`_ |               |          | VR: add rules for traffic between static nat and private   |
|                         |          |               |          | gateway static routes                                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6248`_ |               |          | ui: Fix uploadCustomCertificate form in infraSummary view  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5297`_ |               |          | KVM disk-only based snapshot of volumes instead of taking  |
|                         |          |               |          | VM's full snapshot and extracting disks                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5977`_ |               |          | Synchronization of network devices on newly added hosts    |
|                         |          |               |          | for Persistent Networks                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6104`_ |               |          | Direct download certificates additions and improvements    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6243`_ |               |          | UI: Fix protocol reset after changing provider on Add      |
|                         |          |               |          | Primary Storage                                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6235`_ |               |          | ui: use different icon label for releaseIpAddress action   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6234`_ |               |          | Allow expunging a VM on a deleted host when using host     |
|                         |          |               |          | cache and ConfigDrive userdata service                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6197`_ |               |          | UI: fixes login button not work and Single Sign-On tab     |
|                         |          |               |          | disabled after logout                                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5984`_ |               |          | Persistence of VM stats                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6237`_ |               |          | potential null pointer in condition; AYAI9l8k5Irk9_td-cXb  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6241`_ |               |          | UI: Fix Add secondary storage                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6233`_ |               |          | ui: Project owner (normal user) unable to perform any      |
|                         |          |               |          | operations in the project                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6226`_ |               |          | Display proper gateway length in health check result       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6123`_ |               |          | server: increment deviceid while importing vm data volumes |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#3724`_ |               |          | Storage-based Snapshots for KVM VMs                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6187`_ |               |          | api: Prevent modifying acl rules order for default ACLs    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6227`_ |               |          | upgrade: update minreq.sysvmtemplate.version to the latest |
|                         |          |               |          | template version                                           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6228`_ |               |          | Support JaCoCo and other quality checks                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6196`_ |               |          | UI: Fixes removing undesired API parameters on form submit |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6218`_ |               |          | Allow storage.overprovisioning.factor to be <1             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6225`_ |               |          | .github: fix workflow settings and allow branch pushes to  |
|                         |          |               |          | main by com…                                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6221`_ |               |          | .github: add merge conflict checker per RM request         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6217`_ |               |          | .github: fix first PR welcome message by boring-cyborg     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6190`_ |               |          | Added new field to updateBackupOffering API.               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6211`_ |               |          | Probot integrations                                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6210`_ |               |          | .asf.yaml: dummy fix to re-kick asf-infra integration      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6193`_ |               |          | UI: Logout before login                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6207`_ |               |          | api: add vpcname to networkacl response                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6156`_ |               |          | api: Update account type when updating account role        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6198`_ |               |          | server: fix list reserved/free public ips in project       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6189`_ |               |          | VR: Do not add iptables rules for the revoked ip addresses |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6188`_ |               |          | VR: add '-m <protocol>' for tcp or udp protocol            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6206`_ |               |          | ui: fix acl rules listing                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6204`_ |               |          | ui: Fix label for LUN number                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6183`_ |               |          | test: update test_kubernetes_clusters.py to support        |
|                         |          |               |          | advanced zone with security groups                         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6139`_ |               |          | agent: Detect existing hosts with UEFI support             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6192`_ |               |          | Remove duplicate entry from `.gitignore`                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6182`_ |               |          | UI: Fix minor UI issues                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6164`_ |               |          | Mount disabled storage pool on host reboot                 |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6132`_ |               |          | CKS: Support deployment of CKS clusters on Advanced zones  |
|                         |          |               |          | with security groups                                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6181`_ |               |          | ui,refactor: fix missing label in update network form      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6175`_ |               |          | KVM: Enhance CPU speed detection on hosts                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6178`_ |               |          | ui: fix vpc tier redirect to show details                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6162`_ |               |          | UI - Fixes UI bugs                                         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6165`_ |               |          | SAML: replace first number with random alphabet if request |
|                         |          |               |          | ID starts with a number                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6177`_ |               |          | UI: fix update public IP ranges                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6176`_ |               |          | ui: Fix scale kubernetes (cks) cluster form                |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6173`_ |               |          | [KVM] Ensure configdrive path is edited properly during    |
|                         |          |               |          | live migration                                             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6146`_ |               |          | configDrive: Fix failure to delete (unstarted) VM          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6168`_ |               |          | api: Fix reset configuration                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6171`_ |               |          | Avoid multiple if else                                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6161`_ |               |          | Fix spelling                                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6174`_ |               |          | UI: fix create l2 network offering with userdata           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6170`_ |               |          | ui, Adv zone + SG: Fix invocation of create/revoke APIs    |
|                         |          |               |          | for ingress/egress security group rules                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#4687`_ |               |          | Add Python flake8 linting for W291 trailing whitespace     |
|                         |          |               |          | with Super-Linter                                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6143`_ |               |          | api: Remove redundant API parameters                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#4636`_ |               |          | Prevent vm's from stopping while enabling maintenance mode |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6147`_ |               |          | kvm: support multiple local storage pools                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6159`_ |               |          | ui: Remove misleading anchor tags for users                |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6157`_ |               |          | ui: Fix wrong label entity.type                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6134`_ |               |          | Fix linux native bridge for SUSE in cloudutils             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6152`_ |               |          | travis: Fix failing travis tests on main                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6158`_ |               |          | ui: Fix router link access                                 |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6151`_ |               |          | UI: Prevent passing boottype/bootmode when template is     |
|                         |          |               |          | deploy-as-is                                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6140`_ |               |          | Set UefiCapabilty for all hypervisors in hostresponse      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6138`_ |               |          | ui: Support to specify security groups when                |
|                         |          |               |          | updating/editing a VM (adv zone + SG)                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6130`_ |               |          | Router health check notification mail to show router name  |
|                         |          |               |          | next to UUID                                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6122`_ |               |          | account check made explicit - cleanup                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6120`_ |               |          | server: fix NPE when router.service.offering is set due to |
|                         |          |               |          | service/disk offering refactoring                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6137`_ |               |          | ui: Fix icon on Load Balancing view tab                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6116`_ |               |          | Fix migration of VM with volume on Ubuntu                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6136`_ |               |          | api: Allow updating VM settings when custom constrained    |
|                         |          |               |          | offering is used                                           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6046`_ |               |          | New feature: Reserve and release Public IPs                |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6135`_ |               |          | UI: Fix change offering type                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5602`_ |               |          | Create profiles to download systemvm-templates             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5664`_ |               |          | alert: Send alert for ha'ed vm's                           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6126`_ |               |          | Revert "Honour isrecursive above listall"                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6119`_ |               |          | Travis - fix test failures observed                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6118`_ |               |          | api: Fix issue observed with message publish on creation   |
|                         |          |               |          | of domain                                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6110`_ |               |          | UI - Fixes error form.getFieldValue is not a function in   |
|                         |          |               |          | change user password form                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6091`_ |               |          | ui: update npm dependencies to latest                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6106`_ |               |          | ui: Fix CreateKubernetesCluster for ha                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6108`_ |               |          | UI: Fixes the style/css of deploy VM with stay on-page     |
|                         |          |               |          | button.                                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6076`_ |               |          | cks: Fix missing .service files when bootstraping in cks   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6109`_ |               |          | UI: Fix alignment of message                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6117`_ |               |          | UI: Show protocol on zone wide storage                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6031`_ |               |          | Update VM priority (cpu_shares) when live scaling it       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6113`_ |               |          | travis: run nosetests-3.4                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6096`_ |               |          | ui: fix physical network guest traffic type tab            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6095`_ |               |          | ui: fix mac learning warning visibility in add network     |
|                         |          |               |          | offering                                                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6081`_ |               |          | [UI] Dont show project view menu when user doesn't have    |
|                         |          |               |          | permission                                                 |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6093`_ |               |          | UI: Fixes domain navigation to back                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6098`_ |               |          | ui: fix bulk destroy vm with expunge                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6099`_ |               |          | ui: fix deploy vm stay on page                             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6045`_ |               |          | Honour isrecursive above listall                           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6089`_ |               |          | UI: Fix storage pool label for protocol                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6079`_ |               |          | Fix get upload params NPE                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6057`_ |               |          | server: mark volume snapshots as Destroyed if it does not  |
|                         |          |               |          | exist on primary and secondary storage when delete a       |
|                         |          |               |          | volume                                                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6083`_ |               |          | ui: Fix dashboard links                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6086`_ |               |          | UI: Fix route to domain details                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6085`_ |               |          | UI: Fix Dedicating resource to a domain                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6077`_ |               |          | UI: Reload page on closing Bulk Action modal               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6048`_ |               |          | Refactor account type                                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5151`_ |               |          | UI: Upgrade to Vue3 library                                |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6075`_ |               |          | ui: Set vm logo to osdisplayname to avoid multiple api     |
|                         |          |               |          | calls                                                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6072`_ |               |          | UI: Fix navigation to domains                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6069`_ |               |          | Adapt script to bash version 3                             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5009`_ |               |          | api: Warn if query parameters have multiple values         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6064`_ |               |          | Fix spelling                                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6070`_ |               |          | ui: Add user initials as avatar if no icon present         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6065`_ |               |          | ui: Add link to account role in listview                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6059`_ |               |          | Upgrade netty version                                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6066`_ |               |          | UI: Fix issue on volume snapshots wizard                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5993`_ |               |          | no axis                                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6051`_ |               |          | UI: update vm with userdata                                |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6061`_ |               |          | Fix spelling. Change `Occured` to `Occurred`               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6056`_ |               |          | Fix osx build                                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6050`_ |               |          | Check the network access when deploying VM in Advanced     |
|                         |          |               |          | Security Group.                                            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6018`_ |               |          | Allow specifying disk size, min/max iops for offering      |
|                         |          |               |          | linked with custom disk offering                           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6032`_ |               |          | api: Fix search by name                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6053`_ |               |          | Fix NPE on CIDR list check                                 |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6055`_ |               |          | UI: Missing message on VMware VM import for not found      |
|                         |          |               |          | networks                                                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6054`_ |               |          | Fix API parameter description for boottype/bootmode        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6028`_ |               |          | Upgrade Tomcat embed version                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6055`_ |               |          | UI: Missing message on VMware VM import for not found      |
|                         |          |               |          | networks                                                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6041`_ |               |          | Fix spelling                                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#6019`_ |               |          | Use default timeout and retransmission values for the NFS  |
|                         |          |               |          | mount.                                                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.17.0.0                | `#5965`_ |               |          | Multiple SSH Keys support                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+

245 Issues listed

.. _`#6418`: https://github.com/apache/cloudstack/pull/6418
.. _`#6423`: https://github.com/apache/cloudstack/pull/6423
.. _`#6422`: https://github.com/apache/cloudstack/pull/6422
.. _`#6415`: https://github.com/apache/cloudstack/pull/6415
.. _`#6421`: https://github.com/apache/cloudstack/pull/6421
.. _`#6416`: https://github.com/apache/cloudstack/pull/6416
.. _`#6417`: https://github.com/apache/cloudstack/pull/6417
.. _`#6405`: https://github.com/apache/cloudstack/pull/6405
.. _`#6393`: https://github.com/apache/cloudstack/pull/6393
.. _`#6404`: https://github.com/apache/cloudstack/pull/6404
.. _`#6399`: https://github.com/apache/cloudstack/pull/6399
.. _`#6400`: https://github.com/apache/cloudstack/pull/6400
.. _`#6407`: https://github.com/apache/cloudstack/pull/6407
.. _`#6402`: https://github.com/apache/cloudstack/pull/6402
.. _`#6397`: https://github.com/apache/cloudstack/pull/6397
.. _`#6356`: https://github.com/apache/cloudstack/pull/6356
.. _`#6392`: https://github.com/apache/cloudstack/pull/6392
.. _`#6394`: https://github.com/apache/cloudstack/pull/6394
.. _`#6332`: https://github.com/apache/cloudstack/pull/6332
.. _`#6388`: https://github.com/apache/cloudstack/pull/6388
.. _`#6385`: https://github.com/apache/cloudstack/pull/6385
.. _`#6389`: https://github.com/apache/cloudstack/pull/6389
.. _`#6380`: https://github.com/apache/cloudstack/pull/6380
.. _`#6377`: https://github.com/apache/cloudstack/pull/6377
.. _`#6387`: https://github.com/apache/cloudstack/pull/6387
.. _`#6384`: https://github.com/apache/cloudstack/pull/6384
.. _`#6378`: https://github.com/apache/cloudstack/pull/6378
.. _`#6383`: https://github.com/apache/cloudstack/pull/6383
.. _`#6376`: https://github.com/apache/cloudstack/pull/6376
.. _`#6382`: https://github.com/apache/cloudstack/pull/6382
.. _`#6379`: https://github.com/apache/cloudstack/pull/6379
.. _`#6371`: https://github.com/apache/cloudstack/pull/6371
.. _`#6375`: https://github.com/apache/cloudstack/pull/6375
.. _`#6368`: https://github.com/apache/cloudstack/pull/6368
.. _`#6370`: https://github.com/apache/cloudstack/pull/6370
.. _`#6364`: https://github.com/apache/cloudstack/pull/6364
.. _`#6361`: https://github.com/apache/cloudstack/pull/6361
.. _`#6362`: https://github.com/apache/cloudstack/pull/6362
.. _`#6363`: https://github.com/apache/cloudstack/pull/6363
.. _`#6360`: https://github.com/apache/cloudstack/pull/6360
.. _`#6355`: https://github.com/apache/cloudstack/pull/6355
.. _`#6354`: https://github.com/apache/cloudstack/pull/6354
.. _`#6347`: https://github.com/apache/cloudstack/pull/6347
.. _`#6353`: https://github.com/apache/cloudstack/pull/6353
.. _`#6343`: https://github.com/apache/cloudstack/pull/6343
.. _`#6345`: https://github.com/apache/cloudstack/pull/6345
.. _`#6340`: https://github.com/apache/cloudstack/pull/6340
.. _`#6336`: https://github.com/apache/cloudstack/pull/6336
.. _`#6337`: https://github.com/apache/cloudstack/pull/6337
.. _`#6328`: https://github.com/apache/cloudstack/pull/6328
.. _`#6335`: https://github.com/apache/cloudstack/pull/6335
.. _`#6329`: https://github.com/apache/cloudstack/pull/6329
.. _`#6324`: https://github.com/apache/cloudstack/pull/6324
.. _`#6323`: https://github.com/apache/cloudstack/pull/6323
.. _`#6333`: https://github.com/apache/cloudstack/pull/6333
.. _`#6325`: https://github.com/apache/cloudstack/pull/6325
.. _`#6281`: https://github.com/apache/cloudstack/pull/6281
.. _`#6322`: https://github.com/apache/cloudstack/pull/6322
.. _`#6319`: https://github.com/apache/cloudstack/pull/6319
.. _`#6317`: https://github.com/apache/cloudstack/pull/6317
.. _`#6315`: https://github.com/apache/cloudstack/pull/6315
.. _`#6314`: https://github.com/apache/cloudstack/pull/6314
.. _`#6283`: https://github.com/apache/cloudstack/pull/6283
.. _`#5786`: https://github.com/apache/cloudstack/pull/5786
.. _`#6313`: https://github.com/apache/cloudstack/pull/6313
.. _`#6311`: https://github.com/apache/cloudstack/pull/6311
.. _`#6312`: https://github.com/apache/cloudstack/pull/6312
.. _`#5997`: https://github.com/apache/cloudstack/pull/5997
.. _`#6309`: https://github.com/apache/cloudstack/pull/6309
.. _`#6308`: https://github.com/apache/cloudstack/pull/6308
.. _`#6301`: https://github.com/apache/cloudstack/pull/6301
.. _`#6297`: https://github.com/apache/cloudstack/pull/6297
.. _`#6296`: https://github.com/apache/cloudstack/pull/6296
.. _`#6303`: https://github.com/apache/cloudstack/pull/6303
.. _`#6200`: https://github.com/apache/cloudstack/pull/6200
.. _`#6306`: https://github.com/apache/cloudstack/pull/6306
.. _`#6245`: https://github.com/apache/cloudstack/pull/6245
.. _`#5588`: https://github.com/apache/cloudstack/pull/5588
.. _`#6300`: https://github.com/apache/cloudstack/pull/6300
.. _`#6299`: https://github.com/apache/cloudstack/pull/6299
.. _`#6201`: https://github.com/apache/cloudstack/pull/6201
.. _`#4774`: https://github.com/apache/cloudstack/pull/4774
.. _`#5831`: https://github.com/apache/cloudstack/pull/5831
.. _`#5382`: https://github.com/apache/cloudstack/pull/5382
.. _`#6287`: https://github.com/apache/cloudstack/pull/6287
.. _`#6289`: https://github.com/apache/cloudstack/pull/6289
.. _`#6288`: https://github.com/apache/cloudstack/pull/6288
.. _`#6290`: https://github.com/apache/cloudstack/pull/6290
.. _`#5848`: https://github.com/apache/cloudstack/pull/5848
.. _`#6286`: https://github.com/apache/cloudstack/pull/6286
.. _`#5902`: https://github.com/apache/cloudstack/pull/5902
.. _`#6284`: https://github.com/apache/cloudstack/pull/6284
.. _`#5769`: https://github.com/apache/cloudstack/pull/5769
.. _`#6285`: https://github.com/apache/cloudstack/pull/6285
.. _`#6279`: https://github.com/apache/cloudstack/pull/6279
.. _`#6149`: https://github.com/apache/cloudstack/pull/6149
.. _`#6275`: https://github.com/apache/cloudstack/pull/6275
.. _`#6185`: https://github.com/apache/cloudstack/pull/6185
.. _`#6265`: https://github.com/apache/cloudstack/pull/6265
.. _`#6268`: https://github.com/apache/cloudstack/pull/6268
.. _`#6267`: https://github.com/apache/cloudstack/pull/6267
.. _`#6261`: https://github.com/apache/cloudstack/pull/6261
.. _`#6244`: https://github.com/apache/cloudstack/pull/6244
.. _`#6007`: https://github.com/apache/cloudstack/pull/6007
.. _`#6238`: https://github.com/apache/cloudstack/pull/6238
.. _`#6262`: https://github.com/apache/cloudstack/pull/6262
.. _`#6260`: https://github.com/apache/cloudstack/pull/6260
.. _`#6257`: https://github.com/apache/cloudstack/pull/6257
.. _`#6258`: https://github.com/apache/cloudstack/pull/6258
.. _`#4739`: https://github.com/apache/cloudstack/pull/4739
.. _`#6254`: https://github.com/apache/cloudstack/pull/6254
.. _`#6250`: https://github.com/apache/cloudstack/pull/6250
.. _`#6256`: https://github.com/apache/cloudstack/pull/6256
.. _`#6253`: https://github.com/apache/cloudstack/pull/6253
.. _`#6160`: https://github.com/apache/cloudstack/pull/6160
.. _`#6255`: https://github.com/apache/cloudstack/pull/6255
.. _`#6153`: https://github.com/apache/cloudstack/pull/6153
.. _`#6248`: https://github.com/apache/cloudstack/pull/6248
.. _`#5297`: https://github.com/apache/cloudstack/pull/5297
.. _`#5977`: https://github.com/apache/cloudstack/pull/5977
.. _`#6104`: https://github.com/apache/cloudstack/pull/6104
.. _`#6243`: https://github.com/apache/cloudstack/pull/6243
.. _`#6235`: https://github.com/apache/cloudstack/pull/6235
.. _`#6234`: https://github.com/apache/cloudstack/pull/6234
.. _`#6197`: https://github.com/apache/cloudstack/pull/6197
.. _`#5984`: https://github.com/apache/cloudstack/pull/5984
.. _`#6237`: https://github.com/apache/cloudstack/pull/6237
.. _`#6241`: https://github.com/apache/cloudstack/pull/6241
.. _`#6233`: https://github.com/apache/cloudstack/pull/6233
.. _`#6226`: https://github.com/apache/cloudstack/pull/6226
.. _`#6123`: https://github.com/apache/cloudstack/pull/6123
.. _`#3724`: https://github.com/apache/cloudstack/pull/3724
.. _`#6187`: https://github.com/apache/cloudstack/pull/6187
.. _`#6227`: https://github.com/apache/cloudstack/pull/6227
.. _`#6228`: https://github.com/apache/cloudstack/pull/6228
.. _`#6196`: https://github.com/apache/cloudstack/pull/6196
.. _`#6218`: https://github.com/apache/cloudstack/pull/6218
.. _`#6225`: https://github.com/apache/cloudstack/pull/6225
.. _`#6221`: https://github.com/apache/cloudstack/pull/6221
.. _`#6217`: https://github.com/apache/cloudstack/pull/6217
.. _`#6190`: https://github.com/apache/cloudstack/pull/6190
.. _`#6211`: https://github.com/apache/cloudstack/pull/6211
.. _`#6210`: https://github.com/apache/cloudstack/pull/6210
.. _`#6193`: https://github.com/apache/cloudstack/pull/6193
.. _`#6207`: https://github.com/apache/cloudstack/pull/6207
.. _`#6156`: https://github.com/apache/cloudstack/pull/6156
.. _`#6198`: https://github.com/apache/cloudstack/pull/6198
.. _`#6189`: https://github.com/apache/cloudstack/pull/6189
.. _`#6188`: https://github.com/apache/cloudstack/pull/6188
.. _`#6206`: https://github.com/apache/cloudstack/pull/6206
.. _`#6204`: https://github.com/apache/cloudstack/pull/6204
.. _`#6183`: https://github.com/apache/cloudstack/pull/6183
.. _`#6139`: https://github.com/apache/cloudstack/pull/6139
.. _`#6192`: https://github.com/apache/cloudstack/pull/6192
.. _`#6182`: https://github.com/apache/cloudstack/pull/6182
.. _`#6164`: https://github.com/apache/cloudstack/pull/6164
.. _`#6132`: https://github.com/apache/cloudstack/pull/6132
.. _`#6181`: https://github.com/apache/cloudstack/pull/6181
.. _`#6175`: https://github.com/apache/cloudstack/pull/6175
.. _`#6178`: https://github.com/apache/cloudstack/pull/6178
.. _`#6162`: https://github.com/apache/cloudstack/pull/6162
.. _`#6165`: https://github.com/apache/cloudstack/pull/6165
.. _`#6177`: https://github.com/apache/cloudstack/pull/6177
.. _`#6176`: https://github.com/apache/cloudstack/pull/6176
.. _`#6173`: https://github.com/apache/cloudstack/pull/6173
.. _`#6146`: https://github.com/apache/cloudstack/pull/6146
.. _`#6168`: https://github.com/apache/cloudstack/pull/6168
.. _`#6171`: https://github.com/apache/cloudstack/pull/6171
.. _`#6161`: https://github.com/apache/cloudstack/pull/6161
.. _`#6174`: https://github.com/apache/cloudstack/pull/6174
.. _`#6170`: https://github.com/apache/cloudstack/pull/6170
.. _`#4687`: https://github.com/apache/cloudstack/pull/4687
.. _`#6143`: https://github.com/apache/cloudstack/pull/6143
.. _`#4636`: https://github.com/apache/cloudstack/pull/4636
.. _`#6147`: https://github.com/apache/cloudstack/pull/6147
.. _`#6159`: https://github.com/apache/cloudstack/pull/6159
.. _`#6157`: https://github.com/apache/cloudstack/pull/6157
.. _`#6134`: https://github.com/apache/cloudstack/pull/6134
.. _`#6152`: https://github.com/apache/cloudstack/pull/6152
.. _`#6158`: https://github.com/apache/cloudstack/pull/6158
.. _`#6151`: https://github.com/apache/cloudstack/pull/6151
.. _`#6140`: https://github.com/apache/cloudstack/pull/6140
.. _`#6138`: https://github.com/apache/cloudstack/pull/6138
.. _`#6130`: https://github.com/apache/cloudstack/pull/6130
.. _`#6122`: https://github.com/apache/cloudstack/pull/6122
.. _`#6120`: https://github.com/apache/cloudstack/pull/6120
.. _`#6137`: https://github.com/apache/cloudstack/pull/6137
.. _`#6116`: https://github.com/apache/cloudstack/pull/6116
.. _`#6136`: https://github.com/apache/cloudstack/pull/6136
.. _`#6046`: https://github.com/apache/cloudstack/pull/6046
.. _`#6135`: https://github.com/apache/cloudstack/pull/6135
.. _`#5602`: https://github.com/apache/cloudstack/pull/5602
.. _`#5664`: https://github.com/apache/cloudstack/pull/5664
.. _`#6126`: https://github.com/apache/cloudstack/pull/6126
.. _`#6119`: https://github.com/apache/cloudstack/pull/6119
.. _`#6118`: https://github.com/apache/cloudstack/pull/6118
.. _`#6110`: https://github.com/apache/cloudstack/pull/6110
.. _`#6091`: https://github.com/apache/cloudstack/pull/6091
.. _`#6106`: https://github.com/apache/cloudstack/pull/6106
.. _`#6108`: https://github.com/apache/cloudstack/pull/6108
.. _`#6076`: https://github.com/apache/cloudstack/pull/6076
.. _`#6109`: https://github.com/apache/cloudstack/pull/6109
.. _`#6117`: https://github.com/apache/cloudstack/pull/6117
.. _`#6031`: https://github.com/apache/cloudstack/pull/6031
.. _`#6113`: https://github.com/apache/cloudstack/pull/6113
.. _`#6096`: https://github.com/apache/cloudstack/pull/6096
.. _`#6095`: https://github.com/apache/cloudstack/pull/6095
.. _`#6081`: https://github.com/apache/cloudstack/pull/6081
.. _`#6093`: https://github.com/apache/cloudstack/pull/6093
.. _`#6098`: https://github.com/apache/cloudstack/pull/6098
.. _`#6099`: https://github.com/apache/cloudstack/pull/6099
.. _`#6045`: https://github.com/apache/cloudstack/pull/6045
.. _`#6089`: https://github.com/apache/cloudstack/pull/6089
.. _`#6079`: https://github.com/apache/cloudstack/pull/6079
.. _`#6057`: https://github.com/apache/cloudstack/pull/6057
.. _`#6083`: https://github.com/apache/cloudstack/pull/6083
.. _`#6086`: https://github.com/apache/cloudstack/pull/6086
.. _`#6085`: https://github.com/apache/cloudstack/pull/6085
.. _`#6077`: https://github.com/apache/cloudstack/pull/6077
.. _`#6048`: https://github.com/apache/cloudstack/pull/6048
.. _`#5151`: https://github.com/apache/cloudstack/pull/5151
.. _`#6075`: https://github.com/apache/cloudstack/pull/6075
.. _`#6072`: https://github.com/apache/cloudstack/pull/6072
.. _`#6069`: https://github.com/apache/cloudstack/pull/6069
.. _`#5009`: https://github.com/apache/cloudstack/pull/5009
.. _`#6064`: https://github.com/apache/cloudstack/pull/6064
.. _`#6070`: https://github.com/apache/cloudstack/pull/6070
.. _`#6065`: https://github.com/apache/cloudstack/pull/6065
.. _`#6059`: https://github.com/apache/cloudstack/pull/6059
.. _`#6066`: https://github.com/apache/cloudstack/pull/6066
.. _`#5993`: https://github.com/apache/cloudstack/pull/5993
.. _`#6051`: https://github.com/apache/cloudstack/pull/6051
.. _`#6061`: https://github.com/apache/cloudstack/pull/6061
.. _`#6056`: https://github.com/apache/cloudstack/pull/6056
.. _`#6050`: https://github.com/apache/cloudstack/pull/6050
.. _`#6018`: https://github.com/apache/cloudstack/pull/6018
.. _`#6032`: https://github.com/apache/cloudstack/pull/6032
.. _`#6053`: https://github.com/apache/cloudstack/pull/6053
.. _`#6055`: https://github.com/apache/cloudstack/pull/6055
.. _`#6054`: https://github.com/apache/cloudstack/pull/6054
.. _`#6028`: https://github.com/apache/cloudstack/pull/6028
.. _`#6055`: https://github.com/apache/cloudstack/pull/6055
.. _`#6041`: https://github.com/apache/cloudstack/pull/6041
.. _`#6019`: https://github.com/apache/cloudstack/pull/6019
.. _`#5965`: https://github.com/apache/cloudstack/pull/5965
