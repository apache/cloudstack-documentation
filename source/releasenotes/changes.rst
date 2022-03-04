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

Changes in |release| since 4.16.0.0
====================================

Apache CloudStack uses GitHub https://github.com/apache/cloudstack/milestone/22?closed=1
 to track its issues.

.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+------------------------------------------------------------+
| Version                 | Github   | Description                                                |
+=========================+==========+============================================================+
| 4.16.1.0                | `#6042`_ | [vmware, ssvm] Scale down of ssvm                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#6029`_ | [KVM] Disconnect the volumes with the proper storage       |
|                         |          | adaptor.                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#6027`_ | prevent <ctrl>-<enter> handler from <space> from toggling  |
|                         |          | checkboxes                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#6034`_ | ui: add VXLAN network identifiers (VNIs) in                |
|                         |          | message.guest.traffic.in.advanced.zone                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#6035`_ | api: update description of internal LB APIs                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#6020`_ | UI: Reword the setting panel warning                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#6003`_ | ui: minor change with help text on dashboard               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#6000`_ | server: reapply checkVmProfileAndHost to check guest os    |
|                         |          | preference                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5863`_ | CKS Enhancements and SystemVM template upgrade             |
|                         |          | improvements                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5972`_ | set pod after migration                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5911`_ | Improve the guest OS hypervisor mappings addition on       |
|                         |          | upgrade.                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5910`_ | [VMware] Update SCSI controllers for VMs                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5959`_ | Quota test fixes                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5978`_ | ui: Allow domain admin to configure subdomain limits       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5879`_ | Role escalation prevention                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5544`_ | Fix of revert RBD snapshots                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5850`_ | api, server: fix add-remove vpn user without vpn owner     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5956`_ | Add disk space in systemVM template registration script    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5968`_ | [issue-5943] xerces 2.12.2                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5953`_ | [issue-5952] upgrade to jetty 9.4.44.v20210927             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5966`_ | replace Random with SecureRandom                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5958`_ | API: Fix listSSHKeyPairs API when listing all resources    |
|                         |          | (listall=true & projectid=-1)                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5875`_ | cleanup: Network Throttling for Additional Networks code   |
|                         |          | in DirectVifDriver.java                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5904`_ | UI - Add Network: shows "Offering for Isolated networks    |
|                         |          | with no Source Nat service" on Network Offering for normal |
|                         |          | users                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5962`_ | test: sleep 30s after restarting mgt server in             |
|                         |          | test_kubernetes_supported_versions.py                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5963`_ | Add ID search capability to sshkeypairs                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5949`_ | [issue-5948] upgrade bouncycastle due to cve               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5954`_ | Skip systemVM template registration for Simulator          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5851`_ | packaging: display First Install and Onboarding Message    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5878`_ | maven: migrate short-term to reload4j v1.2.18              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5857`_ | server,config: respect storage.max.volume.size and make it |
|                         |          | dynamic                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5942`_ | [issue-5939] upgrade commons-compress to 1.21              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5517`_ | Fix #3448 quota calculation for monthly tariffs            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5933`_ | ui: fix select networks for template nic                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5947`_ | [issue-5946] upgrade to xstream 1.4.19                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5944`_ | [issue-5943] upgrade to xerces 2.12.2                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5859`_ | add logging to deployment planners                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5931`_ | ui: fix ssh keypair navigation                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5912`_ | Added hot plugging of vifs in case of VMware isolated      |
|                         |          | networks                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5870`_ | VMware7 support: Add schema changes for update2 and        |
|                         |          | update3                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5866`_ | Filter usage for project                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5506`_ | kvm: Use lscpu to get cpu max speed                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5929`_ | ui: fix related key for section                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5920`_ | server: allow normal users to create isolated network      |
|                         |          | without source nat                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5400`_ | vm-import: fix unmanaged instance listing                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5473`_ | api,server: add params for updatehypervisorcapabilities    |
|                         |          | API                                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5852`_ | server: find suitable disk offering for volume upload      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5892`_ | [XenServer/XCP-ng] Sync the 'platform' setting according   |
|                         |          | to the 'cpu.corespersocket' setting                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5908`_ | Update proper destroy status when SSVM is destroyed.       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5896`_ | Make sure other than user VMs can have multiple NICs in a  |
|                         |          | network                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5873`_ | Do not restart VPC tiers with cleanup                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5887`_ | ui: fix filtering readonly details while VM update         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5886`_ | [XenServer/XCP-ng] Pass the image store NFS version on     |
|                         |          | storage commands                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5785`_ | Add idempotent primary keys on tables missing them         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5900`_ | Allow direct download templates from IPv6 host address.    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5620`_ | Adding placeholders for custom NSP vues                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5893`_ | UI - Added option to allow users to select volumes when    |
|                         |          | doing destroy the list of VMs                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5884`_ | UI: Fixes asynchronous when destroying wrong item VM       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5881`_ | packaging: use modern systemctl enable/disable             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5861`_ | [VMware][Deploy-as-is] OVF properties not importing when   |
|                         |          | template is uploaded from local                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5825`_ | [Vmware][Deploy-as-is] Refactor the OVF parsing            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5434`_ | ui: add custom form for update template                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5872`_ | Removed redundant parsing of VMSnapshot usage record.      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5889`_ | ui: show password with success notification                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5865`_ | fill volume attached field                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5880`_ | [UI] Fix domain resources field not being updated with     |
|                         |          | backend data                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5844`_ | server: fix regular user can create isolated network       |
|                         |          | without sourcenat                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5871`_ | Delete ldap config from UI                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5869`_ | UI - Fixes Pod, Cluster selected is incorrect on addHost   |
|                         |          | dialog                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5846`_ | Prevent upgrade failures if there are existing annotations |
|                         |          | permissions                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5487`_ | ui: fix create user domain, account selection              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5584`_ | UI - Add a setting to config.json that allows users to set |
|                         |          | theme                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5856`_ | ui: fix deploy vm in basic zone                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5855`_ | UI: Fixes switching between domains with SAML user         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5858`_ | ui: show account configure limits tab for domain-admin     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5663`_ | UI - Cancel all requests api, async jobs when user logs    |
|                         |          | out                                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5653`_ | UI - Deploy VM with params from the template, iso, network |
|                         |          | pages                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5828`_ | server: fix update vm with unconstrained offering          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5853`_ | ui: fix getDiagnosticsData files field                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5810`_ | ipv6: disable IPv6-only shared network with VR             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5849`_ | ui: fix paging in enable static NAT form                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5790`_ | Add toggle button on the UI for list including elements in |
|                         |          | projects.                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5847`_ | ui: update vm haenable only for supported vms              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5839`_ | server: fix enable/disable static nat if userdata is not   |
|                         |          | supported                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5841`_ | Storage pool absent                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5784`_ | network: fix vm can be deployed on L2 network of other     |
|                         |          | accounts                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5658`_ | remove VmWorkJob after adding a nic to a vm                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5843`_ | UI - Fix Locked "Override Root Disk Size" switch           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5726`_ | UI: Add s3 provider option to create secondary storage     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5748`_ | Prevent null values on Vmware appliances details that are  |
|                         |          | missing a default value                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5801`_ | Set RAW format to RBD DATADISK                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5840`_ | ui: fix create network/vpc offering form                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5833`_ | api: fix typo Destroy volume can be recovered              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5822`_ | server: fix vm can be recovered by other accounts          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5829`_ | UI - Hide shrink disk option on XCP-NG/Xenserver           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5750`_ | use physical size instead of virtual size for migration.   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5827`_ | server: do not return inaccessible entity details to       |
|                         |          | normal users                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5812`_ | UI: Fix new UI missing 4 parameters when adding a          |
|                         |          | BareMetal host                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#4230`_ | Enable resetting config values to default value            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5816`_ | LDAP truststore per domain                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5819`_ | UI - Refactoring $notification according to the old        |
|                         |          | version                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5647`_ | assume a property is one when it isn't a number            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5528`_ | test: fix component test test_configdrive.py               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5714`_ | UI: Automatically refill tariff label information after    |
|                         |          | editing.                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5809`_ | ui: fix add network offering for vpc                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5549`_ | UI - Add clear all notification button                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5628`_ | UI: Add footer text option for login screen                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5684`_ | (ccc2021 hackathon ) kvm: add hosts using cloudstack ssh   |
|                         |          | private key                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5755`_ | kvm: support qemu-system-x86>=5.2                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5752`_ | [VMware] Fix service offerings listing on appliances       |
|                         |          | deployment options                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5789`_ | Randomize managed volume copy host                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5796`_ | Fix UI issue 5777 Root disk size is not shown as 'Disk     |
|                         |          | Size' on VM deployment.                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5798`_ | ui: show tags only for supported resources                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5802`_ | kvm: don't always force scsi controller for aarch64 VMs    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5814`_ | ui: Fix configure Sticky policy form                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5690`_ | UI - Fixes cannot add new port forwarding rules after auto |
|                         |          | select VM next time                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5757`_ | network: update ip in lb/pf/dnat tables when update vm nic |
|                         |          | ip                                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5804`_ | UI: show SSH keys step in VM deployment only if user can   |
|                         |          | 'listSSHKeyPairs'                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5753`_ | server: Fix NPE while deleting a domain                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5723`_ | server: Fix NPE while adding network to VPC                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5806`_ | UI: Remove unused gravatar fetch                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5800`_ | Provision to sort ISOs from UI, and Updated Templates/ISOs |
|                         |          | API response to return in the order of sortkey.            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5562`_ | cleanup of unused code and cleanup of cleanup procedure    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5791`_ | Allow force reboot VM from user account, to start VM on    |
|                         |          | the same host.                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5782`_ | api: Fix search cluster by name                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5762`_ | Enhance log message in FirstFitPlanner                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5710`_ | UI: Fixes error when delete domain                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5758`_ | Fix NPE on migrateVirtualMachineWithVolume                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5779`_ | UI: fix create Isolated/L2 network form                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5763`_ | Increase the length for parameters that expect a list of   |
|                         |          | domain IDs.                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5767`_ | travis: install python3-setuptools                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5745`_ | conditional broadcastUri                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5738`_ | internal ref replaced by uuid                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5708`_ | vmware: fix cpu reservation during vm scale                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5734`_ | UI - Fixes the next button not working when adding more    |
|                         |          | physical networks                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5735`_ | [VMware] Improve volume file search on the datastore while |
|                         |          | computing the VM snapshot chain size.                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5729`_ | server: fix non-root users are able to list system         |
|                         |          | networks                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5744`_ | UI bug fix: 'Invalid ip address' when change vm ip address |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5746`_ | check security group in basic zones during deploy          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5737`_ | UI: Enable cancel host maintenance when resource state is  |
|                         |          | 'ErrorInPrepareForMaintenance'                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5701`_ | server: update capacity_state of host cpu core after       |
|                         |          | disable/enable a host                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5740`_ | Fix wrong logger class in *Cmd.java                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5720`_ | Removed redundant call for VM snapshot chain size, in      |
|                         |          | VMware.                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5736`_ | Fix NPE on scale VM operation after the corresponding      |
|                         |          | template is del…                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5675`_ | server bug fix: remove network details when network is     |
|                         |          | removed                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5704`_ | engine/schema: fix findActiveAccountById in                |
|                         |          | AccountDaoImpl.java                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5692`_ | KVM : Fixes UEFI XML Definition Error                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5200`_ | UI: Autoscroll to Error Field                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5648`_ | IPv6: fix deploy vm issue in ipv6-only networks without VR |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5670`_ | server: set network rate for additional public IPs         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5672`_ | ui-primary-storage: hide provider if Linstor protocol      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5682`_ | UI : Fix SSL certificate submit button not working         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5693`_ | UI: Fixes incorrect auto-select in Add network to VM       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.1.0                | `#5671`_ | CsDhcp.py: fix runtests.sh error                           |
+-------------------------+----------+------------------------------------------------------------+

154 Issues listed

.. _`#6042`: https://github.com/apache/cloudstack/pull/6042 
.. _`#6029`: https://github.com/apache/cloudstack/pull/6029 
.. _`#6027`: https://github.com/apache/cloudstack/pull/6027 
.. _`#6034`: https://github.com/apache/cloudstack/pull/6034 
.. _`#6035`: https://github.com/apache/cloudstack/pull/6035 
.. _`#6020`: https://github.com/apache/cloudstack/pull/6020 
.. _`#6003`: https://github.com/apache/cloudstack/pull/6003 
.. _`#6000`: https://github.com/apache/cloudstack/pull/6000 
.. _`#5863`: https://github.com/apache/cloudstack/pull/5863 
.. _`#5972`: https://github.com/apache/cloudstack/pull/5972 
.. _`#5911`: https://github.com/apache/cloudstack/pull/5911 
.. _`#5910`: https://github.com/apache/cloudstack/pull/5910 
.. _`#5959`: https://github.com/apache/cloudstack/pull/5959 
.. _`#5978`: https://github.com/apache/cloudstack/pull/5978 
.. _`#5879`: https://github.com/apache/cloudstack/pull/5879 
.. _`#5544`: https://github.com/apache/cloudstack/pull/5544 
.. _`#5850`: https://github.com/apache/cloudstack/pull/5850 
.. _`#5956`: https://github.com/apache/cloudstack/pull/5956 
.. _`#5968`: https://github.com/apache/cloudstack/pull/5968 
.. _`#5953`: https://github.com/apache/cloudstack/pull/5953 
.. _`#5966`: https://github.com/apache/cloudstack/pull/5966 
.. _`#5958`: https://github.com/apache/cloudstack/pull/5958 
.. _`#5875`: https://github.com/apache/cloudstack/pull/5875 
.. _`#5904`: https://github.com/apache/cloudstack/pull/5904 
.. _`#5962`: https://github.com/apache/cloudstack/pull/5962 
.. _`#5963`: https://github.com/apache/cloudstack/pull/5963 
.. _`#5949`: https://github.com/apache/cloudstack/pull/5949 
.. _`#5954`: https://github.com/apache/cloudstack/pull/5954 
.. _`#5851`: https://github.com/apache/cloudstack/pull/5851 
.. _`#5878`: https://github.com/apache/cloudstack/pull/5878 
.. _`#5857`: https://github.com/apache/cloudstack/pull/5857 
.. _`#5942`: https://github.com/apache/cloudstack/pull/5942 
.. _`#5517`: https://github.com/apache/cloudstack/pull/5517 
.. _`#5933`: https://github.com/apache/cloudstack/pull/5933 
.. _`#5947`: https://github.com/apache/cloudstack/pull/5947 
.. _`#5944`: https://github.com/apache/cloudstack/pull/5944 
.. _`#5859`: https://github.com/apache/cloudstack/pull/5859 
.. _`#5931`: https://github.com/apache/cloudstack/pull/5931 
.. _`#5912`: https://github.com/apache/cloudstack/pull/5912 
.. _`#5870`: https://github.com/apache/cloudstack/pull/5870 
.. _`#5866`: https://github.com/apache/cloudstack/pull/5866 
.. _`#5506`: https://github.com/apache/cloudstack/pull/5506 
.. _`#5929`: https://github.com/apache/cloudstack/pull/5929 
.. _`#5920`: https://github.com/apache/cloudstack/pull/5920 
.. _`#5400`: https://github.com/apache/cloudstack/pull/5400 
.. _`#5473`: https://github.com/apache/cloudstack/pull/5473 
.. _`#5852`: https://github.com/apache/cloudstack/pull/5852 
.. _`#5892`: https://github.com/apache/cloudstack/pull/5892 
.. _`#5908`: https://github.com/apache/cloudstack/pull/5908 
.. _`#5896`: https://github.com/apache/cloudstack/pull/5896 
.. _`#5873`: https://github.com/apache/cloudstack/pull/5873 
.. _`#5887`: https://github.com/apache/cloudstack/pull/5887 
.. _`#5886`: https://github.com/apache/cloudstack/pull/5886 
.. _`#5785`: https://github.com/apache/cloudstack/pull/5785 
.. _`#5900`: https://github.com/apache/cloudstack/pull/5900 
.. _`#5620`: https://github.com/apache/cloudstack/pull/5620 
.. _`#5893`: https://github.com/apache/cloudstack/pull/5893 
.. _`#5884`: https://github.com/apache/cloudstack/pull/5884 
.. _`#5881`: https://github.com/apache/cloudstack/pull/5881 
.. _`#5861`: https://github.com/apache/cloudstack/pull/5861 
.. _`#5825`: https://github.com/apache/cloudstack/pull/5825 
.. _`#5434`: https://github.com/apache/cloudstack/pull/5434 
.. _`#5872`: https://github.com/apache/cloudstack/pull/5872 
.. _`#5889`: https://github.com/apache/cloudstack/pull/5889 
.. _`#5865`: https://github.com/apache/cloudstack/pull/5865 
.. _`#5880`: https://github.com/apache/cloudstack/pull/5880 
.. _`#5844`: https://github.com/apache/cloudstack/pull/5844 
.. _`#5871`: https://github.com/apache/cloudstack/pull/5871 
.. _`#5869`: https://github.com/apache/cloudstack/pull/5869 
.. _`#5846`: https://github.com/apache/cloudstack/pull/5846 
.. _`#5487`: https://github.com/apache/cloudstack/pull/5487 
.. _`#5584`: https://github.com/apache/cloudstack/pull/5584 
.. _`#5856`: https://github.com/apache/cloudstack/pull/5856 
.. _`#5855`: https://github.com/apache/cloudstack/pull/5855 
.. _`#5858`: https://github.com/apache/cloudstack/pull/5858 
.. _`#5663`: https://github.com/apache/cloudstack/pull/5663 
.. _`#5653`: https://github.com/apache/cloudstack/pull/5653 
.. _`#5828`: https://github.com/apache/cloudstack/pull/5828 
.. _`#5853`: https://github.com/apache/cloudstack/pull/5853 
.. _`#5810`: https://github.com/apache/cloudstack/pull/5810 
.. _`#5849`: https://github.com/apache/cloudstack/pull/5849 
.. _`#5790`: https://github.com/apache/cloudstack/pull/5790 
.. _`#5847`: https://github.com/apache/cloudstack/pull/5847 
.. _`#5839`: https://github.com/apache/cloudstack/pull/5839 
.. _`#5841`: https://github.com/apache/cloudstack/pull/5841 
.. _`#5784`: https://github.com/apache/cloudstack/pull/5784 
.. _`#5658`: https://github.com/apache/cloudstack/pull/5658 
.. _`#5843`: https://github.com/apache/cloudstack/pull/5843 
.. _`#5726`: https://github.com/apache/cloudstack/pull/5726 
.. _`#5748`: https://github.com/apache/cloudstack/pull/5748 
.. _`#5801`: https://github.com/apache/cloudstack/pull/5801 
.. _`#5840`: https://github.com/apache/cloudstack/pull/5840 
.. _`#5833`: https://github.com/apache/cloudstack/pull/5833 
.. _`#5822`: https://github.com/apache/cloudstack/pull/5822 
.. _`#5829`: https://github.com/apache/cloudstack/pull/5829 
.. _`#5750`: https://github.com/apache/cloudstack/pull/5750 
.. _`#5827`: https://github.com/apache/cloudstack/pull/5827 
.. _`#5812`: https://github.com/apache/cloudstack/pull/5812 
.. _`#4230`: https://github.com/apache/cloudstack/pull/4230 
.. _`#5816`: https://github.com/apache/cloudstack/pull/5816 
.. _`#5819`: https://github.com/apache/cloudstack/pull/5819 
.. _`#5647`: https://github.com/apache/cloudstack/pull/5647 
.. _`#5528`: https://github.com/apache/cloudstack/pull/5528 
.. _`#5714`: https://github.com/apache/cloudstack/pull/5714 
.. _`#5809`: https://github.com/apache/cloudstack/pull/5809 
.. _`#5549`: https://github.com/apache/cloudstack/pull/5549 
.. _`#5628`: https://github.com/apache/cloudstack/pull/5628 
.. _`#5684`: https://github.com/apache/cloudstack/pull/5684 
.. _`#5755`: https://github.com/apache/cloudstack/pull/5755 
.. _`#5752`: https://github.com/apache/cloudstack/pull/5752 
.. _`#5789`: https://github.com/apache/cloudstack/pull/5789 
.. _`#5796`: https://github.com/apache/cloudstack/pull/5796 
.. _`#5798`: https://github.com/apache/cloudstack/pull/5798 
.. _`#5802`: https://github.com/apache/cloudstack/pull/5802 
.. _`#5814`: https://github.com/apache/cloudstack/pull/5814 
.. _`#5690`: https://github.com/apache/cloudstack/pull/5690 
.. _`#5757`: https://github.com/apache/cloudstack/pull/5757 
.. _`#5804`: https://github.com/apache/cloudstack/pull/5804 
.. _`#5753`: https://github.com/apache/cloudstack/pull/5753 
.. _`#5723`: https://github.com/apache/cloudstack/pull/5723 
.. _`#5806`: https://github.com/apache/cloudstack/pull/5806 
.. _`#5800`: https://github.com/apache/cloudstack/pull/5800 
.. _`#5562`: https://github.com/apache/cloudstack/pull/5562 
.. _`#5791`: https://github.com/apache/cloudstack/pull/5791 
.. _`#5782`: https://github.com/apache/cloudstack/pull/5782 
.. _`#5762`: https://github.com/apache/cloudstack/pull/5762 
.. _`#5710`: https://github.com/apache/cloudstack/pull/5710 
.. _`#5758`: https://github.com/apache/cloudstack/pull/5758 
.. _`#5779`: https://github.com/apache/cloudstack/pull/5779 
.. _`#5763`: https://github.com/apache/cloudstack/pull/5763 
.. _`#5767`: https://github.com/apache/cloudstack/pull/5767 
.. _`#5745`: https://github.com/apache/cloudstack/pull/5745 
.. _`#5738`: https://github.com/apache/cloudstack/pull/5738 
.. _`#5708`: https://github.com/apache/cloudstack/pull/5708 
.. _`#5734`: https://github.com/apache/cloudstack/pull/5734 
.. _`#5735`: https://github.com/apache/cloudstack/pull/5735 
.. _`#5729`: https://github.com/apache/cloudstack/pull/5729 
.. _`#5744`: https://github.com/apache/cloudstack/pull/5744 
.. _`#5746`: https://github.com/apache/cloudstack/pull/5746 
.. _`#5737`: https://github.com/apache/cloudstack/pull/5737 
.. _`#5701`: https://github.com/apache/cloudstack/pull/5701 
.. _`#5740`: https://github.com/apache/cloudstack/pull/5740 
.. _`#5720`: https://github.com/apache/cloudstack/pull/5720 
.. _`#5736`: https://github.com/apache/cloudstack/pull/5736 
.. _`#5675`: https://github.com/apache/cloudstack/pull/5675 
.. _`#5704`: https://github.com/apache/cloudstack/pull/5704 
.. _`#5692`: https://github.com/apache/cloudstack/pull/5692 
.. _`#5200`: https://github.com/apache/cloudstack/pull/5200 
.. _`#5648`: https://github.com/apache/cloudstack/pull/5648 
.. _`#5670`: https://github.com/apache/cloudstack/pull/5670 
.. _`#5672`: https://github.com/apache/cloudstack/pull/5672 
.. _`#5682`: https://github.com/apache/cloudstack/pull/5682 
.. _`#5693`: https://github.com/apache/cloudstack/pull/5693 
.. _`#5671`: https://github.com/apache/cloudstack/pull/5671 


Changes in 4.16.0.0 since 4.15
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
| 4.16.0.0                | `#5435`_ | Fix public IP actions buttons not working unless           |
|                         |          | refreshing the page                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5432`_ | api, ui: return default ui pagesize as part of capability  |
|                         |          | response                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5427`_ | ui: fix add management ip range form                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5431`_ | Hide settings button if not on development mode            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5429`_ | ui: show nicAdapter selection for VMware non-readfromova   |
|                         |          | template                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5398`_ | Prevent double counting storage pools                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5358`_ | Fix potential NullPointerException in findStoragePool      |
|                         |          | (VolumeOrchestrator)                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5416`_ | travis: Fix failing test due to change in test name        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5067`_ | Keep volume policies after migrating it to another primary |
|                         |          | storage                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#3975`_ | Issue #3974 Deploying mysql-ha jar file into its own       |
|                         |          | path...                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5103`_ | Extend the Annotations framework                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5401`_ | marvin: fix exception logging                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5396`_ | cleanup: kvm-storage - fix misleading error log            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5390`_ | server: fix reset sshkey is broken in master/4.16          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4534`_ | Migrate vm across clusters                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5402`_ | UI: Add router links to notifications and show error       |
|                         |          | description                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5387`_ | api, ui: fix NPE with deployVirtualMachine when null       |
|                         |          | boottype                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5408`_ | Legacy UI: Display Accounts Tab to Project Admins          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5066`_ | CLOUDSTACK-10436:remind users to use correct permission    |
|                         |          | for tmp dir and fixed an NPE                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5404`_ | Allow public templates with no url to be migrated          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5394`_ | ui: Honour default.ui.page.size                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5259`_ | usage: create backup usage record for vmId-offeringId pair |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5307`_ | Filter disk / service offerings by domain at DB level      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5339`_ | server: check server capacity when start/deploy a vm       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5333`_ | vmware: delete snapshot disk after backup to secondary     |
|                         |          | storage                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5403`_ | Add 4.15.2 schema and upgrade path                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5082`_ | component test ports/fixes in python3                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5399`_ | travis: fix consistent failures noticed on few tests       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5376`_ | Use source IP from same subnet for snat                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5375`_ | vr: ipsec/l2tp vpn secret with no ID selectors             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5374`_ | [VMware] Cancel the pending tasks for a worker VM before   |
|                         |          | destroying it                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5379`_ | api: List details of template download state for stores    |
|                         |          | corresponding to a zone                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5380`_ | vmware: check checksum before copying systemvm ISO to      |
|                         |          | decide if it is needed                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5392`_ | UI - Scale VM - Fix compute offering selection not working |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4852`_ | Allow host cert renewals even if client auth strictness is |
|                         |          | false                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5393`_ | ui: Refresh page on deployvm result                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5373`_ | server: do not remove volume from DB if fail to expunge it |
|                         |          | from primary storage or secondary storage                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5335`_ | xcp-ng: allow passing vm boot options                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5349`_ | Fix of creating volumes from snapshots without backup to   |
|                         |          | secondary storage                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5366`_ | updated maven dependency due to #5363                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5385`_ | engine/schema: Use same upgrade path as 4.15.1-4.16.0 as   |
|                         |          | for 4.15.2                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5371`_ | server: improve attach volume in specific cases            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5311`_ | [VMware] Start VM with deploy-as-is template having        |
|                         |          | multiple controller types                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5377`_ | [VMware] Added Worker VM tags for few cloned VMs while     |
|                         |          | performing some volume operations.                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5368`_ | ui: Fix action bar in place                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5364`_ | server: allow destroy/recover volumes which are attached   |
|                         |          | to removed vms                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4701`_ | Added support for removing unused port groups on VMWare    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5384`_ | ubuntu: Fix failure to scp diagnostic data file from SSVM  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5356`_ | server: detach data disks before destroying vms            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#1257`_ | [VMware DRS] Adding new host to DRS cluster does not       |
|                         |          | participate in load balancing.                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5367`_ | ui: Fix search with same parameters                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5360`_ | ui: Go back for delete actions before querying async job   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5357`_ | Externalize VMWare stats time window config                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4570`_ | Externalize KVM Agent's option to change migration thread  |
|                         |          | timeout                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5187`_ | Added ability to create schemas only when using            |
|                         |          | cloudstack-setup-data…                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5319`_ | vr: reload dnsmasq when start vms                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5351`_ | Externalize vm stats increment in memory                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4662`_ | Feat/ram reservation                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5354`_ | Fix security_groups for c8/suse                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5359`_ | UI - Add storage name to delete primary/secondary storage  |
|                         |          | dialog                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5337`_ | Bypass empty string check for username and password        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5345`_ | UI - VM - hide button take vm volume snapshot for          |
|                         |          | Destroyed state                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5341`_ | remove doubles before save                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5355`_ | ui: Support to view template download progress across all  |
|                         |          | stores                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4586`_ | Externalize kvm agent storage reboot configuration         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4878`_ | Support vm dynamic scaling with kvm                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5321`_ | Remove storage scope validation on KVM live migration      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5194`_ | adapt condition to use the correct letter for pvlan types  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5331`_ | vr: cleanup files in /var/cache/cloud/processed every day  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5348`_ | security group: fix component test                         |
|                         |          | test_multiple_nic_support.py failures                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5328`_ | Fix iptable rules when chain reference count is 0          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5346`_ | test: Fix travis failure - test_outofbandmanagement.py     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4618`_ | Allow users to update volume name                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5342`_ | add license header in HostMetricsResponseTest.java         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5326`_ | ui: Update placeholders for adding new tier                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5110`_ | Adding SUSE 15 support                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5318`_ | Fix iptable rules in ubuntu 20 for bridge name             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5217`_ | Possiblity to choose between docker and podman from the    |
|                         |          | command line                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5329`_ | metrics: fix hostsmetricsresponse for zero cpu, locale     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5303`_ | UI - Zone wizard - Fixes wrong add resource step with      |
|                         |          | localstorageenabled                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5320`_ | server: use id column as secondary sort criteria with      |
|                         |          | sortKey                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5327`_ | s2svpn: Set initial state as Connecting                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5317`_ | systemvmtemplate: bump to Debian 11.0.0 systemvmtemplate   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5158`_ | Adding support for RHEL8 binary-compatible variants        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5323`_ | UI - systemVM - Fix error message `jobid` not found when   |
|                         |          | moving to another host                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5325`_ | ui (importUnmanagedInstance) : Show project list to which  |
|                         |          | the instance is to be imported                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4776`_ | Add sent and received bytes to listNetworks and            |
|                         |          | listVirtualMachines.                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4780`_ | Add SharedMountPoint to KVMs supported storage pool types  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4399`_ | PR multi tags in compute offering [#4398]                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5312`_ | Add missing command - syncStoragePool in main branch       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5304`_ | compatibility fix for Packer v1.7.4, update debian         |
|                         |          | template to 10.10.0                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5273`_ | Externalize config to enable manually setting CPU topology |
|                         |          | on KVM VM                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5258`_ | vmware: get recommended disk controller only when root or  |
|                         |          | data disk controller is osdefault                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5274`_ | db: make *_details.value non-nullable                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5242`_ | Add internal cs name to vm during the ingest               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4630`_ | disable hot add memory and cpu via vm settings             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5305`_ | Add missing labels and sort them                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4699`_ | Add new registers in guest_os                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5249`_ | Global setting to select preferred storage pool            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5052`_ | UI: Dark mode toggle button on Management Server           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5301`_ | ui: fix display host hypervisorversion                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5289`_ | test/vmware: add live migratevmwithvolume test and fix     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4885`_ | UI: Add multiple management server support                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5298`_ | UI - Fixes - Ctrl+Enter events error                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5299`_ | ui: Fix sending false for isdynamicallyscalable, haenable  |
|                         |          | in EditVM                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4378`_ | server: Optional destination host when migrate a vm        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5295`_ | ui: Prettify ManageInstances.vue                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5254`_ | kubernetes: Deploy kubernetes-provider when creating a     |
|                         |          | cluster                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4551`_ | Cleanup volume information from db when deleted            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4685`_ | Display last updated time for VM                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4737`_ | Change GET/POST request max length of VM user data to      |
|                         |          | 4K/1M                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5270`_ | server: skip zone check for PERHOST iso during attachIso   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5288`_ | Fix migration issue in                                     |
|                         |          | UserVmManagerImpl.migrateVirtualMachineWithVolume          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5287`_ | UI - Zone Wizard - Fixes the IP range form fields are too  |
|                         |          | narrow                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5282`_ | Fix regression on create volume from snapshot              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5275`_ | vr: restart conntrackd instead of '/usr/sbin/conntrackd    |
|                         |          | -d'                                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5292`_ | ui: Show host as unsecure in listview                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4111`_ | API-call to declare host as Degraded                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5269`_ | ui: fix capitalise filter                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5285`_ | ui: fix handle action API response                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5283`_ | ui: Fix failure in deletion of templates                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5278`_ | ui: Add 'on / off' to status icon and make it case         |
|                         |          | insensitive                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5272`_ | Add YouTube channel link in the README                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5262`_ | [TEST] - Test unit - Fix failing UI unit test main branch  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5257`_ | ui: fix import instance form for recent changes            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5043`_ | Allow updating the storage/host tags of service offerings  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5241`_ | Improve HA logs                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4714`_ | Cleaning up code and enhancing a few IP management logs    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5263`_ | ui: Fix failing UI                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5219`_ | [TEST] - Test unit - Fix failing UI unit test 4.15 branch  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5236`_ | server: fix VR health check in vmware basic zone           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5253`_ | UI -  zone wizard - change the argument of params.ipv6dns2 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5252`_ | ui: fix import instance form root disk label               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4257`_ | remove the unnecessary check for tags when migrating       |
|                         |          | volumes                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4768`_ | display nics deviceid and order nics by deviceid on Nics   |
|                         |          | tab of insta…                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5239`_ | Externalize KVM Agent storage's timeout configuration      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4959`_ | Improve logs on ConsoleProxyManagerImpl and refactor a few |
|                         |          | process                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5224`_ | ui: submit form with false boolean params                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5205`_ | ui: fix create shared network with multi-zone              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5231`_ | api: Fix pagination for list PublicIPAddresses             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5245`_ | ui: Update header notice if job failed                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5246`_ | ui: Fix comparator for boolean                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5247`_ | ui: Fix current for vmsnapshots                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5237`_ | [UI] Add Shift key for noVNC consoles                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5075`_ | ui: vmware vm import-unmanage                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4616`_ | Add logs to api removeVpnUser                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5225`_ | Fix of shrinking volumes with QCOW2 format                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4766`_ | UI: Submit the form when press CTRL + ENTER                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5233`_ | ui bug fix: scalevm is disabled when vm is Stopped         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5206`_ | UI: only display host information, if they are relevant    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5232`_ | ui: Fix refresh issue                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5186`_ | Remove condition that are prevent resizing for root        |
|                         |          | volumes (vmware)                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5119`_ | Externalize tls version and security protocols             |
|                         |          | configuration on mail sending                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5163`_ | add entity-type to message when no UUID is found for a DB  |
|                         |          | ID                                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5214`_ | ui: Refresh after async job completed only on current /    |
|                         |          | parent page                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5221`_ | ui: Fix async poll job                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5222`_ | ui: Replace bulk delete icons                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5210`_ | api: Add 'created' field to API response                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5218`_ | Revert "Externalize kvm agent storage timeout              |
|                         |          | configuration"                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4782`_ | UI: Refactor async job polling codebase-wide               |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4585`_ | Externalize kvm agent storage timeout configuration        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5213`_ | Do remove volume only on expunge                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4640`_ | Added disk provisioning type support for VMWare            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5034`_ | UI: bulk action support for various resources              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5211`_ | Fix deprecation of CIDR_LIST parameter                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4790`_ | Externalize secondary storage capacity threshold           |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5193`_ | kvm: pre-add 32 PCI controller for hot-plug issue on       |
|                         |          | ARM64/aarch64                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5012`_ | KVM NFS disk IO driver supporting IO_URING                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5073`_ | systemvmtemplate: use latest LTS kernel from buster-ports  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5184`_ | server: fix network access for addNicToVirtualMachine API  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5030`_ | refactor: migrate vm with storage                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5170`_ | vmware: fix migrate vm with volume                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5199`_ | UI: deploy VM - FIX missing custom iops field              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5197`_ | UI: fix NIC table on instance view                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5178`_ | [UI] zone wizard: change edit traffic type form of VMware  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5144`_ | configdrive: fix some failures in                          |
|                         |          | tests/component/test_configdrive.py                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5136`_ | apiserver : Ensure required parameters are not empty       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5064`_ | ui: refactor get api params in forms                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5133`_ | ui: refactor labels with tooltip in forms                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5182`_ | ui: Fix traversal to domain details via domain router-link |
|                         |          | of a resource                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4575`_ | Enhance log messages with host name                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5183`_ | expunge vm: Allow expunging a VM in destroyed state        |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5139`_ | marvin: make deployDataCenter.py script compatible with    |
|                         |          | python 2 and 3                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4037`_ | Document cidrlist parameter deprecation                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5165`_ | Prevent starting a VM in destroyed state (or any state but |
|                         |          | Stopped)                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5167`_ | UI - zone wizard - fix undefined property when setting RBD |
|                         |          | primary storage                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5176`_ | [UI] secondary storage - Display text and change the badge |
|                         |          | color of the Read-only column                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5173`_ | Some changes of the german translation                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5164`_ | kvm: fix VM HA on zone-wide storage pools                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5154`_ | Fix NPE when no recipients configured for sending alerts   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5142`_ | Fix NPE during removal of VM from Network                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5171`_ | Updated some offensive words in kubernetes plugin/service  |
|                         |          | with inclusive words/terms.                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5125`_ | volume: Fix deletion of Uploaded volumes                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4796`_ | db, server: refactor host_view to prevent duplicate        |
|                         |          | entries                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4843`_ | ui: deployvm - Add option to stay on page                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5162`_ | On Upgrade, Replace the DB properties having master and    |
|                         |          | slave(s), with source and replica(s) respectively for      |
|                         |          | inclusiveness                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5106`_ | tests: Fix test failures for Local storage and Basic zones |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5146`_ | (auto) formatting and cleanup fixes for test_volumes       |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5140`_ | Display proper names in error message                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#4886`_ | server: list routers by healthchecksfailed                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.16.0.0                | `#5128`_ | tests: Skip test_persistent_networks if kvm and ovs        |
+-------------------------+----------+------------------------------------------------------------+

328 Issues listed

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
.. _`#5435`: https://github.com/apache/cloudstack/pull/5435 
.. _`#5432`: https://github.com/apache/cloudstack/pull/5432 
.. _`#5427`: https://github.com/apache/cloudstack/pull/5427 
.. _`#5431`: https://github.com/apache/cloudstack/pull/5431 
.. _`#5429`: https://github.com/apache/cloudstack/pull/5429 
.. _`#5398`: https://github.com/apache/cloudstack/pull/5398 
.. _`#5358`: https://github.com/apache/cloudstack/pull/5358 
.. _`#5416`: https://github.com/apache/cloudstack/pull/5416 
.. _`#5067`: https://github.com/apache/cloudstack/pull/5067 
.. _`#3975`: https://github.com/apache/cloudstack/pull/3975 
.. _`#5103`: https://github.com/apache/cloudstack/pull/5103 
.. _`#5401`: https://github.com/apache/cloudstack/pull/5401 
.. _`#5396`: https://github.com/apache/cloudstack/pull/5396 
.. _`#5390`: https://github.com/apache/cloudstack/pull/5390 
.. _`#4534`: https://github.com/apache/cloudstack/pull/4534 
.. _`#5402`: https://github.com/apache/cloudstack/pull/5402 
.. _`#5387`: https://github.com/apache/cloudstack/pull/5387 
.. _`#5408`: https://github.com/apache/cloudstack/pull/5408 
.. _`#5066`: https://github.com/apache/cloudstack/pull/5066 
.. _`#5404`: https://github.com/apache/cloudstack/pull/5404 
.. _`#5394`: https://github.com/apache/cloudstack/pull/5394 
.. _`#5259`: https://github.com/apache/cloudstack/pull/5259 
.. _`#5307`: https://github.com/apache/cloudstack/pull/5307 
.. _`#5339`: https://github.com/apache/cloudstack/pull/5339 
.. _`#5333`: https://github.com/apache/cloudstack/pull/5333 
.. _`#5403`: https://github.com/apache/cloudstack/pull/5403 
.. _`#5082`: https://github.com/apache/cloudstack/pull/5082 
.. _`#5399`: https://github.com/apache/cloudstack/pull/5399 
.. _`#5376`: https://github.com/apache/cloudstack/pull/5376 
.. _`#5375`: https://github.com/apache/cloudstack/pull/5375 
.. _`#5374`: https://github.com/apache/cloudstack/pull/5374 
.. _`#5379`: https://github.com/apache/cloudstack/pull/5379 
.. _`#5380`: https://github.com/apache/cloudstack/pull/5380 
.. _`#5392`: https://github.com/apache/cloudstack/pull/5392 
.. _`#4852`: https://github.com/apache/cloudstack/pull/4852 
.. _`#5393`: https://github.com/apache/cloudstack/pull/5393 
.. _`#5373`: https://github.com/apache/cloudstack/pull/5373 
.. _`#5335`: https://github.com/apache/cloudstack/pull/5335 
.. _`#5349`: https://github.com/apache/cloudstack/pull/5349 
.. _`#5366`: https://github.com/apache/cloudstack/pull/5366 
.. _`#5385`: https://github.com/apache/cloudstack/pull/5385 
.. _`#5371`: https://github.com/apache/cloudstack/pull/5371 
.. _`#5311`: https://github.com/apache/cloudstack/pull/5311 
.. _`#5377`: https://github.com/apache/cloudstack/pull/5377 
.. _`#5368`: https://github.com/apache/cloudstack/pull/5368 
.. _`#5364`: https://github.com/apache/cloudstack/pull/5364 
.. _`#4701`: https://github.com/apache/cloudstack/pull/4701 
.. _`#5384`: https://github.com/apache/cloudstack/pull/5384 
.. _`#5356`: https://github.com/apache/cloudstack/pull/5356 
.. _`#1257`: https://github.com/apache/cloudstack/pull/1257 
.. _`#5367`: https://github.com/apache/cloudstack/pull/5367 
.. _`#5360`: https://github.com/apache/cloudstack/pull/5360 
.. _`#5357`: https://github.com/apache/cloudstack/pull/5357 
.. _`#4570`: https://github.com/apache/cloudstack/pull/4570 
.. _`#5187`: https://github.com/apache/cloudstack/pull/5187 
.. _`#5319`: https://github.com/apache/cloudstack/pull/5319 
.. _`#5351`: https://github.com/apache/cloudstack/pull/5351 
.. _`#4662`: https://github.com/apache/cloudstack/pull/4662 
.. _`#5354`: https://github.com/apache/cloudstack/pull/5354 
.. _`#5359`: https://github.com/apache/cloudstack/pull/5359 
.. _`#5337`: https://github.com/apache/cloudstack/pull/5337 
.. _`#5345`: https://github.com/apache/cloudstack/pull/5345 
.. _`#5341`: https://github.com/apache/cloudstack/pull/5341 
.. _`#5355`: https://github.com/apache/cloudstack/pull/5355 
.. _`#4586`: https://github.com/apache/cloudstack/pull/4586 
.. _`#4878`: https://github.com/apache/cloudstack/pull/4878 
.. _`#5321`: https://github.com/apache/cloudstack/pull/5321 
.. _`#5194`: https://github.com/apache/cloudstack/pull/5194 
.. _`#5331`: https://github.com/apache/cloudstack/pull/5331 
.. _`#5348`: https://github.com/apache/cloudstack/pull/5348 
.. _`#5328`: https://github.com/apache/cloudstack/pull/5328 
.. _`#5346`: https://github.com/apache/cloudstack/pull/5346 
.. _`#4618`: https://github.com/apache/cloudstack/pull/4618 
.. _`#5342`: https://github.com/apache/cloudstack/pull/5342 
.. _`#5326`: https://github.com/apache/cloudstack/pull/5326 
.. _`#5110`: https://github.com/apache/cloudstack/pull/5110 
.. _`#5318`: https://github.com/apache/cloudstack/pull/5318 
.. _`#5217`: https://github.com/apache/cloudstack/pull/5217 
.. _`#5329`: https://github.com/apache/cloudstack/pull/5329 
.. _`#5303`: https://github.com/apache/cloudstack/pull/5303 
.. _`#5320`: https://github.com/apache/cloudstack/pull/5320 
.. _`#5327`: https://github.com/apache/cloudstack/pull/5327 
.. _`#5317`: https://github.com/apache/cloudstack/pull/5317 
.. _`#5158`: https://github.com/apache/cloudstack/pull/5158 
.. _`#5323`: https://github.com/apache/cloudstack/pull/5323 
.. _`#5325`: https://github.com/apache/cloudstack/pull/5325 
.. _`#4776`: https://github.com/apache/cloudstack/pull/4776 
.. _`#4780`: https://github.com/apache/cloudstack/pull/4780 
.. _`#4399`: https://github.com/apache/cloudstack/pull/4399 
.. _`#5312`: https://github.com/apache/cloudstack/pull/5312 
.. _`#5304`: https://github.com/apache/cloudstack/pull/5304 
.. _`#5273`: https://github.com/apache/cloudstack/pull/5273 
.. _`#5258`: https://github.com/apache/cloudstack/pull/5258 
.. _`#5274`: https://github.com/apache/cloudstack/pull/5274 
.. _`#5242`: https://github.com/apache/cloudstack/pull/5242 
.. _`#4630`: https://github.com/apache/cloudstack/pull/4630 
.. _`#5305`: https://github.com/apache/cloudstack/pull/5305 
.. _`#4699`: https://github.com/apache/cloudstack/pull/4699 
.. _`#5249`: https://github.com/apache/cloudstack/pull/5249 
.. _`#5052`: https://github.com/apache/cloudstack/pull/5052 
.. _`#5301`: https://github.com/apache/cloudstack/pull/5301 
.. _`#5289`: https://github.com/apache/cloudstack/pull/5289 
.. _`#4885`: https://github.com/apache/cloudstack/pull/4885 
.. _`#5298`: https://github.com/apache/cloudstack/pull/5298 
.. _`#5299`: https://github.com/apache/cloudstack/pull/5299 
.. _`#4378`: https://github.com/apache/cloudstack/pull/4378 
.. _`#5295`: https://github.com/apache/cloudstack/pull/5295 
.. _`#5254`: https://github.com/apache/cloudstack/pull/5254 
.. _`#4551`: https://github.com/apache/cloudstack/pull/4551 
.. _`#4685`: https://github.com/apache/cloudstack/pull/4685 
.. _`#4737`: https://github.com/apache/cloudstack/pull/4737 
.. _`#5270`: https://github.com/apache/cloudstack/pull/5270 
.. _`#5288`: https://github.com/apache/cloudstack/pull/5288 
.. _`#5287`: https://github.com/apache/cloudstack/pull/5287 
.. _`#5282`: https://github.com/apache/cloudstack/pull/5282 
.. _`#5275`: https://github.com/apache/cloudstack/pull/5275 
.. _`#5292`: https://github.com/apache/cloudstack/pull/5292 
.. _`#4111`: https://github.com/apache/cloudstack/pull/4111 
.. _`#5269`: https://github.com/apache/cloudstack/pull/5269 
.. _`#5285`: https://github.com/apache/cloudstack/pull/5285 
.. _`#5283`: https://github.com/apache/cloudstack/pull/5283 
.. _`#5278`: https://github.com/apache/cloudstack/pull/5278 
.. _`#5272`: https://github.com/apache/cloudstack/pull/5272 
.. _`#5262`: https://github.com/apache/cloudstack/pull/5262 
.. _`#5257`: https://github.com/apache/cloudstack/pull/5257 
.. _`#5043`: https://github.com/apache/cloudstack/pull/5043 
.. _`#5241`: https://github.com/apache/cloudstack/pull/5241 
.. _`#4714`: https://github.com/apache/cloudstack/pull/4714 
.. _`#5263`: https://github.com/apache/cloudstack/pull/5263 
.. _`#5219`: https://github.com/apache/cloudstack/pull/5219 
.. _`#5236`: https://github.com/apache/cloudstack/pull/5236 
.. _`#5253`: https://github.com/apache/cloudstack/pull/5253 
.. _`#5252`: https://github.com/apache/cloudstack/pull/5252 
.. _`#4257`: https://github.com/apache/cloudstack/pull/4257 
.. _`#4768`: https://github.com/apache/cloudstack/pull/4768 
.. _`#5239`: https://github.com/apache/cloudstack/pull/5239 
.. _`#4959`: https://github.com/apache/cloudstack/pull/4959 
.. _`#5224`: https://github.com/apache/cloudstack/pull/5224 
.. _`#5205`: https://github.com/apache/cloudstack/pull/5205 
.. _`#5231`: https://github.com/apache/cloudstack/pull/5231 
.. _`#5245`: https://github.com/apache/cloudstack/pull/5245 
.. _`#5246`: https://github.com/apache/cloudstack/pull/5246 
.. _`#5247`: https://github.com/apache/cloudstack/pull/5247 
.. _`#5237`: https://github.com/apache/cloudstack/pull/5237 
.. _`#5075`: https://github.com/apache/cloudstack/pull/5075 
.. _`#4616`: https://github.com/apache/cloudstack/pull/4616 
.. _`#5225`: https://github.com/apache/cloudstack/pull/5225 
.. _`#4766`: https://github.com/apache/cloudstack/pull/4766 
.. _`#5233`: https://github.com/apache/cloudstack/pull/5233 
.. _`#5206`: https://github.com/apache/cloudstack/pull/5206 
.. _`#5232`: https://github.com/apache/cloudstack/pull/5232 
.. _`#5186`: https://github.com/apache/cloudstack/pull/5186 
.. _`#5149`: https://github.com/apache/cloudstack/pull/5149 
.. _`#5119`: https://github.com/apache/cloudstack/pull/5119 
.. _`#5163`: https://github.com/apache/cloudstack/pull/5163 
.. _`#5214`: https://github.com/apache/cloudstack/pull/5214 
.. _`#5221`: https://github.com/apache/cloudstack/pull/5221 
.. _`#5222`: https://github.com/apache/cloudstack/pull/5222 
.. _`#5210`: https://github.com/apache/cloudstack/pull/5210 
.. _`#5218`: https://github.com/apache/cloudstack/pull/5218 
.. _`#4782`: https://github.com/apache/cloudstack/pull/4782 
.. _`#4585`: https://github.com/apache/cloudstack/pull/4585 
.. _`#5213`: https://github.com/apache/cloudstack/pull/5213 
.. _`#4640`: https://github.com/apache/cloudstack/pull/4640 
.. _`#5034`: https://github.com/apache/cloudstack/pull/5034 
.. _`#5211`: https://github.com/apache/cloudstack/pull/5211 
.. _`#4790`: https://github.com/apache/cloudstack/pull/4790 
.. _`#5193`: https://github.com/apache/cloudstack/pull/5193 
.. _`#5012`: https://github.com/apache/cloudstack/pull/5012 
.. _`#5073`: https://github.com/apache/cloudstack/pull/5073 
.. _`#5184`: https://github.com/apache/cloudstack/pull/5184 
.. _`#5030`: https://github.com/apache/cloudstack/pull/5030 
.. _`#5170`: https://github.com/apache/cloudstack/pull/5170 
.. _`#5199`: https://github.com/apache/cloudstack/pull/5199 
.. _`#5197`: https://github.com/apache/cloudstack/pull/5197 
.. _`#5178`: https://github.com/apache/cloudstack/pull/5178 
.. _`#5144`: https://github.com/apache/cloudstack/pull/5144 
.. _`#5136`: https://github.com/apache/cloudstack/pull/5136 
.. _`#5064`: https://github.com/apache/cloudstack/pull/5064 
.. _`#5133`: https://github.com/apache/cloudstack/pull/5133 
.. _`#5182`: https://github.com/apache/cloudstack/pull/5182 
.. _`#4575`: https://github.com/apache/cloudstack/pull/4575 
.. _`#5183`: https://github.com/apache/cloudstack/pull/5183 
.. _`#5139`: https://github.com/apache/cloudstack/pull/5139 
.. _`#4037`: https://github.com/apache/cloudstack/pull/4037 
.. _`#5165`: https://github.com/apache/cloudstack/pull/5165 
.. _`#5167`: https://github.com/apache/cloudstack/pull/5167 
.. _`#5176`: https://github.com/apache/cloudstack/pull/5176 
.. _`#5173`: https://github.com/apache/cloudstack/pull/5173 
.. _`#5164`: https://github.com/apache/cloudstack/pull/5164 
.. _`#5154`: https://github.com/apache/cloudstack/pull/5154 
.. _`#5142`: https://github.com/apache/cloudstack/pull/5142 
.. _`#5171`: https://github.com/apache/cloudstack/pull/5171 
.. _`#5125`: https://github.com/apache/cloudstack/pull/5125 
.. _`#4796`: https://github.com/apache/cloudstack/pull/4796 
.. _`#4843`: https://github.com/apache/cloudstack/pull/4843 
.. _`#5162`: https://github.com/apache/cloudstack/pull/5162 
.. _`#5106`: https://github.com/apache/cloudstack/pull/5106 
.. _`#5146`: https://github.com/apache/cloudstack/pull/5146 
.. _`#5140`: https://github.com/apache/cloudstack/pull/5140 
.. _`#4886`: https://github.com/apache/cloudstack/pull/4886 
.. _`#5128`: https://github.com/apache/cloudstack/pull/5128 
