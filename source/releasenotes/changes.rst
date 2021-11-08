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


Changes in |release| since 4.15.2.0
===================================

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


Changes in 4.15.2.0 since 4.15.1.0
===================================

Apache CloudStack uses GitHub https://github.com/apache/cloudstack/milestone/20?closed=1
to track its issues.

.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+------------------------------------------------------------+
| Version                 | Github   | Description                                                |
+=========================+==========+============================================================+
| 4.15.2.0                | `#5463`_ | UI: list static routes with listall=true                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5435`_ | Fix public IP actions buttons not working unless           |
|                         |          | refreshing the page                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5432`_ | api, ui: return default ui pagesize as part of capability  |
|                         |          | response                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5427`_ | ui: fix add management ip range form                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5431`_ | Hide settings button if not on development mode            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5429`_ | ui: show nicAdapter selection for VMware non-readfromova   |
|                         |          | template                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5387`_ | api, ui: fix NPE with deployVirtualMachine when null       |
|                         |          | boottype                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5408`_ | Legacy UI: Display Accounts Tab to Project Admins          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5404`_ | Allow public templates with no url to be migrated          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5394`_ | ui: Honour default.ui.page.size                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5259`_ | usage: create backup usage record for vmId-offeringId pair |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5307`_ | Filter disk / service offerings by domain at DB level      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5339`_ | server: check server capacity when start/deploy a vm       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5333`_ | vmware: delete snapshot disk after backup to secondary     |
|                         |          | storage                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5403`_ | Add 4.15.2 schema and upgrade path                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5376`_ | Use source IP from same subnet for snat                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5375`_ | vr: ipsec/l2tp vpn secret with no ID selectors             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5374`_ | [VMware] Cancel the pending tasks for a worker VM before   |
|                         |          | destroying it                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5379`_ | api: List details of template download state for stores    |
|                         |          | corresponding to a zone                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5380`_ | vmware: check checksum before copying systemvm ISO to      |
|                         |          | decide if it is needed                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5392`_ | UI - Scale VM - Fix compute offering selection not working |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5393`_ | ui: Refresh page on deployvm result                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5373`_ | server: do not remove volume from DB if fail to expunge it |
|                         |          | from primary storage or secondary storage                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5335`_ | xcp-ng: allow passing vm boot options                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5349`_ | Fix of creating volumes from snapshots without backup to   |
|                         |          | secondary storage                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5366`_ | updated maven dependency due to #5363                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5311`_ | [VMware] Start VM with deploy-as-is template having        |
|                         |          | multiple controller types                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5377`_ | [VMware] Added Worker VM tags for few cloned VMs while     |
|                         |          | performing some volume operations.                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5364`_ | server: allow destroy/recover volumes which are attached   |
|                         |          | to removed vms                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5384`_ | ubuntu: Fix failure to scp diagnostic data file from SSVM  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5356`_ | server: detach data disks before destroying vms            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5367`_ | ui: Fix search with same parameters                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5360`_ | ui: Go back for delete actions before querying async job   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5319`_ | vr: reload dnsmasq when start vms                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5354`_ | Fix security_groups for c8/suse                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5359`_ | UI - Add storage name to delete primary/secondary storage  |
|                         |          | dialog                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5345`_ | UI - VM - hide button take vm volume snapshot for          |
|                         |          | Destroyed state                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5331`_ | vr: cleanup files in /var/cache/cloud/processed every day  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5348`_ | security group: fix component test                         |
|                         |          | test_multiple_nic_support.py failures                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5328`_ | Fix iptable rules when chain reference count is 0          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5342`_ | add license header in HostMetricsResponseTest.java         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5326`_ | ui: Update placeholders for adding new tier                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5318`_ | Fix iptable rules in ubuntu 20 for bridge name             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5329`_ | metrics: fix hostsmetricsresponse for zero cpu, locale     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5303`_ | UI - Zone wizard - Fixes wrong add resource step with      |
|                         |          | localstorageenabled                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5327`_ | s2svpn: Set initial state as Connecting                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5304`_ | compatibility fix for Packer v1.7.4, update debian         |
|                         |          | template to 10.10.0                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5258`_ | vmware: get recommended disk controller only when root or  |
|                         |          | data disk controller is osdefault                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5052`_ | UI: Dark mode toggle button on Management Server           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5301`_ | ui: fix display host hypervisorversion                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#4885`_ | UI: Add multiple management server support                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5270`_ | server: skip zone check for PERHOST iso during attachIso   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5287`_ | UI - Zone Wizard - Fixes the IP range form fields are too  |
|                         |          | narrow                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5275`_ | vr: restart conntrackd instead of '/usr/sbin/conntrackd    |
|                         |          | -d'                                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5292`_ | ui: Show host as unsecure in listview                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5269`_ | ui: fix capitalise filter                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5278`_ | ui: Add 'on / off' to status icon and make it case         |
|                         |          | insensitive                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5219`_ | [TEST] - Test unit - Fix failing UI unit test 4.15 branch  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5253`_ | UI -  zone wizard - change the argument of params.ipv6dns2 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5224`_ | ui: submit form with false boolean params                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5205`_ | ui: fix create shared network with multi-zone              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5231`_ | api: Fix pagination for list PublicIPAddresses             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5246`_ | ui: Fix comparator for boolean                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5247`_ | ui: Fix current for vmsnapshots                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5225`_ | Fix of shrinking volumes with QCOW2 format                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5206`_ | UI: only display host information, if they are relevant    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5214`_ | ui: Refresh after async job completed only on current /    |
|                         |          | parent page                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#4782`_ | UI: Refactor async job polling codebase-wide               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5193`_ | kvm: pre-add 32 PCI controller for hot-plug issue on       |
|                         |          | ARM64/aarch64                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5184`_ | server: fix network access for addNicToVirtualMachine API  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5199`_ | UI: deploy VM - FIX missing custom iops field              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5197`_ | UI: fix NIC table on instance view                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5144`_ | configdrive: fix some failures in                          |
|                         |          | tests/component/test_configdrive.py                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5064`_ | ui: refactor get api params in forms                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#5164`_ | kvm: fix VM HA on zone-wide storage pools                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.2.0                | `#4843`_ | ui: deployvm - Add option to stay on page                  |
+-------------------------+----------+------------------------------------------------------------+

76 Issues listed

.. _`#5463`: https://github.com/apache/cloudstack/pull/5463
.. _`#5435`: https://github.com/apache/cloudstack/pull/5435
.. _`#5432`: https://github.com/apache/cloudstack/pull/5432
.. _`#5427`: https://github.com/apache/cloudstack/pull/5427
.. _`#5431`: https://github.com/apache/cloudstack/pull/5431
.. _`#5429`: https://github.com/apache/cloudstack/pull/5429
.. _`#5387`: https://github.com/apache/cloudstack/pull/5387
.. _`#5408`: https://github.com/apache/cloudstack/pull/5408
.. _`#5404`: https://github.com/apache/cloudstack/pull/5404
.. _`#5394`: https://github.com/apache/cloudstack/pull/5394
.. _`#5259`: https://github.com/apache/cloudstack/pull/5259
.. _`#5307`: https://github.com/apache/cloudstack/pull/5307
.. _`#5339`: https://github.com/apache/cloudstack/pull/5339
.. _`#5333`: https://github.com/apache/cloudstack/pull/5333
.. _`#5403`: https://github.com/apache/cloudstack/pull/5403
.. _`#5376`: https://github.com/apache/cloudstack/pull/5376
.. _`#5375`: https://github.com/apache/cloudstack/pull/5375
.. _`#5374`: https://github.com/apache/cloudstack/pull/5374
.. _`#5379`: https://github.com/apache/cloudstack/pull/5379
.. _`#5380`: https://github.com/apache/cloudstack/pull/5380
.. _`#5392`: https://github.com/apache/cloudstack/pull/5392
.. _`#5393`: https://github.com/apache/cloudstack/pull/5393
.. _`#5373`: https://github.com/apache/cloudstack/pull/5373
.. _`#5335`: https://github.com/apache/cloudstack/pull/5335
.. _`#5349`: https://github.com/apache/cloudstack/pull/5349
.. _`#5366`: https://github.com/apache/cloudstack/pull/5366
.. _`#5311`: https://github.com/apache/cloudstack/pull/5311
.. _`#5377`: https://github.com/apache/cloudstack/pull/5377
.. _`#5364`: https://github.com/apache/cloudstack/pull/5364
.. _`#5384`: https://github.com/apache/cloudstack/pull/5384
.. _`#5356`: https://github.com/apache/cloudstack/pull/5356
.. _`#5367`: https://github.com/apache/cloudstack/pull/5367
.. _`#5360`: https://github.com/apache/cloudstack/pull/5360
.. _`#5319`: https://github.com/apache/cloudstack/pull/5319
.. _`#5354`: https://github.com/apache/cloudstack/pull/5354
.. _`#5359`: https://github.com/apache/cloudstack/pull/5359
.. _`#5345`: https://github.com/apache/cloudstack/pull/5345
.. _`#5331`: https://github.com/apache/cloudstack/pull/5331
.. _`#5348`: https://github.com/apache/cloudstack/pull/5348
.. _`#5328`: https://github.com/apache/cloudstack/pull/5328
.. _`#5342`: https://github.com/apache/cloudstack/pull/5342
.. _`#5326`: https://github.com/apache/cloudstack/pull/5326
.. _`#5318`: https://github.com/apache/cloudstack/pull/5318
.. _`#5329`: https://github.com/apache/cloudstack/pull/5329
.. _`#5303`: https://github.com/apache/cloudstack/pull/5303
.. _`#5327`: https://github.com/apache/cloudstack/pull/5327
.. _`#5304`: https://github.com/apache/cloudstack/pull/5304
.. _`#5258`: https://github.com/apache/cloudstack/pull/5258
.. _`#5052`: https://github.com/apache/cloudstack/pull/5052
.. _`#5301`: https://github.com/apache/cloudstack/pull/5301
.. _`#4885`: https://github.com/apache/cloudstack/pull/4885
.. _`#5270`: https://github.com/apache/cloudstack/pull/5270
.. _`#5287`: https://github.com/apache/cloudstack/pull/5287
.. _`#5275`: https://github.com/apache/cloudstack/pull/5275
.. _`#5292`: https://github.com/apache/cloudstack/pull/5292
.. _`#5269`: https://github.com/apache/cloudstack/pull/5269
.. _`#5278`: https://github.com/apache/cloudstack/pull/5278
.. _`#5219`: https://github.com/apache/cloudstack/pull/5219
.. _`#5253`: https://github.com/apache/cloudstack/pull/5253
.. _`#5224`: https://github.com/apache/cloudstack/pull/5224
.. _`#5205`: https://github.com/apache/cloudstack/pull/5205
.. _`#5231`: https://github.com/apache/cloudstack/pull/5231
.. _`#5246`: https://github.com/apache/cloudstack/pull/5246
.. _`#5247`: https://github.com/apache/cloudstack/pull/5247
.. _`#5225`: https://github.com/apache/cloudstack/pull/5225
.. _`#5206`: https://github.com/apache/cloudstack/pull/5206
.. _`#5214`: https://github.com/apache/cloudstack/pull/5214
.. _`#4782`: https://github.com/apache/cloudstack/pull/4782
.. _`#5193`: https://github.com/apache/cloudstack/pull/5193
.. _`#5184`: https://github.com/apache/cloudstack/pull/5184
.. _`#5199`: https://github.com/apache/cloudstack/pull/5199
.. _`#5197`: https://github.com/apache/cloudstack/pull/5197
.. _`#5144`: https://github.com/apache/cloudstack/pull/5144
.. _`#5064`: https://github.com/apache/cloudstack/pull/5064
.. _`#5164`: https://github.com/apache/cloudstack/pull/5164
.. _`#4843`: https://github.com/apache/cloudstack/pull/4843


Changes in 4.15.1.0 since 4.15.0.0
===================================

Apache CloudStack uses GitHub https://github.com/apache/cloudstack/milestone/17?closed=1
to track its issues.


.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+------------------------------------------------------------+
| Version                 | Github   | Description                                                |
+=========================+==========+============================================================+
| 4.15.1.0                | `#5164`_ | kvm: fix VM HA on zone-wide storage pools                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4843`_ | ui: deployvm - Add option to stay on page                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5148`_ | Bug/false positive success message vm start                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5160`_ | Fix configuration of ntp server list in systemVMs          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5130`_ | Fix of delete of Ceph's snapshots from secondary storage   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5153`_ | ui: Notify users of new VM password on resetting VM's SSH  |
|                         |          | key                                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5115`_ | packaging: Create cloud user and group if not present      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5123`_ | ui: fix missing component in SearchView                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5132`_ | Change logrotate interval to hourly                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5137`_ | UI: SystemVM - Enabling Quickview for newly resource       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5143`_ | VR: fix source cidr of egress rules are not applied        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5150`_ | UI fix deployVm with rootdisk size wrongly converted       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5129`_ | ui: Notify vm password on reinstall of VM (for password    |
|                         |          | enabled templates)                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5105`_ | server: set correct gateway when update vm nic on shared   |
|                         |          | networks                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5118`_ | Fix typo in error message on login page                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5113`_ | allow big contents from error output in marvin tests       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5078`_ | vxlan: arp does not work between hosts as multicast group  |
|                         |          | is communicated over physical nic instead of linux bridge  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5108`_ | ui: show read from ova only for ova format                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5109`_ | Localization: Hellenic (Greek) Translation                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5095`_ | Failed to scale between Service Offerings with the same    |
|                         |          | root disk size                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5098`_ | ui: add action syncStoragePool                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5097`_ | Update chain info of the volumes after migrate operations  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5076`_ | [Vmware] Fix lsilogcsas controller for deploy-as-is        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5039`_ | maven: Use https for jenkins repo, to fix build with newer |
|                         |          | maven                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5089`_ | ui: fix focus in deployvm form                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5072`_ | Fix of some UEFI related issues                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5085`_ | Root disk size should be listed in GB at                   |
|                         |          | listServiceOffering                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5084`_ | ui: remove redundant columns in list VMs view              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5081`_ | ui: Fix error when no ipv6 address                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5074`_ | Check for VLAN or VXLAN in                                 |
|                         |          | NetworkDaoImpl.listByPhysicalNetworkPvlan                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5063`_ | ui: fix adduser form                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5059`_ | vr: remove old ips with same mac address in dhcpentry      |
|                         |          | databag                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5053`_ | xenserver: attempt eject and destroying patch VBD          |
|                         |          | separately                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5057`_ | Create fcd folder on local storage in VMware vSphere       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5061`_ | Fix string format error                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5017`_ | Usage: usage generated for destroyed VMs with no backups   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5049`_ | FIX Network with SG Disabled still has security group      |
|                         |          | script adding rules on KVM                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5032`_ | [Vmware] Fix worker VM invalid numeric value               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5045`_ | server: fixes NPE on empty vmware.root.disk.controller     |
|                         |          | config                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5048`_ | secondary-storage: fix account template directory size     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5050`_ | ui: pass requireshvm param for register/upload template    |
|                         |          | API                                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5029`_ | Prevent NPE if hypervisor's capabilities are null          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5003`_ | UI: Make 'ACL' field as mandatory and add warning message  |
|                         |          | for default_allow and default_deny                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5033`_ | Fixed invalid ostypeid when not using deployasis           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5006`_ | Disk controller vmware deploy as is                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5010`_ | SystemVM: Set agent state to disconnected on Stopping the  |
|                         |          | systemVM                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5025`_ | setup: pass password in quotes for                         |
|                         |          | cloudstack-setup-databases                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5023`_ | Fix in Marvin - migrate_vm_with_volume                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4644`_ | server: destroy ssvm, cpvm on last host maintenance        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4795`_ | api/server: cpu, memory values with overprovisioning in    |
|                         |          | metrics response                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4647`_ | forceha: fix two issues when (1)stop vm from inside (2)    |
|                         |          | force remove host                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5020`_ | ui: Allow IP range creation for Physical Network - Guest   |
|                         |          | Traffic in Basic Zones                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5022`_ | ui: pass podid for basic zone createvlaniprange            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5013`_ | network/VR: fix dhcp/password/metadata issues on shared    |
|                         |          | networks with multiple subnets                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5015`_ | Fix deploy-as-is not honoured on upload from local         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5014`_ | ui: prevent same string docHelp override                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5011`_ | ui: Display Zone Name instead of Zone UUID in list view    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4871`_ | VMware Datastore Cluster primary storage pool              |
|                         |          | synchronisation                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4842`_ | ui: add tooltips for actions in tab                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#5001`_ | server: NPE may cause management server to not start       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4986`_ | allow zero as cpu speed value in service offerings         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4999`_ | UI: Update treeview when click the refresh button          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4996`_ | Updated since and validations attributes for the           |
|                         |          | ikeversion and splitconnections parameters in vpn customer |
|                         |          | gateway cmd(s)                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4953`_ | Adding VPN options for IKE version and IKE split           |
|                         |          | connections                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4995`_ | Fixed error when passing shell reserved characters to      |
|                         |          | setup databases                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4981`_ | ui: Prevent reset of port-forward rules on cancelling a    |
|                         |          | form                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4987`_ | ui: Adding success message for DomainActionForm            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4988`_ | ui: show VR offering when provider is VR                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4989`_ | UI: Prevent listing network offering with external LB for  |
|                         |          | VPC tiers if a n/w already exists                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4991`_ | ui: Hide reset password button for a Running VM            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4993`_ | ui: Close Create network form from Zones -> Physical       |
|                         |          | Network (Guest) -> Traffic Type view                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4979`_ | ui: show domain paths for offering domain selection        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4980`_ | ui: rename acl reason to description                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4970`_ | CentOS 8: Install libgcrypt v1.8.5 required by libvirt 6.0 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4915`_ | Allow to upgrade service offerings from local <> shared    |
|                         |          | storage pools                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4967`_ | Increase max length for VMInstanceVO.backupVolumes         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4964`_ | ui: Fix Settings Tab view                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4901`_ | [Vmware] Make deploy-as-is optional                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4957`_ | vmware cks: Guard k8s cluster root disk resize if no root  |
|                         |          | disk size passed                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4924`_ | protect against stray snapshot-details without snapshot    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4971`_ | ui: Display 'Add LDAP Account' button when LDAP            |
|                         |          | configuration is added                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4907`_ | vmware: Add force parameter to iso attach/detach           |
|                         |          | operations                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4962`_ | UI: Save the tab and re-activate it after submitting the   |
|                         |          | form.                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4946`_ | api: fix disk/service offering volume response keys        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4948`_ | UI: Show IPv6 address of Instance                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4929`_ | marvin: fix test_scale_vm for xenserver/Xcp-ng             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4951`_ | Adding net tools as a dependency                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4952`_ | ui: Show traffic type in physical networks tab             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4859`_ | CLOUDSTACK-10434:Some APIs should have access check        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4949`_ | ui: Show domain path instead of name                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4950`_ | ui: Fix error in adduser                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4944`_ | Fix NPE on template garbage collection on primary storage  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4758`_ | vmware: fix stopped VM volume migration                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4934`_ | Fix volume state on migrate with                           |
|                         |          | migrateVirtualMachineWithVolume API call                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4909`_ | ui: fix autogen form exec with action mapping options      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4938`_ | cloudian: Set cloudian.connector.enabled as not dynamic    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4926`_ | Add UnavailableCommandException at ExceptionErrorCodeMap   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4918`_ | Stat collector solidfire capacity fix                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4933`_ | UI: Disabled root disk size customization if Service       |
|                         |          | Offering has a fixed size                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4927`_ | debian: remove duplicate agent jar copy                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4923`_ | Support to update disk/network offering tags from UI       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4912`_ | ui: Show diskoffering for create volume from ROOT volume   |
|                         |          | snaps                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4300`_ | engine: add support for VMware 7.0 dependency and          |
|                         |          | hypervisor capability                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4920`_ | UI: Fixes security group egressrule and ingressrule        |
|                         |          | mistake                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4913`_ | test: reduce vr traceroute hops                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4493`_ | Recover VM not able to attach the data disks which were    |
|                         |          | attached before destroy                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4917`_ | UI: Search view - Fixes the color style of the filter icon |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4916`_ | Localization: Korean language support for all features of  |
|                         |          | the new CloudStack UI.                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4910`_ | UI: fix login on UI                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4738`_ | Fix VMware OVF properties copy from template               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4898`_ | VM Snapshot: Prevent vm snapshots being indefinitely stuck |
|                         |          | in Expunging state on deletion failure                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4638`_ | server: fix root disk size on vm reset                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4899`_ | Fix orphan entry on ldap trust map after account removal   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4895`_ | vmware: fix inter-cluster stopped vm and volume migration  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4847`_ | Restricting http access on VR to internal network          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4717`_ | Added recursive fetch of child domains for                 |
|                         |          | listUsageRecords API call                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4801`_ | skip livemigration for centos                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4672`_ | hypervisor: XCP-ng 8.2 support                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4884`_ | host-allocator: check capacity for suitable hosts          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4896`_ | marvin - Fix k8s test failures on VMware                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4679`_ | Disable shrinking QCOW2 volumes                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4099`_ | using forked version of trilead-ssh2 (from org.jenkins-ci) |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4892`_ | UI: Physical Network Setup in Zone Wizard                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4851`_ | [Vmware] Fix worker VMs hardware version small bug         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4802`_ | wiremock version 2.11 is incompatible with java 11         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4773`_ | Fix deploy VM from ISOs with UEFI                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4794`_ | server: filter null details during volume to template      |
|                         |          | creation                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4666`_ | Fix bug in creating shared network                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4769`_ | UI: Save and auto-expand list domain when reloading        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4775`_ | [Backport] #4698 Fix npe when migrating vm with volume     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4894`_ | travis: fix component test failure - persistent networks   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4816`_ | xenserver: retrieve correct name-label for presetup store  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4811`_ | UI: Moves fetchdata() to the created()                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4676`_ | Display public ip addresses for shared network             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4873`_ | Fix no "data-server" DNS record for VPC router             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4888`_ | Disable VR health check for VPC without tiers              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4893`_ | Remove .env.local                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4870`_ | kvm: remove unnecessary new String                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4882`_ | UI: Restored the Basic Networking                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4869`_ | VR: fix rsyslog compresses log files but not release disk  |
|                         |          | space in VR                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4745`_ | ui: allow docHelp override using config.json               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4872`_ | systemvm: remove logrotate config for wtmp and btmp        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#3944`_ | vpc/server: Fix network statistics for vpc                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4675`_ | Bug fix in displaying public IP address of shared networks |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4789`_ | api/server: fix hahost value in listHosts                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4804`_ | server: allow copy cross-zone templates to other zone      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4862`_ | ui: Display root disk size in Compute offering details     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4867`_ | ui: assignVM: Set isrecursive to false when fetching       |
|                         |          | accounts                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4764`_ | UI: Fix create zone wizard on mobile view                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4571`_ | uservmjoindaoimpl: Set free memory to zero if greater than |
|                         |          | total memory                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4864`_ | Add 'break' at RedifshClient request re-try loop (fixed    |
|                         |          | issue from 4846)                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4840`_ | Remove the rule(s) validation with api names while         |
|                         |          | importing a role                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4805`_ | server: create DB entry for storage pool capacity when     |
|                         |          | create storage pool                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4765`_ | UI: Fixes page size changer doesn't show up on mobile mode |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4763`_ | UI: Add cancel button missing on dialog                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4762`_ | UI: Auto-focus input, form                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4829`_ | volume resize: Fix issue with volume resize on VMWare      |
|                         |          | (deploy as-is templates)                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4866`_ | tests: Extend wait time after interrupt (#4815)            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4800`_ | kvm: Do not set backing file format of DATADISK in vm      |
|                         |          | start/migration                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4793`_ | systemvmtemplate: new template for 4.15.1                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4744`_ | UI: Fix update template permission with different domain   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4861`_ | Revert "Add 'break' at RedifshClient request re-try loop"  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4748`_ | Template cleanup : Update vm_template table to set         |
|                         |          | template as removed on deletion                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4846`_ | Add 'break' at RedifshClient request re-try loop           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4857`_ | ui: Disable login button until redirected                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4777`_ | Load modules to support NAT traversal in VR                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4806`_ | vpc: dnsmasq is not started if use.external.dns is true    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4850`_ | ui: Consider overprovisioning when displaying allocated    |
|                         |          | progress                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4856`_ | UI: Fix the style action button                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4855`_ | UI: Fill out the search filter form field after performing |
|                         |          | a filter                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4841`_ | ui: fix add cluster form for vmware                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4845`_ | ui: Fix add primary store during Zone Deployment for       |
|                         |          | PreSetup protocol                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4815`_ | tests: Extend wait time after interrupt                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4767`_ | UI: Fix list view router-link goto account info instead of |
|                         |          | list account                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4820`_ | UI: Edit instance - offer existing Groups                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4831`_ | UI: Network offering selection - Show display text instead |
|                         |          | of the name                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4836`_ | Added info / tooltip for add role and import role dialogs  |
|                         |          | in the UI                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4839`_ | ui: Fix route to ISO From VM's Info Card / Detail View     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4821`_ | ui: Show vm name along with password                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4783`_ | novnc: Hide fullscreen button when not connected           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4779`_ | Fix NPE while cloudstack agent failed to connect to mgt    |
|                         |          | server                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4833`_ | novnc: Fix vm console is not working on firefox if         |
|                         |          | language is not English                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4824`_ | ui: Fixes for action messages and forms                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4823`_ | ui: Show label for view console action                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4822`_ | listprojects: Maintain order of project owners added to a  |
|                         |          | project                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4812`_ | ui: change createAccount to use post                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4832`_ | ui - Project Role Permission: Change default permission    |
|                         |          | type to 'Deny'                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4574`_ | db-schema update 4.15.0 to 4.15.1: correct some guest-os   |
|                         |          | namings                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4670`_ | ui: fix update vm details wrt backend changes              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4691`_ | server: delete template on storage over capacity threshold |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4755`_ | usage: return guest OS type UUID instead of internal DB ID |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4756`_ | Mask libvirtd sockets which prevents cloudstack-agent from |
|                         |          | being setup                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4772`_ | server: use network details from nic network               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4784`_ | ui: Show memory allocated percentage when migrating vm     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4785`_ | test: fix listVolumes call for detach volume migration     |
|                         |          | check                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4786`_ | ui: Show vm name in info card in deployvm                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4787`_ | ui: Show displayname in compute list view                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4788`_ | ui: Fix breadcrumb discrepancy                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4759`_ | UI: German translation corrections                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4761`_ | UI: Fix upload SSL certificate failed in the project view  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4746`_ | ui: FIX error in "Port forward" and "Load Balancing"       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4743`_ | api: remove account from listProjects API response         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4736`_ | novnc: Add source IP check                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4626`_ | server: fix failed to remove template/iso if upload from   |
|                         |          | local fails                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4531`_ | novnc: Accept new novnc client and disconnect old session  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4751`_ | build: deprecate and remove md5 from releases              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4747`_ | cks: fix token TTL, set it to never expire                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4740`_ | get_bridge_physdev returns "device:" instead of "device"   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4639`_ | cks: use HttpsURLConnection for checking api server        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4668`_ | Adjust tests to fix a problem with the container builders  |
|                         |          | (https://github.com/khos2ow/cloudstack-deb-builder)        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4693`_ | server: fix finding pools for volume migration             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4032`_ | Suspending the VM prior to deleting snapshots to avoid     |
|                         |          | corruption, th…                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4047`_ | Look for active templates for VR deployment                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4663`_ | ui: fix add Vmware cluster                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4716`_ | ui: Add guest IP ranges                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4728`_ | UI: add component was missing                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4725`_ | packaging: update Requirements in README                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4713`_ | API: Increase leniency to list templates on secondary      |
|                         |          | stores that have been marked deleted by updating the db    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4615`_ | Secondary storage: Allow store deletion after successful   |
|                         |          | data migration                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4582`_ | Upgrade: check systemvm template before db changes         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4718`_ | UI test: Fix UI test failures in 4.15                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4684`_ | cks: fix CNI release url returning 404                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4688`_ | format of checksum files convenient for automated checking |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4683`_ | ui: fix systevmtype for create service offering form       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4604`_ | api: add zone, vm name params in listVmSnapshot response   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4562`_ | Prevent KVM from performing volume migrations of running   |
|                         |          | instances                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4667`_ | Display account name only if its not null                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4656`_ | Ubuntu 20.04: set Backing Format of qcow2 images in vm     |
|                         |          | start and migration                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4396`_ | Show network name in exception message                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4451`_ | loop optimisation in bash                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4609`_ | API discovery: Prevent overwrite of API parameters in      |
|                         |          | cases where API names are same                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4445`_ | Cleanup domain details when domain is deleted              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4665`_ | ui: fix tags selection for add disk offering               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4651`_ | marvin: fix test failures when changing service offering   |
|                         |          | of a VM                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4627`_ | VR: fix expunging vm will remove dhcp entries of another   |
|                         |          | vm in VR                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4650`_ | test: hardware required for changeserviceoffering          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4653`_ | Update cloud-setup-databases.in - help message fix         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4655`_ | test: fix checksums for test template                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4601`_ | server: Get vm network/disk statistics and update database |
|                         |          | per host                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4623`_ | server: Fix update capacity for hosts take long time if    |
|                         |          | there are many service offerings                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4629`_ | server: prevent update vm read-only details                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4591`_ | server: select root disk based on user input during vm     |
|                         |          | import                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4576`_ | Fix: Use Q35 chipset for UEFI x86_64                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4624`_ | server: fix wrong error message when create isolated       |
|                         |          | network without SourceNat                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4622`_ | server: add possibility to scale vm to current custom      |
|                         |          | offerings on UI                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4602`_ | server: keep networks order and ips while move a vm with   |
|                         |          | multiple networks                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4625`_ | server: throw exception when update vm nic on L2 network   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4633`_ | doc: fix typo in install notes                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4605`_ | packaging: build and bundle UI using npm in deb and rpm    |
|                         |          | packages                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4620`_ | Fix screenshot path on README of /ui directory             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4600`_ | server: fix cannot create vm if another vm with same name  |
|                         |          | has been added and removed on the network                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4491`_ | fix on changeServiceForVirtualMachine when updating        |
|                         |          | read/write rate                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4621`_ | Fixed typo                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4614`_ | vmsnapshot: Add quickview to the list of VM Snapshot       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.1.0                | `#4611`_ | UI Storage Pool Tags: unable to delete last tag            |
+-------------------------+----------+------------------------------------------------------------+

255 Issues listed

.. _`#5164`: https://github.com/apache/cloudstack/pull/5164
.. _`#4843`: https://github.com/apache/cloudstack/pull/4843
.. _`#5148`: https://github.com/apache/cloudstack/pull/5148
.. _`#5160`: https://github.com/apache/cloudstack/pull/5160
.. _`#5130`: https://github.com/apache/cloudstack/pull/5130
.. _`#5153`: https://github.com/apache/cloudstack/pull/5153
.. _`#5115`: https://github.com/apache/cloudstack/pull/5115
.. _`#5123`: https://github.com/apache/cloudstack/pull/5123
.. _`#5132`: https://github.com/apache/cloudstack/pull/5132
.. _`#5137`: https://github.com/apache/cloudstack/pull/5137
.. _`#5143`: https://github.com/apache/cloudstack/pull/5143
.. _`#5150`: https://github.com/apache/cloudstack/pull/5150
.. _`#5129`: https://github.com/apache/cloudstack/pull/5129
.. _`#5105`: https://github.com/apache/cloudstack/pull/5105
.. _`#5118`: https://github.com/apache/cloudstack/pull/5118
.. _`#5113`: https://github.com/apache/cloudstack/pull/5113
.. _`#5078`: https://github.com/apache/cloudstack/pull/5078
.. _`#5108`: https://github.com/apache/cloudstack/pull/5108
.. _`#5109`: https://github.com/apache/cloudstack/pull/5109
.. _`#5095`: https://github.com/apache/cloudstack/pull/5095
.. _`#5098`: https://github.com/apache/cloudstack/pull/5098
.. _`#5097`: https://github.com/apache/cloudstack/pull/5097
.. _`#5076`: https://github.com/apache/cloudstack/pull/5076
.. _`#5039`: https://github.com/apache/cloudstack/pull/5039
.. _`#5089`: https://github.com/apache/cloudstack/pull/5089
.. _`#5072`: https://github.com/apache/cloudstack/pull/5072
.. _`#5085`: https://github.com/apache/cloudstack/pull/5085
.. _`#5084`: https://github.com/apache/cloudstack/pull/5084
.. _`#5081`: https://github.com/apache/cloudstack/pull/5081
.. _`#5074`: https://github.com/apache/cloudstack/pull/5074
.. _`#5063`: https://github.com/apache/cloudstack/pull/5063
.. _`#5059`: https://github.com/apache/cloudstack/pull/5059
.. _`#5053`: https://github.com/apache/cloudstack/pull/5053
.. _`#5057`: https://github.com/apache/cloudstack/pull/5057
.. _`#5061`: https://github.com/apache/cloudstack/pull/5061
.. _`#5017`: https://github.com/apache/cloudstack/pull/5017
.. _`#5049`: https://github.com/apache/cloudstack/pull/5049
.. _`#5032`: https://github.com/apache/cloudstack/pull/5032
.. _`#5045`: https://github.com/apache/cloudstack/pull/5045
.. _`#5048`: https://github.com/apache/cloudstack/pull/5048
.. _`#5050`: https://github.com/apache/cloudstack/pull/5050
.. _`#5029`: https://github.com/apache/cloudstack/pull/5029
.. _`#5003`: https://github.com/apache/cloudstack/pull/5003
.. _`#5033`: https://github.com/apache/cloudstack/pull/5033
.. _`#5006`: https://github.com/apache/cloudstack/pull/5006
.. _`#5010`: https://github.com/apache/cloudstack/pull/5010
.. _`#5025`: https://github.com/apache/cloudstack/pull/5025
.. _`#5023`: https://github.com/apache/cloudstack/pull/5023
.. _`#4644`: https://github.com/apache/cloudstack/pull/4644
.. _`#4795`: https://github.com/apache/cloudstack/pull/4795
.. _`#4647`: https://github.com/apache/cloudstack/pull/4647
.. _`#5020`: https://github.com/apache/cloudstack/pull/5020
.. _`#5022`: https://github.com/apache/cloudstack/pull/5022
.. _`#5013`: https://github.com/apache/cloudstack/pull/5013
.. _`#5015`: https://github.com/apache/cloudstack/pull/5015
.. _`#5014`: https://github.com/apache/cloudstack/pull/5014
.. _`#5011`: https://github.com/apache/cloudstack/pull/5011
.. _`#4871`: https://github.com/apache/cloudstack/pull/4871
.. _`#4842`: https://github.com/apache/cloudstack/pull/4842
.. _`#5001`: https://github.com/apache/cloudstack/pull/5001
.. _`#4986`: https://github.com/apache/cloudstack/pull/4986
.. _`#4999`: https://github.com/apache/cloudstack/pull/4999
.. _`#4996`: https://github.com/apache/cloudstack/pull/4996
.. _`#4953`: https://github.com/apache/cloudstack/pull/4953
.. _`#4995`: https://github.com/apache/cloudstack/pull/4995
.. _`#4981`: https://github.com/apache/cloudstack/pull/4981
.. _`#4987`: https://github.com/apache/cloudstack/pull/4987
.. _`#4988`: https://github.com/apache/cloudstack/pull/4988
.. _`#4989`: https://github.com/apache/cloudstack/pull/4989
.. _`#4991`: https://github.com/apache/cloudstack/pull/4991
.. _`#4993`: https://github.com/apache/cloudstack/pull/4993
.. _`#4979`: https://github.com/apache/cloudstack/pull/4979
.. _`#4980`: https://github.com/apache/cloudstack/pull/4980
.. _`#4970`: https://github.com/apache/cloudstack/pull/4970
.. _`#4915`: https://github.com/apache/cloudstack/pull/4915
.. _`#4967`: https://github.com/apache/cloudstack/pull/4967
.. _`#4964`: https://github.com/apache/cloudstack/pull/4964
.. _`#4901`: https://github.com/apache/cloudstack/pull/4901
.. _`#4957`: https://github.com/apache/cloudstack/pull/4957
.. _`#4924`: https://github.com/apache/cloudstack/pull/4924
.. _`#4971`: https://github.com/apache/cloudstack/pull/4971
.. _`#4907`: https://github.com/apache/cloudstack/pull/4907
.. _`#4962`: https://github.com/apache/cloudstack/pull/4962
.. _`#4946`: https://github.com/apache/cloudstack/pull/4946
.. _`#4948`: https://github.com/apache/cloudstack/pull/4948
.. _`#4929`: https://github.com/apache/cloudstack/pull/4929
.. _`#4951`: https://github.com/apache/cloudstack/pull/4951
.. _`#4952`: https://github.com/apache/cloudstack/pull/4952
.. _`#4859`: https://github.com/apache/cloudstack/pull/4859
.. _`#4949`: https://github.com/apache/cloudstack/pull/4949
.. _`#4950`: https://github.com/apache/cloudstack/pull/4950
.. _`#4944`: https://github.com/apache/cloudstack/pull/4944
.. _`#4758`: https://github.com/apache/cloudstack/pull/4758
.. _`#4934`: https://github.com/apache/cloudstack/pull/4934
.. _`#4909`: https://github.com/apache/cloudstack/pull/4909
.. _`#4938`: https://github.com/apache/cloudstack/pull/4938
.. _`#4926`: https://github.com/apache/cloudstack/pull/4926
.. _`#4918`: https://github.com/apache/cloudstack/pull/4918
.. _`#4933`: https://github.com/apache/cloudstack/pull/4933
.. _`#4927`: https://github.com/apache/cloudstack/pull/4927
.. _`#4923`: https://github.com/apache/cloudstack/pull/4923
.. _`#4912`: https://github.com/apache/cloudstack/pull/4912
.. _`#4300`: https://github.com/apache/cloudstack/pull/4300
.. _`#4920`: https://github.com/apache/cloudstack/pull/4920
.. _`#4913`: https://github.com/apache/cloudstack/pull/4913
.. _`#4493`: https://github.com/apache/cloudstack/pull/4493
.. _`#4917`: https://github.com/apache/cloudstack/pull/4917
.. _`#4916`: https://github.com/apache/cloudstack/pull/4916
.. _`#4910`: https://github.com/apache/cloudstack/pull/4910
.. _`#4738`: https://github.com/apache/cloudstack/pull/4738
.. _`#4898`: https://github.com/apache/cloudstack/pull/4898
.. _`#4638`: https://github.com/apache/cloudstack/pull/4638
.. _`#4899`: https://github.com/apache/cloudstack/pull/4899
.. _`#4895`: https://github.com/apache/cloudstack/pull/4895
.. _`#4847`: https://github.com/apache/cloudstack/pull/4847
.. _`#4717`: https://github.com/apache/cloudstack/pull/4717
.. _`#4801`: https://github.com/apache/cloudstack/pull/4801
.. _`#4672`: https://github.com/apache/cloudstack/pull/4672
.. _`#4884`: https://github.com/apache/cloudstack/pull/4884
.. _`#4896`: https://github.com/apache/cloudstack/pull/4896
.. _`#4679`: https://github.com/apache/cloudstack/pull/4679
.. _`#4099`: https://github.com/apache/cloudstack/pull/4099
.. _`#4892`: https://github.com/apache/cloudstack/pull/4892
.. _`#4851`: https://github.com/apache/cloudstack/pull/4851
.. _`#4802`: https://github.com/apache/cloudstack/pull/4802
.. _`#4773`: https://github.com/apache/cloudstack/pull/4773
.. _`#4794`: https://github.com/apache/cloudstack/pull/4794
.. _`#4666`: https://github.com/apache/cloudstack/pull/4666
.. _`#4769`: https://github.com/apache/cloudstack/pull/4769
.. _`#4775`: https://github.com/apache/cloudstack/pull/4775
.. _`#4894`: https://github.com/apache/cloudstack/pull/4894
.. _`#4816`: https://github.com/apache/cloudstack/pull/4816
.. _`#4811`: https://github.com/apache/cloudstack/pull/4811
.. _`#4676`: https://github.com/apache/cloudstack/pull/4676
.. _`#4873`: https://github.com/apache/cloudstack/pull/4873
.. _`#4888`: https://github.com/apache/cloudstack/pull/4888
.. _`#4893`: https://github.com/apache/cloudstack/pull/4893
.. _`#4870`: https://github.com/apache/cloudstack/pull/4870
.. _`#4882`: https://github.com/apache/cloudstack/pull/4882
.. _`#4869`: https://github.com/apache/cloudstack/pull/4869
.. _`#4745`: https://github.com/apache/cloudstack/pull/4745
.. _`#4872`: https://github.com/apache/cloudstack/pull/4872
.. _`#3944`: https://github.com/apache/cloudstack/pull/3944
.. _`#4675`: https://github.com/apache/cloudstack/pull/4675
.. _`#4789`: https://github.com/apache/cloudstack/pull/4789
.. _`#4804`: https://github.com/apache/cloudstack/pull/4804
.. _`#4862`: https://github.com/apache/cloudstack/pull/4862
.. _`#4867`: https://github.com/apache/cloudstack/pull/4867
.. _`#4764`: https://github.com/apache/cloudstack/pull/4764
.. _`#4571`: https://github.com/apache/cloudstack/pull/4571
.. _`#4864`: https://github.com/apache/cloudstack/pull/4864
.. _`#4840`: https://github.com/apache/cloudstack/pull/4840
.. _`#4805`: https://github.com/apache/cloudstack/pull/4805
.. _`#4765`: https://github.com/apache/cloudstack/pull/4765
.. _`#4763`: https://github.com/apache/cloudstack/pull/4763
.. _`#4762`: https://github.com/apache/cloudstack/pull/4762
.. _`#4829`: https://github.com/apache/cloudstack/pull/4829
.. _`#4866`: https://github.com/apache/cloudstack/pull/4866
.. _`#4800`: https://github.com/apache/cloudstack/pull/4800
.. _`#4793`: https://github.com/apache/cloudstack/pull/4793
.. _`#4744`: https://github.com/apache/cloudstack/pull/4744
.. _`#4861`: https://github.com/apache/cloudstack/pull/4861
.. _`#4748`: https://github.com/apache/cloudstack/pull/4748
.. _`#4846`: https://github.com/apache/cloudstack/pull/4846
.. _`#4857`: https://github.com/apache/cloudstack/pull/4857
.. _`#4777`: https://github.com/apache/cloudstack/pull/4777
.. _`#4806`: https://github.com/apache/cloudstack/pull/4806
.. _`#4850`: https://github.com/apache/cloudstack/pull/4850
.. _`#4856`: https://github.com/apache/cloudstack/pull/4856
.. _`#4855`: https://github.com/apache/cloudstack/pull/4855
.. _`#4841`: https://github.com/apache/cloudstack/pull/4841
.. _`#4845`: https://github.com/apache/cloudstack/pull/4845
.. _`#4815`: https://github.com/apache/cloudstack/pull/4815
.. _`#4767`: https://github.com/apache/cloudstack/pull/4767
.. _`#4820`: https://github.com/apache/cloudstack/pull/4820
.. _`#4831`: https://github.com/apache/cloudstack/pull/4831
.. _`#4836`: https://github.com/apache/cloudstack/pull/4836
.. _`#4839`: https://github.com/apache/cloudstack/pull/4839
.. _`#4821`: https://github.com/apache/cloudstack/pull/4821
.. _`#4783`: https://github.com/apache/cloudstack/pull/4783
.. _`#4779`: https://github.com/apache/cloudstack/pull/4779
.. _`#4833`: https://github.com/apache/cloudstack/pull/4833
.. _`#4824`: https://github.com/apache/cloudstack/pull/4824
.. _`#4823`: https://github.com/apache/cloudstack/pull/4823
.. _`#4822`: https://github.com/apache/cloudstack/pull/4822
.. _`#4812`: https://github.com/apache/cloudstack/pull/4812
.. _`#4832`: https://github.com/apache/cloudstack/pull/4832
.. _`#4574`: https://github.com/apache/cloudstack/pull/4574
.. _`#4670`: https://github.com/apache/cloudstack/pull/4670
.. _`#4691`: https://github.com/apache/cloudstack/pull/4691
.. _`#4755`: https://github.com/apache/cloudstack/pull/4755
.. _`#4756`: https://github.com/apache/cloudstack/pull/4756
.. _`#4772`: https://github.com/apache/cloudstack/pull/4772
.. _`#4784`: https://github.com/apache/cloudstack/pull/4784
.. _`#4785`: https://github.com/apache/cloudstack/pull/4785
.. _`#4786`: https://github.com/apache/cloudstack/pull/4786
.. _`#4787`: https://github.com/apache/cloudstack/pull/4787
.. _`#4788`: https://github.com/apache/cloudstack/pull/4788
.. _`#4759`: https://github.com/apache/cloudstack/pull/4759
.. _`#4761`: https://github.com/apache/cloudstack/pull/4761
.. _`#4746`: https://github.com/apache/cloudstack/pull/4746
.. _`#4743`: https://github.com/apache/cloudstack/pull/4743
.. _`#4736`: https://github.com/apache/cloudstack/pull/4736
.. _`#4626`: https://github.com/apache/cloudstack/pull/4626
.. _`#4531`: https://github.com/apache/cloudstack/pull/4531
.. _`#4751`: https://github.com/apache/cloudstack/pull/4751
.. _`#4747`: https://github.com/apache/cloudstack/pull/4747
.. _`#4740`: https://github.com/apache/cloudstack/pull/4740
.. _`#4639`: https://github.com/apache/cloudstack/pull/4639
.. _`#4668`: https://github.com/apache/cloudstack/pull/4668
.. _`#4693`: https://github.com/apache/cloudstack/pull/4693
.. _`#4032`: https://github.com/apache/cloudstack/pull/4032
.. _`#4047`: https://github.com/apache/cloudstack/pull/4047
.. _`#4663`: https://github.com/apache/cloudstack/pull/4663
.. _`#4716`: https://github.com/apache/cloudstack/pull/4716
.. _`#4728`: https://github.com/apache/cloudstack/pull/4728
.. _`#4725`: https://github.com/apache/cloudstack/pull/4725
.. _`#4713`: https://github.com/apache/cloudstack/pull/4713
.. _`#4615`: https://github.com/apache/cloudstack/pull/4615
.. _`#4582`: https://github.com/apache/cloudstack/pull/4582
.. _`#4718`: https://github.com/apache/cloudstack/pull/4718
.. _`#4684`: https://github.com/apache/cloudstack/pull/4684
.. _`#4688`: https://github.com/apache/cloudstack/pull/4688
.. _`#4683`: https://github.com/apache/cloudstack/pull/4683
.. _`#4604`: https://github.com/apache/cloudstack/pull/4604
.. _`#4562`: https://github.com/apache/cloudstack/pull/4562
.. _`#4667`: https://github.com/apache/cloudstack/pull/4667
.. _`#4656`: https://github.com/apache/cloudstack/pull/4656
.. _`#4396`: https://github.com/apache/cloudstack/pull/4396
.. _`#4451`: https://github.com/apache/cloudstack/pull/4451
.. _`#4609`: https://github.com/apache/cloudstack/pull/4609
.. _`#4445`: https://github.com/apache/cloudstack/pull/4445
.. _`#4665`: https://github.com/apache/cloudstack/pull/4665
.. _`#4651`: https://github.com/apache/cloudstack/pull/4651
.. _`#4627`: https://github.com/apache/cloudstack/pull/4627
.. _`#4650`: https://github.com/apache/cloudstack/pull/4650
.. _`#4653`: https://github.com/apache/cloudstack/pull/4653
.. _`#4655`: https://github.com/apache/cloudstack/pull/4655
.. _`#4601`: https://github.com/apache/cloudstack/pull/4601
.. _`#4623`: https://github.com/apache/cloudstack/pull/4623
.. _`#4629`: https://github.com/apache/cloudstack/pull/4629
.. _`#4591`: https://github.com/apache/cloudstack/pull/4591
.. _`#4576`: https://github.com/apache/cloudstack/pull/4576
.. _`#4624`: https://github.com/apache/cloudstack/pull/4624
.. _`#4622`: https://github.com/apache/cloudstack/pull/4622
.. _`#4602`: https://github.com/apache/cloudstack/pull/4602
.. _`#4625`: https://github.com/apache/cloudstack/pull/4625
.. _`#4633`: https://github.com/apache/cloudstack/pull/4633
.. _`#4605`: https://github.com/apache/cloudstack/pull/4605
.. _`#4620`: https://github.com/apache/cloudstack/pull/4620
.. _`#4600`: https://github.com/apache/cloudstack/pull/4600
.. _`#4491`: https://github.com/apache/cloudstack/pull/4491
.. _`#4621`: https://github.com/apache/cloudstack/pull/4621
.. _`#4614`: https://github.com/apache/cloudstack/pull/4614
.. _`#4611`: https://github.com/apache/cloudstack/pull/4611

Changes in 4.15.0.0 since 4.14
==============================

Apache CloudStack uses GitHub <https://github.com/apache/cloudstack/issues>`_ 
to track its issues.


.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+------------------------------------------------------------+
| Version                 | Github   | Description                                                |
+=========================+==========+============================================================+
| 4.15.0.0                | `#4568`_ | kvm: Fix double-escape issue while creating rbd disk       |
|                         |          | options                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4559`_ | networkorchestrator: Fix typo in exception message         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4553`_ | Fix for mapping guest OS type read from OVF to existing    |
|                         |          | guest OS in C…                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4555`_ | VMware: Fix template upload from local                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4540`_ | Bug/unmanaged ingest exceptions #4539                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4529`_ | vr: Ensuring dnsmasq.leases file is populated              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4522`_ | template: Ensuring template is cross zone if type changed  |
|                         |          | to system                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4516`_ | Fix hypervisor type cast to string                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4533`_ | db upgrade: use "create or replace view" instead of "alter |
|                         |          | view"                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4536`_ | CLOUDSTACK-10423:Potential sensitive information           |
|                         |          | disclosure                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4538`_ | CLOUDSTACK-10425:Potential sensitive information           |
|                         |          | disclosure                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4511`_ | listphysicalnetworks: Honouring keyword parameter          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4530`_ | extract volume: Fix NPE when Volume exists on secondary    |
|                         |          | store but doesn't have a download URL                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4532`_ | apidoc issue                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4526`_ | db: Fix description of volume.stats.interval which is in   |
|                         |          | milliseconds…                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4527`_ | kvm: set cpu topology only if cpucore per socket is set    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4525`_ | xenserver: check and eject patch vbd for systemvms         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4523`_ | Fix warning when setup cloudstack-common                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4497`_ | kvm: FIX cpucorespersocket is not working on KVM           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4521`_ | change debug to warn for unknown exceptions                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4507`_ | Fix failure in validating IP address in case of multiple   |
|                         |          | Management Servers                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4515`_ | Update log output for FirstFitPlanner                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4518`_ | ui: deprecate old UI and move to legacy to be served at    |
|                         |          | /client/legacy                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4510`_ | Adding zone name to physicalnetworkresponse                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4501`_ | Disallowing udp for lb rules for haproxy                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4505`_ | Make global setting "secstorage.max.migrate.sessions"      |
|                         |          | non-dynamic                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4499`_ | Adding cpuallocated percentage and value to host and       |
|                         |          | hostsformigrationresponse                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4496`_ | kvm: fix router.aggregation.command.each.timeout is reset  |
|                         |          | to 600 when update other kvm configs                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4495`_ | fix failures with test_multiple_nic_support.py             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4500`_ | Fix hosts for migration count                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4494`_ | sql: Fix Zones are returned in a random order (#3934)      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4489`_ | vr: fix python exception when configure VRs                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4361`_ | Add vpcid in usage network response                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4486`_ | Add event for VM recovery operation                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4483`_ | Display VPC name to which the network belongs to           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4425`_ | Setting snapshot removed on timeout                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4392`_ | Fixed double slash in secret breaking db insert            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4467`_ | vpc: fix ips on wrong interfaces after rebooting vpc vrs   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4480`_ | Fix migrateVMwithVolumes API in case of multiple volumes   |
|                         |          | on VMware                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4478`_ | Adding memoryallocatedpercentage & memoryallocatedbytes to |
|                         |          | HostsResponse & HostsForMigrationResponse                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4466`_ | VR: fix logging is not working and logs are not appended   |
|                         |          | to /var/log/cloud.log                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4458`_ | Fix k8s cluster upgrade in shared networks                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4487`_ | accountresponse: Fix domainpath description                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4459`_ | createkubertetesbinariesiso: Saving images in network and  |
|                         |          | dashboard yaml                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4485`_ | Fixing misleading HostMetricsResponse param description    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4461`_ | Fix destroying k8s cluster on shared networks              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4476`_ | Removed sensitive info from UI when volume attach/detach   |
|                         |          | fails                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4078`_ | Cleanup download urls when SSVM destroyed                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4428`_ | Moved dedicated hosts to the end of the resultset when     |
|                         |          | selecting an e…                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4475`_ | Fix: Data migration                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4452`_ | Consider other conditions while listing templates with id  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4446`_ | Check all mgt server connectivity                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4469`_ | Fix: Listing projects comprising of only the user's on     |
|                         |          | listAll=true                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4464`_ | Fix IndexOutOfBoundsException when creating basic network  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4289`_ | default teardown methods with reversed() handling          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4465`_ | fix login issue post upgrade                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4456`_ | Returning nic details in KubernetesClusterResponse         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4418`_ | Create Event in case of OOBM failure                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4327`_ | Re-enable IP address usage hiding                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4437`_ | [Bug fix] VMware: Fix for SSVM recreation on deployasis    |
|                         |          | systemVM templates                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4442`_ | Preventing port 53 being added as lb rule when dns service |
|                         |          | is availab…                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4439`_ | Added compress option to dnsmasq log files                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4430`_ | FIX issue in VR if remote access vpn is enabled            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4440`_ | fix pbm url download                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4408`_ | Hiding system reserved IP addresses                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4341`_ | Allow to configure root disk size via Service Offering     |
|                         |          | (diskoffering of type Service).                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4388`_ | fix NPE in volumes statistics                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4435`_ | server: fix format error with memorywithoverprovisioning   |
|                         |          | in list hosts response                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4177`_ | Prevent deploying IPv6 network if Zone has no IPv6 DNS     |
|                         |          | configured                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4429`_ | FIX s2svpn connection stuck on Pending state               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4359`_ | Failed to update host password if username/password is not |
|                         |          | saved in db                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4426`_ | DB: fix wrong category id of guest os 'Other PV            |
|                         |          | Virtio-SCSI (64-bit)'                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4432`_ | Unable to create snapshot from vm snapshot                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4144`_ | Fix Usage failed to get pid                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3945`_ | server: update template to another template type           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4363`_ | Ability to put a server in Down state to maintenance       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4417`_ | Modify alter view to drop/create view                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4414`_ | Adding public ip to listKubernetesClusterResponse          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4367`_ | Remove cpu core from op_host_capacity when host is deleted |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4427`_ | packaging/deb: Include cloudstack-guest-tool into          |
|                         |          | cloudstack-agent DEB package                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4420`_ | Including instance details in KubernetesClusterResponse    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4415`_ | CKS : More log changes from uuid to name                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4307`_ | [VMware] vSphere advanced capabilities and Full OVF        |
|                         |          | properties support                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4375`_ | Fixing count for findHostsForMigration                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#2206`_ | [CLOUDSTACK-10020] Changes to make marvin work with        |
|                         |          | projects and VPCs                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4409`_ | Enhance UpdateDiskOfferingCmd                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4413`_ | systemvm: fix proc.find in CsProcess.py                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4360`_ | server: Update use_bytes of storage pools                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4193`_ | Fix usage record count                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4411`_ | Display Kubernetes cluster name instead of uuid            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4412`_ | Validating type parameter and including all types          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#67`_   | CLOUDSTACK-8157: Add absolute schema references to support |
|                         |          | MySQL 5.6 better                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3946`_ | server: add global configuration for default router        |
|                         |          | service offering                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4387`_ | Fix JsonSyntaxException when creating API command response |
|                         |          | #4355                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4407`_ | packaging: enable Parallel Collector GC for management     |
|                         |          | server                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4395`_ | support for data migration of incremental snaps on xen     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4194`_ | enable update tags on disk offerings                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4251`_ | Handle with VM snapshot events                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4405`_ | Re-add affinity group                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4377`_ | server: fix issue that vm guest os type is reset after     |
|                         |          | updatetemplate                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4381`_ | kvm: fix wrong VM CPU usage                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4228`_ | Dont add host back after agent service restart             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4348`_ | vmware: use hotPlugMemoryIncrementSize only for valid      |
|                         |          | value                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4404`_ | scalekubernetesclustercmd: Making id a required field [NPE |
|                         |          | Fix]                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4383`_ | Host is counted twice if it has multiple host tags in      |
|                         |          | Prometheus exporter                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4382`_ | debian/control: add uuid-runtime to cloudstack-common,     |
|                         |          | ufw/apparmor to cloudstack-agent                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4379`_ | Add global configuration for max cpu/ram in service        |
|                         |          | offerings                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4373`_ | Handles creation /var/run/cloud folder for creation of     |
|                         |          | lock file while modifyvxlan.sh script is run               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4366`_ | Consider maintenance mode as offline for prometheus stats  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4365`_ | Export dedicated host stats to prometheus                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4397`_ | List VMs by Security Group & HA                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4376`_ | server: Fix some cpuspeed issues while create service      |
|                         |          | offering                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4374`_ | Fixing searchAndCount searchAndDistinctCount when sc is    |
|                         |          | null                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4389`_ | Fixed vm-templates not being removed from primary storage  |
|                         |          | with storag…                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4271`_ | hypervisor: Add Citrix Hypervisor 8x product name support  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4321`_ | VMware: match hardware version for worker VM when taking a |
|                         |          | snapshot                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4354`_ | createaccountcmd: Improving account param description      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4352`_ | Retry redfish requests                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4269`_ | cks: assorted fixes, test refactoring                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4338`_ | server: check guest os preference of last host when start  |
|                         |          | a vm                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4345`_ | Binding listening socket to all address for remote debug   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4340`_ | Changing test_pvlan vlan id to prevent conflict with smoke |
|                         |          | tests env config                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4190`_ | Broadcast URI not set to vxlan, but vlan (Fix #3040)       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4328`_ | vmware: search unmanaged instances using hypervisor name   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4336`_ | vmware: while plugging in nics get existing sorted nic     |
|                         |          | devices                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4305`_ | Changing dependency from python3-distutils to              |
|                         |          | python3-distutils-extra                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4335`_ | agent: Compare indirect agent lb algorithm when cloudstack |
|                         |          | agent conn…                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4319`_ | Fix "data-server" dns entry in /etc/hosts after a new      |
|                         |          | deployment                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4303`_ | Ubuntu 20.04: Fix systemvm cannot start up                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4239`_ | Disabling managing firewall - cloudstack-setup-management  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4323`_ | systemvm: Update novnc                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4319`_ | Fix "data-server" dns entry in /etc/hosts after a new      |
|                         |          | deployment                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4331`_ | change upgrade path to 4.14 (from 4.13) and intensify      |
|                         |          | check                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4333`_ | Minor message update                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4294`_ | Create template from detached data-disks on VMWare         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4316`_ | Handle listProjects API to list projects with user as      |
|                         |          | members when listAll=true                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4309`_ | cks: fix logging exception on create cluster               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4326`_ | ui: call logout before login to clear old sessionkey       |
|                         |          | cookies                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4315`_ | Adding acl name to listNetworkAcl, listNetwork,            |
|                         |          | listPrivateGateway, listVpcs responses                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4053`_ | Secondary Storage Usage Improvements                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4312`_ | Increase wait time before running the ssvm health check    |
|                         |          | script on SSVM reboot                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4320`_ | Change Global setting type for allow.user.create.projects  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4317`_ | Display acl name in listNetworks response                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4297`_ | Incorrect md5sums for systemVM templates results in        |
|                         |          | failure to download templates to other image stores        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4306`_ | Ubuntu 20.04: Fix issue while build package on ubuntu      |
|                         |          | 20.04                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4301`_ | Ubuntu 20.04: restart libvirtd instead of libvirt-bin      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4291`_ | Manage influxDB Batches avoiding OutOfMemory Exception     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4284`_ | Fixed delayed power state update after vm shutdown         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4279`_ | Avoid Null pointer at DomainChecker and enhance            |
|                         |          | AssignVMCmd                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4020`_ | server: move UpdateDefaultNic to vm work job queue         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4258`_ | List networks using networkofferingid                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3996`_ | UI: Hide cpuspeed for custom constrained offering          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3902`_ | vrouter: Save PlaceHolder nic for VR if network does not   |
|                         |          | have source nat                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4288`_ | client: explicitly define SslContextFactory::Server for    |
|                         |          | https                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4287`_ | Update Java Rados from v0.5.0 to v0.6.0                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4266`_ | Adding os type id to the usage record response for virtual |
|                         |          | machines                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4264`_ | Changed test failure to warning                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4272`_ | Fixed rolling restart on VPC network                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4274`_ | engine: honour bypass VLAN id/range for L2 networks        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4278`_ | Usage-server update message improvement                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4219`_ | iscsi session cleanup now configurable, filters iscsi      |
|                         |          | partitions                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4040`_ | [KVM] Enable PVLAN support on L2 networks                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4275`_ | Display hypervisor type for VM snapshot                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4180`_ | Added nfs minor version support                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4068`_ | Adding Centos8, Ubuntu 20.04, XCPNG8.1 Support             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4268`_ | Prevent NullPointerException on GenericDaoBase             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4262`_ | fix test failure                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4207`_ | Human readable sizes in logs                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4254`_ | Name public network appropriately to avoid conflicts       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4128`_ | Role based users in Projects                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4213`_ | Search vm snapshots using tags                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4255`_ | Prevent null pointer on listPublicIpAddress cmd            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4256`_ | Fix comparison using nullable objects                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4260`_ | cks: fix for null hypervisor type                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4016`_ | Fixed private gateway can't be deleted                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4253`_ | Fix sed command failure in Mac OS.                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4249`_ | Host SSVM Debian ISO on download.cloudstack.org            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4243`_ | Update SystemVM debian iso from 10.4.0 to 10.5.0           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4019`_ | server: Move restoreVM to vm work job queue                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4165`_ | Allow renaming cluster, host, and storage                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4220`_ | Fix cpuallocated value in findHostsForMIgration api        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4225`_ | vmware: volume utilisation is always zero                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4000`_ | vm: Reset deviceId to fix missing nic with vm              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4231`_ | kvm/ceph: Only if a port number has been specified define  |
|                         |          | in the XML                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4116`_ | cks: fix template, deployment issues                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3952`_ | vrouter: remove a POSTROUTING rule for port forwarding in  |
|                         |          | VPC router                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4175`_ | Redfish Client & Redfish OOBM Driver                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4035`_ | Document how to pass CIDRs lists API calls                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4214`_ | Bug fixes for primate                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4226`_ | Removed check on SSLEngine client mode                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4188`_ | Fix snapshots garbage collection                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4138`_ | Fixed incorrect error message on invalid template type     |
|                         |          | download                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4156`_ | Fixed removal of hosts from certsmap when running          |
|                         |          | certificate auto-renew                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4172`_ | [VMware] Support to attach more than 15 data disks in      |
|                         |          | VMware VM                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4196`_ | VMware: Guest OS Mappings fix                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4176`_ | server: Purge all cookies on logout, set /client path on   |
|                         |          | login                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4202`_ | server: don't export B&R APIs if feature is not enabled    |
|                         |          | globally                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3979`_ | Limit API from trying to start a VM that is already        |
|                         |          | running                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4174`_ | Set prometheus.exporter.enable as not dynamic              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4117`_ | [VMware] Explicitly controlling VM hardware version        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4071`_ | Dynamic roles improvements                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4186`_ | Adding pagination for quotaSummary and quotaTariffList     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4001`_ | server: Dedicated hosts should be 'Not Suitable' while     |
|                         |          | find host for m migration                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3976`_ | Enable sending hypervior host name via metadata - VR and   |
|                         |          | Config Drive                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4103`_ | [VMware] Enable unmanaging guest VMs                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4148`_ | server: Do not resize volume of running vm on KVM host if  |
|                         |          | host is not Up or not Enabled                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4171`_ | vr: fix backup router health check                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4167`_ | Adding missing fields to API responses                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4164`_ | Adding listall to listLdapConfigurations                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4154`_ | server: fix for wrong affinity group count                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4004`_ | Fixed null pointer and deployment issue on Xenserver with  |
|                         |          | L2 Guest network with configDrive                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4162`_ | Exception Message rephrasing                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4132`_ | Fix delete network with no services                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4145`_ | Fixing listVirtualMachinesMetrics to extend ListVMsCmd     |
|                         |          | instead of ListVMsCmdByAdmin                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3998`_ | NPE when VM is planned to migrate to other host during     |
|                         |          | dynamic scaling                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4085`_ | Fix duplicate user entries for vpn usage                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4140`_ | Adding showunique parameter to list templates and isos     |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4007`_ | Restarting all networks that needs a restart in a VPC      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4003`_ | Logging framework to use only log4j                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4121`_ | server: fix TransactionLegacy DB connection leaks due to   |
|                         |          | DB switching by B&R thread                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3991`_ | Multiple dynamic VM Scaling APIs can create duplicate      |
|                         |          | usage events for the same time                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4070`_ | Update cloud-set-guest-password.in                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4130`_ | Fixed null pointer after deleting snapshot, GC and cross   |
|                         |          | cluster vm migration on XCP-NG                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4122`_ | Maximum data volumes limit is picked from "default"        |
|                         |          | version of hypervisor, instead of actual hypervisor        |
|                         |          | version                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3982`_ | Updated 3 error messages to replace the word 'matches'     |
|                         |          | with 'match'                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4073`_ | Display network name for IP in shared networks             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4075`_ | Search VR using redundant state                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3949`_ | Fix: catch CloudRuntimeException in                        |
|                         |          | LibvirtGetVolumeStatsCommandWrapper.java                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3955`_ | docker: upgrade to ubuntu 18.04 and fix some issues        |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3980`_ | Fix String.format unused/misused arguments                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4048`_ | Update DpdkDriverImpl.java to support DPDK trunk           |
|                         |          | interfaces                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4083`_ | Allow set IPv6 when deploying advanced network  Zone with  |
|                         |          | SG via UI                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4142`_ | Invalid character encountered in file ui/l10n/pt_BR.js at  |
|                         |          | line 1134 for encoding UTF-8.                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4109`_ | add support for XCP-ng 7/8 to create it's heartbeat LVM    |
|                         |          | properly                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4077`_ | Disable searching by instance name for customers           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4021`_ | Boot into hardware setup menu on Vmware                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3965`_ | server: Honor vm.destroy.forcestop when expunge a vm       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4104`_ | Debian10 support                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4017`_ | [UI] Update ISO permissions                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4079`_ | Fixed HA migrated storage error                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4046`_ | Display image store disk size used and total disk size     |
|                         |          | stats                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4013`_ | Allow IMG extension for QCOW2 format                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4062`_ | [VMware] Cannot migrate VM on PVLAN shared network         |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4119`_ | kvm: bump jna version to latest                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4126`_ | Enhance KVM running VM snapshot exception log              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4123`_ | Improved kvmvmactivitycheck.sh output                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4065`_ | Enable revocation checking for uploaded certificates       |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4124`_ | Missing python3 libvirt bindings                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3794`_ | create Volume Access Groups per cluster instead of         |
|                         |          | CloudStack-RandomUUID()                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4100`_ | RabbitMQ log enhancement                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3921`_ | Updated vmware virtual hardware version in                 |
|                         |          | systemvmtemplate build script                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4110`_ | cleanup of redundant check for sameOwner                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4092`_ | engine/schema: add empty DB upgrade path from 4.14.0.0 to  |
|                         |          | 4.15.0.0                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4097`_ | Adding novnc license exclusion                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#3967`_ | noVNC console integration                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.15.0.0                | `#4087`_ | python format                                              |
+-------------------------+----------+------------------------------------------------------------+

256 Issues listed

.. _`#4568`: https://github.com/apache/cloudstack/pull/4568 
.. _`#4559`: https://github.com/apache/cloudstack/pull/4559 
.. _`#4553`: https://github.com/apache/cloudstack/pull/4553 
.. _`#4555`: https://github.com/apache/cloudstack/pull/4555 
.. _`#4540`: https://github.com/apache/cloudstack/pull/4540 
.. _`#4529`: https://github.com/apache/cloudstack/pull/4529 
.. _`#4522`: https://github.com/apache/cloudstack/pull/4522 
.. _`#4516`: https://github.com/apache/cloudstack/pull/4516 
.. _`#4533`: https://github.com/apache/cloudstack/pull/4533 
.. _`#4536`: https://github.com/apache/cloudstack/pull/4536 
.. _`#4538`: https://github.com/apache/cloudstack/pull/4538 
.. _`#4511`: https://github.com/apache/cloudstack/pull/4511 
.. _`#4530`: https://github.com/apache/cloudstack/pull/4530 
.. _`#4532`: https://github.com/apache/cloudstack/pull/4532 
.. _`#4526`: https://github.com/apache/cloudstack/pull/4526 
.. _`#4527`: https://github.com/apache/cloudstack/pull/4527 
.. _`#4525`: https://github.com/apache/cloudstack/pull/4525 
.. _`#4523`: https://github.com/apache/cloudstack/pull/4523 
.. _`#4497`: https://github.com/apache/cloudstack/pull/4497 
.. _`#4521`: https://github.com/apache/cloudstack/pull/4521 
.. _`#4507`: https://github.com/apache/cloudstack/pull/4507 
.. _`#4515`: https://github.com/apache/cloudstack/pull/4515 
.. _`#4518`: https://github.com/apache/cloudstack/pull/4518 
.. _`#4510`: https://github.com/apache/cloudstack/pull/4510 
.. _`#4501`: https://github.com/apache/cloudstack/pull/4501 
.. _`#4505`: https://github.com/apache/cloudstack/pull/4505 
.. _`#4499`: https://github.com/apache/cloudstack/pull/4499 
.. _`#4496`: https://github.com/apache/cloudstack/pull/4496 
.. _`#4495`: https://github.com/apache/cloudstack/pull/4495 
.. _`#4500`: https://github.com/apache/cloudstack/pull/4500 
.. _`#4494`: https://github.com/apache/cloudstack/pull/4494 
.. _`#4489`: https://github.com/apache/cloudstack/pull/4489 
.. _`#4361`: https://github.com/apache/cloudstack/pull/4361 
.. _`#4486`: https://github.com/apache/cloudstack/pull/4486 
.. _`#4483`: https://github.com/apache/cloudstack/pull/4483 
.. _`#4425`: https://github.com/apache/cloudstack/pull/4425 
.. _`#4392`: https://github.com/apache/cloudstack/pull/4392 
.. _`#4467`: https://github.com/apache/cloudstack/pull/4467 
.. _`#4480`: https://github.com/apache/cloudstack/pull/4480 
.. _`#4478`: https://github.com/apache/cloudstack/pull/4478 
.. _`#4466`: https://github.com/apache/cloudstack/pull/4466 
.. _`#4458`: https://github.com/apache/cloudstack/pull/4458 
.. _`#4487`: https://github.com/apache/cloudstack/pull/4487 
.. _`#4459`: https://github.com/apache/cloudstack/pull/4459 
.. _`#4485`: https://github.com/apache/cloudstack/pull/4485 
.. _`#4461`: https://github.com/apache/cloudstack/pull/4461 
.. _`#4476`: https://github.com/apache/cloudstack/pull/4476 
.. _`#4078`: https://github.com/apache/cloudstack/pull/4078 
.. _`#4428`: https://github.com/apache/cloudstack/pull/4428 
.. _`#4475`: https://github.com/apache/cloudstack/pull/4475 
.. _`#4452`: https://github.com/apache/cloudstack/pull/4452 
.. _`#4446`: https://github.com/apache/cloudstack/pull/4446 
.. _`#4469`: https://github.com/apache/cloudstack/pull/4469 
.. _`#4464`: https://github.com/apache/cloudstack/pull/4464 
.. _`#4289`: https://github.com/apache/cloudstack/pull/4289 
.. _`#4465`: https://github.com/apache/cloudstack/pull/4465 
.. _`#4456`: https://github.com/apache/cloudstack/pull/4456 
.. _`#4418`: https://github.com/apache/cloudstack/pull/4418 
.. _`#4327`: https://github.com/apache/cloudstack/pull/4327 
.. _`#4437`: https://github.com/apache/cloudstack/pull/4437 
.. _`#4442`: https://github.com/apache/cloudstack/pull/4442 
.. _`#4439`: https://github.com/apache/cloudstack/pull/4439 
.. _`#4430`: https://github.com/apache/cloudstack/pull/4430 
.. _`#4440`: https://github.com/apache/cloudstack/pull/4440 
.. _`#4408`: https://github.com/apache/cloudstack/pull/4408 
.. _`#4341`: https://github.com/apache/cloudstack/pull/4341 
.. _`#4388`: https://github.com/apache/cloudstack/pull/4388 
.. _`#4435`: https://github.com/apache/cloudstack/pull/4435 
.. _`#4177`: https://github.com/apache/cloudstack/pull/4177 
.. _`#4429`: https://github.com/apache/cloudstack/pull/4429 
.. _`#4359`: https://github.com/apache/cloudstack/pull/4359 
.. _`#4426`: https://github.com/apache/cloudstack/pull/4426 
.. _`#4432`: https://github.com/apache/cloudstack/pull/4432 
.. _`#4144`: https://github.com/apache/cloudstack/pull/4144 
.. _`#3945`: https://github.com/apache/cloudstack/pull/3945 
.. _`#4363`: https://github.com/apache/cloudstack/pull/4363 
.. _`#4417`: https://github.com/apache/cloudstack/pull/4417 
.. _`#4414`: https://github.com/apache/cloudstack/pull/4414 
.. _`#4367`: https://github.com/apache/cloudstack/pull/4367 
.. _`#4427`: https://github.com/apache/cloudstack/pull/4427 
.. _`#4420`: https://github.com/apache/cloudstack/pull/4420 
.. _`#4415`: https://github.com/apache/cloudstack/pull/4415 
.. _`#4307`: https://github.com/apache/cloudstack/pull/4307 
.. _`#4375`: https://github.com/apache/cloudstack/pull/4375 
.. _`#2206`: https://github.com/apache/cloudstack/pull/2206 
.. _`#4409`: https://github.com/apache/cloudstack/pull/4409 
.. _`#4413`: https://github.com/apache/cloudstack/pull/4413 
.. _`#4360`: https://github.com/apache/cloudstack/pull/4360 
.. _`#4193`: https://github.com/apache/cloudstack/pull/4193 
.. _`#4411`: https://github.com/apache/cloudstack/pull/4411 
.. _`#4412`: https://github.com/apache/cloudstack/pull/4412 
.. _`#67`: https://github.com/apache/cloudstack/pull/67 
.. _`#3946`: https://github.com/apache/cloudstack/pull/3946 
.. _`#4387`: https://github.com/apache/cloudstack/pull/4387 
.. _`#4407`: https://github.com/apache/cloudstack/pull/4407 
.. _`#4395`: https://github.com/apache/cloudstack/pull/4395 
.. _`#4194`: https://github.com/apache/cloudstack/pull/4194 
.. _`#4251`: https://github.com/apache/cloudstack/pull/4251 
.. _`#4405`: https://github.com/apache/cloudstack/pull/4405 
.. _`#4377`: https://github.com/apache/cloudstack/pull/4377 
.. _`#4381`: https://github.com/apache/cloudstack/pull/4381 
.. _`#4228`: https://github.com/apache/cloudstack/pull/4228 
.. _`#4348`: https://github.com/apache/cloudstack/pull/4348 
.. _`#4404`: https://github.com/apache/cloudstack/pull/4404 
.. _`#4383`: https://github.com/apache/cloudstack/pull/4383 
.. _`#4382`: https://github.com/apache/cloudstack/pull/4382 
.. _`#4379`: https://github.com/apache/cloudstack/pull/4379 
.. _`#4373`: https://github.com/apache/cloudstack/pull/4373 
.. _`#4366`: https://github.com/apache/cloudstack/pull/4366 
.. _`#4365`: https://github.com/apache/cloudstack/pull/4365 
.. _`#4397`: https://github.com/apache/cloudstack/pull/4397 
.. _`#4376`: https://github.com/apache/cloudstack/pull/4376 
.. _`#4374`: https://github.com/apache/cloudstack/pull/4374 
.. _`#4389`: https://github.com/apache/cloudstack/pull/4389 
.. _`#4271`: https://github.com/apache/cloudstack/pull/4271 
.. _`#4321`: https://github.com/apache/cloudstack/pull/4321 
.. _`#4354`: https://github.com/apache/cloudstack/pull/4354 
.. _`#4352`: https://github.com/apache/cloudstack/pull/4352 
.. _`#4269`: https://github.com/apache/cloudstack/pull/4269 
.. _`#4338`: https://github.com/apache/cloudstack/pull/4338 
.. _`#4345`: https://github.com/apache/cloudstack/pull/4345 
.. _`#4340`: https://github.com/apache/cloudstack/pull/4340 
.. _`#4190`: https://github.com/apache/cloudstack/pull/4190 
.. _`#4328`: https://github.com/apache/cloudstack/pull/4328 
.. _`#4336`: https://github.com/apache/cloudstack/pull/4336 
.. _`#4305`: https://github.com/apache/cloudstack/pull/4305 
.. _`#4335`: https://github.com/apache/cloudstack/pull/4335 
.. _`#4319`: https://github.com/apache/cloudstack/pull/4319 
.. _`#4303`: https://github.com/apache/cloudstack/pull/4303 
.. _`#4239`: https://github.com/apache/cloudstack/pull/4239 
.. _`#4323`: https://github.com/apache/cloudstack/pull/4323 
.. _`#4319`: https://github.com/apache/cloudstack/pull/4319 
.. _`#4331`: https://github.com/apache/cloudstack/pull/4331 
.. _`#4333`: https://github.com/apache/cloudstack/pull/4333 
.. _`#4294`: https://github.com/apache/cloudstack/pull/4294 
.. _`#4316`: https://github.com/apache/cloudstack/pull/4316 
.. _`#4309`: https://github.com/apache/cloudstack/pull/4309 
.. _`#4326`: https://github.com/apache/cloudstack/pull/4326 
.. _`#4315`: https://github.com/apache/cloudstack/pull/4315 
.. _`#4053`: https://github.com/apache/cloudstack/pull/4053 
.. _`#4312`: https://github.com/apache/cloudstack/pull/4312 
.. _`#4320`: https://github.com/apache/cloudstack/pull/4320 
.. _`#4317`: https://github.com/apache/cloudstack/pull/4317 
.. _`#4297`: https://github.com/apache/cloudstack/pull/4297 
.. _`#4306`: https://github.com/apache/cloudstack/pull/4306 
.. _`#4301`: https://github.com/apache/cloudstack/pull/4301 
.. _`#4291`: https://github.com/apache/cloudstack/pull/4291 
.. _`#4284`: https://github.com/apache/cloudstack/pull/4284 
.. _`#4279`: https://github.com/apache/cloudstack/pull/4279 
.. _`#4020`: https://github.com/apache/cloudstack/pull/4020 
.. _`#4258`: https://github.com/apache/cloudstack/pull/4258 
.. _`#3996`: https://github.com/apache/cloudstack/pull/3996 
.. _`#3902`: https://github.com/apache/cloudstack/pull/3902 
.. _`#4288`: https://github.com/apache/cloudstack/pull/4288 
.. _`#4287`: https://github.com/apache/cloudstack/pull/4287 
.. _`#4266`: https://github.com/apache/cloudstack/pull/4266 
.. _`#4264`: https://github.com/apache/cloudstack/pull/4264 
.. _`#4272`: https://github.com/apache/cloudstack/pull/4272 
.. _`#4274`: https://github.com/apache/cloudstack/pull/4274 
.. _`#4278`: https://github.com/apache/cloudstack/pull/4278 
.. _`#4219`: https://github.com/apache/cloudstack/pull/4219 
.. _`#4040`: https://github.com/apache/cloudstack/pull/4040 
.. _`#4275`: https://github.com/apache/cloudstack/pull/4275 
.. _`#4180`: https://github.com/apache/cloudstack/pull/4180 
.. _`#4068`: https://github.com/apache/cloudstack/pull/4068 
.. _`#4268`: https://github.com/apache/cloudstack/pull/4268 
.. _`#4262`: https://github.com/apache/cloudstack/pull/4262 
.. _`#4207`: https://github.com/apache/cloudstack/pull/4207 
.. _`#4254`: https://github.com/apache/cloudstack/pull/4254 
.. _`#4128`: https://github.com/apache/cloudstack/pull/4128 
.. _`#4213`: https://github.com/apache/cloudstack/pull/4213 
.. _`#4255`: https://github.com/apache/cloudstack/pull/4255 
.. _`#4256`: https://github.com/apache/cloudstack/pull/4256 
.. _`#4260`: https://github.com/apache/cloudstack/pull/4260 
.. _`#4016`: https://github.com/apache/cloudstack/pull/4016 
.. _`#4253`: https://github.com/apache/cloudstack/pull/4253 
.. _`#4249`: https://github.com/apache/cloudstack/pull/4249 
.. _`#4243`: https://github.com/apache/cloudstack/pull/4243 
.. _`#4019`: https://github.com/apache/cloudstack/pull/4019 
.. _`#4165`: https://github.com/apache/cloudstack/pull/4165 
.. _`#4220`: https://github.com/apache/cloudstack/pull/4220 
.. _`#4225`: https://github.com/apache/cloudstack/pull/4225 
.. _`#4000`: https://github.com/apache/cloudstack/pull/4000 
.. _`#4231`: https://github.com/apache/cloudstack/pull/4231 
.. _`#4116`: https://github.com/apache/cloudstack/pull/4116 
.. _`#3952`: https://github.com/apache/cloudstack/pull/3952 
.. _`#4175`: https://github.com/apache/cloudstack/pull/4175 
.. _`#4035`: https://github.com/apache/cloudstack/pull/4035 
.. _`#4214`: https://github.com/apache/cloudstack/pull/4214 
.. _`#4226`: https://github.com/apache/cloudstack/pull/4226 
.. _`#4188`: https://github.com/apache/cloudstack/pull/4188 
.. _`#4138`: https://github.com/apache/cloudstack/pull/4138 
.. _`#4156`: https://github.com/apache/cloudstack/pull/4156 
.. _`#4172`: https://github.com/apache/cloudstack/pull/4172 
.. _`#4196`: https://github.com/apache/cloudstack/pull/4196 
.. _`#4176`: https://github.com/apache/cloudstack/pull/4176 
.. _`#4202`: https://github.com/apache/cloudstack/pull/4202 
.. _`#3979`: https://github.com/apache/cloudstack/pull/3979 
.. _`#4174`: https://github.com/apache/cloudstack/pull/4174 
.. _`#4117`: https://github.com/apache/cloudstack/pull/4117 
.. _`#4071`: https://github.com/apache/cloudstack/pull/4071 
.. _`#4186`: https://github.com/apache/cloudstack/pull/4186 
.. _`#4001`: https://github.com/apache/cloudstack/pull/4001 
.. _`#3976`: https://github.com/apache/cloudstack/pull/3976 
.. _`#4103`: https://github.com/apache/cloudstack/pull/4103 
.. _`#4148`: https://github.com/apache/cloudstack/pull/4148 
.. _`#4171`: https://github.com/apache/cloudstack/pull/4171 
.. _`#4167`: https://github.com/apache/cloudstack/pull/4167 
.. _`#4164`: https://github.com/apache/cloudstack/pull/4164 
.. _`#4154`: https://github.com/apache/cloudstack/pull/4154 
.. _`#4004`: https://github.com/apache/cloudstack/pull/4004 
.. _`#4162`: https://github.com/apache/cloudstack/pull/4162 
.. _`#4132`: https://github.com/apache/cloudstack/pull/4132 
.. _`#4145`: https://github.com/apache/cloudstack/pull/4145 
.. _`#3998`: https://github.com/apache/cloudstack/pull/3998 
.. _`#4085`: https://github.com/apache/cloudstack/pull/4085 
.. _`#4140`: https://github.com/apache/cloudstack/pull/4140 
.. _`#4007`: https://github.com/apache/cloudstack/pull/4007 
.. _`#4003`: https://github.com/apache/cloudstack/pull/4003 
.. _`#4121`: https://github.com/apache/cloudstack/pull/4121 
.. _`#3991`: https://github.com/apache/cloudstack/pull/3991 
.. _`#4070`: https://github.com/apache/cloudstack/pull/4070 
.. _`#4130`: https://github.com/apache/cloudstack/pull/4130 
.. _`#4122`: https://github.com/apache/cloudstack/pull/4122 
.. _`#3982`: https://github.com/apache/cloudstack/pull/3982 
.. _`#4073`: https://github.com/apache/cloudstack/pull/4073 
.. _`#4075`: https://github.com/apache/cloudstack/pull/4075 
.. _`#3949`: https://github.com/apache/cloudstack/pull/3949 
.. _`#3955`: https://github.com/apache/cloudstack/pull/3955 
.. _`#3980`: https://github.com/apache/cloudstack/pull/3980 
.. _`#4048`: https://github.com/apache/cloudstack/pull/4048 
.. _`#4083`: https://github.com/apache/cloudstack/pull/4083 
.. _`#4142`: https://github.com/apache/cloudstack/pull/4142 
.. _`#4109`: https://github.com/apache/cloudstack/pull/4109 
.. _`#4077`: https://github.com/apache/cloudstack/pull/4077 
.. _`#4021`: https://github.com/apache/cloudstack/pull/4021 
.. _`#3965`: https://github.com/apache/cloudstack/pull/3965 
.. _`#4104`: https://github.com/apache/cloudstack/pull/4104 
.. _`#4017`: https://github.com/apache/cloudstack/pull/4017 
.. _`#4079`: https://github.com/apache/cloudstack/pull/4079 
.. _`#4046`: https://github.com/apache/cloudstack/pull/4046 
.. _`#4013`: https://github.com/apache/cloudstack/pull/4013 
.. _`#4062`: https://github.com/apache/cloudstack/pull/4062 
.. _`#4119`: https://github.com/apache/cloudstack/pull/4119 
.. _`#4126`: https://github.com/apache/cloudstack/pull/4126 
.. _`#4123`: https://github.com/apache/cloudstack/pull/4123 
.. _`#4065`: https://github.com/apache/cloudstack/pull/4065 
.. _`#4124`: https://github.com/apache/cloudstack/pull/4124 
.. _`#3794`: https://github.com/apache/cloudstack/pull/3794 
.. _`#4100`: https://github.com/apache/cloudstack/pull/4100 
.. _`#3921`: https://github.com/apache/cloudstack/pull/3921 
.. _`#4110`: https://github.com/apache/cloudstack/pull/4110 
.. _`#4092`: https://github.com/apache/cloudstack/pull/4092 
.. _`#4097`: https://github.com/apache/cloudstack/pull/4097 
.. _`#3967`: https://github.com/apache/cloudstack/pull/3967 
.. _`#4087`: https://github.com/apache/cloudstack/pull/4087 
