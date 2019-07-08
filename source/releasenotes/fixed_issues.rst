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



Issues Fixed in |release|
=========================

Apache CloudStack now uses GitHub <https://github.com/apache/cloudstack/issues>`_ 
to track its issues. links to the GitHub pull requests have been included at the end
of each section. 

Apache CloudStack previously used `Jira <https://issues.apache.org/jira/browse/CLOUDSTACK>`_ 
to track its issues and `Github <https://github.com/apache/cloudstack/pulls>`_ for 
pull requests. All new features and bugs for |version| have been merged through
Github pull requests.  A subset of these changes are tracked in Jira, which have a 
standard naming convention of "CLOUDSTACK-NNNN" where "NNNN" is the issue number.

Issues Fixed in 4.11.3.0
------------------------

.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+------------------------------------------------------------+
| Version                 | Github   | Description                                                |
+=========================+==========+============================================================+
| 4.11.3.0                | `#3381`_ | schema: add 4.11.2 to 4.11.3 systemvmtemplate upgrade path |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3075`_ | KVM: Prevent regenerating keystore on provisionCertificate |
|                         |          | API                                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3373`_ | router: support multi-homed VMs in VPC                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3366`_ | Fix rule duplication with static NAT rules                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3194`_ | Suspending a VM before snapshot deletion (see PR #3193)    |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3370`_ | ssvm: apply MTU value on storage/management nic if         |
|                         |          | available                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#2995`_ | KVM: Improvements on upload direct download certificates   |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3351`_ | Have persistent DHCP leases file on VRs and cleanup        |
|                         |          | /etc/hosts on VM deletion                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3310`_ | Fix removing static NAT rules with Juniper SRX             |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3361`_ | Fix 4.11 VR Issues with Multiple Public Subnets            |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3206`_ | server: allow dedicate ip range to a domain if ips are     |
|                         |          | used by an account in the domain                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3205`_ | server: update dhcp configurations in vrs while update     |
|                         |          | default nic of running vms                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3362`_ | vmware: fix potential NPE when memory hotplug capability   |
|                         |          | is checked                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3338`_ | ui: fix enable static nat only towards first nic and not   |
|                         |          | on any other interface                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3359`_ | Ui: Reset multiselect actions when refreshing listView in  |
|                         |          | Instance page                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3342`_ | VPC: Fail to restart VPC with cleanup if there are         |
|                         |          | multiple public IPs in different subnets                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3348`_ | fix duplicate tag exception as CloudRuntimeException       |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3333`_ | server: ssh-keygen in PEM format and reduce main systemvm  |
|                         |          | patching script                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3239`_ | KVM: Fix agents dont reconnect post maintenance            |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3278`_ | systemvm: new qemu-guest-agent based patching for KVM      |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3276`_ | Allow VM that has never started to have volumes attached   |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3204`_ | server: Fix exception while update domain resource count   |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3269`_ | packaging: systemctl daemon-reload after agent install or  |
|                         |          | upgrade                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3266`_ | packaging: don't skip unit tests while building packages   |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3238`_ | client: don't disable TLSv1, TLSv1.1 by default that       |
|                         |          | breaks VMware env                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#2869`_ | Fix some Marvin smoke tests                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3158`_ | Allow users of all types to create L2 networks             |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3210`_ | systemd: Fix -Dpid arg passing to systemd usage service    |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3163`_ | systemd: fix services to allow TLS configurations via      |
|                         |          | java.security.ciphers                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3122`_ | Add back ability to disable backup of snapshot to          |
|                         |          | secondary                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3139`_ | packaging: management default file cleanup                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3134`_ | keystore: don't restart systemvm cloud.service post cert   |
|                         |          | import                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3105`_ | VmwareStorageLayoutHelper throws StackOverflowError fix    |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3095`_ | Prevent corner case for infinite PrepareForMaintenance     |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3106`_ | marvin: add missing test data for test_migration smoketest |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3098`_ | Add support for keyword in listSSHKeyPairs command search  |
|                         |          | (#2920)                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#2894`_ | api: don't throttle api discovery for listApis command     |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3024`_ | travis: fail fast if --with-marvin fails with nose         |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3005`_ | Discover tags field on superclass of API responses         |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3076`_ | security: increase keystore setup/import timeout           |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3030`_ | correct permissions in spec file and fix class path        |
|                         |          | specified variable                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3066`_ | API: move ostypeid from DB id to DB uuid, backports #2528  |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3037`_ | kvm: when untagged vxlan is used, use the default          |
|                         |          | guest/public bridge                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#2990`_ | Security Group: add secondary ips to the correct ipset     |
|                         |          | based on ip family (4.11)                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3055`_ | marvin: add missing default test data                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3038`_ | surefire: ignore system classloader to make tests run      |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3021`_ | Skip network migration tests for not supported hypervisors |
|                         |          | instead of failing                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.11.3.0                | `#3417   | schema: add 4.11.2 to 4.11.3 systemvmtemplate upgrade path |
+-------------------------+----------+------------------------------------------------------------+


48 Issues listed

GitHub links to listed issues:

.. _`#3381`: https://github.com/apache/cloudstack/pull/3381 
.. _`#3075`: https://github.com/apache/cloudstack/pull/3075 
.. _`#3373`: https://github.com/apache/cloudstack/pull/3373 
.. _`#3366`: https://github.com/apache/cloudstack/pull/3366 
.. _`#3194`: https://github.com/apache/cloudstack/pull/3194 
.. _`#3370`: https://github.com/apache/cloudstack/pull/3370 
.. _`#2995`: https://github.com/apache/cloudstack/pull/2995 
.. _`#3351`: https://github.com/apache/cloudstack/pull/3351 
.. _`#3310`: https://github.com/apache/cloudstack/pull/3310 
.. _`#3361`: https://github.com/apache/cloudstack/pull/3361 
.. _`#3206`: https://github.com/apache/cloudstack/pull/3206 
.. _`#3205`: https://github.com/apache/cloudstack/pull/3205 
.. _`#3362`: https://github.com/apache/cloudstack/pull/3362 
.. _`#3338`: https://github.com/apache/cloudstack/pull/3338 
.. _`#3359`: https://github.com/apache/cloudstack/pull/3359 
.. _`#3342`: https://github.com/apache/cloudstack/pull/3342 
.. _`#3348`: https://github.com/apache/cloudstack/pull/3348 
.. _`#3333`: https://github.com/apache/cloudstack/pull/3333 
.. _`#3239`: https://github.com/apache/cloudstack/pull/3239 
.. _`#3278`: https://github.com/apache/cloudstack/pull/3278 
.. _`#3276`: https://github.com/apache/cloudstack/pull/3276 
.. _`#3204`: https://github.com/apache/cloudstack/pull/3204 
.. _`#3269`: https://github.com/apache/cloudstack/pull/3269 
.. _`#3266`: https://github.com/apache/cloudstack/pull/3266 
.. _`#3238`: https://github.com/apache/cloudstack/pull/3238 
.. _`#2869`: https://github.com/apache/cloudstack/pull/2869 
.. _`#3158`: https://github.com/apache/cloudstack/pull/3158 
.. _`#3210`: https://github.com/apache/cloudstack/pull/3210 
.. _`#3163`: https://github.com/apache/cloudstack/pull/3163 
.. _`#3122`: https://github.com/apache/cloudstack/pull/3122 
.. _`#3139`: https://github.com/apache/cloudstack/pull/3139 
.. _`#3134`: https://github.com/apache/cloudstack/pull/3134 
.. _`#3105`: https://github.com/apache/cloudstack/pull/3105 
.. _`#3095`: https://github.com/apache/cloudstack/pull/3095 
.. _`#3106`: https://github.com/apache/cloudstack/pull/3106 
.. _`#3098`: https://github.com/apache/cloudstack/pull/3098 
.. _`#2894`: https://github.com/apache/cloudstack/pull/2894 
.. _`#3024`: https://github.com/apache/cloudstack/pull/3024 
.. _`#3005`: https://github.com/apache/cloudstack/pull/3005 
.. _`#3076`: https://github.com/apache/cloudstack/pull/3076 
.. _`#3030`: https://github.com/apache/cloudstack/pull/3030 
.. _`#3066`: https://github.com/apache/cloudstack/pull/3066 
.. _`#3037`: https://github.com/apache/cloudstack/pull/3037 
.. _`#2990`: https://github.com/apache/cloudstack/pull/2990 
.. _`#3055`: https://github.com/apache/cloudstack/pull/3055 
.. _`#3038`: https://github.com/apache/cloudstack/pull/3038 
.. _`#3021`: https://github.com/apache/cloudstack/pull/3021
.. _`#3417`: https://github.com/apache/cloudstack/pull/3417




Issues Fixed in 4.11.2.0
------------------------

.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| Version                 | Github   | Type          | Priority | Description                                                |
+=========================+==========+===============+==========+============================================================+
| 4.11.2.0                | `#3021`_ |               |          | Skip network migration tests for not supported hypervisors |
|                         |          |               |          | instead of failing                                         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#3022`_ |               |          | systemvmtemplate: update debian 9.6 iso url and checksum   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#3012`_ |               |          | CLOUDSTACK-3009: Fixed resource calculation CPU, RAM for   |
|                         |          |               |          | accounts.                                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#3018`_ |               |          | Prevent error on GroupAnswers on VR creation               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#3007`_ |               |          | Add missing ConfigDrive entries on existing zones after    |
|                         |          |               |          | upgrade                                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2980`_ |               |          | [4.11] Fix set initial reservation on public IP ranges     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#3010`_ |               |          | Fix DirectNetworkGuru canHandle checks for lowercase       |
|                         |          |               |          | isolation methods                                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2984`_ |               |          | kvm: reset KVM host on heartbeat failure                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2928`_ |               |          | Migrating VM from ISO failures                             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2979`_ |               |          | vr: defer was broken in VR because of json name change     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2927`_ |               |          | server: fix unwanted txn commit warning messages           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2923`_ |               |          | Improved perfomance on creating VM (KVM)                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2926`_ |               |          | network: on rolling restart force stop old routers         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2915`_ |               |          | packaging: install plugins at                              |
|                         |          |               |          | /usr/share/cloudstack-management/lib                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2916`_ |               |          | systemvm: Ensure cloud service reboots after failure       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2907`_ |               |          | client: mgmt server listen default to 0.0.0.0              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2911`_ |               |          | Unify templates/ISOs checksum API output                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2900`_ |               |          | network: Allow ability to disable rolling restart feature  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2904`_ |               |          | agent: Fixes #2899 on shutdown don't allow server          |
|                         |          |               |          | reconnection                                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2902`_ |               |          | Add checksum sanity validation on template registration    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2903`_ |               |          | Set http level to INFO as default                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2892`_ |               |          | vr: memory and swap optimizations                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2876`_ |               |          | PULL_REQUEST_TEMPLATE: simplify and remove unpopular       |
|                         |          |               |          | sections                                                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2888`_ |               |          | router: Fixes #2719 program VR nics by device id order for |
|                         |          |               |          | VPC                                                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2889`_ |               |          | Fixes: #2881 Improve Exception message                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2884`_ |               |          | add date to usage server logs                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2879`_ |               |          | ca: Fixes #2877 mgmt server cert should have all addrs of  |
|                         |          |               |          | default nic                                                |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2878`_ |               |          | Fixed Issue 2868, libvirt resize notify failure            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2875`_ |               |          | CertUtils: export private key to pem format correctly      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2866`_ |               |          | systemvm: baremetal-vr: reduce memory usage                |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2743`_ |               |          | CLOUDSTACK-10380: Fix startvm giving another pw after pw   |
|                         |          |               |          | reset                                                      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2860`_ |               |          | packaging: Fixes #2857 don't overwrite agent logrotate     |
|                         |          |               |          | config                                                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2859`_ |               |          | agent: Fixes #2858 agent LB not working                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2855`_ |               |          | systemvm: export $TYPE before patching ssvm/cpvm           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2852`_ |               |          | Make networkofferingid required in migrateNetwork          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2846`_ |               |          | Fix PowerReportMissing for new VRs                         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2840`_ |               |          | Fix for Vmware full clones update                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2799`_ |               |          | systemvmtemplate: new 4.11.2 template and fixes            |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2829`_ |               |          | CLOUDSTACK-9473: storage pool capacity check when volume   |
|                         |          |               |          | is resized or migrated                                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2824`_ |               |          | Fix SystemVMs running in Xen HVM mode are not configured   |
|                         |          |               |          | (#2760)                                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2836`_ |               |          | Volume snapshot recurring schedule not showing             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2825`_ |               |          | expunge if flag is set                                     |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2832`_ |               |          | Bigger partiton table for SVM & ambigous redirect bugfix   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2806`_ |               |          | ajusting dict to pass on if tests later on code, in this   |
|                         |          |               |          | way arping i?                                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2819`_ |               |          | KVM hook script include                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2091`_ |               |          | CLOUDSTACK-8609: [VMware] VM is not accessible after       |
|                         |          |               |          | migration across clusters                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2815`_ |               |          | display translation labels as html instead of plain text   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2722`_ |               |          | CLOUDSTACK-10310 Fix KVM reboot on storage issue           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2810`_ |               |          | Project drop-down refresh data fix                         |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2809`_ |               |          | Backport Update DBCP version to 4.11                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2811`_ |               |          | Fix a typo in                                              |
|                         |          |               |          | server/src/com/cloud/vm/UserVmManagerImpl.java             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2776`_ |               |          | Issue 2774: Changed the implementation of                  |
|                         |          |               |          | isVolumeOnManagedStorage(VolumeInfo) to?                   |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2794`_ |               |          | vmware: reboot VR after mac updates                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2790`_ |               |          | add height sizing to detail view so that it renders all    |
|                         |          |               |          | detail items                                               |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2788`_ |               |          | data table header cursor type and title                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2785`_ |               |          | change dashboard events cursor to default to prevent user  |
|                         |          |               |          | confusion                                                  |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2784`_ |               |          | insert plugin css files before custom.css file             |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2782`_ |               |          | add ipaddress input field to 'Add network to VM' form      |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2791`_ |               |          | router: Fixes #2789 fix proper mark based packet routing   |
|                         |          |               |          | across interfaces                                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2792`_ |               |          | Fix issue when multiple cidrs with different sizes are     |
|                         |          |               |          | assigned on a VR                                           |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2781`_ |               |          | hvm checkbox visibility                                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2775`_ |               |          | Fix typo in ISO url                                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2778`_ |               |          | reset ssh key pair visibility                              |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2769`_ |               |          | Fix config drive iso path on Vmware                        |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2747`_ |               |          | systemvm: Update ISO URLs to the latest                    |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2734`_ |               |          | Fix invalid consoleproxy url after upgrade                 |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2767`_ |               |          | storage traffic type reset ui fix                          |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2757`_ |               |          | register template kvm context ui fix                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2709`_ |               |          | check volumes for state when retrieving pool for           |
|                         |          |               |          | configDrive creation                                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2728`_ |               |          | Consistence POM version for 4.11.x.y                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+
| 4.11.2.0                | `#2727`_ |               |          | maven: bump up vmware sdk jar to 6.7                       |
+-------------------------+----------+---------------+----------+------------------------------------------------------------+

71 Issues listed

GitHub links to listed issues:

.. _`#3021`: https://github.com/apache/cloudstack/pull/3021 
.. _`#3022`: https://github.com/apache/cloudstack/pull/3022 
.. _`#3012`: https://github.com/apache/cloudstack/pull/3012 
.. _`#3018`: https://github.com/apache/cloudstack/pull/3018 
.. _`#3007`: https://github.com/apache/cloudstack/pull/3007 
.. _`#2980`: https://github.com/apache/cloudstack/pull/2980 
.. _`#3010`: https://github.com/apache/cloudstack/pull/3010 
.. _`#2984`: https://github.com/apache/cloudstack/pull/2984 
.. _`#2928`: https://github.com/apache/cloudstack/pull/2928 
.. _`#2979`: https://github.com/apache/cloudstack/pull/2979 
.. _`#2927`: https://github.com/apache/cloudstack/pull/2927 
.. _`#2923`: https://github.com/apache/cloudstack/pull/2923 
.. _`#2926`: https://github.com/apache/cloudstack/pull/2926 
.. _`#2915`: https://github.com/apache/cloudstack/pull/2915 
.. _`#2916`: https://github.com/apache/cloudstack/pull/2916 
.. _`#2907`: https://github.com/apache/cloudstack/pull/2907 
.. _`#2911`: https://github.com/apache/cloudstack/pull/2911 
.. _`#2900`: https://github.com/apache/cloudstack/pull/2900 
.. _`#2904`: https://github.com/apache/cloudstack/pull/2904 
.. _`#2902`: https://github.com/apache/cloudstack/pull/2902 
.. _`#2903`: https://github.com/apache/cloudstack/pull/2903 
.. _`#2892`: https://github.com/apache/cloudstack/pull/2892 
.. _`#2876`: https://github.com/apache/cloudstack/pull/2876 
.. _`#2888`: https://github.com/apache/cloudstack/pull/2888 
.. _`#2889`: https://github.com/apache/cloudstack/pull/2889 
.. _`#2884`: https://github.com/apache/cloudstack/pull/2884 
.. _`#2879`: https://github.com/apache/cloudstack/pull/2879 
.. _`#2878`: https://github.com/apache/cloudstack/pull/2878 
.. _`#2875`: https://github.com/apache/cloudstack/pull/2875 
.. _`#2866`: https://github.com/apache/cloudstack/pull/2866 
.. _`#2743`: https://github.com/apache/cloudstack/pull/2743 
.. _`#2860`: https://github.com/apache/cloudstack/pull/2860 
.. _`#2859`: https://github.com/apache/cloudstack/pull/2859 
.. _`#2855`: https://github.com/apache/cloudstack/pull/2855 
.. _`#2852`: https://github.com/apache/cloudstack/pull/2852 
.. _`#2846`: https://github.com/apache/cloudstack/pull/2846 
.. _`#2840`: https://github.com/apache/cloudstack/pull/2840 
.. _`#2799`: https://github.com/apache/cloudstack/pull/2799 
.. _`#2829`: https://github.com/apache/cloudstack/pull/2829 
.. _`#2824`: https://github.com/apache/cloudstack/pull/2824 
.. _`#2836`: https://github.com/apache/cloudstack/pull/2836 
.. _`#2825`: https://github.com/apache/cloudstack/pull/2825 
.. _`#2832`: https://github.com/apache/cloudstack/pull/2832 
.. _`#2806`: https://github.com/apache/cloudstack/pull/2806 
.. _`#2819`: https://github.com/apache/cloudstack/pull/2819 
.. _`#2091`: https://github.com/apache/cloudstack/pull/2091 
.. _`#2815`: https://github.com/apache/cloudstack/pull/2815 
.. _`#2722`: https://github.com/apache/cloudstack/pull/2722 
.. _`#2810`: https://github.com/apache/cloudstack/pull/2810 
.. _`#2809`: https://github.com/apache/cloudstack/pull/2809 
.. _`#2811`: https://github.com/apache/cloudstack/pull/2811 
.. _`#2776`: https://github.com/apache/cloudstack/pull/2776 
.. _`#2794`: https://github.com/apache/cloudstack/pull/2794 
.. _`#2790`: https://github.com/apache/cloudstack/pull/2790 
.. _`#2788`: https://github.com/apache/cloudstack/pull/2788 
.. _`#2785`: https://github.com/apache/cloudstack/pull/2785 
.. _`#2784`: https://github.com/apache/cloudstack/pull/2784 
.. _`#2782`: https://github.com/apache/cloudstack/pull/2782 
.. _`#2791`: https://github.com/apache/cloudstack/pull/2791 
.. _`#2792`: https://github.com/apache/cloudstack/pull/2792 
.. _`#2781`: https://github.com/apache/cloudstack/pull/2781 
.. _`#2775`: https://github.com/apache/cloudstack/pull/2775 
.. _`#2778`: https://github.com/apache/cloudstack/pull/2778 
.. _`#2769`: https://github.com/apache/cloudstack/pull/2769 
.. _`#2747`: https://github.com/apache/cloudstack/pull/2747 
.. _`#2734`: https://github.com/apache/cloudstack/pull/2734 
.. _`#2767`: https://github.com/apache/cloudstack/pull/2767 
.. _`#2757`: https://github.com/apache/cloudstack/pull/2757 
.. _`#2709`: https://github.com/apache/cloudstack/pull/2709 
.. _`#2728`: https://github.com/apache/cloudstack/pull/2728 
.. _`#2727`: https://github.com/apache/cloudstack/pull/2727 



Issues Fixed in 4.11.1.0
------------------------

.. cssclass:: table-striped table-bordered table-hover

+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| Branches                | Github   | Jira               | Type          | Priority | Description                                                |
+=========================+==========+====================+===============+==========+============================================================+
| 4.11                    | `#2712`_ |                    |               |          | reuse ip for non redundant VPC                             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2714`_ |                    |               |          | send unsupported answer only when applicable               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2715`_ |                    |               |          | smoketest: Fix test_vm_life_cycle secure migration tests   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2493`_ | CLOUDSTACK-10326_  | Bug           | Major    | Prevent hosts fall into Maintenance when there are running |
|                         |          |                    |               |          | VMs on it                                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2716`_ |                    |               |          | configdrive: make fewer mountpoints on hosts               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2681`_ |                    |               |          | Source NAT option on Private Gateway                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2670`_ |                    |               |          | Removing an old, unused NetApp plug-in                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2710`_ |                    |               |          | comply with api key constraint                             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2699`_ |                    |               |          | remove old config artifacts from update path               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2705`_ | CLOUDSTACK-10381_  | Bug           | Blocker  | [ConfigDrive] Password is missing after reset password     |
|                         |          |                    |               |          | sequence                                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2704`_ |                    |               |          | ui: fix create VPC dialog box failure when zone is SG      |
|                         |          |                    |               |          | enabled                                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2693`_ |                    |               |          | Fix to enable Advanced zones with Security groups and      |
|                         |          |                    |               |          | VXLAN isolation type                                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2697`_ |                    |               |          | agent: Avoid sudo, renew certificates assuming root        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2686`_ |                    |               |          | Fixes #2685: broken SXM support                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2696`_ |                    |               |          | Fix LibvirtStorageAdaptor.java                             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2683`_ |                    |               |          | Add default L2 network offerings                           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2694`_ |                    |               |          | Do not send conserve mode param on L2 network offering     |
|                         |          |                    |               |          | creation from the UI                                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2688`_ | CLOUDSTACK-10382_  | Bug           | Major    | [ConfigDrive] cloud-get-vm-data-configdrive.in is          |
|                         |          |                    |               |          | incorrect                                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2672`_ | CLOUDSTACK-10377_  | Bug           | Major    | Nuage VSP regression fails in NetworksWithCleanup test     |
|                         |          |                    |               |          | since introduction of fix for CLOUDSTACK-9114 in ACS       |
|                         |          |                    |               |          | 4.11&master                                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2674`_ |                    |               |          | Create unit test cases for 'ConfigDriveBuilder' class      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2673`_ |                    |               |          | Fix test_configdrive.py and test_nuage_configdrive         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2676`_ |                    |               |          | Fix two typos (from uanble to unable).                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2669`_ |                    |               |          | conditional template filter                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2664`_ |                    |               |          | revert dedicate vlan code removal                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2663`_ |                    |               |          | server: Calculate fresh capacity per VM                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2667`_ | CLOUDSTACK-10375_  | Bug           | Minor    | Do not create                                              |
|                         |          |                    |               |          | DefaultNuageVspSharedNetworkOfferingWithSGService          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2661`_ |                    |               |          | Make uploadSslCert a POST request instead of a GET         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2639`_ | CLOUDSTACK-10276_  | Bug           | Major    | View volumes from primary storage not working when storage |
|                         |          |                    |               |          | UUID is not a UUID                                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2653`_ |                    |               |          | Generate MAC address if the MAC in command                 |
|                         |          |                    |               |          | addNicToVirtualMachine is invalid                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2656`_ |                    |               |          | Only perform certain actions here with managed storage if  |
|                         |          |                    |               |          | the VM is s?                                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2651`_ | CLOUDSTACK-10290_  | Bug           | Major    | Config drive - only supported for secondary storage        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2473`_ | CLOUDSTACK-10309_  | Improvement   | Minor    | VMs with HA enabled, power back on if shutdown from guest  |
|                         |          |                    |               |          | OS                                                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2655`_ |                    |               |          | Handle Ceph.                                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2630`_ |                    |               |          | Host Affinity plugin                                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2652`_ |                    |               |          | Fix register iso in all zones                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2629`_ |                    |               |          | Fix primary storage count when deleting volumes            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2638`_ |                    |               |          | agent: Fixes #2633 don't wait for pending tasks on         |
|                         |          |                    |               |          | reconnection                                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2645`_ |                    |               |          | config-drive: use hostname of VM instance of internal VM   |
|                         |          |                    |               |          | id                                                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2646`_ |                    |               |          | Don't skip tests while packaging Centos7                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2635`_ |                    |               |          | router: Fixes #2544 run passwd server on dhcpserver IP on  |
|                         |          |                    |               |          | rVR                                                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2634`_ | CLOUDSTACK-9184_   | Bug           | Major    | [VMware] vmware.ports.per.dvportgroup global setting is    |
|                         |          |                    |               |          | not useful from vCenter 5.0 onwards                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2508`_ | CLOUDSTACK-9114_   | Improvement   | Major    | restartnetwork with cleanup should not update/restart both |
|                         |          |                    |               |          | routers at once                                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2584`_ |                    |               |          | Enhance and cleanup DatabaseUpgradeChecker                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2600`_ | CLOUDSTACK-10362_  | Improvement   | Major    | Inconsistent method names                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2627`_ |                    |               |          | Catch error in packagin script and fail the build          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2615`_ |                    |               |          | config-drive: support user data on L2 networks             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2632`_ |                    |               |          | listostypes: Fixes #2529 return boolean than string in     |
|                         |          |                    |               |          | response                                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2621`_ |                    |               |          | Backports for 4.11 branch                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2619`_ |                    |               |          | Remove "self-injection" of AccountManagerImpl              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2607`_ |                    |               |          | Allow changing disk offering of VMs' root volume during    |
|                         |          |                    |               |          | volume migration                                           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2626`_ |                    |               |          | bionic: allow Ubuntu 18.04 to be added as KVM host         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2623`_ |                    |               |          | fixes #2611                                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2628`_ |                    |               |          | Create upgrade path from 4.9.3.1 to 4.11.1.0               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2612`_ |                    |               |          | [migrateVolume API method] Filter disk offerings based on  |
|                         |          |                    |               |          | target storage pool selected                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1940`_ | CLOUDSTACK-9781_   | Bug           | Major    | ACS records ID in events tables instead of UUID.           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2608`_ |                    |               |          | API: move ostypeid from DB id to DB uuid                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#2471`_ | CLOUDSTACK-10311_  | Improvement   | Major    | Agent Log Rotate variable replace bug                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2606`_ |                    |               |          | When creating a new account (via domain admin) it is       |
|                         |          |                    |               |          | possible to select ?root admin? as the role for the new    |
|                         |          |                    |               |          | user                                                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2601`_ | CLOUDSTACK-10364_  | Improvement   | Major    | Inconsiste "setXXX" method names.                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2599`_ | CLOUDSTACK-10363_  | Improvement   | Major    | Inconsistent "getXXX" and "listXXX" method names.          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2598`_ | CLOUDSTACK-10360_  | Improvement   | Major    | Inconsistent method name                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2605`_ |                    |               |          | xenserver: Add support for XS 7.3, 7.4 and XCP-ng 7.4      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2428`_ | CLOUDSTACK-10253_  | Bug           | Minor    | JSON response returns boolean as string                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2536`_ |                    |               |          | fix typo c&p bug in externalId feature UI                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2486`_ | CLOUDSTACK-10323_  | Improvement   | Major    | Change disk offering when volume is migrated to different  |
|                         |          |                    |               |          | type of storage pool.                                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2422`_ | CLOUDSTACK-10254_  | Improvement   | Major    | Require checkstyle to verify package names against         |
|                         |          |                    |               |          | directory structure                                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2566`_ | CLOUDSTACK-10288_  | Bug           | Major    | Config drive - Usedata corruption when gzipped             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2573`_ | CLOUDSTACK-10356_  | Bug           | Major    | Fix Some Potential NPE                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2412`_ | CLOUDSTACK-9677_   | Improvement   | Major    | Swift Storage Policy support for Secondary Storage         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2594`_ |                    |               |          | Remove 'NetworkManagerTestComponentLibrary' empty class    |
|                         |          |                    |               |          | and related configurations                                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2597`_ |                    |               |          | UpdateUserCmd: apiSecretKey refers to itself               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2498`_ | CLOUDSTACK-10327_  | Bug           | Critical | SSO fails with error "Session Expired", except for root    |
|                         |          |                    |               |          | admin                                                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2591`_ | CLOUDSTACK-10359_  | Improvement   | Major    | Inconsistent method names                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2590`_ |                    |               |          | network: Fix security groups for CentOS                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2582`_ |                    |               |          | cs-45to411-ugrade-fix: database errors during upgrade to   |
|                         |          |                    |               |          | 4.11                                                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2577`_ |                    |               |          | Prevent NPE if guest OS mapping is missing while           |
|                         |          |                    |               |          | prioritizing hosts                                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2579`_ |                    |               |          | router: fix routing table for marked packets               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2589`_ |                    |               |          | Remove packaging job from pull request template            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2588`_ |                    |               |          | capacity: remove unused threadpool                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2505`_ | CLOUDSTACK-10333_  | Improvement   | Major    | Secure VM Live migration for KVM                           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2580`_ | CLOUDSTACK-10357_  | Improvement   | Minor    | Log messages that do not match with their method function  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2587`_ |                    |               |          | Remove empty VPN test class                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2586`_ |                    |               |          | Use double quotes with 'RROUTER' variable in "common.sh"   |
|                         |          |                    |               |          | script                                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2576`_ |                    |               |          | Fix Python code checkstyle execute by                      |
|                         |          |                    |               |          | "systemvm\test\runtests.sh"                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2562`_ |                    |               |          | consoleproxy: use consoleproxy.domain for non-ssl enable   |
|                         |          |                    |               |          | env                                                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2554`_ |                    |               |          | agent: Add logging to libvirt qemu hook and cleanup        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2511`_ | CLOUDSTACK-10344_  | Bug           | Major    | Sometimes a bug happens when moving ACL rules (changing    |
|                         |          |                    |               |          | their order with drag and drop)                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2572`_ |                    |               |          | Remove 'todb' in favor of 'encodeURIComponent'.            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2553`_ |                    |               |          | Update inconsistent debugging info in catch block          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2499`_ |                    |               |          | Updates to capacity management                             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2570`_ |                    |               |          | Improve README                                             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2568`_ |                    |               |          | Log command output in CsHelper.execute command             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2559`_ |                    |               |          | Upgrade path 4.11 through 4.11.1 to 4.12                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2567`_ |                    |               |          | [Vmware] Fix for OVF parsing error                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2563`_ | CLOUDSTACK-10304_  | Bug           | Major    | SystemVM - Apache Web Server Version Number Information    |
|                         |          |                    |               |          | Disclosure                                                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2555`_ |                    |               |          | Remove 'md5Hashed' variable from Javascript.               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2390`_ | CLOUDSTACK-10214_  | Bug           | Major    | Unable to remove local primary storage                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2564`_ |                    |               |          | [Docs] Fix URL error from installation instructions        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2557`_ |                    |               |          | Add "Fixes: number" to PR template for auto-closing issues |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2404`_ | CLOUDSTACK-10230_  | Bug           | Critical | User is able to change to ?Guest OS type? that has been    |
|                         |          |                    |               |          | removed                                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2550`_ |                    |               |          | debian: Use only `-l` for libvirtd default file on debian  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2560`_ |                    |               |          | ui: Make zonal dashboard larger                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2401`_ | CLOUDSTACK-10226_  | Bug           | Major    | CloudStack is not importing Local storage properly         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2462`_ | CLOUDSTACK-10301_  | Bug           | Major    | Allow updating the network ACL list name and Description   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2490`_ |                    |               |          | Create database upgrade from 4.11.0.0 to 4.11.1.0 & VMWare |
|                         |          |                    |               |          | version to OS mappings                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2538`_ |                    |               |          | Remove deprecated tomcat configuration file instead of     |
|                         |          |                    |               |          | moving it                                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2517`_ |                    |               |          | manual mapped ldap fix                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2552`_ |                    |               |          | debian: remove old usage jars during upgrade               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2535`_ |                    |               |          | Create an easy way to enable Java remote Debug for ACS     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2526`_ |                    |               |          | add issue template for github issues                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2522`_ |                    |               |          | indicate scope of tests in checklist                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2519`_ | CLOUDSTACK-10287_  | Bug           | Major    | Make el7 rpms to depend on OpenJDK8                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2520`_ |                    |               |          | make Broadcast- and IsolationURI visible to admin          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2515`_ |                    |               |          | Fix Successfully typo                                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2414`_ | CLOUDSTACK-10241_  | Bug           | Major    | Duplicated file SRs being created in XenServer pools       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2512`_ |                    |               |          | Only use the host if its Resource State is Enabled.        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2492`_ |                    |               |          | Fix the name of the column used to hold IPv4 range in      |
|                         |          |                    |               |          | 'vlan' table.                                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2496`_ | CLOUDSTACK-10332_  | Enhancement   | Major    | Users are not able to change/edit the protocol of an ACL   |
|                         |          |                    |               |          | rule                                                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2449`_ | CLOUDSTACK-10278_  | Bug           | Major    | Adding a SQL table column is not Idempotent                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2510`_ | CLOUDSTACK-10334_  | Improvement   | Major    | Inadequate information for handling catch clauses          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2506`_ | CLOUDSTACK-10341_  | Task          | Major    | Systemvmtemplate 4.11 changes                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2513`_ | CLOUDSTACK-10227_  | Bug           | Blocker  | Stabilization fixes for master/4.11                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2465`_ | CLOUDSTACK-10232_  | Enhancement   | Major    | SystemVMs and VR to run as HVM on XenServer                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2438`_ | CLOUDSTACK-10307_  | Improvement   | Minor    | Remove unused things from HostDaoImpl                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2507`_ | CLOUDSTACK-10319_  | Bug           | Major    | Prefer TLSv1.2 and deprecate TLS 1.0/1.1                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2397`_ | CLOUDSTACK-10221_  | Improvement   | Major    | Allow specification of IPv6 details when creating Basic    |
|                         |          |                    |               |          | Network                                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2481`_ | CLOUDSTACK-10320_  | Bug           | Major    | Invalid pair for response object breaking response parsing |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2468`_ | CLOUDSTACK-10341_  | Task          | Major    | Systemvmtemplate 4.11 changes                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2504`_ | CLOUDSTACK-10340_  | Task          | Major    | Add setter in vminstancevo                                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2497`_ | CLOUDSTACK-10331_  | Bug           | Minor    | Error 404 for /client/scripts/vm_snapshots.js              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2408`_ | CLOUDSTACK-10231_  | Bug           | Major    | Asserted fixes for Direct Download on KVM                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2494`_ | CLOUDSTACK-10329_  | Enhancement   | Major    | Button in ACL rules page to export all rules as a CSV file |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2495`_ |                    |               |          | Fix typo in Packaging script                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2489`_ | CLOUDSTACK-10330_  | Improvement   | Major    | Introduce a standard PULL REQUEST template                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2491`_ |                    |               |          | Fix "agent-lb" project                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2469`_ | CLOUDSTACK-10132_  | Improvement   | Major    | Extend Multiple Management Servers Support for agents to   |
|                         |          |                    |               |          | allow sorting algorithms                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2458`_ | CLOUDSTACK-10296_  | Bug           | Major    | Fix timestamp difference in heartbeat script for rVRs      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2433`_ | CLOUDSTACK-10268_  | Improvement   | Minor    | Fix and enhance package script                             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2387`_ | CLOUDSTACK-8855_   | Bug           | Major    | Improve Error Message for Host Alert State                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2482`_ | CLOUDSTACK-10321_  | Bug           | Major    | CPU Cap for KVM                                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2483`_ | CLOUDSTACK-10303_  | Improvement   | Major    | refactor plugins/nuagevsp tests to run from its own        |
|                         |          |                    |               |          | test_data.py file                                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2442`_ | CLOUDSTACK-10147_  | Bug           | Major    | Disabled Xenserver cluster can still deploy VMs            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2484`_ |                    |               |          | createNetworkACL: number has the wrong doc                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2475`_ | CLOUDSTACK-10314_  | Improvement   | Minor    | Add Text-Field to each ACL Rule                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2485`_ |                    |               |          | Bump the version of Debian net-installer to 9.4.0          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2480`_ | CLOUDSTACK-10319_  | Bug           | Major    | Prefer TLSv1.2 and deprecate TLS 1.0/1.1                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2470`_ | CLOUDSTACK-10197_  | Bug           | Major    | XenServer 7.1: Cannot mount  xentool iso from cloudstack   |
|                         |          |                    |               |          | on VMs                                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2476`_ | CLOUDSTACK-10317_  | Bug           | Minor    | In case of multiple-public ips, snat fails to work for     |
|                         |          |                    |               |          | addtional public nics/network for guest traffic            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2425`_ | CLOUDSTACK-10240_  | Improvement   | Major    | ACS cannot migrate a volume from local to shared storage   |
|                         |          |                    |               |          | (for XenServer)                                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2448`_ | CLOUDSTACK-10274_  | Bug           | Major    | L2 network refused to be designed on VXLAN physical        |
|                         |          |                    |               |          | network                                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2478`_ | CLOUDSTACK-10318_  | Bug           | Major    | Bug on sorting ACL rules list in chrome                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2437`_ | CLOUDSTACK-10257_  | Improvement   | Minor    | Create template/volume does not allow to specify HVM       |
|                         |          |                    |               |          | requirement                                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2439`_ | CLOUDSTACK-10259_  | Bug           | Minor    | Missing float part of secondary storage data when          |
|                         |          |                    |               |          | calculating secondary storage usage in listAccounts        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2392`_ |                    |               |          | dateutil: constistency of tzdate input and output          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2463`_ | CLOUDSTACK-10302_  | Task          | Major    | Create database path upgrade from 4.11.0.0 to 4.12.0.0     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2464`_ | CLOUDSTACK-10299_  | Bug           | Minor    | Network listing return error in project mode               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2244`_ | CLOUDSTACK-10054_  | Bug           | Major    | Volume download times out in 3600 seconds                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2467`_ | CLOUDSTACK-10306_  | Bug           | Minor    | Update vmware dependency vim jar to 6.5 version            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2460`_ | CLOUDSTACK-10298_  | Bug           | Major    | Recreation of an earlier deleted Nuage managed isolated or |
|                         |          |                    |               |          | vpc tier network fails                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2466`_ | CLOUDSTACK-10305_  | Bug           | Major    | Rare race condition in KVM migration                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2443`_ | CLOUDSTACK-9338_   | Bug           | Major    | updateResourceCount not accounting resources of VMs with   |
|                         |          |                    |               |          | custom service offering                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2451`_ | CLOUDSTACK-10284_  | Bug           | Major    | Creating a snapshot from VM Snapshot generates error if    |
|                         |          |                    |               |          | hypervisor is not KVM.                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2454`_ | CLOUDSTACK-10283_  | Bug           | Major    | Use sudo to execute keystore setup/import for kvm agents,  |
|                         |          |                    |               |          | and fail on keystore setup failures                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2457`_ | CLOUDSTACK-10295_  | Improvement   | Major    | Marvin: add support for password-enabled templates         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2456`_ | CLOUDSTACK-10293_  | Bug           | Major    | Single view network ACL rules listing                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2402`_ | CLOUDSTACK-10128_  | Bug           | Critical | Template from snapshot not merging vhd files               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2432`_ | CLOUDSTACK-10294_  | Improvement   | Major    | Updated code-styling and improvements to security_group.py |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2450`_ | CLOUDSTACK-10282_  | Bug           | Major    | SystemVM - filrewall rules incorrect                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2452`_ | CLOUDSTACK-10285_  | Bug           | Critical | 4.10.0.0 users face upgrade issues when upgrading to       |
|                         |          |                    |               |          | 4.11.0.0                                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2441`_ | CLOUDSTACK-10261_  | Bug           | Critical | Nuage: Multinic: Libvirt nuage-extenstion metadata         |
|                         |          |                    |               |          | contains only one interface.                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2420`_ | CLOUDSTACK-10247_  | Bug           | Major    | L2 network not shared on projects                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2424`_ | CLOUDSTACK-10251_  | Bug           | Major    | HTTPS downloader for Direct Download templates failure     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2421`_ | CLOUDSTACK-10243_  | Bug           | Major    | Updating metadata might hang on VR on "ip rule show"       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2406`_ | CLOUDSTACK-9663_   | Improvement   | Trivial  | updateRole should return updated role as json              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2445`_ | CLOUDSTACK-10218_  | Bug           | Major    | forced network update to a nuage network offering with vr  |
|                         |          |                    |               |          | fails with IllegalArgumentException                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2444`_ | CLOUDSTACK-10269_  | Bug           | Major    | Allow deletion of roles without causing concurrent         |
|                         |          |                    |               |          | exception                                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2405`_ | CLOUDSTACK-10146_  | Bug           | Major    | Bypass Secondary Storage for KVM templates                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2398`_ | CLOUDSTACK-10222_  | Bug           | Major    | Clean previous snaphosts from primary storage when taking  |
|                         |          |                    |               |          | new one                                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2431`_ | CLOUDSTACK-10225_  | Improvement   | Major    | Deprecate com.cloud.utils.StringUtils                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+

.. _`#2712`: https://github.com/apache/cloudstack/pull/2712
.. _`#2714`: https://github.com/apache/cloudstack/pull/2714
.. _`#2715`: https://github.com/apache/cloudstack/pull/2715
.. _`#2493`: https://github.com/apache/cloudstack/pull/2493
.. _CLOUDSTACK-10326: https://issues.apache.org/jira/browse/CLOUDSTACK-10326
.. _`#2716`: https://github.com/apache/cloudstack/pull/2716
.. _`#2681`: https://github.com/apache/cloudstack/pull/2681
.. _`#2670`: https://github.com/apache/cloudstack/pull/2670
.. _`#2710`: https://github.com/apache/cloudstack/pull/2710
.. _`#2706`: https://github.com/apache/cloudstack/pull/2706
.. _`#2699`: https://github.com/apache/cloudstack/pull/2699
.. _`#2705`: https://github.com/apache/cloudstack/pull/2705
.. _CLOUDSTACK-10381: https://issues.apache.org/jira/browse/CLOUDSTACK-10381
.. _`#2704`: https://github.com/apache/cloudstack/pull/2704
.. _`#2693`: https://github.com/apache/cloudstack/pull/2693
.. _`#2697`: https://github.com/apache/cloudstack/pull/2697
.. _`#2686`: https://github.com/apache/cloudstack/pull/2686
.. _`#2696`: https://github.com/apache/cloudstack/pull/2696
.. _`#2683`: https://github.com/apache/cloudstack/pull/2683
.. _`#2694`: https://github.com/apache/cloudstack/pull/2694
.. _`#2688`: https://github.com/apache/cloudstack/pull/2688
.. _CLOUDSTACK-10382: https://issues.apache.org/jira/browse/CLOUDSTACK-10382
.. _`#2672`: https://github.com/apache/cloudstack/pull/2672
.. _CLOUDSTACK-10377: https://issues.apache.org/jira/browse/CLOUDSTACK-10377
.. _`#2674`: https://github.com/apache/cloudstack/pull/2674
.. _`#2673`: https://github.com/apache/cloudstack/pull/2673
.. _`#2676`: https://github.com/apache/cloudstack/pull/2676
.. _`#2669`: https://github.com/apache/cloudstack/pull/2669
.. _`#2669`: https://github.com/apache/cloudstack/pull/2669
.. _`#2664`: https://github.com/apache/cloudstack/pull/2664
.. _`#2663`: https://github.com/apache/cloudstack/pull/2663
.. _`#2667`: https://github.com/apache/cloudstack/pull/2667
.. _CLOUDSTACK-10375: https://issues.apache.org/jira/browse/CLOUDSTACK-10375
.. _`#2661`: https://github.com/apache/cloudstack/pull/2661
.. _`#2639`: https://github.com/apache/cloudstack/pull/2639
.. _CLOUDSTACK-10276: https://issues.apache.org/jira/browse/CLOUDSTACK-10276
.. _`#2653`: https://github.com/apache/cloudstack/pull/2653
.. _`#2656`: https://github.com/apache/cloudstack/pull/2656
.. _`#2651`: https://github.com/apache/cloudstack/pull/2651
.. _CLOUDSTACK-10290: https://issues.apache.org/jira/browse/CLOUDSTACK-10290
.. _`#2651`: https://github.com/apache/cloudstack/pull/2651
.. _CLOUDSTACK-10290: https://issues.apache.org/jira/browse/CLOUDSTACK-10290
.. _`#2473`: https://github.com/apache/cloudstack/pull/2473
.. _CLOUDSTACK-10309: https://issues.apache.org/jira/browse/CLOUDSTACK-10309
.. _`#2473`: https://github.com/apache/cloudstack/pull/2473
.. _CLOUDSTACK-10309: https://issues.apache.org/jira/browse/CLOUDSTACK-10309
.. _`#2655`: https://github.com/apache/cloudstack/pull/2655
.. _`#2630`: https://github.com/apache/cloudstack/pull/2630
.. _`#2652`: https://github.com/apache/cloudstack/pull/2652
.. _`#2629`: https://github.com/apache/cloudstack/pull/2629
.. _`#2638`: https://github.com/apache/cloudstack/pull/2638
.. _`#2638`: https://github.com/apache/cloudstack/pull/2638
.. _`#2645`: https://github.com/apache/cloudstack/pull/2645
.. _`#2645`: https://github.com/apache/cloudstack/pull/2645
.. _`#2646`: https://github.com/apache/cloudstack/pull/2646
.. _`#2635`: https://github.com/apache/cloudstack/pull/2635
.. _`#2635`: https://github.com/apache/cloudstack/pull/2635
.. _`#2634`: https://github.com/apache/cloudstack/pull/2634
.. _CLOUDSTACK-9184: https://issues.apache.org/jira/browse/CLOUDSTACK-9184
.. _`#2634`: https://github.com/apache/cloudstack/pull/2634
.. _CLOUDSTACK-9184: https://issues.apache.org/jira/browse/CLOUDSTACK-9184
.. _`#2508`: https://github.com/apache/cloudstack/pull/2508
.. _CLOUDSTACK-9114: https://issues.apache.org/jira/browse/CLOUDSTACK-9114
.. _`#2508`: https://github.com/apache/cloudstack/pull/2508
.. _CLOUDSTACK-9114: https://issues.apache.org/jira/browse/CLOUDSTACK-9114
.. _`#2584`: https://github.com/apache/cloudstack/pull/2584
.. _`#2600`: https://github.com/apache/cloudstack/pull/2600
.. _CLOUDSTACK-10362: https://issues.apache.org/jira/browse/CLOUDSTACK-10362
.. _`#2627`: https://github.com/apache/cloudstack/pull/2627
.. _`#2615`: https://github.com/apache/cloudstack/pull/2615
.. _`#2632`: https://github.com/apache/cloudstack/pull/2632
.. _`#2621`: https://github.com/apache/cloudstack/pull/2621
.. _`#2619`: https://github.com/apache/cloudstack/pull/2619
.. _`#2607`: https://github.com/apache/cloudstack/pull/2607
.. _`#2626`: https://github.com/apache/cloudstack/pull/2626
.. _`#2623`: https://github.com/apache/cloudstack/pull/2623
.. _`#2628`: https://github.com/apache/cloudstack/pull/2628
.. _`#2628`: https://github.com/apache/cloudstack/pull/2628
.. _`#2612`: https://github.com/apache/cloudstack/pull/2612
.. _`#1940`: https://github.com/apache/cloudstack/pull/1940
.. _CLOUDSTACK-9781: https://issues.apache.org/jira/browse/CLOUDSTACK-9781
.. _`#2608`: https://github.com/apache/cloudstack/pull/2608
.. _`#2574`: https://github.com/apache/cloudstack/pull/2574
.. _`#2471`: https://github.com/apache/cloudstack/pull/2471
.. _CLOUDSTACK-10311: https://issues.apache.org/jira/browse/CLOUDSTACK-10311
.. _`#2606`: https://github.com/apache/cloudstack/pull/2606
.. _`#2601`: https://github.com/apache/cloudstack/pull/2601
.. _CLOUDSTACK-10364: https://issues.apache.org/jira/browse/CLOUDSTACK-10364
.. _`#2599`: https://github.com/apache/cloudstack/pull/2599
.. _CLOUDSTACK-10363: https://issues.apache.org/jira/browse/CLOUDSTACK-10363
.. _`#2598`: https://github.com/apache/cloudstack/pull/2598
.. _CLOUDSTACK-10360: https://issues.apache.org/jira/browse/CLOUDSTACK-10360
.. _`#2605`: https://github.com/apache/cloudstack/pull/2605
.. _`#2428`: https://github.com/apache/cloudstack/pull/2428
.. _CLOUDSTACK-10253: https://issues.apache.org/jira/browse/CLOUDSTACK-10253
.. _`#2536`: https://github.com/apache/cloudstack/pull/2536
.. _`#2486`: https://github.com/apache/cloudstack/pull/2486
.. _CLOUDSTACK-10323: https://issues.apache.org/jira/browse/CLOUDSTACK-10323
.. _`#2422`: https://github.com/apache/cloudstack/pull/2422
.. _CLOUDSTACK-10254: https://issues.apache.org/jira/browse/CLOUDSTACK-10254
.. _`#2566`: https://github.com/apache/cloudstack/pull/2566
.. _CLOUDSTACK-10288: https://issues.apache.org/jira/browse/CLOUDSTACK-10288
.. _`#2573`: https://github.com/apache/cloudstack/pull/2573
.. _CLOUDSTACK-10356: https://issues.apache.org/jira/browse/CLOUDSTACK-10356
.. _`#2412`: https://github.com/apache/cloudstack/pull/2412
.. _CLOUDSTACK-9677: https://issues.apache.org/jira/browse/CLOUDSTACK-9677
.. _`#2594`: https://github.com/apache/cloudstack/pull/2594
.. _`#2597`: https://github.com/apache/cloudstack/pull/2597
.. _`#2498`: https://github.com/apache/cloudstack/pull/2498
.. _CLOUDSTACK-10327: https://issues.apache.org/jira/browse/CLOUDSTACK-10327
.. _`#2591`: https://github.com/apache/cloudstack/pull/2591
.. _CLOUDSTACK-10359: https://issues.apache.org/jira/browse/CLOUDSTACK-10359
.. _`#2590`: https://github.com/apache/cloudstack/pull/2590
.. _`#2582`: https://github.com/apache/cloudstack/pull/2582
.. _`#2577`: https://github.com/apache/cloudstack/pull/2577
.. _`#2579`: https://github.com/apache/cloudstack/pull/2579
.. _`#2589`: https://github.com/apache/cloudstack/pull/2589
.. _`#2588`: https://github.com/apache/cloudstack/pull/2588
.. _`#2505`: https://github.com/apache/cloudstack/pull/2505
.. _CLOUDSTACK-10333: https://issues.apache.org/jira/browse/CLOUDSTACK-10333
.. _`#2580`: https://github.com/apache/cloudstack/pull/2580
.. _CLOUDSTACK-10357: https://issues.apache.org/jira/browse/CLOUDSTACK-10357
.. _`#2587`: https://github.com/apache/cloudstack/pull/2587
.. _`#2586`: https://github.com/apache/cloudstack/pull/2586
.. _`#2576`: https://github.com/apache/cloudstack/pull/2576
.. _`#2562`: https://github.com/apache/cloudstack/pull/2562
.. _`#2554`: https://github.com/apache/cloudstack/pull/2554
.. _`#2511`: https://github.com/apache/cloudstack/pull/2511
.. _CLOUDSTACK-10344: https://issues.apache.org/jira/browse/CLOUDSTACK-10344
.. _`#2572`: https://github.com/apache/cloudstack/pull/2572
.. _`#2553`: https://github.com/apache/cloudstack/pull/2553
.. _`#2499`: https://github.com/apache/cloudstack/pull/2499
.. _`#2570`: https://github.com/apache/cloudstack/pull/2570
.. _`#2568`: https://github.com/apache/cloudstack/pull/2568
.. _`#2559`: https://github.com/apache/cloudstack/pull/2559
.. _`#2567`: https://github.com/apache/cloudstack/pull/2567
.. _`#2563`: https://github.com/apache/cloudstack/pull/2563
.. _CLOUDSTACK-10304: https://issues.apache.org/jira/browse/CLOUDSTACK-10304
.. _`#2555`: https://github.com/apache/cloudstack/pull/2555
.. _`#2390`: https://github.com/apache/cloudstack/pull/2390
.. _CLOUDSTACK-10214: https://issues.apache.org/jira/browse/CLOUDSTACK-10214
.. _`#2564`: https://github.com/apache/cloudstack/pull/2564
.. _`#2557`: https://github.com/apache/cloudstack/pull/2557
.. _`#2404`: https://github.com/apache/cloudstack/pull/2404
.. _CLOUDSTACK-10230: https://issues.apache.org/jira/browse/CLOUDSTACK-10230
.. _`#2550`: https://github.com/apache/cloudstack/pull/2550
.. _`#2560`: https://github.com/apache/cloudstack/pull/2560
.. _`#2401`: https://github.com/apache/cloudstack/pull/2401
.. _CLOUDSTACK-10226: https://issues.apache.org/jira/browse/CLOUDSTACK-10226
.. _`#2462`: https://github.com/apache/cloudstack/pull/2462
.. _CLOUDSTACK-10301: https://issues.apache.org/jira/browse/CLOUDSTACK-10301
.. _`#2490`: https://github.com/apache/cloudstack/pull/2490
.. _`#2538`: https://github.com/apache/cloudstack/pull/2538
.. _`#2517`: https://github.com/apache/cloudstack/pull/2517
.. _`#2552`: https://github.com/apache/cloudstack/pull/2552
.. _`#2535`: https://github.com/apache/cloudstack/pull/2535
.. _`#2526`: https://github.com/apache/cloudstack/pull/2526
.. _`#2522`: https://github.com/apache/cloudstack/pull/2522
.. _`#2519`: https://github.com/apache/cloudstack/pull/2519
.. _CLOUDSTACK-10287: https://issues.apache.org/jira/browse/CLOUDSTACK-10287
.. _`#2520`: https://github.com/apache/cloudstack/pull/2520
.. _`#2515`: https://github.com/apache/cloudstack/pull/2515
.. _`#2414`: https://github.com/apache/cloudstack/pull/2414
.. _CLOUDSTACK-10241: https://issues.apache.org/jira/browse/CLOUDSTACK-10241
.. _`#2512`: https://github.com/apache/cloudstack/pull/2512
.. _`#2492`: https://github.com/apache/cloudstack/pull/2492
.. _`#2496`: https://github.com/apache/cloudstack/pull/2496
.. _CLOUDSTACK-10332: https://issues.apache.org/jira/browse/CLOUDSTACK-10332
.. _`#2449`: https://github.com/apache/cloudstack/pull/2449
.. _CLOUDSTACK-10278: https://issues.apache.org/jira/browse/CLOUDSTACK-10278
.. _`#2510`: https://github.com/apache/cloudstack/pull/2510
.. _CLOUDSTACK-10334: https://issues.apache.org/jira/browse/CLOUDSTACK-10334
.. _`#2506`: https://github.com/apache/cloudstack/pull/2506
.. _CLOUDSTACK-10341: https://issues.apache.org/jira/browse/CLOUDSTACK-10341
.. _`#2506`: https://github.com/apache/cloudstack/pull/2506
.. _CLOUDSTACK-10341: https://issues.apache.org/jira/browse/CLOUDSTACK-10341
.. _`#2513`: https://github.com/apache/cloudstack/pull/2513
.. _CLOUDSTACK-10227: https://issues.apache.org/jira/browse/CLOUDSTACK-10227
.. _`#2513`: https://github.com/apache/cloudstack/pull/2513
.. _CLOUDSTACK-10227: https://issues.apache.org/jira/browse/CLOUDSTACK-10227
.. _`#2465`: https://github.com/apache/cloudstack/pull/2465
.. _CLOUDSTACK-10232: https://issues.apache.org/jira/browse/CLOUDSTACK-10232
.. _`#2438`: https://github.com/apache/cloudstack/pull/2438
.. _CLOUDSTACK-10307: https://issues.apache.org/jira/browse/CLOUDSTACK-10307
.. _`#2465`: https://github.com/apache/cloudstack/pull/2465
.. _CLOUDSTACK-10232: https://issues.apache.org/jira/browse/CLOUDSTACK-10232
.. _`#2507`: https://github.com/apache/cloudstack/pull/2507
.. _CLOUDSTACK-10319: https://issues.apache.org/jira/browse/CLOUDSTACK-10319
.. _`#2507`: https://github.com/apache/cloudstack/pull/2507
.. _CLOUDSTACK-10319: https://issues.apache.org/jira/browse/CLOUDSTACK-10319
.. _`#2397`: https://github.com/apache/cloudstack/pull/2397
.. _CLOUDSTACK-10221: https://issues.apache.org/jira/browse/CLOUDSTACK-10221
.. _`#2481`: https://github.com/apache/cloudstack/pull/2481
.. _CLOUDSTACK-10320: https://issues.apache.org/jira/browse/CLOUDSTACK-10320
.. _`#2468`: https://github.com/apache/cloudstack/pull/2468
.. _CLOUDSTACK-10341: https://issues.apache.org/jira/browse/CLOUDSTACK-10341
.. _`#2504`: https://github.com/apache/cloudstack/pull/2504
.. _CLOUDSTACK-10340: https://issues.apache.org/jira/browse/CLOUDSTACK-10340
.. _`#2497`: https://github.com/apache/cloudstack/pull/2497
.. _CLOUDSTACK-10331: https://issues.apache.org/jira/browse/CLOUDSTACK-10331
.. _`#2408`: https://github.com/apache/cloudstack/pull/2408
.. _CLOUDSTACK-10231: https://issues.apache.org/jira/browse/CLOUDSTACK-10231
.. _`#2494`: https://github.com/apache/cloudstack/pull/2494
.. _CLOUDSTACK-10329: https://issues.apache.org/jira/browse/CLOUDSTACK-10329
.. _`#2495`: https://github.com/apache/cloudstack/pull/2495
.. _`#2489`: https://github.com/apache/cloudstack/pull/2489
.. _CLOUDSTACK-10330: https://issues.apache.org/jira/browse/CLOUDSTACK-10330
.. _`#2491`: https://github.com/apache/cloudstack/pull/2491
.. _`#2469`: https://github.com/apache/cloudstack/pull/2469
.. _CLOUDSTACK-10132: https://issues.apache.org/jira/browse/CLOUDSTACK-10132
.. _`#2458`: https://github.com/apache/cloudstack/pull/2458
.. _CLOUDSTACK-10296: https://issues.apache.org/jira/browse/CLOUDSTACK-10296
.. _`#2433`: https://github.com/apache/cloudstack/pull/2433
.. _CLOUDSTACK-10268: https://issues.apache.org/jira/browse/CLOUDSTACK-10268
.. _`#2387`: https://github.com/apache/cloudstack/pull/2387
.. _CLOUDSTACK-8855: https://issues.apache.org/jira/browse/CLOUDSTACK-8855
.. _`#2482`: https://github.com/apache/cloudstack/pull/2482
.. _CLOUDSTACK-10321: https://issues.apache.org/jira/browse/CLOUDSTACK-10321
.. _`#2483`: https://github.com/apache/cloudstack/pull/2483
.. _CLOUDSTACK-10303: https://issues.apache.org/jira/browse/CLOUDSTACK-10303
.. _`#2442`: https://github.com/apache/cloudstack/pull/2442
.. _CLOUDSTACK-10147: https://issues.apache.org/jira/browse/CLOUDSTACK-10147
.. _`#2484`: https://github.com/apache/cloudstack/pull/2484
.. _`#2475`: https://github.com/apache/cloudstack/pull/2475
.. _CLOUDSTACK-10314: https://issues.apache.org/jira/browse/CLOUDSTACK-10314
.. _`#2485`: https://github.com/apache/cloudstack/pull/2485
.. _`#2480`: https://github.com/apache/cloudstack/pull/2480
.. _CLOUDSTACK-10319: https://issues.apache.org/jira/browse/CLOUDSTACK-10319
.. _`#2470`: https://github.com/apache/cloudstack/pull/2470
.. _CLOUDSTACK-10197: https://issues.apache.org/jira/browse/CLOUDSTACK-10197
.. _`#2476`: https://github.com/apache/cloudstack/pull/2476
.. _CLOUDSTACK-10317: https://issues.apache.org/jira/browse/CLOUDSTACK-10317
.. _`#2425`: https://github.com/apache/cloudstack/pull/2425
.. _CLOUDSTACK-10240: https://issues.apache.org/jira/browse/CLOUDSTACK-10240
.. _`#2448`: https://github.com/apache/cloudstack/pull/2448
.. _CLOUDSTACK-10274: https://issues.apache.org/jira/browse/CLOUDSTACK-10274
.. _`#2478`: https://github.com/apache/cloudstack/pull/2478
.. _CLOUDSTACK-10318: https://issues.apache.org/jira/browse/CLOUDSTACK-10318
.. _`#2437`: https://github.com/apache/cloudstack/pull/2437
.. _CLOUDSTACK-10257: https://issues.apache.org/jira/browse/CLOUDSTACK-10257
.. _`#2439`: https://github.com/apache/cloudstack/pull/2439
.. _CLOUDSTACK-10259: https://issues.apache.org/jira/browse/CLOUDSTACK-10259
.. _`#2392`: https://github.com/apache/cloudstack/pull/2392
.. _`#2463`: https://github.com/apache/cloudstack/pull/2463
.. _CLOUDSTACK-10302: https://issues.apache.org/jira/browse/CLOUDSTACK-10302
.. _`#2464`: https://github.com/apache/cloudstack/pull/2464
.. _CLOUDSTACK-10299: https://issues.apache.org/jira/browse/CLOUDSTACK-10299
.. _`#2244`: https://github.com/apache/cloudstack/pull/2244
.. _CLOUDSTACK-10054: https://issues.apache.org/jira/browse/CLOUDSTACK-10054
.. _`#2467`: https://github.com/apache/cloudstack/pull/2467
.. _CLOUDSTACK-10306: https://issues.apache.org/jira/browse/CLOUDSTACK-10306
.. _`#2460`: https://github.com/apache/cloudstack/pull/2460
.. _CLOUDSTACK-10298: https://issues.apache.org/jira/browse/CLOUDSTACK-10298
.. _`#2466`: https://github.com/apache/cloudstack/pull/2466
.. _CLOUDSTACK-10305: https://issues.apache.org/jira/browse/CLOUDSTACK-10305
.. _`#2443`: https://github.com/apache/cloudstack/pull/2443
.. _CLOUDSTACK-9338: https://issues.apache.org/jira/browse/CLOUDSTACK-9338
.. _`#2451`: https://github.com/apache/cloudstack/pull/2451
.. _CLOUDSTACK-10284: https://issues.apache.org/jira/browse/CLOUDSTACK-10284
.. _`#2454`: https://github.com/apache/cloudstack/pull/2454
.. _CLOUDSTACK-10283: https://issues.apache.org/jira/browse/CLOUDSTACK-10283
.. _`#2457`: https://github.com/apache/cloudstack/pull/2457
.. _CLOUDSTACK-10295: https://issues.apache.org/jira/browse/CLOUDSTACK-10295
.. _`#2456`: https://github.com/apache/cloudstack/pull/2456
.. _CLOUDSTACK-10293: https://issues.apache.org/jira/browse/CLOUDSTACK-10293
.. _`#2402`: https://github.com/apache/cloudstack/pull/2402
.. _CLOUDSTACK-10128: https://issues.apache.org/jira/browse/CLOUDSTACK-10128
.. _`#2432`: https://github.com/apache/cloudstack/pull/2432
.. _CLOUDSTACK-10294: https://issues.apache.org/jira/browse/CLOUDSTACK-10294
.. _`#2450`: https://github.com/apache/cloudstack/pull/2450
.. _CLOUDSTACK-10282: https://issues.apache.org/jira/browse/CLOUDSTACK-10282
.. _`#2452`: https://github.com/apache/cloudstack/pull/2452
.. _CLOUDSTACK-10285: https://issues.apache.org/jira/browse/CLOUDSTACK-10285
.. _`#2441`: https://github.com/apache/cloudstack/pull/2441
.. _CLOUDSTACK-10261: https://issues.apache.org/jira/browse/CLOUDSTACK-10261
.. _`#2420`: https://github.com/apache/cloudstack/pull/2420
.. _CLOUDSTACK-10247: https://issues.apache.org/jira/browse/CLOUDSTACK-10247
.. _`#2424`: https://github.com/apache/cloudstack/pull/2424
.. _CLOUDSTACK-10251: https://issues.apache.org/jira/browse/CLOUDSTACK-10251
.. _`#2421`: https://github.com/apache/cloudstack/pull/2421
.. _CLOUDSTACK-10243: https://issues.apache.org/jira/browse/CLOUDSTACK-10243
.. _`#2406`: https://github.com/apache/cloudstack/pull/2406
.. _CLOUDSTACK-9663: https://issues.apache.org/jira/browse/CLOUDSTACK-9663
.. _`#2445`: https://github.com/apache/cloudstack/pull/2445
.. _CLOUDSTACK-10218: https://issues.apache.org/jira/browse/CLOUDSTACK-10218
.. _`#2444`: https://github.com/apache/cloudstack/pull/2444
.. _CLOUDSTACK-10269: https://issues.apache.org/jira/browse/CLOUDSTACK-10269
.. _`#2405`: https://github.com/apache/cloudstack/pull/2405
.. _CLOUDSTACK-10146: https://issues.apache.org/jira/browse/CLOUDSTACK-10146
.. _`#2398`: https://github.com/apache/cloudstack/pull/2398
.. _CLOUDSTACK-10222: https://issues.apache.org/jira/browse/CLOUDSTACK-10222
.. _`#2431`: https://github.com/apache/cloudstack/pull/2431
.. _CLOUDSTACK-10225: https://issues.apache.org/jira/browse/CLOUDSTACK-10225

Issues Fixed in 4.11.0.0
------------------------

.. cssclass:: table-striped table-bordered table-hover

+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| Branches                | Github   | Jira               | Type          | Priority | Description                                                |
+=========================+==========+====================+===============+==========+============================================================+
| 4.11                    | `#2097`_ | CLOUDSTACK-9813_   | New Feature   | Major    | Use configdrive for userdata, metadata & password          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2146`_ | CLOUDSTACK-4757_   | New Feature   | Minor    | Support OVA files with multiple disks for templates        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2394`_ | CLOUDSTACK-10109_  | New Feature   | Major    | Enable dedication of public IPs to SSVM and CPVM           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2295`_ | CLOUDSTACK-10109_  | New Feature   | Major    | Enable dedication of public IPs to SSVM and CPVM           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2381`_ | CLOUDSTACK-10117_  | New Feature   | Major    | LDAP mapping on domain level                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2368`_ | CLOUDSTACK-10126_  | New Feature   | Major    | Separate Subnet for CPVM and SSVM                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2046`_ | CLOUDSTACK-7958_   | New Feature   | Minor    | Limit user login to specific subnets                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2374`_ | CLOUDSTACK-10024_  | New Feature   | Major    | Physical Networking Migration                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2301`_ | CLOUDSTACK-10121_  | New Feature   | Major    | move user API                                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2360`_ | CLOUDSTACK-10189_  | New Feature   | Major    | Support for "VSD managed" networks with Nuage Networks     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2281`_ | CLOUDSTACK-10102_  | New Feature   | Major    | New Network Type (L2)                                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2048`_ | CLOUDSTACK-9880_   | New Feature   | Major    | Expansion of Management IP Range.                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2294`_ | CLOUDSTACK-10039_  | New Feature   | Major    | Adding IOPS/GB offering                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2356`_ | CLOUDSTACK-8313_   | New Feature   | Major    | Local Storage overprovisioning should be possible          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2028`_ | CLOUDSTACK-9853_   | New Feature   | Major    | IPv6 Prefix Delegation support in Basic Networking         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1981`_ | CLOUDSTACK-9806_   | New Feature   | Major    | Nuage domain template selection per VPC                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2325`_ | CLOUDSTACK-9998_   | New Feature   | Major    | CloudStack exporter for Prometheus                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2284`_ | CLOUDSTACK-10103_  | New Feature   | Major    | Cloudian Connector for CloudStack                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2297`_ | CLOUDSTACK-9957_   | New Feature   | Major    | Annotations on entities                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2181`_ | CLOUDSTACK-9957_   | New Feature   | Major    | Annotations on entities                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2286`_ | CLOUDSTACK-9993_   | New Feature   | Major    | Secure Agent Communications                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2287`_ | CLOUDSTACK-9998_   | New Feature   | Major    | CloudStack exporter for Prometheus                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2278`_ | CLOUDSTACK-9993_   | New Feature   | Major    | Secure Agent Communications                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1707`_ | CLOUDSTACK-9397_   | New Feature   | Major    | Add Watchdog timer to KVM Instances                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2143`_ | CLOUDSTACK-9949_   | New Feature   | Minor    | add ability to specify mac address when                    |
|                         |          |                    |               |          | deployVirtualMachine or addNicToVirtualMachine is called   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2256`_ | CLOUDSTACK-9782_   | New Feature   | Major    | Host HA                                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2239`_ | CLOUDSTACK-9993_   | New Feature   | Major    | Secure Agent Communications                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2222`_ | CLOUDSTACK-10022_  | New Feature   | Minor    | Allow domain admin to create and delete subdomains         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2026`_ | CLOUDSTACK-9861_   | New Feature   | Major    | Expire VM snapshots after configured duration              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2218`_ | CLOUDSTACK-9782_   | New Feature   | Major    | Host HA                                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11*                   | `#2407`_ | CLOUDSTACK-10227_  | Bug           | Blocker  | Stabilization fixes for master/4.11                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2403`_ | CLOUDSTACK-10227_  | Bug           | Blocker  | Stabilization fixes for master/4.11                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2396`_ | CLOUDSTACK-10220_  | Bug           | Major    | IPv4 NIC alias is not added on Virtual Router in Basic     |
|                         |          |                    |               |          | Networking when NIC has IPv6 address                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2362`_ | CLOUDSTACK-10188_  | Bug           | Major    | Resource Accounting for primary storage is Broken          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2393`_ | CLOUDSTACK-10217_  | Bug           | Major    | When IPv4 address of Instance is updated DHCP data is not  |
|                         |          |                    |               |          | cleared on VR                                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2388`_ | CLOUDSTACK-10212_  | Bug           | Major    | Changing IPv4 Address of NIC in Basic Networking does not  |
|                         |          |                    |               |          | update the gateway                                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2379`_ | CLOUDSTACK-10146_  | Bug           | Major    | Bypass Secondary Storage for KVM templates                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2391`_ | CLOUDSTACK-10215_  | Bug           | Major    | Excessive log4j debug level in CPVM, SSVM could lead to FS |
|                         |          |                    |               |          | overflow                                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2139`_ | CLOUDSTACK-9921_   | Bug           | Major    | NPE when garbage collector is running                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2088`_ | CLOUDSTACK-9892_   | Bug           | Critical | Primary storage resource check is broken when using root   |
|                         |          |                    |               |          | disk size override to deploy VM                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2365`_ | CLOUDSTACK-10197_  | Bug           | Major    | XenServer 7.1: Cannot mount  xentool iso from cloudstack   |
|                         |          |                    |               |          | on VMs                                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2073`_ | CLOUDSTACK-9896_   | Bug           | Minor    | ListDedicatedXXX doesn't respect pagination                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2386`_ | CLOUDSTACK-9632_   | Bug           | Major    | Upgrade bountycastle to 1.55+                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2315`_ | CLOUDSTACK-9025_   | Bug           | Critical | Unable to deploy VM instance from template if template     |
|                         |          |                    |               |          | spin from linked clone snapshot                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2274`_ | CLOUDSTACK-10096_  | Bug           | Major    | Can't reset api.integration.port and                       |
|                         |          |                    |               |          | usage.sanity.check.interval back to null                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2282`_ | CLOUDSTACK-10104_  | Bug           | Major    | Optimize database transactions in ListDomain API to        |
|                         |          |                    |               |          | improve performance                                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2385`_ | CLOUDSTACK-10211_  | Bug           | Major    | test_nuage_public_sharednetwork_userdata fails due to      |
|                         |          |                    |               |          | errortext changed                                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2260`_ | CLOUDSTACK-10065_  | Bug           | Major    | Optimize SQL queries in listTemplate API to improve        |
|                         |          |                    |               |          | performance.                                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1740`_ | CLOUDSTACK-9572_   | Bug           | Major    | Snapshot on primary storage not cleaned up after Storage   |
|                         |          |                    |               |          | migration                                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2104`_ | CLOUDSTACK-9908_   | Bug           | Major    | Primary Storage allocated capacity goes very high after VM |
|                         |          |                    |               |          | snapshot                                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2378`_ | CLOUDSTACK-10205_  | Bug           | Major    | LinkDomainToLdap returns internal id                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1773`_ | CLOUDSTACK-9607_   | Bug           | Major    | Preventing template deletion when template is in use.      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2149`_ | CLOUDSTACK-9932_   | Bug           | Major    | Snapshot is getting deleted while volume creation from the |
|                         |          |                    |               |          | snapshot is in progress                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2156`_ | CLOUDSTACK-9971_   | Bug           | Minor    | Bugfix/listaccounts parameter consistency                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2373`_ | CLOUDSTACK-10202_  | Bug           | Major    | createSnapshotPolicy API create multiple entries in DB for |
|                         |          |                    |               |          | same volume.                                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2344`_ | CLOUDSTACK-10163_  | Bug           | Major    | Component tests health check                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1760`_ | CLOUDSTACK-9593_   | Bug           | Major    | User data check is inconsistent with python                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2352`_ | CLOUDSTACK-10175_  | Bug           | Major    | Listing VPCs with a domain account and project id -1       |
|                         |          |                    |               |          | returns all the VPCs in the syste                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2347`_ | CLOUDSTACK-10166_  | Bug           | Minor    | Cannot add a tag to a NetworkACL (rule not list) in CS     |
|                         |          |                    |               |          | with a user in a project or in an account                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2375`_ | CLOUDSTACK-9456_   | Bug           | Major    | Migrate master to use Java8 and Spring4                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2211`_ | CLOUDSTACK-10013_  | Bug           | Major    | Migrate to Debian9 systemvmtemplate                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#2304`_ | CLOUDSTACK-10127_  | Bug           | Critical | 4.9 / 4.10 KVM + openvswitch + vpc + static nat /          |
|                         |          |                    |               |          | secondary ip on eth2                                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2208`_ | CLOUDSTACK-9542_   | Bug           | Major    | listNics API does not return data as per API documentation |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2351`_ | CLOUDSTACK-10173_  | Bug           | Major    | Guest/Public nics on VR should pick network rate from      |
|                         |          |                    |               |          | network offering                                           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2370`_ | CLOUDSTACK-9595_   | Bug           | Major    | Transactions are not getting retried in case of database   |
|                         |          |                    |               |          | deadlock errors                                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2366`_ | CLOUDSTACK-10168_  | Bug           | Major    | VR duplicate entries in /etc/hosts when reusing VM name    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2042`_ | CLOUDSTACK-9875_   | Bug           | Major    | Unable to re-apply Explicit dedication to VM               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2364`_ | CLOUDSTACK-10195_  | Bug           | Minor    | CloudStack MySQL HA problem -- No database selected        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2361`_ | CLOUDSTACK-10190_  | Bug           | Major    | Duplicate public VLAN for two different admin accounts.    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2247`_ | CLOUDSTACK-10012_  | Bug           | Major    | Migrate to Embedded Jetty based mgmt server                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1964`_ | CLOUDSTACK-9800_   | Bug           | Major    | Enable inline mode for NetScaler device                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1762`_ | CLOUDSTACK-9595_   | Bug           | Major    | Transactions are not getting retried in case of database   |
|                         |          |                    |               |          | deadlock errors                                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2308`_ | CLOUDSTACK-8908_   | Bug           | Major    | After copying the template charging for that template is   |
|                         |          |                    |               |          | stopped                                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2354`_ | CLOUDSTACK-10176_  | Bug           | Major    | VM Start Api Job returns success for failed Job            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2353`_ | CLOUDSTACK-9986_   | Bug           | Major    | Consider overcommit ratios with total/threshold values in  |
|                         |          |                    |               |          | Metrics View                                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2358`_ | CLOUDSTACK-9736_   | Bug           | Minor    | Incoherent validation and error message when you change    |
|                         |          |                    |               |          | the vm.password.length configuration parameter             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2326`_ | CLOUDSTACK-10184_  | Bug           | Major    | Re-work method QuotaResponseBuilderImpl.startOfNextDay and |
|                         |          |                    |               |          | its test cases                                             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2267`_ | CLOUDSTACK-10077_  | Bug           | Major    | Allow account to use the same site-2-site VPN gateway with |
|                         |          |                    |               |          | different configs for several VPCs                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2337`_ | CLOUDSTACK-10157_  | Bug           | Major    | Wrong notification while migration                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2355`_ | CLOUDSTACK-10177_  | Bug           | Major    | NPE when programming Security Groups with KVM              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2349`_ | CLOUDSTACK-10070_  | Bug           | Major    | Extend travis run to include more component tests          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2312`_ | CLOUDSTACK-7793_   | Bug           | Critical | [Snapshots]Create Snaphot with "quiesce" option set to     |
|                         |          |                    |               |          | true fails with "InvalidParameterValueException: can't     |
|                         |          |                    |               |          | handle quiescevm equal true for volume snapshot"           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2345`_ | CLOUDSTACK-10164_  | Bug           | Blocker  | UI - not able to create a VPC                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2263`_ | CLOUDSTACK-10070_  | Bug           | Major    | Extend travis run to include more component tests          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2342`_ | CLOUDSTACK-9586_   | Bug           | Critical | When using local storage with Xenserver prepareTemplate    |
|                         |          |                    |               |          | does not work with multiple primary store                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2124`_ | CLOUDSTACK-9432_   | Bug           | Critical | Dedicate Cluster to Domain always creates an affinity      |
|                         |          |                    |               |          | group owned by the root domain                             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2322`_ | CLOUDSTACK-10140_  | Bug           | Critical | When template is created from snapshot template.properties |
|                         |          |                    |               |          | are corrupted                                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2335`_ | CLOUDSTACK-10154_  | Bug           | Major    | test failures in smoketest                                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2341`_ | CLOUDSTACK-10160_  | Bug           | Major    | KVM VirtIO-SCSI not defined properly in Libvirt XML        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2321`_ | CLOUDSTACK-10138_  | Bug           | Major    | Load br_netfilter in security_group management script      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2334`_ | CLOUDSTACK-10152_  | Bug           | Major    | egress destination cidr with 0.0.0.0/0 is failing          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2310`_ | CLOUDSTACK-10133_  | Bug           | Major    | Local storage overprovisioning for ext file system         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2303`_ | CLOUDSTACK-10123_  | Bug           | Major    | VmWork job gets deleted before the parent job had time to  |
|                         |          |                    |               |          | fetch its result                                           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2329`_ | CLOUDSTACK-10012_  | Bug           | Major    | Migrate to Embedded Jetty based mgmt server                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2327`_ | CLOUDSTACK-10129_  | Bug           | Trivial  | Show instances attached to a network/VR via navigation     |
|                         |          |                    |               |          | from VRs->instances                                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2313`_ | CLOUDSTACK-10135_  | Bug           | Major    | ACL rules order is not maintained for ACL_OUTBOUND in VPC  |
|                         |          |                    |               |          | VR                                                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2316`_ | CLOUDSTACK-10137_  | Bug           | Major    | Re-installation fails for cloudstack-management            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2157`_ | CLOUDSTACK-9961_   | Bug           | Major    | Accept domain name for gateway while creating              |
|                         |          |                    |               |          | Vpncustomergateway                                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2306`_ | CLOUDSTACK-10129_  | Bug           | Trivial  | Show instances attached to a network/VR via navigation     |
|                         |          |                    |               |          | from VRs->instances                                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2273`_ | CLOUDSTACK-10090_  | Bug           | Major    | createPortForwardingRule api call accepts 'halt' as        |
|                         |          |                    |               |          | Protocol which Stops VR                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2240`_ | CLOUDSTACK-10051_  | Bug           | Major    | Mouse Scrolling is not working in instance VM console      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2291`_ | CLOUDSTACK-10111_  | Bug           | Minor    | Fix validation for parameter "vm.password.length"          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2302`_ | CLOUDSTACK-10122_  | Bug           | Major    | Unrelated error message                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2250`_ | CLOUDSTACK-10057_  | Bug           | Major    | ListNetworkOfferingsCmd does not return the correct count  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2268`_ | CLOUDSTACK-10081_  | Bug           | Major    | CloudUtils getDevInfo function only checks for KVM         |
|                         |          |                    |               |          | bridgePort and not OVS                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2293`_ | CLOUDSTACK-10047_  | Bug           | Major    | DVSwitch improvements                                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2288`_ | CLOUDSTACK-10107_  | Bug           | Major    | VMware VM fails to start if it has more than 7 nics        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2257`_ | CLOUDSTACK-10060_  | Bug           | Minor    | ListUsage API always displays the Virtual size as '0' for  |
|                         |          |                    |               |          | Usage type=9 (snapshot)                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2246`_ | CLOUDSTACK-10046_  | Bug           | Major    | checksum is not verified during registerTemplate           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2074`_ | CLOUDSTACK-9899_   | Bug           | Major    | allow download without checking first for MS behind        |
|                         |          |                    |               |          | firewall                                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2279`_ | CLOUDSTACK-9584_   | Bug           | Major    | Increase component tests coverage in Travis run            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2277`_ | CLOUDSTACK-10099_  | Bug           | Major    | GUI invokes migrateVirtualMachine instead of               |
|                         |          |                    |               |          | migrateVirtualMachineWithVolume                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2269`_ | CLOUDSTACK-10083_  | Bug           | Minor    | SSH keys are not created when starting from maintenance    |
|                         |          |                    |               |          | mode                                                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#876`_  | CLOUDSTACK-8865_   | Bug           | Major    | Adding SR doesn't create Storage_pool_host_ref entry for   |
|                         |          |                    |               |          | disabled host                                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1252`_ | CLOUDSTACK-9182_   | Bug           | Major    | Some running VMs turned off on manual migration when auto  |
|                         |          |                    |               |          | migration failed while host preparing for maintenance      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2153`_ | CLOUDSTACK-9956_   | Bug           | Major    | File search on the vmware datastore may select wrong file  |
|                         |          |                    |               |          | if there are multiple files with same name                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2078`_ | CLOUDSTACK-9902_   | Bug           | Minor    | consoleproxy.sslEnabled global config variable is not      |
|                         |          |                    |               |          | present in default install                                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2252`_ | CLOUDSTACK-10067_  | Bug           | Major    | Fix a case where a user 'ro' or 'roo' exists on the system |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2248`_ | CLOUDSTACK-10056_  | Bug           | Minor    | Cannot specify root disk controller when creating VM       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2243`_ | CLOUDSTACK-10019_  | Bug           | Major    | template.properties has hardcoded id                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2261`_ | CLOUDSTACK-10068_  | Bug           | Major    | smoketest/test_iso.py reports assertion failure            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2054`_ | CLOUDSTACK-9886_   | Bug           | Major    | After restarting cloudstack-management , It takes time to  |
|                         |          |                    |               |          | connect hosts                                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#955`_  | CLOUDSTACK-8969_   | Bug           | Major    | VPN customer gateway can't be registered with hostname     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#2262`_ | CLOUDSTACK-10069_  | Bug           | Major    | During release add sha512 suffix to sha 512 checksum/file  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2253`_ | CLOUDSTACK-10061_  | Bug           | Major    | When starting a VM, make sure it has the correct volume    |
|                         |          |                    |               |          | access group                                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2254`_ | CLOUDSTACK-10058_  | Bug           | Major    | Error while opening the Settings tab in Secondary storage  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1733`_ | CLOUDSTACK-9563_   | Bug           | Major    | ExtractTemplate returns malformed URL after migrating NFS  |
|                         |          |                    |               |          | to s3                                                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2188`_ | CLOUDSTACK-10004_  | Bug           | Major    | On deletion, Vmware volume snapshots are left behind with  |
|                         |          |                    |               |          | message 'the snapshot has child, can't delete it on the    |
|                         |          |                    |               |          | storage'                                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#914`_  | CLOUDSTACK-8939_   | Bug           | Major    | VM Snapshot size with memory is not correctly calculated   |
|                         |          |                    |               |          | in cloud.usage_event (XenServer)                           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1985`_ | CLOUDSTACK-9812_   | Bug           | Major    | Update "updatePortForwardingRule" pi to include additional |
|                         |          |                    |               |          | parameter to update the end port in case of port range     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2224`_ | CLOUDSTACK-10032_  | Bug           | Major    | Database entries for templates created from snapshots      |
|                         |          |                    |               |          | disappear after management-server service restart          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2109`_ | CLOUDSTACK-9922_   | Bug           | Major    | Unable  to use 8081 port for Load balancing                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2216`_ | CLOUDSTACK-10027_  | Bug           | Minor    | Repeating the same list for Internal LB in VPC             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2174`_ | CLOUDSTACK-9996_   | Bug           | Major    | bug in network resource that juniper srx firewall          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2186`_ | CLOUDSTACK-10002_  | Bug           | Major    | Restart network with cleanup spawns Redundant Routers(In   |
|                         |          |                    |               |          | Default Network Offering)                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1246`_ | CLOUDSTACK-9165_   | Bug           | Major    | unable to use reserved IP range in a network for external  |
|                         |          |                    |               |          | VMs                                                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#2241`_ | CLOUDSTACK-10052_  | Bug           | Major    | Upgrading to 4.9.2 causes confusion/issues around dynamic  |
|                         |          |                    |               |          | roles usage                                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2221`_ | CLOUDSTACK-10030_  | Bug           | Minor    | Public IPs assgined to the VPC are not reacheable from     |
|                         |          |                    |               |          | inside VPC                                                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2154`_ | CLOUDSTACK-9967_   | Bug           | Major    | [VPC] static nat on additional public subnet ip is not     |
|                         |          |                    |               |          | working.                                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1878`_ | CLOUDSTACK-9717_   | Bug           | Major    | [VMware] RVRs have mismatching MAC addresses for extra     |
|                         |          |                    |               |          | public NICs                                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2013`_ | CLOUDSTACK-9734_   | Bug           | Major    | Destroy VM Fails sometimes                                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2159`_ | CLOUDSTACK-9964_   | Bug           | Critical | Snapahots are getting deleted if VM is assigned to another |
|                         |          |                    |               |          | user                                                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2163`_ | CLOUDSTACK-9939_   | Bug           | Major    | Volumes stuck in Creating state while restarting the       |
|                         |          |                    |               |          | Management Server when the volume creation is in progress  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1919`_ | CLOUDSTACK-9763_   | Bug           | Major    | vpc: can not ssh to instance after vpc restart             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2215`_ | CLOUDSTACK-10026_  | Bug           | Major    | Page for Internal LB VM stucking while loading             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2180`_ | CLOUDSTACK-9999_   | Bug           | Major    | vpc tiers do not work if vpc has more than 8 tiers         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2223`_ | CLOUDSTACK-10031_  | Bug           | Major    | change default configuration for                           |
|                         |          |                    |               |          | router.aggregation.command.each.timeout from 3 to 600      |
|                         |          |                    |               |          | seconds.                                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2182`_ | CLOUDSTACK-10000_  | Bug           | Major    | Remote access vpn user does not work if user password      |
|                         |          |                    |               |          | contains '#'                                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#2233`_ | CLOUDSTACK-10042_  | Bug           | Major    | UI doesn't show ICMP Type and Code for Security Group      |
|                         |          |                    |               |          | rules                                                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2228`_ | CLOUDSTACK-10036_  | Bug           | Major    | Decrease timeout of failing unit test                      |
|                         |          |                    |               |          | HypervisorUtilsTest.java                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1774`_ | CLOUDSTACK-9608_   | Bug           | Major    | Errored State and Abandoned state Templates are not        |
|                         |          |                    |               |          | displayed on UI                                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2144`_ | CLOUDSTACK-9955_   | Bug           | Minor    | Featured Templates/Iso's created by Root/admin user are    |
|                         |          |                    |               |          | not visible to Domain Admin users                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#1966`_ | CLOUDSTACK-9801_   | Bug           | Critical | IPSec VPN does not work after vRouter reboot or recreate   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#2220`_ | CLOUDSTACK-9708_   | Bug           | Major    | Router deployment failed due to two threads start VR       |
|                         |          |                    |               |          | simultaneosuly                                             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1912`_ | CLOUDSTACK-9749_   | Bug           | Critical | cloudstack master vpc_internal_lb feature is broken as     |
|                         |          |                    |               |          | port 8080 is in use by password server on lb VM            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2138`_ | CLOUDSTACK-9944_   | Bug           | Major    | In clustered Management Server, Sometimes hosts stays in   |
|                         |          |                    |               |          | disconnected state.                                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#883`_  | CLOUDSTACK-8906_   | Bug           | Major    | /var/log/cloud/ doesn't get logrotated on xenserver        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2119`_ | CLOUDSTACK-9925_   | Bug           | Minor    | Quota: fix tariff description for memory. Tariff value is  |
|                         |          |                    |               |          | for 1MB of RAM used per month (not hour).                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2145`_ | CLOUDSTACK-9697_   | Bug           | Major    | Better error message on UI user if tries to shrink the VM  |
|                         |          |                    |               |          | ROOT volume size                                           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2137`_ | CLOUDSTACK-9950_   | Bug           | Major    | listUsageRecords doesnt return required fields             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2008`_ | CLOUDSTACK-9840_   | Bug           | Major    | Datetime format of snapshot events is inconsistent with    |
|                         |          |                    |               |          | other events                                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2142`_ | CLOUDSTACK-9954_   | Bug           | Major    | Unable to create service offering with networkrate=0       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2171`_ | CLOUDSTACK-9990_   | Bug           | Minor    | Account name is giving null in event tab after successful  |
|                         |          |                    |               |          | creation of account                                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#1925`_ | CLOUDSTACK-9751_   | Bug           | Major    | if a public IP is assigned to a VM when VR is in starting  |
|                         |          |                    |               |          | state, it does not get applied to the vport in Nuage VSD   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#1798`_ | CLOUDSTACK-9631_   | Bug           | Major    | updateVMAffinityGroup must require one of the list         |
|                         |          |                    |               |          | parameter                                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#2201`_ | CLOUDSTACK-10016_  | Bug           | Major    | VPC VR doesn't respond to DNS requests from remote access  |
|                         |          |                    |               |          | vpn clients                                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1959`_ | CLOUDSTACK-9786_   | Bug           | Major    | API reference guide entry for associateIpAddress needs a   |
|                         |          |                    |               |          | fix                                                        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#1933`_ | CLOUDSTACK-9569_   | Bug           | Critical | VR on shared network not starting on KVM                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2298`_ | CLOUDSTACK-9620_   | Improvement   | Major    | Improvements for Managed Storage                           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2152`_ | CLOUDSTACK-10229_  | Improvement   | Trivial  | SSVM logging improvement when using Swift as               |
|                         |          |                    |               |          | secondary-storage                                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2389`_ | CLOUDSTACK-10213_  | Improvement   | Major    | Allow specify SSH key lengh                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2292`_ | CLOUDSTACK-10108_  | Improvement   | Minor    | ConfigKey based approach for reading 'ping' configuaration |
|                         |          |                    |               |          | for Management Server                                      |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2384`_ | CLOUDSTACK-10210_  | Improvement   | Trivial  | remove test file                                           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1554`_ | CLOUDSTACK-9602_   | Improvement   | Major    | Add resource type name in response                         |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2035`_ | CLOUDSTACK-9867_   | Improvement   | Major    | VM snapshots - not charged for the primary storage they    |
|                         |          |                    |               |          | use up                                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1934`_ | CLOUDSTACK-9772_   | Improvement   | Major    | Perform HEAD request to retrieve header information        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2348`_ | CLOUDSTACK-10196_  | Improvement   | Minor    | Remove ejb-api 3.0 dependency                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2184`_ | CLOUDSTACK-10003_  | Improvement   | Major    | automatic configure juniper srx/vsrx nat loopback          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2332`_ | CLOUDSTACK-10156_  | Improvement   | Minor    | Fix Coverity new problems CID(1349987, 1349986, 1347248)   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2219`_ | CLOUDSTACK-9989_   | Improvement   | Major    | Extend smoketests suite                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2005`_ | CLOUDSTACK-9450_   | Improvement   | Major    | Network Offering for VPC based on DB flag                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2242`_ | CLOUDSTACK-9958_   | Improvement   | Major    | Include tags of resources in listUsageRecords API          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2158`_ | CLOUDSTACK-9972_   | Improvement   | Major    | Enhance listVolume API to include physical size and        |
|                         |          |                    |               |          | utilization.                                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2004`_ | CLOUDSTACK-9832_   | Improvement   | Major    | Do not assign public IP NIC to the VPC VR when the VPC     |
|                         |          |                    |               |          | offering does not contain VpcVirtualRouter as a SourceNat  |
|                         |          |                    |               |          | provider                                                   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2238`_ | CLOUDSTACK-10053_  | Improvement   | Major    | Performance improvement: Caching of external id's          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2296`_ | CLOUDSTACK-10007_  | Improvement   | Major    | Isolation methods are hard coded enum, replace by registry |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2280`_ | CLOUDSTACK-10101_  | Improvement   | Major    | Present the full domain name when listing user's domains   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2285`_ | CLOUDSTACK-9859_   | Improvement   | Major    | Retirement of midonet plugin (final removal ticket)        |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2266`_ | CLOUDSTACK-10073_  | Improvement   | Trivial  | KVM host RAM overprovisioning                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2249`_ | CLOUDSTACK-10007_  | Improvement   | Major    | Isolation methods are hard coded enum, replace by registry |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1443`_ | CLOUDSTACK-9314_   | Improvement   | Trivial  | Remove unused code from XenServerStorageProcessor and      |
|                         |          |                    |               |          | change methods access level                                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2044`_ | CLOUDSTACK-9877_   | Improvement   | Major    | remove fully cloned deleted templates from primary storage |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2101`_ | CLOUDSTACK-9915_   | Improvement   | Major    | ListSnapshots API does not provide virtual size            |
|                         |          |                    |               |          | information of the snapshots                               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2123`_ | CLOUDSTACK-9914_   | Improvement   | Trivial  | Alter quota_tariff to support currency values up to 5      |
|                         |          |                    |               |          | decimal places                                             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1936`_ | CLOUDSTACK-9773_   | Improvement   | Major    | Don't break API output with non-printable characters       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2236`_ | CLOUDSTACK-10044_  | Improvement   | Major    | Update rule permission of a role permission                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2193`_ | CLOUDSTACK-10007_  | Improvement   | Major    | Isolation methods are hard coded enum, replace by registry |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2130`_ | CLOUDSTACK-8961_   | Improvement   | Major    | Making the VPN user management more intutive               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2200`_ | CLOUDSTACK-10015_  | Improvement   | Minor    | Return storage provider with call to list storage pools    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2350`_ |                    |               |          | Cloudstack 10170 - fixes resource tags security bugs and   |
|                         |          |                    |               |          | adds account tags support                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2383`_ |                    |               |          | "isdynamicallyscalable" Field to UpdateTemplate Response   |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2045`_ |                    |               |          | Fix snmptrap alert bug                                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2258`_ |                    |               |          | Cloudstack 10064: Secondary storage Usage for              |
|                         |          |                    |               |          | uploadedVolume is not collected                            |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1637`_ |                    |               |          | Command route not available on CentOS 7                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2367`_ |                    |               |          | Fix ACL_INBOUND/OUTBOUND rules for PrivateGateway          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2371`_ |                    |               |          | README: Happy Holidays, may the cloud be with you in 2018! |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1437`_ |                    |               |          | removed unused HypervDummyResourceBase class               |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2346`_ |                    |               |          | Add XenServer 7.1 and 7.2 interoperablility                |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2359`_ |                    |               |          | doc: replace virutal by virtual (typo)                     |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2324`_ |                    |               |          | Remove annotation and "depends-on" declaration not needed  |
|                         |          |                    |               |          | at cloud-engine-storage-image                              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1723`_ |                    |               |          | Fix GroupBy (+ having) condition and tests                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2307`_ |                    |               |          | packging: Raise compat mode to 9                           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2245`_ |                    |               |          | increased jetty timeout                                    |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2235`_ |                    |               |          | repo has moved                                             |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2039`_ |                    |               |          | rbd: Use libvirt to create new volumes and not rados-java  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#2094`_ |                    |               |          | Agent logrotation                                          |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.9*                    | `#2212`_ |                    |               |          | appliance: fix progress version in Gemfile                 |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2205`_ |                    |               |          | Add NULL checks for various objects in SolidFire           |
|                         |          |                    |               |          | integration test API                                       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1784`_ |                    |               |          | CS-505: Marvin test to check VR internal DNS Service       |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#1655`_ |                    |               |          | Fix ajaxviewer.js to solve console on Firefox              |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.11                    | `#2175`_ |                    |               |          | 4.10 to 4.11 upgrade path                                  |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+
| 4.10*                   | `#2176`_ |                    |               |          | Travis: use oraclejdk8 for 4.10+                           |
+-------------------------+----------+--------------------+---------------+----------+------------------------------------------------------------+

.. _`#2407`: https://github.com/apache/cloudstack/pull/2407
.. _CLOUDSTACK-10227: https://issues.apache.org/jira/browse/CLOUDSTACK-10227
.. _`#2403`: https://github.com/apache/cloudstack/pull/2403
.. _`#2298`: https://github.com/apache/cloudstack/pull/2298
.. _CLOUDSTACK-9620: https://issues.apache.org/jira/browse/CLOUDSTACK-9620
.. _`#2396`: https://github.com/apache/cloudstack/pull/2396
.. _CLOUDSTACK-10220: https://issues.apache.org/jira/browse/CLOUDSTACK-10220
.. _`#2152`: https://github.com/apache/cloudstack/pull/2152
.. _CLOUDSTACK-10229: https://issues.apache.org/jira/browse/CLOUDSTACK-10229
.. _`#2097`: https://github.com/apache/cloudstack/pull/2097
.. _CLOUDSTACK-9813: https://issues.apache.org/jira/browse/CLOUDSTACK-9813
.. _`#2362`: https://github.com/apache/cloudstack/pull/2362
.. _CLOUDSTACK-10188: https://issues.apache.org/jira/browse/CLOUDSTACK-10188
.. _`#2146`: https://github.com/apache/cloudstack/pull/2146
.. _CLOUDSTACK-4757: https://issues.apache.org/jira/browse/CLOUDSTACK-4757
.. _`#2394`: https://github.com/apache/cloudstack/pull/2394
.. _CLOUDSTACK-10109: https://issues.apache.org/jira/browse/CLOUDSTACK-10109
.. _`#2393`: https://github.com/apache/cloudstack/pull/2393
.. _CLOUDSTACK-10217: https://issues.apache.org/jira/browse/CLOUDSTACK-10217
.. _`#2350`: https://github.com/apache/cloudstack/pull/2350
.. _`#2388`: https://github.com/apache/cloudstack/pull/2388
.. _CLOUDSTACK-10212: https://issues.apache.org/jira/browse/CLOUDSTACK-10212
.. _`#2379`: https://github.com/apache/cloudstack/pull/2379
.. _CLOUDSTACK-10146: https://issues.apache.org/jira/browse/CLOUDSTACK-10146
.. _`#2389`: https://github.com/apache/cloudstack/pull/2389
.. _CLOUDSTACK-10213: https://issues.apache.org/jira/browse/CLOUDSTACK-10213
.. _`#2391`: https://github.com/apache/cloudstack/pull/2391
.. _CLOUDSTACK-10215: https://issues.apache.org/jira/browse/CLOUDSTACK-10215
.. _`#2139`: https://github.com/apache/cloudstack/pull/2139
.. _CLOUDSTACK-9921: https://issues.apache.org/jira/browse/CLOUDSTACK-9921
.. _`#2088`: https://github.com/apache/cloudstack/pull/2088
.. _CLOUDSTACK-9892: https://issues.apache.org/jira/browse/CLOUDSTACK-9892
.. _`#2365`: https://github.com/apache/cloudstack/pull/2365
.. _CLOUDSTACK-10197: https://issues.apache.org/jira/browse/CLOUDSTACK-10197
.. _`#2073`: https://github.com/apache/cloudstack/pull/2073
.. _CLOUDSTACK-9896: https://issues.apache.org/jira/browse/CLOUDSTACK-9896
.. _`#2386`: https://github.com/apache/cloudstack/pull/2386
.. _CLOUDSTACK-9632: https://issues.apache.org/jira/browse/CLOUDSTACK-9632
.. _`#2295`: https://github.com/apache/cloudstack/pull/2295
.. _`#2381`: https://github.com/apache/cloudstack/pull/2381
.. _CLOUDSTACK-10117: https://issues.apache.org/jira/browse/CLOUDSTACK-10117
.. _`#2315`: https://github.com/apache/cloudstack/pull/2315
.. _CLOUDSTACK-9025: https://issues.apache.org/jira/browse/CLOUDSTACK-9025
.. _`#2274`: https://github.com/apache/cloudstack/pull/2274
.. _CLOUDSTACK-10096: https://issues.apache.org/jira/browse/CLOUDSTACK-10096
.. _`#2282`: https://github.com/apache/cloudstack/pull/2282
.. _CLOUDSTACK-10104: https://issues.apache.org/jira/browse/CLOUDSTACK-10104
.. _`#2368`: https://github.com/apache/cloudstack/pull/2368
.. _CLOUDSTACK-10126: https://issues.apache.org/jira/browse/CLOUDSTACK-10126
.. _`#2385`: https://github.com/apache/cloudstack/pull/2385
.. _CLOUDSTACK-10211: https://issues.apache.org/jira/browse/CLOUDSTACK-10211
.. _`#2260`: https://github.com/apache/cloudstack/pull/2260
.. _CLOUDSTACK-10065: https://issues.apache.org/jira/browse/CLOUDSTACK-10065
.. _`#2292`: https://github.com/apache/cloudstack/pull/2292
.. _CLOUDSTACK-10108: https://issues.apache.org/jira/browse/CLOUDSTACK-10108
.. _`#1740`: https://github.com/apache/cloudstack/pull/1740
.. _CLOUDSTACK-9572: https://issues.apache.org/jira/browse/CLOUDSTACK-9572
.. _`#2104`: https://github.com/apache/cloudstack/pull/2104
.. _CLOUDSTACK-9908: https://issues.apache.org/jira/browse/CLOUDSTACK-9908
.. _`#2384`: https://github.com/apache/cloudstack/pull/2384
.. _CLOUDSTACK-10210: https://issues.apache.org/jira/browse/CLOUDSTACK-10210
.. _`#2378`: https://github.com/apache/cloudstack/pull/2378
.. _CLOUDSTACK-10205: https://issues.apache.org/jira/browse/CLOUDSTACK-10205
.. _`#2383`: https://github.com/apache/cloudstack/pull/2383
.. _`#1773`: https://github.com/apache/cloudstack/pull/1773
.. _CLOUDSTACK-9607: https://issues.apache.org/jira/browse/CLOUDSTACK-9607
.. _`#2046`: https://github.com/apache/cloudstack/pull/2046
.. _CLOUDSTACK-7958: https://issues.apache.org/jira/browse/CLOUDSTACK-7958
.. _`#2149`: https://github.com/apache/cloudstack/pull/2149
.. _CLOUDSTACK-9932: https://issues.apache.org/jira/browse/CLOUDSTACK-9932
.. _`#2156`: https://github.com/apache/cloudstack/pull/2156
.. _CLOUDSTACK-9971: https://issues.apache.org/jira/browse/CLOUDSTACK-9971
.. _`#2374`: https://github.com/apache/cloudstack/pull/2374
.. _CLOUDSTACK-10024: https://issues.apache.org/jira/browse/CLOUDSTACK-10024
.. _`#2373`: https://github.com/apache/cloudstack/pull/2373
.. _CLOUDSTACK-10202: https://issues.apache.org/jira/browse/CLOUDSTACK-10202
.. _`#2344`: https://github.com/apache/cloudstack/pull/2344
.. _CLOUDSTACK-10163: https://issues.apache.org/jira/browse/CLOUDSTACK-10163
.. _`#2301`: https://github.com/apache/cloudstack/pull/2301
.. _CLOUDSTACK-10121: https://issues.apache.org/jira/browse/CLOUDSTACK-10121
.. _`#1554`: https://github.com/apache/cloudstack/pull/1554
.. _CLOUDSTACK-9602: https://issues.apache.org/jira/browse/CLOUDSTACK-9602
.. _`#1760`: https://github.com/apache/cloudstack/pull/1760
.. _CLOUDSTACK-9593: https://issues.apache.org/jira/browse/CLOUDSTACK-9593
.. _`#2035`: https://github.com/apache/cloudstack/pull/2035
.. _CLOUDSTACK-9867: https://issues.apache.org/jira/browse/CLOUDSTACK-9867
.. _`#2360`: https://github.com/apache/cloudstack/pull/2360
.. _CLOUDSTACK-10189: https://issues.apache.org/jira/browse/CLOUDSTACK-10189
.. _`#2352`: https://github.com/apache/cloudstack/pull/2352
.. _CLOUDSTACK-10175: https://issues.apache.org/jira/browse/CLOUDSTACK-10175
.. _`#2045`: https://github.com/apache/cloudstack/pull/2045
.. _`#1934`: https://github.com/apache/cloudstack/pull/1934
.. _CLOUDSTACK-9772: https://issues.apache.org/jira/browse/CLOUDSTACK-9772
.. _`#2258`: https://github.com/apache/cloudstack/pull/2258
.. _`#2347`: https://github.com/apache/cloudstack/pull/2347
.. _CLOUDSTACK-10166: https://issues.apache.org/jira/browse/CLOUDSTACK-10166
.. _`#2375`: https://github.com/apache/cloudstack/pull/2375
.. _CLOUDSTACK-9456: https://issues.apache.org/jira/browse/CLOUDSTACK-9456
.. _`#2211`: https://github.com/apache/cloudstack/pull/2211
.. _CLOUDSTACK-10013: https://issues.apache.org/jira/browse/CLOUDSTACK-10013
.. _`#1637`: https://github.com/apache/cloudstack/pull/1637
.. _`#2304`: https://github.com/apache/cloudstack/pull/2304
.. _CLOUDSTACK-10127: https://issues.apache.org/jira/browse/CLOUDSTACK-10127
.. _`#2208`: https://github.com/apache/cloudstack/pull/2208
.. _CLOUDSTACK-9542: https://issues.apache.org/jira/browse/CLOUDSTACK-9542
.. _`#2351`: https://github.com/apache/cloudstack/pull/2351
.. _CLOUDSTACK-10173: https://issues.apache.org/jira/browse/CLOUDSTACK-10173
.. _`#2367`: https://github.com/apache/cloudstack/pull/2367
.. _`#2370`: https://github.com/apache/cloudstack/pull/2370
.. _CLOUDSTACK-9595: https://issues.apache.org/jira/browse/CLOUDSTACK-9595
.. _`#2366`: https://github.com/apache/cloudstack/pull/2366
.. _CLOUDSTACK-10168: https://issues.apache.org/jira/browse/CLOUDSTACK-10168
.. _`#2371`: https://github.com/apache/cloudstack/pull/2371
.. _`#2042`: https://github.com/apache/cloudstack/pull/2042
.. _CLOUDSTACK-9875: https://issues.apache.org/jira/browse/CLOUDSTACK-9875
.. _`#2281`: https://github.com/apache/cloudstack/pull/2281
.. _CLOUDSTACK-10102: https://issues.apache.org/jira/browse/CLOUDSTACK-10102
.. _`#2048`: https://github.com/apache/cloudstack/pull/2048
.. _CLOUDSTACK-9880: https://issues.apache.org/jira/browse/CLOUDSTACK-9880
.. _`#2364`: https://github.com/apache/cloudstack/pull/2364
.. _CLOUDSTACK-10195: https://issues.apache.org/jira/browse/CLOUDSTACK-10195
.. _`#2361`: https://github.com/apache/cloudstack/pull/2361
.. _CLOUDSTACK-10190: https://issues.apache.org/jira/browse/CLOUDSTACK-10190
.. _`#1437`: https://github.com/apache/cloudstack/pull/1437
.. _`#2247`: https://github.com/apache/cloudstack/pull/2247
.. _CLOUDSTACK-10012: https://issues.apache.org/jira/browse/CLOUDSTACK-10012
.. _`#1964`: https://github.com/apache/cloudstack/pull/1964
.. _CLOUDSTACK-9800: https://issues.apache.org/jira/browse/CLOUDSTACK-9800
.. _`#1762`: https://github.com/apache/cloudstack/pull/1762
.. _`#2348`: https://github.com/apache/cloudstack/pull/2348
.. _CLOUDSTACK-10196: https://issues.apache.org/jira/browse/CLOUDSTACK-10196
.. _`#2184`: https://github.com/apache/cloudstack/pull/2184
.. _CLOUDSTACK-10003: https://issues.apache.org/jira/browse/CLOUDSTACK-10003
.. _`#2308`: https://github.com/apache/cloudstack/pull/2308
.. _CLOUDSTACK-8908: https://issues.apache.org/jira/browse/CLOUDSTACK-8908
.. _`#2294`: https://github.com/apache/cloudstack/pull/2294
.. _CLOUDSTACK-10039: https://issues.apache.org/jira/browse/CLOUDSTACK-10039
.. _`#2346`: https://github.com/apache/cloudstack/pull/2346
.. _`#2354`: https://github.com/apache/cloudstack/pull/2354
.. _CLOUDSTACK-10176: https://issues.apache.org/jira/browse/CLOUDSTACK-10176
.. _`#2353`: https://github.com/apache/cloudstack/pull/2353
.. _CLOUDSTACK-9986: https://issues.apache.org/jira/browse/CLOUDSTACK-9986
.. _`#2359`: https://github.com/apache/cloudstack/pull/2359
.. _`#2356`: https://github.com/apache/cloudstack/pull/2356
.. _CLOUDSTACK-8313: https://issues.apache.org/jira/browse/CLOUDSTACK-8313
.. _`#2358`: https://github.com/apache/cloudstack/pull/2358
.. _CLOUDSTACK-9736: https://issues.apache.org/jira/browse/CLOUDSTACK-9736
.. _`#2326`: https://github.com/apache/cloudstack/pull/2326
.. _CLOUDSTACK-10184: https://issues.apache.org/jira/browse/CLOUDSTACK-10184
.. _`#2267`: https://github.com/apache/cloudstack/pull/2267
.. _CLOUDSTACK-10077: https://issues.apache.org/jira/browse/CLOUDSTACK-10077
.. _`#2337`: https://github.com/apache/cloudstack/pull/2337
.. _CLOUDSTACK-10157: https://issues.apache.org/jira/browse/CLOUDSTACK-10157
.. _`#2355`: https://github.com/apache/cloudstack/pull/2355
.. _CLOUDSTACK-10177: https://issues.apache.org/jira/browse/CLOUDSTACK-10177
.. _`#2349`: https://github.com/apache/cloudstack/pull/2349
.. _CLOUDSTACK-10070: https://issues.apache.org/jira/browse/CLOUDSTACK-10070
.. _`#2312`: https://github.com/apache/cloudstack/pull/2312
.. _CLOUDSTACK-7793: https://issues.apache.org/jira/browse/CLOUDSTACK-7793
.. _`#2345`: https://github.com/apache/cloudstack/pull/2345
.. _CLOUDSTACK-10164: https://issues.apache.org/jira/browse/CLOUDSTACK-10164
.. _`#2263`: https://github.com/apache/cloudstack/pull/2263
.. _`#2342`: https://github.com/apache/cloudstack/pull/2342
.. _CLOUDSTACK-9586: https://issues.apache.org/jira/browse/CLOUDSTACK-9586
.. _`#2124`: https://github.com/apache/cloudstack/pull/2124
.. _CLOUDSTACK-9432: https://issues.apache.org/jira/browse/CLOUDSTACK-9432
.. _`#2322`: https://github.com/apache/cloudstack/pull/2322
.. _CLOUDSTACK-10140: https://issues.apache.org/jira/browse/CLOUDSTACK-10140
.. _`#2335`: https://github.com/apache/cloudstack/pull/2335
.. _CLOUDSTACK-10154: https://issues.apache.org/jira/browse/CLOUDSTACK-10154
.. _`#2341`: https://github.com/apache/cloudstack/pull/2341
.. _CLOUDSTACK-10160: https://issues.apache.org/jira/browse/CLOUDSTACK-10160
.. _`#2321`: https://github.com/apache/cloudstack/pull/2321
.. _CLOUDSTACK-10138: https://issues.apache.org/jira/browse/CLOUDSTACK-10138
.. _`#2334`: https://github.com/apache/cloudstack/pull/2334
.. _CLOUDSTACK-10152: https://issues.apache.org/jira/browse/CLOUDSTACK-10152
.. _`#2332`: https://github.com/apache/cloudstack/pull/2332
.. _CLOUDSTACK-10156: https://issues.apache.org/jira/browse/CLOUDSTACK-10156
.. _`#2028`: https://github.com/apache/cloudstack/pull/2028
.. _CLOUDSTACK-9853: https://issues.apache.org/jira/browse/CLOUDSTACK-9853
.. _`#2310`: https://github.com/apache/cloudstack/pull/2310
.. _CLOUDSTACK-10133: https://issues.apache.org/jira/browse/CLOUDSTACK-10133
.. _`#2219`: https://github.com/apache/cloudstack/pull/2219
.. _CLOUDSTACK-9989: https://issues.apache.org/jira/browse/CLOUDSTACK-9989
.. _`#2303`: https://github.com/apache/cloudstack/pull/2303
.. _CLOUDSTACK-10123: https://issues.apache.org/jira/browse/CLOUDSTACK-10123
.. _`#2329`: https://github.com/apache/cloudstack/pull/2329
.. _`#1981`: https://github.com/apache/cloudstack/pull/1981
.. _CLOUDSTACK-9806: https://issues.apache.org/jira/browse/CLOUDSTACK-9806
.. _`#2324`: https://github.com/apache/cloudstack/pull/2324
.. _`#2005`: https://github.com/apache/cloudstack/pull/2005
.. _CLOUDSTACK-9450: https://issues.apache.org/jira/browse/CLOUDSTACK-9450
.. _`#2327`: https://github.com/apache/cloudstack/pull/2327
.. _CLOUDSTACK-10129: https://issues.apache.org/jira/browse/CLOUDSTACK-10129
.. _`#2325`: https://github.com/apache/cloudstack/pull/2325
.. _CLOUDSTACK-9998: https://issues.apache.org/jira/browse/CLOUDSTACK-9998
.. _`#2313`: https://github.com/apache/cloudstack/pull/2313
.. _CLOUDSTACK-10135: https://issues.apache.org/jira/browse/CLOUDSTACK-10135
.. _`#2316`: https://github.com/apache/cloudstack/pull/2316
.. _CLOUDSTACK-10137: https://issues.apache.org/jira/browse/CLOUDSTACK-10137
.. _`#2157`: https://github.com/apache/cloudstack/pull/2157
.. _CLOUDSTACK-9961: https://issues.apache.org/jira/browse/CLOUDSTACK-9961
.. _`#1723`: https://github.com/apache/cloudstack/pull/1723
.. _`#2306`: https://github.com/apache/cloudstack/pull/2306
.. _`#2273`: https://github.com/apache/cloudstack/pull/2273
.. _CLOUDSTACK-10090: https://issues.apache.org/jira/browse/CLOUDSTACK-10090
.. _`#2242`: https://github.com/apache/cloudstack/pull/2242
.. _CLOUDSTACK-9958: https://issues.apache.org/jira/browse/CLOUDSTACK-9958
.. _`#2307`: https://github.com/apache/cloudstack/pull/2307
.. _`#2240`: https://github.com/apache/cloudstack/pull/2240
.. _CLOUDSTACK-10051: https://issues.apache.org/jira/browse/CLOUDSTACK-10051
.. _`#2158`: https://github.com/apache/cloudstack/pull/2158
.. _CLOUDSTACK-9972: https://issues.apache.org/jira/browse/CLOUDSTACK-9972
.. _`#2291`: https://github.com/apache/cloudstack/pull/2291
.. _CLOUDSTACK-10111: https://issues.apache.org/jira/browse/CLOUDSTACK-10111
.. _`#2302`: https://github.com/apache/cloudstack/pull/2302
.. _CLOUDSTACK-10122: https://issues.apache.org/jira/browse/CLOUDSTACK-10122
.. _`#2004`: https://github.com/apache/cloudstack/pull/2004
.. _CLOUDSTACK-9832: https://issues.apache.org/jira/browse/CLOUDSTACK-9832
.. _`#2238`: https://github.com/apache/cloudstack/pull/2238
.. _CLOUDSTACK-10053: https://issues.apache.org/jira/browse/CLOUDSTACK-10053
.. _`#2250`: https://github.com/apache/cloudstack/pull/2250
.. _CLOUDSTACK-10057: https://issues.apache.org/jira/browse/CLOUDSTACK-10057
.. _`#2268`: https://github.com/apache/cloudstack/pull/2268
.. _CLOUDSTACK-10081: https://issues.apache.org/jira/browse/CLOUDSTACK-10081
.. _`#2293`: https://github.com/apache/cloudstack/pull/2293
.. _CLOUDSTACK-10047: https://issues.apache.org/jira/browse/CLOUDSTACK-10047
.. _`#2284`: https://github.com/apache/cloudstack/pull/2284
.. _CLOUDSTACK-10103: https://issues.apache.org/jira/browse/CLOUDSTACK-10103
.. _`#2288`: https://github.com/apache/cloudstack/pull/2288
.. _CLOUDSTACK-10107: https://issues.apache.org/jira/browse/CLOUDSTACK-10107
.. _`#2297`: https://github.com/apache/cloudstack/pull/2297
.. _CLOUDSTACK-9957: https://issues.apache.org/jira/browse/CLOUDSTACK-9957
.. _`#2296`: https://github.com/apache/cloudstack/pull/2296
.. _CLOUDSTACK-10007: https://issues.apache.org/jira/browse/CLOUDSTACK-10007
.. _`#2181`: https://github.com/apache/cloudstack/pull/2181
.. _`#2257`: https://github.com/apache/cloudstack/pull/2257
.. _CLOUDSTACK-10060: https://issues.apache.org/jira/browse/CLOUDSTACK-10060
.. _`#2286`: https://github.com/apache/cloudstack/pull/2286
.. _CLOUDSTACK-9993: https://issues.apache.org/jira/browse/CLOUDSTACK-9993
.. _`#2287`: https://github.com/apache/cloudstack/pull/2287
.. _`#2246`: https://github.com/apache/cloudstack/pull/2246
.. _CLOUDSTACK-10046: https://issues.apache.org/jira/browse/CLOUDSTACK-10046
.. _`#2074`: https://github.com/apache/cloudstack/pull/2074
.. _CLOUDSTACK-9899: https://issues.apache.org/jira/browse/CLOUDSTACK-9899
.. _`#2280`: https://github.com/apache/cloudstack/pull/2280
.. _CLOUDSTACK-10101: https://issues.apache.org/jira/browse/CLOUDSTACK-10101
.. _`#2285`: https://github.com/apache/cloudstack/pull/2285
.. _CLOUDSTACK-9859: https://issues.apache.org/jira/browse/CLOUDSTACK-9859
.. _`#2278`: https://github.com/apache/cloudstack/pull/2278
.. _`#2279`: https://github.com/apache/cloudstack/pull/2279
.. _CLOUDSTACK-9584: https://issues.apache.org/jira/browse/CLOUDSTACK-9584
.. _`#2277`: https://github.com/apache/cloudstack/pull/2277
.. _CLOUDSTACK-10099: https://issues.apache.org/jira/browse/CLOUDSTACK-10099
.. _`#2266`: https://github.com/apache/cloudstack/pull/2266
.. _CLOUDSTACK-10073: https://issues.apache.org/jira/browse/CLOUDSTACK-10073
.. _`#2249`: https://github.com/apache/cloudstack/pull/2249
.. _`#1707`: https://github.com/apache/cloudstack/pull/1707
.. _CLOUDSTACK-9397: https://issues.apache.org/jira/browse/CLOUDSTACK-9397
.. _`#2269`: https://github.com/apache/cloudstack/pull/2269
.. _CLOUDSTACK-10083: https://issues.apache.org/jira/browse/CLOUDSTACK-10083
.. _`#876`: https://github.com/apache/cloudstack/pull/876
.. _CLOUDSTACK-8865: https://issues.apache.org/jira/browse/CLOUDSTACK-8865
.. _`#1252`: https://github.com/apache/cloudstack/pull/1252
.. _CLOUDSTACK-9182: https://issues.apache.org/jira/browse/CLOUDSTACK-9182
.. _`#2153`: https://github.com/apache/cloudstack/pull/2153
.. _CLOUDSTACK-9956: https://issues.apache.org/jira/browse/CLOUDSTACK-9956
.. _`#2078`: https://github.com/apache/cloudstack/pull/2078
.. _CLOUDSTACK-9902: https://issues.apache.org/jira/browse/CLOUDSTACK-9902
.. _`#2252`: https://github.com/apache/cloudstack/pull/2252
.. _CLOUDSTACK-10067: https://issues.apache.org/jira/browse/CLOUDSTACK-10067
.. _`#2143`: https://github.com/apache/cloudstack/pull/2143
.. _CLOUDSTACK-9949: https://issues.apache.org/jira/browse/CLOUDSTACK-9949
.. _`#2248`: https://github.com/apache/cloudstack/pull/2248
.. _CLOUDSTACK-10056: https://issues.apache.org/jira/browse/CLOUDSTACK-10056
.. _`#2243`: https://github.com/apache/cloudstack/pull/2243
.. _CLOUDSTACK-10019: https://issues.apache.org/jira/browse/CLOUDSTACK-10019
.. _`#2261`: https://github.com/apache/cloudstack/pull/2261
.. _CLOUDSTACK-10068: https://issues.apache.org/jira/browse/CLOUDSTACK-10068
.. _`#2054`: https://github.com/apache/cloudstack/pull/2054
.. _CLOUDSTACK-9886: https://issues.apache.org/jira/browse/CLOUDSTACK-9886
.. _`#955`: https://github.com/apache/cloudstack/pull/955
.. _CLOUDSTACK-8969: https://issues.apache.org/jira/browse/CLOUDSTACK-8969
.. _`#2262`: https://github.com/apache/cloudstack/pull/2262
.. _CLOUDSTACK-10069: https://issues.apache.org/jira/browse/CLOUDSTACK-10069
.. _`#2256`: https://github.com/apache/cloudstack/pull/2256
.. _CLOUDSTACK-9782: https://issues.apache.org/jira/browse/CLOUDSTACK-9782
.. _`#2253`: https://github.com/apache/cloudstack/pull/2253
.. _CLOUDSTACK-10061: https://issues.apache.org/jira/browse/CLOUDSTACK-10061
.. _`#2254`: https://github.com/apache/cloudstack/pull/2254
.. _CLOUDSTACK-10058: https://issues.apache.org/jira/browse/CLOUDSTACK-10058
.. _`#1733`: https://github.com/apache/cloudstack/pull/1733
.. _CLOUDSTACK-9563: https://issues.apache.org/jira/browse/CLOUDSTACK-9563
.. _`#2188`: https://github.com/apache/cloudstack/pull/2188
.. _CLOUDSTACK-10004: https://issues.apache.org/jira/browse/CLOUDSTACK-10004
.. _`#914`: https://github.com/apache/cloudstack/pull/914
.. _CLOUDSTACK-8939: https://issues.apache.org/jira/browse/CLOUDSTACK-8939
.. _`#1985`: https://github.com/apache/cloudstack/pull/1985
.. _CLOUDSTACK-9812: https://issues.apache.org/jira/browse/CLOUDSTACK-9812
.. _`#2224`: https://github.com/apache/cloudstack/pull/2224
.. _CLOUDSTACK-10032: https://issues.apache.org/jira/browse/CLOUDSTACK-10032
.. _`#1443`: https://github.com/apache/cloudstack/pull/1443
.. _CLOUDSTACK-9314: https://issues.apache.org/jira/browse/CLOUDSTACK-9314
.. _`#2109`: https://github.com/apache/cloudstack/pull/2109
.. _CLOUDSTACK-9922: https://issues.apache.org/jira/browse/CLOUDSTACK-9922
.. _`#2216`: https://github.com/apache/cloudstack/pull/2216
.. _CLOUDSTACK-10027: https://issues.apache.org/jira/browse/CLOUDSTACK-10027
.. _`#2245`: https://github.com/apache/cloudstack/pull/2245
.. _`#2239`: https://github.com/apache/cloudstack/pull/2239
.. _`#2044`: https://github.com/apache/cloudstack/pull/2044
.. _CLOUDSTACK-9877: https://issues.apache.org/jira/browse/CLOUDSTACK-9877
.. _`#2174`: https://github.com/apache/cloudstack/pull/2174
.. _CLOUDSTACK-9996: https://issues.apache.org/jira/browse/CLOUDSTACK-9996
.. _`#2101`: https://github.com/apache/cloudstack/pull/2101
.. _CLOUDSTACK-9915: https://issues.apache.org/jira/browse/CLOUDSTACK-9915
.. _`#2123`: https://github.com/apache/cloudstack/pull/2123
.. _CLOUDSTACK-9914: https://issues.apache.org/jira/browse/CLOUDSTACK-9914
.. _`#2186`: https://github.com/apache/cloudstack/pull/2186
.. _CLOUDSTACK-10002: https://issues.apache.org/jira/browse/CLOUDSTACK-10002
.. _`#1246`: https://github.com/apache/cloudstack/pull/1246
.. _CLOUDSTACK-9165: https://issues.apache.org/jira/browse/CLOUDSTACK-9165
.. _`#2241`: https://github.com/apache/cloudstack/pull/2241
.. _CLOUDSTACK-10052: https://issues.apache.org/jira/browse/CLOUDSTACK-10052
.. _`#2222`: https://github.com/apache/cloudstack/pull/2222
.. _CLOUDSTACK-10022: https://issues.apache.org/jira/browse/CLOUDSTACK-10022
.. _`#2221`: https://github.com/apache/cloudstack/pull/2221
.. _CLOUDSTACK-10030: https://issues.apache.org/jira/browse/CLOUDSTACK-10030
.. _`#2154`: https://github.com/apache/cloudstack/pull/2154
.. _CLOUDSTACK-9967: https://issues.apache.org/jira/browse/CLOUDSTACK-9967
.. _`#1878`: https://github.com/apache/cloudstack/pull/1878
.. _CLOUDSTACK-9717: https://issues.apache.org/jira/browse/CLOUDSTACK-9717
.. _`#2013`: https://github.com/apache/cloudstack/pull/2013
.. _CLOUDSTACK-9734: https://issues.apache.org/jira/browse/CLOUDSTACK-9734
.. _`#2159`: https://github.com/apache/cloudstack/pull/2159
.. _CLOUDSTACK-9964: https://issues.apache.org/jira/browse/CLOUDSTACK-9964
.. _`#2163`: https://github.com/apache/cloudstack/pull/2163
.. _CLOUDSTACK-9939: https://issues.apache.org/jira/browse/CLOUDSTACK-9939
.. _`#1919`: https://github.com/apache/cloudstack/pull/1919
.. _CLOUDSTACK-9763: https://issues.apache.org/jira/browse/CLOUDSTACK-9763
.. _`#1936`: https://github.com/apache/cloudstack/pull/1936
.. _CLOUDSTACK-9773: https://issues.apache.org/jira/browse/CLOUDSTACK-9773
.. _`#2223`: https://github.com/apache/cloudstack/pull/2223
.. _CLOUDSTACK-10031: https://issues.apache.org/jira/browse/CLOUDSTACK-10031
.. _`#2215`: https://github.com/apache/cloudstack/pull/2215
.. _CLOUDSTACK-10026: https://issues.apache.org/jira/browse/CLOUDSTACK-10026
.. _`#2180`: https://github.com/apache/cloudstack/pull/2180
.. _CLOUDSTACK-9999: https://issues.apache.org/jira/browse/CLOUDSTACK-9999
.. _`#2236`: https://github.com/apache/cloudstack/pull/2236
.. _CLOUDSTACK-10044: https://issues.apache.org/jira/browse/CLOUDSTACK-10044
.. _`#2235`: https://github.com/apache/cloudstack/pull/2235
.. _`#2182`: https://github.com/apache/cloudstack/pull/2182
.. _CLOUDSTACK-10000: https://issues.apache.org/jira/browse/CLOUDSTACK-10000
.. _`#2233`: https://github.com/apache/cloudstack/pull/2233
.. _CLOUDSTACK-10042: https://issues.apache.org/jira/browse/CLOUDSTACK-10042
.. _`#2228`: https://github.com/apache/cloudstack/pull/2228
.. _CLOUDSTACK-10036: https://issues.apache.org/jira/browse/CLOUDSTACK-10036
.. _`#2026`: https://github.com/apache/cloudstack/pull/2026
.. _CLOUDSTACK-9861: https://issues.apache.org/jira/browse/CLOUDSTACK-9861
.. _`#1774`: https://github.com/apache/cloudstack/pull/1774
.. _CLOUDSTACK-9608: https://issues.apache.org/jira/browse/CLOUDSTACK-9608
.. _`#2039`: https://github.com/apache/cloudstack/pull/2039
.. _`#2144`: https://github.com/apache/cloudstack/pull/2144
.. _CLOUDSTACK-9955: https://issues.apache.org/jira/browse/CLOUDSTACK-9955
.. _`#1966`: https://github.com/apache/cloudstack/pull/1966
.. _CLOUDSTACK-9801: https://issues.apache.org/jira/browse/CLOUDSTACK-9801
.. _`#2220`: https://github.com/apache/cloudstack/pull/2220
.. _CLOUDSTACK-9708: https://issues.apache.org/jira/browse/CLOUDSTACK-9708
.. _`#1912`: https://github.com/apache/cloudstack/pull/1912
.. _CLOUDSTACK-9749: https://issues.apache.org/jira/browse/CLOUDSTACK-9749
.. _`#2138`: https://github.com/apache/cloudstack/pull/2138
.. _CLOUDSTACK-9944: https://issues.apache.org/jira/browse/CLOUDSTACK-9944
.. _`#2193`: https://github.com/apache/cloudstack/pull/2193
.. _`#2218`: https://github.com/apache/cloudstack/pull/2218
.. _`#883`: https://github.com/apache/cloudstack/pull/883
.. _CLOUDSTACK-8906: https://issues.apache.org/jira/browse/CLOUDSTACK-8906
.. _`#2119`: https://github.com/apache/cloudstack/pull/2119
.. _CLOUDSTACK-9925: https://issues.apache.org/jira/browse/CLOUDSTACK-9925
.. _`#2145`: https://github.com/apache/cloudstack/pull/2145
.. _CLOUDSTACK-9697: https://issues.apache.org/jira/browse/CLOUDSTACK-9697
.. _`#2137`: https://github.com/apache/cloudstack/pull/2137
.. _CLOUDSTACK-9950: https://issues.apache.org/jira/browse/CLOUDSTACK-9950
.. _`#2008`: https://github.com/apache/cloudstack/pull/2008
.. _CLOUDSTACK-9840: https://issues.apache.org/jira/browse/CLOUDSTACK-9840
.. _`#2094`: https://github.com/apache/cloudstack/pull/2094
.. _`#2142`: https://github.com/apache/cloudstack/pull/2142
.. _CLOUDSTACK-9954: https://issues.apache.org/jira/browse/CLOUDSTACK-9954
.. _`#2130`: https://github.com/apache/cloudstack/pull/2130
.. _CLOUDSTACK-8961: https://issues.apache.org/jira/browse/CLOUDSTACK-8961
.. _`#2212`: https://github.com/apache/cloudstack/pull/2212
.. _`#2171`: https://github.com/apache/cloudstack/pull/2171
.. _CLOUDSTACK-9990: https://issues.apache.org/jira/browse/CLOUDSTACK-9990
.. _`#2205`: https://github.com/apache/cloudstack/pull/2205
.. _`#1925`: https://github.com/apache/cloudstack/pull/1925
.. _CLOUDSTACK-9751: https://issues.apache.org/jira/browse/CLOUDSTACK-9751
.. _`#1798`: https://github.com/apache/cloudstack/pull/1798
.. _CLOUDSTACK-9631: https://issues.apache.org/jira/browse/CLOUDSTACK-9631
.. _`#2201`: https://github.com/apache/cloudstack/pull/2201
.. _CLOUDSTACK-10016: https://issues.apache.org/jira/browse/CLOUDSTACK-10016
.. _`#1784`: https://github.com/apache/cloudstack/pull/1784
.. _`#2200`: https://github.com/apache/cloudstack/pull/2200
.. _CLOUDSTACK-10015: https://issues.apache.org/jira/browse/CLOUDSTACK-10015
.. _`#1655`: https://github.com/apache/cloudstack/pull/1655
.. _`#1959`: https://github.com/apache/cloudstack/pull/1959
.. _CLOUDSTACK-9786: https://issues.apache.org/jira/browse/CLOUDSTACK-9786
.. _`#1933`: https://github.com/apache/cloudstack/pull/1933
.. _CLOUDSTACK-9569: https://issues.apache.org/jira/browse/CLOUDSTACK-9569
.. _`#2175`: https://github.com/apache/cloudstack/pull/2175
.. _`#2176`: https://github.com/apache/cloudstack/pull/2176
