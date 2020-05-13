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

Issues Fixed in 4.13.1.0
========================


Issues Fixed in 4.13.1.0
------------------------

.. cssclass:: table-striped table-bordered table-hover

+-------------------------+----------+------------------------------------------------------------+
| Version                 | Github   | Description                                                |
+=========================+==========+============================================================+
| 4.13.1.0                | `#4042`_ | Fixed guest vlan range going missing when using zone       |
|                         |          | wizard                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#4043`_ | Volume deleted during cold migration if Secondary Storage  |
|                         |          | over 90% full                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#4033`_ | kvm: suspend/resume in deleting vm snapshot on kvm         |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3969`_ | Snapshot deletion issues                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#4025`_ | server: Cannot list affinity group if there are hosts      |
|                         |          | dedicated to domain                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#4002`_ | server: Search zone-wide storage pool when allocation      |
|                         |          | algothrim is firstfitleastconsumed                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#4005`_ | Fixed create template from snapshot never returning        |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3995`_ | UI bug fix: Cannot deploy VM from ISO                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3993`_ | Fixes raw templates not downloading                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3977`_ | With basic zone and VMware hypervisor, VR fails to start   |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3973`_ | systemd dependency on db                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3989`_ | server: export full response view for zones response for   |
|                         |          | root admin                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3971`_ | Updated upgrade path                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3932`_ | Prevent overflow on StatsCollector.java                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3948`_ | server: password is not displayed when reinstall a vm or   |
|                         |          | reset ssh key                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3943`_ | vr: fix password server run with empty gateway in isolated |
|                         |          | network with RVRs                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3651`_ | Fix simulator docker db deploy issue (apache#3397)         |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3947`_ | server: fix database exception while searching network     |
|                         |          | offerings                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3935`_ | Fix VM with ISO attached migration issue                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3924`_ | Fixed error on data volumes lager than 2.14TB when         |
|                         |          | creating instances on VMware                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3911`_ | kvm: fix/optimize propogating configs                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3847`_ | VR: Fix Redundant VRouter guest network on wrong interface |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3898`_ | vrouter: reload keepalived instead of restart and fix      |
|                         |          | password server issues when add/remove vpc tier            |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3907`_ | Allow port 80/8080 accessible only from guest network      |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3916`_ | server: fix issue while list ssh keypairs by keyword       |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3913`_ | Fix dhcp infinite lease time                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3904`_ | Avoid duplicate alerts when router state changes           |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3903`_ | VR: Send VM password to all Running VRs in network/vpc     |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3894`_ | api: Fix count and item issues returned by list APIs       |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3905`_ | Fix network rules issue if default egress policy is Allow  |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3491`_ | KVM: Propagating changes on host parameters to the agents  |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3879`_ | kvm: Enable virtio drivers based on guest os display name  |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3884`_ | kvm: fix exception in volume stats after storage migration |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3864`_ | Ignore site to site vpn status check on internallbvm       |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3871`_ | Fixed duplicate id error when creating VM work jobs        |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3873`_ | Fixed root volume resize from ui                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3876`_ | server: use host record related to a ssvm/cpvm             |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3870`_ | systemvm: list systemvm does not return agent state and    |
|                         |          | version                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3854`_ | Install python-dnspython or python-dns to fix issue with   |
|                         |          | cloudstack-setup-management                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3865`_ | Fixed default text missing from network selection on       |
|                         |          | instance wizard                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3857`_ | vr: add missing rule for port forwarding rule in vpc       |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3851`_ | vpc: set traffic type of private gateway IP to Public to   |
|                         |          | fix keepalived misconfiguration                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3867`_ | Usage event to store zone id while uploading template and  |
|                         |          | volume                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3861`_ | test: check more connectivity in test_privategw_acl.py     |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3803`_ | Bug fix : set restart_required to 0 after restarting       |
|                         |          | network                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3791`_ | server: fix checking disk offering access for snapshot     |
|                         |          | volume                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3832`_ | ui bug fix: cannot assign vms to internal lb in VPC        |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3855`_ | kvm: Fix router migration issue when router has            |
|                         |          | control/public nics onother physical network than guest    |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3383`_ | template: copy md5 mismatch                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3819`_ | Clean up inactive iscsi sessions when VMs get moved due to |
|                         |          | crashes                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3604`_ | Fix Policy Based Routing for private gateway static routes |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3840`_ | Fix listing management server by parameters                |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3834`_ | Fix: The metrics view API response is not super-set of     |
|                         |          | resources response keys                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3848`_ | vr: fix vr in unknown state (more)                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3726`_ | vrouter: reload haproxy when cfg file is updated           |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3846`_ | Fix for "Impossible to edit domain settings in UI"         |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3845`_ | travis: use https based maven repo mirror                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3761`_ | [FIX] [BACKPORT] [4.13] Rethrow takeVMSnapshot() exception |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3758`_ | server: Fix NPE while update displayvm on vm with dynamic  |
|                         |          | service offering                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3728`_ | server: double check host capacity when start/migrate a vm |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3727`_ | server: Capacity check should take vms in Migrating state  |
|                         |          | into calculation                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3477`_ | RvR: Set up metadata/password/dhcp server on gateway IP    |
|                         |          | instead of guest IP in RVR                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3825`_ | fixed inconsistency of IP on VR when VR is destroyed and   |
|                         |          | recrea…                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3759`_ | server: fix resource count error when upgrade a vm         |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3806`_ | python/c++ formatting in java corrected                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3795`_ | Agent lb on svm                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3776`_ | Add missing HA config keys                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3778`_ | Endless settings on templates and instances                |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3743`_ | only update powerstate if sure it is the latest            |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3682`_ | ui: fix migrate host form no host popup                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3658`_ | client: fix for jetty session timeout                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3662`_ | Increase DHCP lease time to infinite                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3793`_ | ui: fix for truncated name for project accounts            |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3597`_ | kvm: Logrotate should not touch agent.log                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3721`_ | network: cleanup dhcp/dns entries while remove a nic from  |
|                         |          | vm                                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3715`_ | break session only on illegal origin                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3755`_ | Added zone check for attach iso                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3729`_ | config: add isdynamic flag in configuration response       |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3733`_ | filter hosts to query on zone wide storage                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3747`_ | convert protocal names to be found as labels               |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3754`_ | Once again allow a VM to be on multiple networks from VPCs |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3767`_ | create template from snapshot regression (partly reverted) |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3765`_ | Honour promiscuous mode from networkOffering               |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3617`_ | [KVM] Agent LB Fix: Connections from disabled KVM host     |
|                         |          | agents are refused                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3640`_ | consoleproxy: Enable console for vms in Stopping/Migrating |
|                         |          | state                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3635`_ | server: acquire IPv4 address when add secondary IP to nic  |
|                         |          | if IP is not specified                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3636`_ | kvm: fix issue that network rules for secondary IPs are    |
|                         |          | not applied                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3678`_ | vpc: fix acl rule with protocol number is not applied      |
|                         |          | correctly in vpc vr                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3605`_ | fix issue #3590 'Revert Ceph/RBD Snapshot'                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3612`_ | systemvm: for ip route show command don't use the throw    |
|                         |          | command                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3666`_ | snapshot failure diagnostics unhidden                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3620`_ | Small additional NuageVsp cleanups (#3146)                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3648`_ | Security Group: limit returns in get_bridge_physdev to 1   |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3627`_ | server: Do NOT cleanup dhcp and dns when stop a vm         |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3608`_ | server: Cleanup dhcp and dns entries only on expunging VM  |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3574`_ | `service is-active` output check for "failed"              |
+-------------------------+----------+------------------------------------------------------------+
| 4.13.1.0                | `#3582`_ | systemvmtemplate: Fix Debian 9 iso url                     |
+-------------------------+----------+------------------------------------------------------------+
97 Issues listed

.. _`#4042`: https://github.com/apache/cloudstack/pull/4042
.. _`#4043`: https://github.com/apache/cloudstack/pull/4043
.. _`#4033`: https://github.com/apache/cloudstack/pull/4033
.. _`#3969`: https://github.com/apache/cloudstack/pull/3969
.. _`#4025`: https://github.com/apache/cloudstack/pull/4025
.. _`#4002`: https://github.com/apache/cloudstack/pull/4002
.. _`#4005`: https://github.com/apache/cloudstack/pull/4005
.. _`#3995`: https://github.com/apache/cloudstack/pull/3995
.. _`#3993`: https://github.com/apache/cloudstack/pull/3993
.. _`#3977`: https://github.com/apache/cloudstack/pull/3977
.. _`#3973`: https://github.com/apache/cloudstack/pull/3973
.. _`#3989`: https://github.com/apache/cloudstack/pull/3989
.. _`#3971`: https://github.com/apache/cloudstack/pull/3971
.. _`#3932`: https://github.com/apache/cloudstack/pull/3932
.. _`#3948`: https://github.com/apache/cloudstack/pull/3948
.. _`#3943`: https://github.com/apache/cloudstack/pull/3943
.. _`#3651`: https://github.com/apache/cloudstack/pull/3651
.. _`#3947`: https://github.com/apache/cloudstack/pull/3947
.. _`#3935`: https://github.com/apache/cloudstack/pull/3935
.. _`#3924`: https://github.com/apache/cloudstack/pull/3924
.. _`#3911`: https://github.com/apache/cloudstack/pull/3911
.. _`#3847`: https://github.com/apache/cloudstack/pull/3847
.. _`#3898`: https://github.com/apache/cloudstack/pull/3898
.. _`#3907`: https://github.com/apache/cloudstack/pull/3907
.. _`#3916`: https://github.com/apache/cloudstack/pull/3916
.. _`#3913`: https://github.com/apache/cloudstack/pull/3913
.. _`#3904`: https://github.com/apache/cloudstack/pull/3904
.. _`#3903`: https://github.com/apache/cloudstack/pull/3903
.. _`#3894`: https://github.com/apache/cloudstack/pull/3894
.. _`#3905`: https://github.com/apache/cloudstack/pull/3905
.. _`#3491`: https://github.com/apache/cloudstack/pull/3491
.. _`#3879`: https://github.com/apache/cloudstack/pull/3879
.. _`#3884`: https://github.com/apache/cloudstack/pull/3884
.. _`#3864`: https://github.com/apache/cloudstack/pull/3864
.. _`#3871`: https://github.com/apache/cloudstack/pull/3871
.. _`#3873`: https://github.com/apache/cloudstack/pull/3873
.. _`#3876`: https://github.com/apache/cloudstack/pull/3876
.. _`#3870`: https://github.com/apache/cloudstack/pull/3870
.. _`#3854`: https://github.com/apache/cloudstack/pull/3854
.. _`#3865`: https://github.com/apache/cloudstack/pull/3865
.. _`#3857`: https://github.com/apache/cloudstack/pull/3857
.. _`#3851`: https://github.com/apache/cloudstack/pull/3851
.. _`#3867`: https://github.com/apache/cloudstack/pull/3867
.. _`#3861`: https://github.com/apache/cloudstack/pull/3861
.. _`#3803`: https://github.com/apache/cloudstack/pull/3803
.. _`#3791`: https://github.com/apache/cloudstack/pull/3791
.. _`#3832`: https://github.com/apache/cloudstack/pull/3832
.. _`#3855`: https://github.com/apache/cloudstack/pull/3855
.. _`#3383`: https://github.com/apache/cloudstack/pull/3383
.. _`#3819`: https://github.com/apache/cloudstack/pull/3819
.. _`#3604`: https://github.com/apache/cloudstack/pull/3604
.. _`#3840`: https://github.com/apache/cloudstack/pull/3840
.. _`#3834`: https://github.com/apache/cloudstack/pull/3834
.. _`#3848`: https://github.com/apache/cloudstack/pull/3848
.. _`#3726`: https://github.com/apache/cloudstack/pull/3726
.. _`#3846`: https://github.com/apache/cloudstack/pull/3846
.. _`#3845`: https://github.com/apache/cloudstack/pull/3845
.. _`#3761`: https://github.com/apache/cloudstack/pull/3761
.. _`#3758`: https://github.com/apache/cloudstack/pull/3758
.. _`#3728`: https://github.com/apache/cloudstack/pull/3728
.. _`#3727`: https://github.com/apache/cloudstack/pull/3727
.. _`#3477`: https://github.com/apache/cloudstack/pull/3477
.. _`#3825`: https://github.com/apache/cloudstack/pull/3825
.. _`#3759`: https://github.com/apache/cloudstack/pull/3759
.. _`#3806`: https://github.com/apache/cloudstack/pull/3806
.. _`#3795`: https://github.com/apache/cloudstack/pull/3795
.. _`#3776`: https://github.com/apache/cloudstack/pull/3776
.. _`#3778`: https://github.com/apache/cloudstack/pull/3778
.. _`#3743`: https://github.com/apache/cloudstack/pull/3743
.. _`#3682`: https://github.com/apache/cloudstack/pull/3682
.. _`#3658`: https://github.com/apache/cloudstack/pull/3658
.. _`#3662`: https://github.com/apache/cloudstack/pull/3662
.. _`#3793`: https://github.com/apache/cloudstack/pull/3793
.. _`#3597`: https://github.com/apache/cloudstack/pull/3597
.. _`#3721`: https://github.com/apache/cloudstack/pull/3721
.. _`#3715`: https://github.com/apache/cloudstack/pull/3715
.. _`#3755`: https://github.com/apache/cloudstack/pull/3755
.. _`#3729`: https://github.com/apache/cloudstack/pull/3729
.. _`#3733`: https://github.com/apache/cloudstack/pull/3733
.. _`#3747`: https://github.com/apache/cloudstack/pull/3747
.. _`#3754`: https://github.com/apache/cloudstack/pull/3754
.. _`#3767`: https://github.com/apache/cloudstack/pull/3767
.. _`#3765`: https://github.com/apache/cloudstack/pull/3765
.. _`#3617`: https://github.com/apache/cloudstack/pull/3617
.. _`#3640`: https://github.com/apache/cloudstack/pull/3640
.. _`#3635`: https://github.com/apache/cloudstack/pull/3635
.. _`#3636`: https://github.com/apache/cloudstack/pull/3636
.. _`#3678`: https://github.com/apache/cloudstack/pull/3678
.. _`#3605`: https://github.com/apache/cloudstack/pull/3605
.. _`#3612`: https://github.com/apache/cloudstack/pull/3612
.. _`#3666`: https://github.com/apache/cloudstack/pull/3666
.. _`#3620`: https://github.com/apache/cloudstack/pull/3620
.. _`#3648`: https://github.com/apache/cloudstack/pull/3648
.. _`#3627`: https://github.com/apache/cloudstack/pull/3627
.. _`#3608`: https://github.com/apache/cloudstack/pull/3608
.. _`#3574`: https://github.com/apache/cloudstack/pull/3574
.. _`#3582`: https://github.com/apache/cloudstack/pull/3582

Changes in 4.13.0.0 since 4.12.0.0
===================================


.. cssclass:: table-striped table-bordered table-hover


+-----------+----------+--------------------------------------------------------------------------------+
| Version   | Github   | Description                                                                    |
+===========+==========+================================================================================+
| 4.13.0.0  | `#3574`_ | `service is-active` output check for "failed"                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3519`_ | kvm/cloudstack-guest-tool: Tool to query Qemu Guest Agent                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3582`_ | systemvmtemplate: Fix Debian 9 iso url                                         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3571`_ | Unable to deploy VMs via UI in advanced networks with SG and IPv6 cidr         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3567`_ | fix xenserver 7.1.0 os mapping typo                                            |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3566`_ | server: fix NPE for the case where volume is not attached to a VM              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3564`_ | add vSphere 6.7.3 and update 6.7.2 & 6.7.1                                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3560`_ | Display VM snapshot tags on usage records                                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3549`_ | add detailed hypervisor and guest OS data                                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3551`_ | Prevent NullPointer on a network with removed IP ranges/"VLANs"                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3547`_ | 4.13/master stabilisation PR                                                   |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3271`_ | VMware: Allow configuring appliances on the VM instance wizard when OVF        |
|           |          | properties are available                                                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3545`_ | ui: fix for custom constrained offering params range check                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3533`_ | KVM local migration issue #3521                                                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3537`_ | Revert #3152                                                                   |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3535`_ | Misc fixes to sharing templates functionality                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3534`_ | Misc fixes around API permissions, global settings and template UX             |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3480`_ | engine, server, services: fix for respecting secondary storage threshold limit |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3529`_ | Add size to list usage records for VMSnapShotOnPrimary (type 27)               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3528`_ | [UI] Improve visibility of dropdown menus on dialogs                           |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3524`_ | Fix VR bootstrapping/connection state in KVM                                   |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3152`_ | Refactoring to remove duplicate code.                                          |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3470`_ | Datera storage plugin                                                          |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3500`_ | kvm/bridge: Allow Link Local Cidr (cloud0 interface) to be configured          |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3492`_ | remove depcrecated pip option --allow-external                                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3486`_ | filter volumes by host when refreshing stats                                   |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3511`_ | [Vmware] Fix bad ovf null error when registering template                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3502`_ | Rbd snapshot rollback                                                          |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3501`_ | Fix stop VM issue on basic zones                                               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3430`_ | server: fix the subnet overlap checking logic for tagged and untagged vlans    |
|           |          | when adding ipranges                                                           |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3494`_ | Fix hardcoded max data volumes when VM has been created but not started before |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3473`_ | vmware: fix volume stats logic                                                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3504`_ | Set integration.api.port to 0 (zero) as default.                               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3374`_ | KVM: Enhancements for direct download feature                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3495`_ | UI: Fix SystemVMs public range dedication                                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3248`_ | Enable service offerings to be scoped to domain(s) and zone(s)                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3489`_ | server: fix public IP association/disassociation to new network                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3454`_ | Add support for new heuristics based VM Deployement for admins                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3476`_ | master: travis and trillian smoketests fixes and stabilisation                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3483`_ | api: fix account deletion event description                                    |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3319`_ | Use IDE as the bus type for root disks and VIRTIO for data disks on platforms  |
|           |          | without support for para virtualization when using managed storage             |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3479`_ | ui: fix custom offerings selection in upload volume form                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3465`_ | vr: Fix vpc router in UNKNOWN state                                            |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3475`_ | Allowing template owner to download template                                   |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3457`_ | Fix bug in counting items for search query                                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3393`_ | Fix removing SRX port forwarding rules, improve add/remove logic               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3468`_ | network: allow icmp code 16 in firewall rules                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3297`_ | Support copy tags from template/iso image to VM from deploy vm command         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3472`_ | travis: use explicit change directory and use -pl to build rat check           |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3467`_ | schema: add support for XenServer 7.1.2 (LTS)                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3463`_ | quota: fix issue of QuotaType name                                             |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3331`_ | api/server: Add option 'details' to listProjects and listAccounts              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3462`_ | Count Starting along with Running VMs for user dispersing planner              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3466`_ | travis: use openjdk8 and xenial (ubuntu 16.04)                                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3412`_ | Allow for the VM Hostname to be edited  when VM is switched off                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3336`_ | Sort list of templates, serviceOfferings, diskOfferings etc in the deploy VM   |
|           |          | wizard                                                                         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3306`_ | server: reduce execution time while listing project if projects have many      |
|           |          | resource tags                                                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3451`_ | [UI] Fix wrap text for accounts on project view                                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3449`_ | utils: reverse ip addresses of a nic returned by java to get the first ip      |
|           |          | address                                                                        |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3445`_ | Fix sorting order bug in UI Code with usage of sortkey.algorithm global config |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3435`_ | ui: don't pass account name when in project mode to VMs from sshkeypair        |
|           |          | reference                                                                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3437`_ | systemvm: don't fork to curl to save password                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3421`_ | RvR: VPC redundant vrs run on same hypervisor                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3436`_ | debian: install `file` as cloudstack-management dependency                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3438`_ | ui: fix LB protocol bug                                                        |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3441`_ | Bug fix for distinting between string and map type tags in forms               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3431`_ | Readd custom css                                                               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3432`_ | Remove additional line from config as storagepool isn't available for users    |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3427`_ | engine/schema: add guest-os support and mappings for XenServer 7.6             |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3429`_ | Update config file with tables that users can see                              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3228`_ | api: snapshot, snapshotpolicy tag support                                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3259`_ | server: export granular volume bytes and iops metrics                          |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3240`_ | api: instance and template details are free text                               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3424`_ | KVM Volumes: Limit migration of volumes within the same storage pool.          |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3419`_ | console-proxy: fix potential NPE condition                                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3420`_ | ssvm: use secstorage.ssl.cert.domain as hostname if it does not start with '*' |
|           |          | when upload a template or volume from local                                    |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3422`_ | Fix hostname is localhost in some VRs                                          |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3126`_ | Improve System VM startup and memory usage                                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3418`_ | server: fix potential NPE while ldap authentication                            |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3268`_ | Support sort_key for vpc_offerings table                                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3423`_ | api: Fix API argument documentation to list supported protocols                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3246`_ | server: allow disk offering selection for volume from snapshot                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3406`_ | Add new way to create a volume snapshot from instance quick view tooltip       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3365`_ | KVM: DPDK live migrations                                                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3413`_ | vmware: add support for VMware 6.7                                             |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3415`_ | Fix interval descrption                                                        |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3414`_ | Increase z-index for install-wizard step                                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3219`_ | server: publish volume resize event for volumes                                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3344`_ | server: return usage description with resource names and UUIDs                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3234`_ | api: Set network name as part of the network usage response                    |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3242`_ | server: add support for sorting zones in UI/API                                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3222`_ | volume: fix volume metrics view from returning sensitive info to end user      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3384`_ | Minor: Add .vscode to .gitignore                                               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3235`_ | network: allow ability to specify if network's ipaddress usage need to be      |
|           |          | hidden                                                                         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3407`_ | Fix quick view tooltip loading overlay offset                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3405`_ | kvm: fix qemu hook race condition                                              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3391`_ | ui: fix for disk offering quickview details, actions                           |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3403`_ | ui: Fix quick view tooltip title on multiselect list views                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3386`_ | Fix labels broken by translation code                                          |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3390`_ | Add more info for creating volume snapshots                                    |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3395`_ | ui: adaptations                                                                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3382`_ | ui: fix instance and functionality                                             |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3394`_ | cloudstack: fix forward merge issues                                           |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3398`_ | server: save GUID for KVM cluster                                              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3372`_ | Add to listRouters response the scriptsversion                                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#2983`_ | KVM live storage migration intra cluster from NFS source and destination       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3381`_ | schema: add 4.11.2 to 4.11.3 systemvmtemplate upgrade path                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3329`_ | Fix: Migration target has no matching tags                                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3308`_ | Console Proxy: Ignore META key mask if control was pressed                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3075`_ | KVM: Prevent regenerating keystore on provisionCertificate API                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3251`_ | Add local ISO upload via UI                                                    |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3215`_ | storage: post process locally uploaded multi-disk ova template                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3367`_ | ui: added missing hypervisor options for upload template                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#2913`_ | Deactivate ehcache                                                             |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3373`_ | router: support multi-homed VMs in VPC                                         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3366`_ | Fix rule duplication with static NAT rules                                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3194`_ | Suspending a VM before snapshot deletion (see PR #3193)                        |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3370`_ | ssvm: apply MTU value on storage/management nic if available                   |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#2995`_ | KVM: Improvements on upload direct download certificates                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3351`_ | Have persistent DHCP leases file on VRs and cleanup /etc/hosts on VM deletion  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3310`_ | Fix removing static NAT rules with Juniper SRX                                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3346`_ | Fix template size for managed storage / refactor cloud-install-sys-tmplt and   |
|           |          | createtmplt.sh                                                                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3368`_ | server: fix public IP addresses filtering                                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3361`_ | Fix 4.11 VR Issues with Multiple Public Subnets                                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3206`_ | server: allow dedicate ip range to a domain if ips are used by an account in   |
|           |          | the domain                                                                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3205`_ | server: update dhcp configurations in vrs while update default nic of running  |
|           |          | vms                                                                            |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3362`_ | vmware: fix potential NPE when memory hotplug capability is checked            |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3356`_ | Increase POST timeout for local template upload                                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3358`_ | Update vmware reservations description                                         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3258`_ | Configurable UI branding, keyboard list and hide-able columns through a new    |
|           |          | config.js file                                                                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3338`_ | ui: fix enable static nat only towards first nic and not on any other          |
|           |          | interface                                                                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3359`_ | Ui: Reset multiselect actions when refreshing listView in Instance page        |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3342`_ | VPC: Fail to restart VPC with cleanup if there are multiple public IPs in      |
|           |          | different subnets                                                              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3348`_ | fix duplicate tag exception as CloudRuntimeException                           |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3153`_ | DPDK vHost User mode selection                                                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3243`_ | ui: add memory used column in instance metrics view                            |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3323`_ | User allowed to tag project created by him                                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3335`_ | kvm: disable cpu features if feature starts with '-'                           |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3320`_ | server: fix for inactive service offering for VM                               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3280`_ | Remove code that generated /var/lib/libvirt/images/null on target host         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3199`_ | Fix ip and ip cidr column sorting in tables                                    |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3244`_ | ui: instance settings visibility                                               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3347`_ | Fix correct permissions cloudstack-agent logrotate file for CentOS             |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3333`_ | server: ssh-keygen in PEM format and reduce main systemvm patching script      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3239`_ | KVM: Fix agents dont reconnect post maintenance                                |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3345`_ | Fix iops values when creating a compute offering                               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3218`_ | vmware: don't use redundant worker VM to extract volume                        |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3328`_ | Enhancement scss refactoring                                                   |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3245`_ | server: allows compute offering with or without constraints                    |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3325`_ | slf4j version                                                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3260`_ | base64 userdata encoding fix                                                   |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3326`_ | Bug fix for zone names not appearing in dashboard                              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3146`_ | RIP Nuage Cloudstack Plugin                                                    |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3282`_ | Fix slow vm creation when large sf snapshot count                              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3278`_ | systemvm: new qemu-guest-agent based patching for KVM                          |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3276`_ | Allow VM that has never started to have volumes attached                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3213`_ | server: allow admins to blacklist vm details that users should not see         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3216`_ | api: include tags in listvmsnapshots response                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3307`_ | Feature add scss to css compiler                                               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3227`_ | ubuntu16:  fix three issues with ubuntu 16.04 hosts                            |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3190`_ | Include 'removed' async jobs to check recurring snapshots                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3302`_ | server: sync templates on adding new secondary storage                         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3289`_ | Update to latest InfluxDB (2.15), adding support to Batch Mode                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3204`_ | server: Fix exception while update domain resource count                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3183`_ | Improvements after jquery update                                               |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3173`_ | Mock Scanner, instead of scan the computer running the test.                   |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3225`_ | ui: fix computer diagram css margin that blocks down arrow                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3256`_ | ui: show complete domain for accounts (#2994)                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3212`_ | storage: publish delete usage event for snapshot deletion                      |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3233`_ | ui: don't ignore ''mine" when listing "all" templates in projects              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3269`_ | packaging: systemctl daemon-reload after agent install or upgrade              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3257`_ | server: fix for vm snapshot search (#3208)                                     |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3254`_ | utils: removed port check for url validation (#2802)                           |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3266`_ | packaging: don't skip unit tests while building packages                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3249`_ | [CLOUDSTACK-10406] fix bugs that may cause program crash, change mkdir to      |
|           |          | mkdirs                                                                         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3181`_ | fix incorrect iscsi path stat for managed storage                              |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3214`_ | ui: use executable template filter for users                                   |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3247`_ | Make the API documentation version not *hardcoded* to v4.9.0                   |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3238`_ | client: don't disable TLSv1, TLSv1.1 by default that breaks VMware env         |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3236`_ | schema: add empty DB upgrade path from 4.12.0.0 to 4.13.0.0                    |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#2869`_ | Fix some Marvin smoke tests                                                    |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3161`_ | Fix behavior of multiselect in list view                                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3160`_ | Add start button for multiple instances in list view                           |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3165`_ | debian: cleanup commons-daemon no longer needed by agent                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3211`_ | ui: remove CA certificate button from UI                                       |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3170`_ | NotImplemented as a local exception                                            |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3209`_ | server: make snapshotting on KVM non-blocking                                  |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3158`_ | Allow users of all types to create L2 networks                                 |
+-----------+----------+--------------------------------------------------------------------------------+
| 4.13.0.0  | `#3151`_ | api: rename ListUsageRecords file name to ListUsageRecordsCmd                  |
+-----------+----------+--------------------------------------------------------------------------------+

189 Issues listed

.. _`#3574`: https://github.com/apache/cloudstack/pull/3574 
.. _`#3519`: https://github.com/apache/cloudstack/pull/3519 
.. _`#3582`: https://github.com/apache/cloudstack/pull/3582 
.. _`#3571`: https://github.com/apache/cloudstack/pull/3571 
.. _`#3567`: https://github.com/apache/cloudstack/pull/3567 
.. _`#3566`: https://github.com/apache/cloudstack/pull/3566 
.. _`#3564`: https://github.com/apache/cloudstack/pull/3564 
.. _`#3560`: https://github.com/apache/cloudstack/pull/3560 
.. _`#3549`: https://github.com/apache/cloudstack/pull/3549 
.. _`#3551`: https://github.com/apache/cloudstack/pull/3551 
.. _`#3547`: https://github.com/apache/cloudstack/pull/3547 
.. _`#3271`: https://github.com/apache/cloudstack/pull/3271 
.. _`#3545`: https://github.com/apache/cloudstack/pull/3545 
.. _`#3533`: https://github.com/apache/cloudstack/pull/3533 
.. _`#3537`: https://github.com/apache/cloudstack/pull/3537 
.. _`#3535`: https://github.com/apache/cloudstack/pull/3535 
.. _`#3534`: https://github.com/apache/cloudstack/pull/3534 
.. _`#3480`: https://github.com/apache/cloudstack/pull/3480 
.. _`#3529`: https://github.com/apache/cloudstack/pull/3529 
.. _`#3528`: https://github.com/apache/cloudstack/pull/3528 
.. _`#3524`: https://github.com/apache/cloudstack/pull/3524 
.. _`#3152`: https://github.com/apache/cloudstack/pull/3152 
.. _`#3470`: https://github.com/apache/cloudstack/pull/3470 
.. _`#3500`: https://github.com/apache/cloudstack/pull/3500 
.. _`#3492`: https://github.com/apache/cloudstack/pull/3492 
.. _`#3486`: https://github.com/apache/cloudstack/pull/3486 
.. _`#3511`: https://github.com/apache/cloudstack/pull/3511 
.. _`#3502`: https://github.com/apache/cloudstack/pull/3502 
.. _`#3501`: https://github.com/apache/cloudstack/pull/3501 
.. _`#3430`: https://github.com/apache/cloudstack/pull/3430 
.. _`#3494`: https://github.com/apache/cloudstack/pull/3494 
.. _`#3473`: https://github.com/apache/cloudstack/pull/3473 
.. _`#3504`: https://github.com/apache/cloudstack/pull/3504 
.. _`#3374`: https://github.com/apache/cloudstack/pull/3374 
.. _`#3495`: https://github.com/apache/cloudstack/pull/3495 
.. _`#3248`: https://github.com/apache/cloudstack/pull/3248 
.. _`#3489`: https://github.com/apache/cloudstack/pull/3489 
.. _`#3454`: https://github.com/apache/cloudstack/pull/3454 
.. _`#3476`: https://github.com/apache/cloudstack/pull/3476 
.. _`#3483`: https://github.com/apache/cloudstack/pull/3483 
.. _`#3319`: https://github.com/apache/cloudstack/pull/3319 
.. _`#3479`: https://github.com/apache/cloudstack/pull/3479 
.. _`#3465`: https://github.com/apache/cloudstack/pull/3465 
.. _`#3475`: https://github.com/apache/cloudstack/pull/3475 
.. _`#3457`: https://github.com/apache/cloudstack/pull/3457 
.. _`#3393`: https://github.com/apache/cloudstack/pull/3393 
.. _`#3468`: https://github.com/apache/cloudstack/pull/3468 
.. _`#3297`: https://github.com/apache/cloudstack/pull/3297 
.. _`#3472`: https://github.com/apache/cloudstack/pull/3472 
.. _`#3467`: https://github.com/apache/cloudstack/pull/3467 
.. _`#3463`: https://github.com/apache/cloudstack/pull/3463 
.. _`#3331`: https://github.com/apache/cloudstack/pull/3331 
.. _`#3462`: https://github.com/apache/cloudstack/pull/3462 
.. _`#3466`: https://github.com/apache/cloudstack/pull/3466 
.. _`#3412`: https://github.com/apache/cloudstack/pull/3412 
.. _`#3336`: https://github.com/apache/cloudstack/pull/3336 
.. _`#3306`: https://github.com/apache/cloudstack/pull/3306 
.. _`#3451`: https://github.com/apache/cloudstack/pull/3451 
.. _`#3449`: https://github.com/apache/cloudstack/pull/3449 
.. _`#3445`: https://github.com/apache/cloudstack/pull/3445 
.. _`#3435`: https://github.com/apache/cloudstack/pull/3435 
.. _`#3437`: https://github.com/apache/cloudstack/pull/3437 
.. _`#3421`: https://github.com/apache/cloudstack/pull/3421 
.. _`#3436`: https://github.com/apache/cloudstack/pull/3436 
.. _`#3438`: https://github.com/apache/cloudstack/pull/3438 
.. _`#3441`: https://github.com/apache/cloudstack/pull/3441 
.. _`#3431`: https://github.com/apache/cloudstack/pull/3431 
.. _`#3432`: https://github.com/apache/cloudstack/pull/3432 
.. _`#3427`: https://github.com/apache/cloudstack/pull/3427 
.. _`#3429`: https://github.com/apache/cloudstack/pull/3429 
.. _`#3228`: https://github.com/apache/cloudstack/pull/3228 
.. _`#3259`: https://github.com/apache/cloudstack/pull/3259 
.. _`#3240`: https://github.com/apache/cloudstack/pull/3240 
.. _`#3424`: https://github.com/apache/cloudstack/pull/3424 
.. _`#3419`: https://github.com/apache/cloudstack/pull/3419 
.. _`#3420`: https://github.com/apache/cloudstack/pull/3420 
.. _`#3422`: https://github.com/apache/cloudstack/pull/3422 
.. _`#3126`: https://github.com/apache/cloudstack/pull/3126 
.. _`#3418`: https://github.com/apache/cloudstack/pull/3418 
.. _`#3268`: https://github.com/apache/cloudstack/pull/3268 
.. _`#3423`: https://github.com/apache/cloudstack/pull/3423 
.. _`#3246`: https://github.com/apache/cloudstack/pull/3246 
.. _`#3406`: https://github.com/apache/cloudstack/pull/3406 
.. _`#3365`: https://github.com/apache/cloudstack/pull/3365 
.. _`#3413`: https://github.com/apache/cloudstack/pull/3413 
.. _`#3415`: https://github.com/apache/cloudstack/pull/3415 
.. _`#3414`: https://github.com/apache/cloudstack/pull/3414 
.. _`#3219`: https://github.com/apache/cloudstack/pull/3219 
.. _`#3344`: https://github.com/apache/cloudstack/pull/3344 
.. _`#3234`: https://github.com/apache/cloudstack/pull/3234 
.. _`#3242`: https://github.com/apache/cloudstack/pull/3242 
.. _`#3222`: https://github.com/apache/cloudstack/pull/3222 
.. _`#3384`: https://github.com/apache/cloudstack/pull/3384 
.. _`#3235`: https://github.com/apache/cloudstack/pull/3235 
.. _`#3407`: https://github.com/apache/cloudstack/pull/3407 
.. _`#3405`: https://github.com/apache/cloudstack/pull/3405 
.. _`#3391`: https://github.com/apache/cloudstack/pull/3391 
.. _`#3403`: https://github.com/apache/cloudstack/pull/3403 
.. _`#3386`: https://github.com/apache/cloudstack/pull/3386 
.. _`#3390`: https://github.com/apache/cloudstack/pull/3390 
.. _`#3395`: https://github.com/apache/cloudstack/pull/3395 
.. _`#3382`: https://github.com/apache/cloudstack/pull/3382 
.. _`#3394`: https://github.com/apache/cloudstack/pull/3394 
.. _`#3398`: https://github.com/apache/cloudstack/pull/3398 
.. _`#3372`: https://github.com/apache/cloudstack/pull/3372 
.. _`#2983`: https://github.com/apache/cloudstack/pull/2983 
.. _`#3381`: https://github.com/apache/cloudstack/pull/3381 
.. _`#3329`: https://github.com/apache/cloudstack/pull/3329 
.. _`#3308`: https://github.com/apache/cloudstack/pull/3308 
.. _`#3075`: https://github.com/apache/cloudstack/pull/3075 
.. _`#3251`: https://github.com/apache/cloudstack/pull/3251 
.. _`#3215`: https://github.com/apache/cloudstack/pull/3215 
.. _`#3367`: https://github.com/apache/cloudstack/pull/3367 
.. _`#2913`: https://github.com/apache/cloudstack/pull/2913 
.. _`#3373`: https://github.com/apache/cloudstack/pull/3373 
.. _`#3366`: https://github.com/apache/cloudstack/pull/3366 
.. _`#3194`: https://github.com/apache/cloudstack/pull/3194 
.. _`#3370`: https://github.com/apache/cloudstack/pull/3370 
.. _`#2995`: https://github.com/apache/cloudstack/pull/2995 
.. _`#3351`: https://github.com/apache/cloudstack/pull/3351 
.. _`#3310`: https://github.com/apache/cloudstack/pull/3310 
.. _`#3346`: https://github.com/apache/cloudstack/pull/3346 
.. _`#3368`: https://github.com/apache/cloudstack/pull/3368 
.. _`#3361`: https://github.com/apache/cloudstack/pull/3361 
.. _`#3206`: https://github.com/apache/cloudstack/pull/3206 
.. _`#3205`: https://github.com/apache/cloudstack/pull/3205 
.. _`#3362`: https://github.com/apache/cloudstack/pull/3362 
.. _`#3356`: https://github.com/apache/cloudstack/pull/3356 
.. _`#3358`: https://github.com/apache/cloudstack/pull/3358 
.. _`#3258`: https://github.com/apache/cloudstack/pull/3258 
.. _`#3338`: https://github.com/apache/cloudstack/pull/3338 
.. _`#3359`: https://github.com/apache/cloudstack/pull/3359 
.. _`#3342`: https://github.com/apache/cloudstack/pull/3342 
.. _`#3348`: https://github.com/apache/cloudstack/pull/3348 
.. _`#3153`: https://github.com/apache/cloudstack/pull/3153 
.. _`#3243`: https://github.com/apache/cloudstack/pull/3243 
.. _`#3323`: https://github.com/apache/cloudstack/pull/3323 
.. _`#3335`: https://github.com/apache/cloudstack/pull/3335 
.. _`#3320`: https://github.com/apache/cloudstack/pull/3320 
.. _`#3280`: https://github.com/apache/cloudstack/pull/3280 
.. _`#3199`: https://github.com/apache/cloudstack/pull/3199 
.. _`#3244`: https://github.com/apache/cloudstack/pull/3244 
.. _`#3347`: https://github.com/apache/cloudstack/pull/3347 
.. _`#3333`: https://github.com/apache/cloudstack/pull/3333 
.. _`#3239`: https://github.com/apache/cloudstack/pull/3239 
.. _`#3345`: https://github.com/apache/cloudstack/pull/3345 
.. _`#3218`: https://github.com/apache/cloudstack/pull/3218 
.. _`#3328`: https://github.com/apache/cloudstack/pull/3328 
.. _`#3245`: https://github.com/apache/cloudstack/pull/3245 
.. _`#3325`: https://github.com/apache/cloudstack/pull/3325 
.. _`#3260`: https://github.com/apache/cloudstack/pull/3260 
.. _`#3326`: https://github.com/apache/cloudstack/pull/3326 
.. _`#3146`: https://github.com/apache/cloudstack/pull/3146 
.. _`#3282`: https://github.com/apache/cloudstack/pull/3282 
.. _`#3278`: https://github.com/apache/cloudstack/pull/3278 
.. _`#3276`: https://github.com/apache/cloudstack/pull/3276 
.. _`#3213`: https://github.com/apache/cloudstack/pull/3213 
.. _`#3216`: https://github.com/apache/cloudstack/pull/3216 
.. _`#3307`: https://github.com/apache/cloudstack/pull/3307 
.. _`#3227`: https://github.com/apache/cloudstack/pull/3227 
.. _`#3190`: https://github.com/apache/cloudstack/pull/3190 
.. _`#3302`: https://github.com/apache/cloudstack/pull/3302 
.. _`#3289`: https://github.com/apache/cloudstack/pull/3289 
.. _`#3204`: https://github.com/apache/cloudstack/pull/3204 
.. _`#3183`: https://github.com/apache/cloudstack/pull/3183 
.. _`#3173`: https://github.com/apache/cloudstack/pull/3173 
.. _`#3225`: https://github.com/apache/cloudstack/pull/3225 
.. _`#3256`: https://github.com/apache/cloudstack/pull/3256 
.. _`#3212`: https://github.com/apache/cloudstack/pull/3212 
.. _`#3233`: https://github.com/apache/cloudstack/pull/3233 
.. _`#3269`: https://github.com/apache/cloudstack/pull/3269 
.. _`#3257`: https://github.com/apache/cloudstack/pull/3257 
.. _`#3254`: https://github.com/apache/cloudstack/pull/3254 
.. _`#3266`: https://github.com/apache/cloudstack/pull/3266 
.. _`#3249`: https://github.com/apache/cloudstack/pull/3249 
.. _`#3181`: https://github.com/apache/cloudstack/pull/3181 
.. _`#3214`: https://github.com/apache/cloudstack/pull/3214 
.. _`#3247`: https://github.com/apache/cloudstack/pull/3247 
.. _`#3238`: https://github.com/apache/cloudstack/pull/3238 
.. _`#3236`: https://github.com/apache/cloudstack/pull/3236 
.. _`#2869`: https://github.com/apache/cloudstack/pull/2869 
.. _`#3161`: https://github.com/apache/cloudstack/pull/3161 
.. _`#3160`: https://github.com/apache/cloudstack/pull/3160 
.. _`#3165`: https://github.com/apache/cloudstack/pull/3165 
.. _`#3211`: https://github.com/apache/cloudstack/pull/3211 
.. _`#3170`: https://github.com/apache/cloudstack/pull/3170 
.. _`#3209`: https://github.com/apache/cloudstack/pull/3209 
.. _`#3158`: https://github.com/apache/cloudstack/pull/3158 
.. _`#3151`: https://github.com/apache/cloudstack/pull/3151 
