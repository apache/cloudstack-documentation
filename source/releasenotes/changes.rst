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


Changes in |release| since 4.15
===============================

Apache CloudStack uses GitHub https://github.com/apache/cloudstack/milestone/16?closed=1
to track its issues.

.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+------------------------------------------------------------+
| Version                 | Github   | Description                                                |
+=========================+==========+============================================================+
| 4.16.0.0                | `#5665`_ | Revert "parallel nic adding"                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5659`_ | api,server,engine/schema: admin listvm api clusterid       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5661`_ | linstor-volume-plugin: Only create diskless assignments on |
|                         |          | nodes                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5645`_ | Marvin: change some vlans in test_data.py                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5657`_ | engine/schema: fix build error in #5642                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5642`_ | upgrade/systemvm: add template zone entries                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5646`_ | usage: updateNewMaxId after sanity check                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5629`_ | cks: refactor code to be architecture agnostic             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5644`_ | ui: fix jobid param for migrate VM storage                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5638`_ | UI - Show password after reinstalling VM                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5643`_ | UI: ip6gateway is missing in createNetwork API             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5624`_ | core: use the URL scheme same as iframe for non-SSL        |
|                         |          | enabled consoles                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5586`_ | Check the pool used space from the bytes used in the       |
|                         |          | storage pool stats collector, for  non-default primary     |
|                         |          | storage pools that cannot provide stats.                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5621`_ | ui: Fix wrong label for addBrocadeVcsDevice                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5593`_ | [UI] Fixed RBD storage connection bug when there are       |
|                         |          | multiple '/', '+' characters in 'RADOS Secret' in Add      |
|                         |          | Primary Storage                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5614`_ | Fix duplicate provider field when adding primary storage   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5612`_ | ui: Removing double footer in NSP forms                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5608`_ | UI - Fixes incorrect switching between pages on Port       |
|                         |          | Forwarding & Load Balancing                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5609`_ | ui: Prevent multiple VM selection and list only VMs IP     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5607`_ | UI - Fixes the error of not being able to search for       |
|                         |          | osType selection                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5599`_ | UI - Sort list idps by alphabest                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5597`_ | UI - Hidden features checkbox as user role                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5598`_ | Fix systemVM template name in metadata file                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5601`_ | ui: Prevent users from viewing - Project Configure Limit   |
|                         |          | tab                                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5585`_ | Fixing error in kube smoke tests                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5583`_ | vmware: fix NPE for volume migration CLUSTER to ZONE-wide  |
|                         |          | pool (#5582)                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5580`_ | VPC: support LB in multiple vpc tiers if LB provider is    |
|                         |          | VpcVirtualRouter                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5582`_ | vmware: fix NPE for volume migration CLUSTER to ZONE-wide  |
|                         |          | pool                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5575`_ | Fix storage cleanup corner case preventing VM deletion     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5577`_ | UI - Fix the error of not being able to read the length of |
|                         |          | numeric                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5573`_ | api: Fix response object for various APIs                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5574`_ | CKS: use cluster-autoscaler-standard.yaml in kubernetes    |
|                         |          | repo                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5571`_ | api: Fix RestartNetwork response type                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5565`_ | engine/schema: add unique constraint for sshkeys UUID      |
|                         |          | column                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5572`_ | UI: Restrict viewing project invitation options when       |
|                         |          | configuration is disabled                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5569`_ | UI - Fix display IP Address allow input                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5568`_ | Fix warning caused due to duplicate declaration of plugin  |
|                         |          | - pom.xml                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5561`_ | [KVM] Add the source disk format for disk conversion/copy  |
|                         |          | using 'qemu-img convert', when specified explicitly, for   |
|                         |          | ScaleIO                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5560`_ | Updated storage type of the volume, in the volume          |
|                         |          | response, based on the underlying storage pool             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5557`_ | Use deploy as is for Vmware tests                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5410`_ | CloudStack fails to migrate VM with volume when there are  |
|                         |          | datadisks attatched                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5554`_ | VR: skip dhcp/dns health check in some cases               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5543`_ | xcp-ng: fix vm boot options                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4329`_ | Adding AutoScaling for cks + CKS CoreOS EOL update +       |
|                         |          | systemvmtemplate improvements                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5551`_ | Add empty config value for scope based config setting      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5542`_ | Report the PowerFlex/ScaleIO disk copy failure during      |
|                         |          | volume migration and fail the migration                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5540`_ | kvm available memory calculation optimization              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5539`_ | Fix resize volume and migrate volume to update volume path |
|                         |          | if DRS is applied on volume in datastore cluster           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5471`_ | vmware, network: add maclearning option                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5547`_ | an inject annotation short                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5541`_ | parallel nic adding                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5546`_ | [UI] Edit backup offering                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5530`_ | VR: fix data-server if shared network has multiple ip      |
|                         |          | ranges                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5513`_ | kvm: add VM Settings for virtual GPU hardware type and     |
|                         |          | memory                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5501`_ | server: check service offering (storage) tags when         |
|                         |          | reallocate a ROOT disk                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5532`_ | Remove logic that creates gap for multiple 'source NAT' in |
|                         |          | VR                                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5446`_ | OVS/GRE: bug fixes                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5470`_ | vmware, ui: update portgroup on network update             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5511`_ | Create UpdateBackupOffering API                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5510`_ | Fix export snapshot and template to secondary storage to   |
|                         |          | export only required disk                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5504`_ | Fix permission issue during Diagnostic service garbage     |
|                         |          | collection                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5537`_ | UI - Remove duplicate endipv6 item in shared network       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5526`_ | UI - Fixes modal width by device screen                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5521`_ | server: cannot deploy/start vm if service offering has     |
|                         |          | multiple tags                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4215`_ | Enable account settings to be visible under domain         |
|                         |          | settings                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5522`_ | Datastore cluster protocol in zone wizard for vmware       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5515`_ | simulator: Add support to scale a VM                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4826`_ | Allow storage plugins to get storage/volume stats without  |
|                         |          | sending commands to hosts                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5520`_ | Allow users (User account Role) to delete / archive events |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5469`_ | server: add vm boot details for start vm api               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4617`_ | Provide option to force delete the project                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5503`_ | test_vpc_redundant.py: reduce sleep time from 1 hour to 21 |
|                         |          | mins                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5455`_ | Improve Veeam Plugin logs                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5507`_ | tools/docker: Upgrade to ubuntu 20.04 , MySQL 8 and        |
|                         |          | python3                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5505`_ | marvin: Refactor - cleanup of resource after test run      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5428`_ | resource limit: Fix resource limit check on VM start       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5483`_ | marvin: Fix intermittent failure observed in               |
|                         |          | test_02_list_snapshots_with_removed_data_store             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5419`_ | CPVM: use X509ExtendedTrustManager to skip hostname        |
|                         |          | verification                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5480`_ | Refactor GroupByExtension to improve test logic            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5490`_ | UI: Fix VM state column                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#3804`_ | Display capability info in listNetwork response            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5496`_ | ui: recommend adv zone to new users and show basic zone as |
|                         |          | bottom option                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5495`_ | move broken unmaintained test out of ".../smoke"           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5492`_ | Update README.md                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5486`_ | travis: fix test/integration/component/test_public_ip.py   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5488`_ | ui: Add support to filter role permissions                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5481`_ | ui: fix create account/user with saml                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5485`_ | ui: Fix editVM in projectview                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5454`_ | [UI] Fixes: edit tariff quota and allow user driven        |
|                         |          | backups parameter in Import Backup Offering                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4890`_ | Universal sshkey and password manager script               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5458`_ | New API endpoint to update pod management network IP range |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5472`_ | UI - Fixes search error in selectbox                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5468`_ | api: Fix list templates when no secondary stores present   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5474`_ | change logging during upgrade                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5459`_ | server: Add support to encrypt https.keystore.password in  |
|                         |          | server.properties                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5476`_ | UI: Fixes issue during logout as user / domain admin       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5411`_ | Add New API endpoint: UpdateVlanIpRange                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5464`_ | server: fix list public ip returns duplicated records      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4634`_ | Display vlan ip range for specified domainid               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5465`_ | ui: Move resource icon to first column for VM list view    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5449`_ | [Vmware] Add missing condition to cleanup nics if there    |
|                         |          | are commands to send                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5463`_ | UI: list static routes with listall=true                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5460`_ | Display ACL id for the private gateway                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5453`_ | Updated the event message with proper json format for cmd  |
|                         |          | info and job result                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5369`_ | kvm: Add check if host meets the minimum requirements      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5420`_ | server: allow listing custom offerings for a running VM    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5448`_ | [Vmware] Fix for ovf templates with prefix                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5456`_ | move out broken tests                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4994`_ | Linstor volume plugin                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4635`_ | Persist vpn connection state before restarting             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5388`_ | kvm: honor migrate.wait and abort vm migration job         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5451`_ | ui: Fix Load Balancer Rules alignment issue                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5424`_ | Updated pod response, grouped the parameters: "startip,    |
|                         |          | endip, vlanid, forsystemvms" as ip range response and      |
|                         |          | added to ipranges parameter.                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5447`_ | ui: Refresh Usage dashboard when swapping between Project  |
|                         |          | and Default view                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5157`_ | UI: Support to upload resource icons                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5425`_ | api: Update DNS on changing VM name                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4741`_ | VM has wrong network statistics with multiple nics in      |
|                         |          | shared networks                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5450`_ | UI - Remove white space after detail string in Firefox     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5417`_ | server: skip max guest limit check for KVM host            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5421`_ | server: fix addCluster for vmware, others                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5439`_ | ui: Fix Scale VM failure - missing args when custom        |
|                         |          | compute offering is selected                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5423`_ | ui: select newly created network in deploy vm              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5395`_ | ui: Allow searching in dropdowns                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5441`_ | utils: remove duplicate commons-lang3 dependency           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5438`_ | ui: Send deployvm api call as post                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5437`_ | ui: Remove double footer                                   |
+-------------------------+----------+------------------------------------------------------------+

126 Issues listed

.. _`#5665`: https://github.com/apache/cloudstack/pull/5665 
.. _`#5659`: https://github.com/apache/cloudstack/pull/5659 
.. _`#5661`: https://github.com/apache/cloudstack/pull/5661 
.. _`#5645`: https://github.com/apache/cloudstack/pull/5645 
.. _`#5657`: https://github.com/apache/cloudstack/pull/5657 
.. _`#5642`: https://github.com/apache/cloudstack/pull/5642 
.. _`#5646`: https://github.com/apache/cloudstack/pull/5646 
.. _`#5629`: https://github.com/apache/cloudstack/pull/5629 
.. _`#5644`: https://github.com/apache/cloudstack/pull/5644 
.. _`#5638`: https://github.com/apache/cloudstack/pull/5638 
.. _`#5643`: https://github.com/apache/cloudstack/pull/5643 
.. _`#5624`: https://github.com/apache/cloudstack/pull/5624 
.. _`#5586`: https://github.com/apache/cloudstack/pull/5586 
.. _`#5621`: https://github.com/apache/cloudstack/pull/5621 
.. _`#5593`: https://github.com/apache/cloudstack/pull/5593 
.. _`#5614`: https://github.com/apache/cloudstack/pull/5614 
.. _`#5612`: https://github.com/apache/cloudstack/pull/5612 
.. _`#5608`: https://github.com/apache/cloudstack/pull/5608 
.. _`#5609`: https://github.com/apache/cloudstack/pull/5609 
.. _`#5607`: https://github.com/apache/cloudstack/pull/5607 
.. _`#5599`: https://github.com/apache/cloudstack/pull/5599 
.. _`#5597`: https://github.com/apache/cloudstack/pull/5597 
.. _`#5598`: https://github.com/apache/cloudstack/pull/5598 
.. _`#5601`: https://github.com/apache/cloudstack/pull/5601 
.. _`#5585`: https://github.com/apache/cloudstack/pull/5585 
.. _`#5583`: https://github.com/apache/cloudstack/pull/5583 
.. _`#5580`: https://github.com/apache/cloudstack/pull/5580 
.. _`#5582`: https://github.com/apache/cloudstack/pull/5582 
.. _`#5575`: https://github.com/apache/cloudstack/pull/5575 
.. _`#5577`: https://github.com/apache/cloudstack/pull/5577 
.. _`#5573`: https://github.com/apache/cloudstack/pull/5573 
.. _`#5574`: https://github.com/apache/cloudstack/pull/5574 
.. _`#5571`: https://github.com/apache/cloudstack/pull/5571 
.. _`#5565`: https://github.com/apache/cloudstack/pull/5565 
.. _`#5572`: https://github.com/apache/cloudstack/pull/5572 
.. _`#5569`: https://github.com/apache/cloudstack/pull/5569 
.. _`#5568`: https://github.com/apache/cloudstack/pull/5568 
.. _`#5561`: https://github.com/apache/cloudstack/pull/5561 
.. _`#5560`: https://github.com/apache/cloudstack/pull/5560 
.. _`#5557`: https://github.com/apache/cloudstack/pull/5557 
.. _`#5410`: https://github.com/apache/cloudstack/pull/5410 
.. _`#5554`: https://github.com/apache/cloudstack/pull/5554 
.. _`#5543`: https://github.com/apache/cloudstack/pull/5543 
.. _`#4329`: https://github.com/apache/cloudstack/pull/4329 
.. _`#5551`: https://github.com/apache/cloudstack/pull/5551 
.. _`#5542`: https://github.com/apache/cloudstack/pull/5542 
.. _`#5540`: https://github.com/apache/cloudstack/pull/5540 
.. _`#5539`: https://github.com/apache/cloudstack/pull/5539 
.. _`#5471`: https://github.com/apache/cloudstack/pull/5471 
.. _`#5547`: https://github.com/apache/cloudstack/pull/5547 
.. _`#5541`: https://github.com/apache/cloudstack/pull/5541 
.. _`#5546`: https://github.com/apache/cloudstack/pull/5546 
.. _`#5530`: https://github.com/apache/cloudstack/pull/5530 
.. _`#5513`: https://github.com/apache/cloudstack/pull/5513 
.. _`#5501`: https://github.com/apache/cloudstack/pull/5501 
.. _`#5532`: https://github.com/apache/cloudstack/pull/5532 
.. _`#5446`: https://github.com/apache/cloudstack/pull/5446 
.. _`#5470`: https://github.com/apache/cloudstack/pull/5470 
.. _`#5511`: https://github.com/apache/cloudstack/pull/5511 
.. _`#5510`: https://github.com/apache/cloudstack/pull/5510 
.. _`#5504`: https://github.com/apache/cloudstack/pull/5504 
.. _`#5537`: https://github.com/apache/cloudstack/pull/5537 
.. _`#5526`: https://github.com/apache/cloudstack/pull/5526 
.. _`#5521`: https://github.com/apache/cloudstack/pull/5521 
.. _`#4215`: https://github.com/apache/cloudstack/pull/4215 
.. _`#5522`: https://github.com/apache/cloudstack/pull/5522 
.. _`#5515`: https://github.com/apache/cloudstack/pull/5515 
.. _`#4826`: https://github.com/apache/cloudstack/pull/4826 
.. _`#5520`: https://github.com/apache/cloudstack/pull/5520 
.. _`#5469`: https://github.com/apache/cloudstack/pull/5469 
.. _`#4617`: https://github.com/apache/cloudstack/pull/4617 
.. _`#5503`: https://github.com/apache/cloudstack/pull/5503 
.. _`#5455`: https://github.com/apache/cloudstack/pull/5455 
.. _`#5507`: https://github.com/apache/cloudstack/pull/5507 
.. _`#5505`: https://github.com/apache/cloudstack/pull/5505 
.. _`#5428`: https://github.com/apache/cloudstack/pull/5428 
.. _`#5483`: https://github.com/apache/cloudstack/pull/5483 
.. _`#5419`: https://github.com/apache/cloudstack/pull/5419 
.. _`#5480`: https://github.com/apache/cloudstack/pull/5480 
.. _`#5490`: https://github.com/apache/cloudstack/pull/5490 
.. _`#3804`: https://github.com/apache/cloudstack/pull/3804 
.. _`#5496`: https://github.com/apache/cloudstack/pull/5496 
.. _`#5495`: https://github.com/apache/cloudstack/pull/5495 
.. _`#5492`: https://github.com/apache/cloudstack/pull/5492 
.. _`#5486`: https://github.com/apache/cloudstack/pull/5486 
.. _`#5488`: https://github.com/apache/cloudstack/pull/5488 
.. _`#5481`: https://github.com/apache/cloudstack/pull/5481 
.. _`#5485`: https://github.com/apache/cloudstack/pull/5485 
.. _`#5454`: https://github.com/apache/cloudstack/pull/5454 
.. _`#4890`: https://github.com/apache/cloudstack/pull/4890 
.. _`#5458`: https://github.com/apache/cloudstack/pull/5458 
.. _`#5472`: https://github.com/apache/cloudstack/pull/5472 
.. _`#5468`: https://github.com/apache/cloudstack/pull/5468 
.. _`#5474`: https://github.com/apache/cloudstack/pull/5474 
.. _`#5459`: https://github.com/apache/cloudstack/pull/5459 
.. _`#5476`: https://github.com/apache/cloudstack/pull/5476 
.. _`#5411`: https://github.com/apache/cloudstack/pull/5411 
.. _`#5464`: https://github.com/apache/cloudstack/pull/5464 
.. _`#4634`: https://github.com/apache/cloudstack/pull/4634 
.. _`#5465`: https://github.com/apache/cloudstack/pull/5465 
.. _`#5449`: https://github.com/apache/cloudstack/pull/5449 
.. _`#5463`: https://github.com/apache/cloudstack/pull/5463 
.. _`#5460`: https://github.com/apache/cloudstack/pull/5460 
.. _`#5453`: https://github.com/apache/cloudstack/pull/5453 
.. _`#5369`: https://github.com/apache/cloudstack/pull/5369 
.. _`#5420`: https://github.com/apache/cloudstack/pull/5420 
.. _`#5448`: https://github.com/apache/cloudstack/pull/5448 
.. _`#5456`: https://github.com/apache/cloudstack/pull/5456 
.. _`#4994`: https://github.com/apache/cloudstack/pull/4994 
.. _`#4635`: https://github.com/apache/cloudstack/pull/4635 
.. _`#5388`: https://github.com/apache/cloudstack/pull/5388 
.. _`#5451`: https://github.com/apache/cloudstack/pull/5451 
.. _`#5424`: https://github.com/apache/cloudstack/pull/5424 
.. _`#5447`: https://github.com/apache/cloudstack/pull/5447 
.. _`#5157`: https://github.com/apache/cloudstack/pull/5157 
.. _`#5425`: https://github.com/apache/cloudstack/pull/5425 
.. _`#4741`: https://github.com/apache/cloudstack/pull/4741 
.. _`#5450`: https://github.com/apache/cloudstack/pull/5450 
.. _`#5417`: https://github.com/apache/cloudstack/pull/5417 
.. _`#5421`: https://github.com/apache/cloudstack/pull/5421 
.. _`#5439`: https://github.com/apache/cloudstack/pull/5439 
.. _`#5423`: https://github.com/apache/cloudstack/pull/5423 
.. _`#5395`: https://github.com/apache/cloudstack/pull/5395 
.. _`#5441`: https://github.com/apache/cloudstack/pull/5441 
.. _`#5438`: https://github.com/apache/cloudstack/pull/5438 
.. _`#5437`: https://github.com/apache/cloudstack/pull/5437 

