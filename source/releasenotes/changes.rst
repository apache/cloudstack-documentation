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

Changes in |release| since 4.14.0.0
===================================

Apache CloudStack uses GitHub <https://github.com/apache/cloudstack/milestone/15?closed=1>`_ 
to track its issues.

.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+------------------------------------------------------------+
| Version                 | Github   | Description                                                |
+=========================+==========+============================================================+
| 4.14.1.0                | `#4562`_ | Prevent KVM from performing volume migrations of running   |
|                         |          | instances                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4651`_ | marvin: fix test failures when changing service offering   |
|                         |          | of a VM                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4627`_ | VR: fix expunging vm will remove dhcp entries of another   |
|                         |          | vm in VR                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4650`_ | test: hardware required for changeserviceoffering          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4653`_ | Update cloud-setup-databases.in - help message fix         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4655`_ | test: fix checksums for test template                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4601`_ | server: Get vm network/disk statistics and update database |
|                         |          | per host                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4623`_ | server: Fix update capacity for hosts take long time if    |
|                         |          | there are many service offerings                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4629`_ | server: prevent update vm read-only details                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4591`_ | server: select root disk based on user input during vm     |
|                         |          | import                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4576`_ | Fix: Use Q35 chipset for UEFI x86_64                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4624`_ | server: fix wrong error message when create isolated       |
|                         |          | network without SourceNat                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4622`_ | server: add possibility to scale vm to current custom      |
|                         |          | offerings on UI                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4602`_ | server: keep networks order and ips while move a vm with   |
|                         |          | multiple networks                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4625`_ | server: throw exception when update vm nic on L2 network   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4633`_ | doc: fix typo in install notes                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4600`_ | server: fix cannot create vm if another vm with same name  |
|                         |          | has been added and removed on the network                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4491`_ | fix on changeServiceForVirtualMachine when updating        |
|                         |          | read/write rate                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4621`_ | Fixed typo                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4580`_ | engine/schema: add upgrade path from 4.14.0.0 to 4.14.1.0  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4557`_ | Fixed instance creation failure on dvswitch when using     |
|                         |          | vlan id 4095                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4529`_ | vr: Ensuring dnsmasq.leases file is populated              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4533`_ | db upgrade: use "create or replace view" instead of "alter |
|                         |          | view"                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4532`_ | apidoc issue                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4527`_ | kvm: set cpu topology only if cpucore per socket is set    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4497`_ | kvm: FIX cpucorespersocket is not working on KVM           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4507`_ | Fix failure in validating IP address in case of multiple   |
|                         |          | Management Servers                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4501`_ | Disallowing udp for lb rules for haproxy                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4499`_ | Adding cpuallocated percentage and value to host and       |
|                         |          | hostsformigrationresponse                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4496`_ | kvm: fix router.aggregation.command.each.timeout is reset  |
|                         |          | to 600 when update other kvm configs                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4495`_ | fix failures with test_multiple_nic_support.py             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4500`_ | Fix hosts for migration count                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4489`_ | vr: fix python exception when configure VRs                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4467`_ | vpc: fix ips on wrong interfaces after rebooting vpc vrs   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4478`_ | Adding memoryallocatedpercentage & memoryallocatedbytes to |
|                         |          | HostsResponse & HostsForMigrationResponse                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4466`_ | VR: fix logging is not working and logs are not appended   |
|                         |          | to /var/log/cloud.log                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4458`_ | Fix k8s cluster upgrade in shared networks                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4487`_ | accountresponse: Fix domainpath description                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4459`_ | createkubertetesbinariesiso: Saving images in network and  |
|                         |          | dashboard yaml                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4485`_ | Fixing misleading HostMetricsResponse param description    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4461`_ | Fix destroying k8s cluster on shared networks              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4464`_ | Fix IndexOutOfBoundsException when creating basic network  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4442`_ | Preventing port 53 being added as lb rule when dns service |
|                         |          | is availab…                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4430`_ | FIX issue in VR if remote access vpn is enabled            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4388`_ | fix NPE in volumes statistics                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4435`_ | server: fix format error with memorywithoverprovisioning   |
|                         |          | in list hosts response                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4429`_ | FIX s2svpn connection stuck on Pending state               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4359`_ | Failed to update host password if username/password is not |
|                         |          | saved in db                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4432`_ | Unable to create snapshot from vm snapshot                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#3945`_ | server: update template to another template type           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4367`_ | Remove cpu core from op_host_capacity when host is deleted |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4413`_ | systemvm: fix proc.find in CsProcess.py                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4193`_ | Fix usage record count                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4412`_ | Validating type parameter and including all types          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4407`_ | packaging: enable Parallel Collector GC for management     |
|                         |          | server                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4377`_ | server: fix issue that vm guest os type is reset after     |
|                         |          | updatetemplate                                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4381`_ | kvm: fix wrong VM CPU usage                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4404`_ | scalekubernetesclustercmd: Making id a required field [NPE |
|                         |          | Fix]                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4383`_ | Host is counted twice if it has multiple host tags in      |
|                         |          | Prometheus exporter                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4373`_ | Handles creation /var/run/cloud folder for creation of     |
|                         |          | lock file while modifyvxlan.sh script is run               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4376`_ | server: Fix some cpuspeed issues while create service      |
|                         |          | offering                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4269`_ | cks: assorted fixes, test refactoring                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4338`_ | server: check guest os preference of last host when start  |
|                         |          | a vm                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4190`_ | Broadcast URI not set to vxlan, but vlan (Fix #3040)       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4328`_ | vmware: search unmanaged instances using hypervisor name   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4335`_ | agent: Compare indirect agent lb algorithm when cloudstack |
|                         |          | agent conn…                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4319`_ | Fix "data-server" dns entry in /etc/hosts after a new      |
|                         |          | deployment                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4297`_ | Incorrect md5sums for systemVM templates results in        |
|                         |          | failure to download templates to other image stores        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4291`_ | Manage influxDB Batches avoiding OutOfMemory Exception     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#3996`_ | UI: Hide cpuspeed for custom constrained offering          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#3902`_ | vrouter: Save PlaceHolder nic for VR if network does not   |
|                         |          | have source nat                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4288`_ | client: explicitly define SslContextFactory::Server for    |
|                         |          | https                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4274`_ | engine: honour bypass VLAN id/range for L2 networks        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4219`_ | iscsi session cleanup now configurable, filters iscsi      |
|                         |          | partitions                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4275`_ | Display hypervisor type for VM snapshot                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4213`_ | Search vm snapshots using tags                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4260`_ | cks: fix for null hypervisor type                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4016`_ | Fixed private gateway can't be deleted                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4253`_ | Fix sed command failure in Mac OS.                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4019`_ | server: Move restoreVM to vm work job queue                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4220`_ | Fix cpuallocated value in findHostsForMIgration api        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4225`_ | vmware: volume utilisation is always zero                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4000`_ | vm: Reset deviceId to fix missing nic with vm              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4116`_ | cks: fix template, deployment issues                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#3952`_ | vrouter: remove a POSTROUTING rule for port forwarding in  |
|                         |          | VPC router                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4214`_ | Bug fixes for primate                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4226`_ | Removed check on SSLEngine client mode                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4188`_ | Fix snapshots garbage collection                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4138`_ | Fixed incorrect error message on invalid template type     |
|                         |          | download                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4176`_ | server: Purge all cookies on logout, set /client path on   |
|                         |          | login                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4202`_ | server: don't export B&R APIs if feature is not enabled    |
|                         |          | globally                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4186`_ | Adding pagination for quotaSummary and quotaTariffList     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4001`_ | server: Dedicated hosts should be 'Not Suitable' while     |
|                         |          | find host for m migration                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4148`_ | server: Do not resize volume of running vm on KVM host if  |
|                         |          | host is not Up or not Enabled                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4171`_ | vr: fix backup router health check                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4167`_ | Adding missing fields to API responses                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4164`_ | Adding listall to listLdapConfigurations                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4154`_ | server: fix for wrong affinity group count                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4004`_ | Fixed null pointer and deployment issue on Xenserver with  |
|                         |          | L2 Guest network with configDrive                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4132`_ | Fix delete network with no services                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4145`_ | Fixing listVirtualMachinesMetrics to extend ListVMsCmd     |
|                         |          | instead of ListVMsCmdByAdmin                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4140`_ | Adding showunique parameter to list templates and isos     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4007`_ | Restarting all networks that needs a restart in a VPC      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4121`_ | server: fix TransactionLegacy DB connection leaks due to   |
|                         |          | DB switching by B&R thread                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#3991`_ | Multiple dynamic VM Scaling APIs can create duplicate      |
|                         |          | usage events for the same time                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4130`_ | Fixed null pointer after deleting snapshot, GC and cross   |
|                         |          | cluster vm migration on XCP-NG                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#3949`_ | Fix: catch CloudRuntimeException in                        |
|                         |          | LibvirtGetVolumeStatsCommandWrapper.java                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4142`_ | Invalid character encountered in file ui/l10n/pt_BR.js at  |
|                         |          | line 1134 for encoding UTF-8.                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#3965`_ | server: Honor vm.destroy.forcestop when expunge a vm       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4079`_ | Fixed HA migrated storage error                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4062`_ | [VMware] Cannot migrate VM on PVLAN shared network         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4123`_ | Improved kvmvmactivitycheck.sh output                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.1.0                | `#4124`_ | Missing python3 libvirt bindings                           |
+-------------------------+----------+------------------------------------------------------------+

113 Issues listed

.. _`#4562`: https://github.com/apache/cloudstack/pull/4562 
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
.. _`#4600`: https://github.com/apache/cloudstack/pull/4600 
.. _`#4491`: https://github.com/apache/cloudstack/pull/4491 
.. _`#4621`: https://github.com/apache/cloudstack/pull/4621 
.. _`#4580`: https://github.com/apache/cloudstack/pull/4580 
.. _`#4557`: https://github.com/apache/cloudstack/pull/4557 
.. _`#4529`: https://github.com/apache/cloudstack/pull/4529 
.. _`#4533`: https://github.com/apache/cloudstack/pull/4533 
.. _`#4532`: https://github.com/apache/cloudstack/pull/4532 
.. _`#4527`: https://github.com/apache/cloudstack/pull/4527 
.. _`#4497`: https://github.com/apache/cloudstack/pull/4497 
.. _`#4507`: https://github.com/apache/cloudstack/pull/4507 
.. _`#4501`: https://github.com/apache/cloudstack/pull/4501 
.. _`#4499`: https://github.com/apache/cloudstack/pull/4499 
.. _`#4496`: https://github.com/apache/cloudstack/pull/4496 
.. _`#4495`: https://github.com/apache/cloudstack/pull/4495 
.. _`#4500`: https://github.com/apache/cloudstack/pull/4500 
.. _`#4489`: https://github.com/apache/cloudstack/pull/4489 
.. _`#4467`: https://github.com/apache/cloudstack/pull/4467 
.. _`#4478`: https://github.com/apache/cloudstack/pull/4478 
.. _`#4466`: https://github.com/apache/cloudstack/pull/4466 
.. _`#4458`: https://github.com/apache/cloudstack/pull/4458 
.. _`#4487`: https://github.com/apache/cloudstack/pull/4487 
.. _`#4459`: https://github.com/apache/cloudstack/pull/4459 
.. _`#4485`: https://github.com/apache/cloudstack/pull/4485 
.. _`#4461`: https://github.com/apache/cloudstack/pull/4461 
.. _`#4464`: https://github.com/apache/cloudstack/pull/4464 
.. _`#4442`: https://github.com/apache/cloudstack/pull/4442 
.. _`#4430`: https://github.com/apache/cloudstack/pull/4430 
.. _`#4388`: https://github.com/apache/cloudstack/pull/4388 
.. _`#4435`: https://github.com/apache/cloudstack/pull/4435 
.. _`#4429`: https://github.com/apache/cloudstack/pull/4429 
.. _`#4359`: https://github.com/apache/cloudstack/pull/4359 
.. _`#4432`: https://github.com/apache/cloudstack/pull/4432 
.. _`#3945`: https://github.com/apache/cloudstack/pull/3945 
.. _`#4367`: https://github.com/apache/cloudstack/pull/4367 
.. _`#4413`: https://github.com/apache/cloudstack/pull/4413 
.. _`#4193`: https://github.com/apache/cloudstack/pull/4193 
.. _`#4412`: https://github.com/apache/cloudstack/pull/4412 
.. _`#4407`: https://github.com/apache/cloudstack/pull/4407 
.. _`#4377`: https://github.com/apache/cloudstack/pull/4377 
.. _`#4381`: https://github.com/apache/cloudstack/pull/4381 
.. _`#4404`: https://github.com/apache/cloudstack/pull/4404 
.. _`#4383`: https://github.com/apache/cloudstack/pull/4383 
.. _`#4373`: https://github.com/apache/cloudstack/pull/4373 
.. _`#4376`: https://github.com/apache/cloudstack/pull/4376 
.. _`#4269`: https://github.com/apache/cloudstack/pull/4269 
.. _`#4338`: https://github.com/apache/cloudstack/pull/4338 
.. _`#4190`: https://github.com/apache/cloudstack/pull/4190 
.. _`#4328`: https://github.com/apache/cloudstack/pull/4328 
.. _`#4335`: https://github.com/apache/cloudstack/pull/4335 
.. _`#4319`: https://github.com/apache/cloudstack/pull/4319 
.. _`#4297`: https://github.com/apache/cloudstack/pull/4297 
.. _`#4291`: https://github.com/apache/cloudstack/pull/4291 
.. _`#3996`: https://github.com/apache/cloudstack/pull/3996 
.. _`#3902`: https://github.com/apache/cloudstack/pull/3902 
.. _`#4288`: https://github.com/apache/cloudstack/pull/4288 
.. _`#4274`: https://github.com/apache/cloudstack/pull/4274 
.. _`#4219`: https://github.com/apache/cloudstack/pull/4219 
.. _`#4275`: https://github.com/apache/cloudstack/pull/4275 
.. _`#4213`: https://github.com/apache/cloudstack/pull/4213 
.. _`#4260`: https://github.com/apache/cloudstack/pull/4260 
.. _`#4016`: https://github.com/apache/cloudstack/pull/4016 
.. _`#4253`: https://github.com/apache/cloudstack/pull/4253 
.. _`#4019`: https://github.com/apache/cloudstack/pull/4019 
.. _`#4220`: https://github.com/apache/cloudstack/pull/4220 
.. _`#4225`: https://github.com/apache/cloudstack/pull/4225 
.. _`#4000`: https://github.com/apache/cloudstack/pull/4000 
.. _`#4116`: https://github.com/apache/cloudstack/pull/4116 
.. _`#3952`: https://github.com/apache/cloudstack/pull/3952 
.. _`#4214`: https://github.com/apache/cloudstack/pull/4214 
.. _`#4226`: https://github.com/apache/cloudstack/pull/4226 
.. _`#4188`: https://github.com/apache/cloudstack/pull/4188 
.. _`#4138`: https://github.com/apache/cloudstack/pull/4138 
.. _`#4176`: https://github.com/apache/cloudstack/pull/4176 
.. _`#4202`: https://github.com/apache/cloudstack/pull/4202 
.. _`#4186`: https://github.com/apache/cloudstack/pull/4186 
.. _`#4001`: https://github.com/apache/cloudstack/pull/4001 
.. _`#4148`: https://github.com/apache/cloudstack/pull/4148 
.. _`#4171`: https://github.com/apache/cloudstack/pull/4171 
.. _`#4167`: https://github.com/apache/cloudstack/pull/4167 
.. _`#4164`: https://github.com/apache/cloudstack/pull/4164 
.. _`#4154`: https://github.com/apache/cloudstack/pull/4154 
.. _`#4004`: https://github.com/apache/cloudstack/pull/4004 
.. _`#4132`: https://github.com/apache/cloudstack/pull/4132 
.. _`#4145`: https://github.com/apache/cloudstack/pull/4145 
.. _`#4140`: https://github.com/apache/cloudstack/pull/4140 
.. _`#4007`: https://github.com/apache/cloudstack/pull/4007 
.. _`#4121`: https://github.com/apache/cloudstack/pull/4121 
.. _`#3991`: https://github.com/apache/cloudstack/pull/3991 
.. _`#4130`: https://github.com/apache/cloudstack/pull/4130 
.. _`#3949`: https://github.com/apache/cloudstack/pull/3949 
.. _`#4142`: https://github.com/apache/cloudstack/pull/4142 
.. _`#3965`: https://github.com/apache/cloudstack/pull/3965 
.. _`#4079`: https://github.com/apache/cloudstack/pull/4079 
.. _`#4062`: https://github.com/apache/cloudstack/pull/4062 
.. _`#4123`: https://github.com/apache/cloudstack/pull/4123 
.. _`#4124`: https://github.com/apache/cloudstack/pull/4124

Changes in 4.14.0.0 since 4.13
==============================

Apache CloudStack uses GitHub <https://github.com/apache/cloudstack/issues>`_ 
to track its issues.


.. cssclass:: table-striped table-bordered table-hover


+-------------------------+----------+------------------------------------------------------------+
| Version                 | Github   | Description                                                |
+=========================+==========+============================================================+
| 4.14.0.0                | `#4064`_ | fix dhcp lease entry wrong hostname                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4057`_ | Allow deleting snapshot on local filesystem                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3992`_ | cks: use public links for templates and binaries iso for   |
|                         |          | smoke tests                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4055`_ | db.properties: Enforce UTC timezone by default             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4042`_ | Fixed guest vlan range going missing when using zone       |
|                         |          | wizard                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4043`_ | Volume deleted during cold migration if Secondary Storage  |
|                         |          | over 90% full                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4029`_ | Bring back vm.suspend during deleting VM snapshot          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4033`_ | kvm: suspend/resume in deleting vm snapshot on kvm         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4023`_ | FIX: prevent empty sshkey name.                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3969`_ | Snapshot deletion issues                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4025`_ | server: Cannot list affinity group if there are hosts      |
|                         |          | dedicated to domain                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4014`_ | Improvement on build time and new quality profile          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4002`_ | server: Search zone-wide storage pool when allocation      |
|                         |          | algothrim is firstfitleastconsumed                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3984`_ | Remove rolling-maintenance service from debian rules       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3999`_ | Update schema-41310to41400.sql                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4008`_ | Fix template registration error                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3988`_ | Add support for zulu-11 in cloudstack 4.14                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#4005`_ | Fixed create template from snapshot never returning        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3995`_ | UI bug fix: Cannot deploy VM from ISO                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3993`_ | Fixes raw templates not downloading                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3977`_ | With basic zone and VMware hypervisor, VR fails to start   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3973`_ | systemd dependency on db                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3956`_ | maven quality tool plugins                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3985`_ | NPE fix for System VM's start Command                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3989`_ | server: export full response view for zones response for   |
|                         |          | root admin                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3972`_ | Updated upgrade paths                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3971`_ | Updated upgrade path                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3587`_ | vrouter in redundant mode acquire guest ips from first ip  |
|                         |          | of the tier                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3839`_ | FEATURE-3823: kvm agent hooks                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3638`_ | UEFI Support on CloudStack                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3960`_ | Rename max.retries setting                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3932`_ | Prevent overflow on StatsCollector.java                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3681`_ | Validate disk offering IOPS normal and maximum read/write  |
|                         |          | values                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3962`_ | Make text clear regarding removing data disks.             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3963`_ | Handle port forward rule check for vpc and non vpc         |
|                         |          | Isolated networks                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3610`_ | [KVM] Rolling maintenance                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3948`_ | server: password is not displayed when reinstall a vm or   |
|                         |          | reset ssh key                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3953`_ | Revert "CLOUDSTACK-10271 maven plugin for owasp dependency |
|                         |          | check added"                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3925`_ | Add cache mode param properly                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#2446`_ | CLOUDSTACK-10271 maven plugin for owasp dependency check   |
|                         |          | added                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3657`_ | cleanup for resources left by test_accounts and            |
|                         |          | test_project                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3943`_ | vr: fix password server run with empty gateway in isolated |
|                         |          | network with RVRs                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3940`_ | Regression Fix: Allow full response view to Admin user     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3828`_ | [KVM] Direct download agnostic of the storage provider     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3651`_ | Fix simulator docker db deploy issue (apache#3397)         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3947`_ | server: fix database exception while searching network     |
|                         |          | offerings                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3935`_ | Fix VM with ISO attached migration issue                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3919`_ | Handle EOFException during VR Health Check                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3680`_ | CloudStack Kubernetes Service                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3862`_ | Userdata to display static NAT as public ip instead of VR  |
|                         |          | ip                                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3924`_ | Fixed error on data volumes lager than 2.14TB when         |
|                         |          | creating instances on VMware                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3928`_ | maven: update dependencies                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3911`_ | kvm: fix/optimize propogating configs                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3930`_ | Remove unused guest OS mapping class from Vmware code      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3927`_ | ui: fix merge issue that causes VR duplicates              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3553`_ | CloudStack Backup & Recovery Framework                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3901`_ | Removed unused vars from pom file                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3847`_ | VR: Fix Redundant VRouter guest network on wrong interface |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3898`_ | vrouter: reload keepalived instead of restart and fix      |
|                         |          | password server issues when add/remove vpc tier            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3907`_ | Allow port 80/8080 accessible only from guest network      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3916`_ | server: fix issue while list ssh keypairs by keyword       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3913`_ | Fix dhcp infinite lease time                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3904`_ | Avoid duplicate alerts when router state changes           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3903`_ | VR: Send VM password to all Running VRs in network/vpc     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3894`_ | api: Fix count and item issues returned by list APIs       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3731`_ | Enable Direct Download for systemVM templates              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3899`_ | vpc: add bypassvlanoverlapcheck parameter when create      |
|                         |          | private gateway                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3905`_ | Fix network rules issue if default egress policy is Allow  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3639`_ | Multiple networks support for vms in advanced zone with    |
|                         |          | security group (and kvm support)                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3491`_ | KVM: Propagating changes on host parameters to the agents  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3879`_ | kvm: Enable virtio drivers based on guest os display name  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3739`_ | Add new command to update security group name              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3884`_ | kvm: fix exception in volume stats after storage migration |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3882`_ | remove duplicate index region                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3864`_ | Ignore site to site vpn status check on internallbvm       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3880`_ | simulator: fix travis failure after merging volume         |
|                         |          | destroy/recover                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3871`_ | Fixed duplicate id error when creating VM work jobs        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3873`_ | Fixed root volume resize from ui                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3877`_ | [SECURITY] Use HTTPS to resolve dependencies in Maven      |
|                         |          | Build                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3601`_ | JDK11 support                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3876`_ | server: use host record related to a ssvm/cpvm             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3732`_ | [Vmware] Enable PVLAN support on L2 networks               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3870`_ | systemvm: list systemvm does not return agent state and    |
|                         |          | version                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3688`_ | New feature: Add support to destroy/recover volumes        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3854`_ | Install python-dnspython or python-dns to fix issue with   |
|                         |          | cloudstack-setup-management                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3865`_ | Fixed default text missing from network selection on       |
|                         |          | instance wizard                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3869`_ | packaging: install python-dnspython or python-dns to fix   |
|                         |          | issue with c…                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3805`_ | UI: Display drop down list for VPN customer gateway        |
|                         |          | selection                                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3844`_ | ISSUE-3838: Wrong SSVM behavior causes redownloading for   |
|                         |          | all the templates                                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3865`_ | Fixed default text missing from network selection on       |
|                         |          | instance wizard                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3857`_ | vr: add missing rule for port forwarding rule in vpc       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3851`_ | vpc: set traffic type of private gateway IP to Public to   |
|                         |          | fix keepalived misconfiguration                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3867`_ | Usage event to store zone id while uploading template and  |
|                         |          | volume                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3861`_ | test: check more connectivity in test_privategw_acl.py     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3863`_ | Start all (instead of Disconnected) Site-to-Site VPN       |
|                         |          | connections when VPC VR starts                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3803`_ | Bug fix : set restart_required to 0 after restarting       |
|                         |          | network                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3606`_ | VM ingestion                                               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3836`_ | Bug fix: De-associate IP address if enabling static nat    |
|                         |          | fails                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3807`_ | Enhancement: Allow creating network with duplicate name    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3818`_ | Display numeric value in exception instead of variable     |
|                         |          | name                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3791`_ | server: fix checking disk offering access for snapshot     |
|                         |          | volume                                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3832`_ | ui bug fix: cannot assign vms to internal lb in VPC        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3855`_ | kvm: Fix router migration issue when router has            |
|                         |          | control/public nics onother physical network than guest    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3383`_ | template: copy md5 mismatch                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3819`_ | Clean up inactive iscsi sessions when VMs get moved due to |
|                         |          | crashes                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3575`_ | Health check feature for virtual router                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3275`_ | [CLOUDSTACK-10408] Fix String.replaceAll() to replace()    |
|                         |          | for bet…                                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3604`_ | Fix Policy Based Routing for private gateway static routes |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3760`_ | New feature: Resource count (CPU/RAM) take only running    |
|                         |          | vms into calculation                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3803`_ | Bug fix : set restart_required to 0 after restarting       |
|                         |          | network                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3840`_ | Fix listing management server by parameters                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3834`_ | Fix: The metrics view API response is not super-set of     |
|                         |          | resources response keys                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3848`_ | vr: fix vr in unknown state (more)                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3726`_ | vrouter: reload haproxy when cfg file is updated           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3846`_ | Fix for "Impossible to edit domain settings in UI"         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3845`_ | travis: use https based maven repo mirror                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3835`_ | Update Docker README file                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3813`_ | kvm-local-pool-trailing-slash                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3761`_ | [FIX] [BACKPORT] [4.13] Rethrow takeVMSnapshot() exception |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3758`_ | server: Fix NPE while update displayvm on vm with dynamic  |
|                         |          | service offering                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3728`_ | server: double check host capacity when start/migrate a vm |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3727`_ | server: Capacity check should take vms in Migrating state  |
|                         |          | into calculation                                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3477`_ | RvR: Set up metadata/password/dhcp server on gateway IP    |
|                         |          | instead of guest IP in RVR                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3821`_ | Incorrect param name caused global setting test to fail    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3825`_ | fixed inconsistency of IP on VR when VR is destroyed and   |
|                         |          | recrea…                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3759`_ | server: fix resource count error when upgrade a vm         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3822`_ | set TCP as default protocol in lb list                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3694`_ | Ldap fixes                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3799`_ | Update message when keys are NOT being injected            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3806`_ | python/c++ formatting in java corrected                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3814`_ | Add missing HA config keys (#3776)                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3350`_ | Get Diagnostics: Download logs and diagnostics data from   |
|                         |          | SSVM, CPVM, Router                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3795`_ | Agent lb on svm                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3776`_ | Add missing HA config keys                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3659`_ | Fix typo: the past tense of shutdown is shutdown, not      |
|                         |          | shutdowned                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3800`_ | Revert "Extract systemvm.iso using bsdtar (#3536)"         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3510`_ | Allow additional configuration metadata to VMs             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3736`_ | Add protocol number support for security group rules       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3778`_ | Endless settings on templates and instances                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3796`_ | Revert "Simulator: Better VR Redundant Status Behaviour"   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3743`_ | only update powerstate if sure it is the latest            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3536`_ | Extract systemvm.iso using bsdtar                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3313`_ | Simulator: Better VR Redundant Status Behaviour            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3682`_ | ui: fix migrate host form no host popup                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3658`_ | client: fix for jetty session timeout                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3662`_ | Increase DHCP lease time to infinite                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3793`_ | ui: fix for truncated name for project accounts            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3597`_ | kvm: Logrotate should not touch agent.log                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3721`_ | network: cleanup dhcp/dns entries while remove a nic from  |
|                         |          | vm                                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3790`_ | Bug fix: Dont display empty item in free ip list           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3715`_ | break session only on illegal origin                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3775`_ | New feature: Acquire specific public IP for network        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3755`_ | Added zone check for attach iso                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3782`_ | 4.13                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3729`_ | config: add isdynamic flag in configuration response       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3733`_ | filter hosts to query on zone wide storage                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3747`_ | convert protocal names to be found as labels               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3754`_ | Once again allow a VM to be on multiple networks from VPCs |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3767`_ | create template from snapshot regression (partly reverted) |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3781`_ | Honour promiscuous mode from networkOffering (#3765)       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3765`_ | Honour promiscuous mode from networkOffering               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3772`_ | Revert of the "Revert "Fix virtual template size for       |
|                         |          | managed storage for KVM / refactor                         |
|                         |          | cloud-install-sys-tmplt""                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3425`_ | Better tracking host maintanence and handling of migration |
|                         |          | jobs                                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3774`_ | Revert "Add missing HA config keys"                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3771`_ | Revert "Fix virtual template size for managed storage for  |
|                         |          | KVM / refactor cloud-install-sys-tmplt"                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3371`_ | Fix virtual template size for managed storage for KVM /    |
|                         |          | refactor cloud-install-sys-tmplt                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3737`_ | Add missing HA config keys                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3738`_ | Load Average for KVM                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3769`_ | README: that time of the year!                             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3746`_ | Fix OS category for some OS-es added in 4.13               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3615`_ | Handle Ceph/RBD snapshot delete                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3546`_ | [FIX] Rethrow takeVMSnapshot() exception                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3474`_ | Enhance VM Statistics to add more detail                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3745`_ | Save SSH.PublicKey into user_vm_details regardless of      |
|                         |          | password management.                                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3740`_ | Add support for ecdsa and ed25519 public keys.             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3617`_ | [KVM] Agent LB Fix: Connections from disabled KVM host     |
|                         |          | agents are refused                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3669`_ | server: Fix resource count of primary storage/volume       |
|                         |          | because of Expunged volumes                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3723`_ | a conditional to prevent creation of a field               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3640`_ | consoleproxy: Enable console for vms in Stopping/Migrating |
|                         |          | state                                                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3704`_ | utils: use iproute to get default network interface        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3703`_ | increase width of field in UI                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3696`_ | env config for dual zone simulator                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3695`_ | debian: fix symlink issue post install/upgrade             |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3701`_ | security_group.py: check cidr unstrictly to accept cidrs   |
|                         |          | like 1.1.1.1/24                                            |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3635`_ | server: acquire IPv4 address when add secondary IP to nic  |
|                         |          | if IP is not specified                                     |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3636`_ | kvm: fix issue that network rules for secondary IPs are    |
|                         |          | not applied                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3653`_ | Fix VR creation issue while creating VM on shared network  |
|                         |          | using PVLAN                                                |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3630`_ | New BuildRequires for CentOS 7: python-setuptools          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3650`_ | Add support for vSphere Web SDK 6.7 installation in        |
|                         |          | install-non-oss.sh                                         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3678`_ | vpc: fix acl rule with protocol number is not applied      |
|                         |          | correctly in vpc vr                                        |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3632`_ | add class cleanup method                                   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3682`_ | ui: fix migrate host form no host popup                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3605`_ | fix issue #3590 'Revert Ceph/RBD Snapshot'                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3668`_ | storage: don't select an SSVM that is removed              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3612`_ | systemvm: for ip route show command don't use the throw    |
|                         |          | command                                                    |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3616`_ | Reduce verbosity of Async Job Manager log messages         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3644`_ | IoT/ARM64 support: allow cloudstack-agent on Raspberry Pi  |
|                         |          | 4 (armv8) to use kvm acceleration                          |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3666`_ | snapshot failure diagnostics unhidden                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3623`_ | kvm: Use 'ip' instead of 'brctl'                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3620`_ | Small additional NuageVsp cleanups (#3146)                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3658`_ | client: fix for jetty session timeout                      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3665`_ | ignore patches and unzipped logs                           |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3662`_ | Increase DHCP lease time to infinite                       |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3641`_ | security_group.py: fix NameError: name 'd' is not defined  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3648`_ | Security Group: limit returns in get_bridge_physdev to 1   |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3525`_ | NioServer: retain links by address string to minimize      |
|                         |          | resource leak                                              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3627`_ | server: Do NOT cleanup dhcp and dns when stop a vm         |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3589`_ | kvm/security_group: Make Security Group Python 3           |
|                         |          | compatible                                                 |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3608`_ | server: Cleanup dhcp and dns entries only on expunging VM  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3607`_ | allocator: in case of null guest OS don't fail             |
|                         |          | prioritisation completely                                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3538`_ | Refactoring to remove duplicate code (by Frank/Nuage)      |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3597`_ | kvm: Logrotate should not touch agent.log                  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3591`_ | Deprecate EL6 and Add 4.13-4.14 Upgrade Path               |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3574`_ | `service is-active` output check for "failed"              |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3519`_ | kvm/cloudstack-guest-tool: Tool to query Qemu Guest Agent  |
+-------------------------+----------+------------------------------------------------------------+
| 4.14.0.0                | `#3582`_ | systemvmtemplate: Fix Debian 9 iso url                     |
+-------------------------+----------+------------------------------------------------------------+

216 Issues listed

.. _`#4064`: https://github.com/apache/cloudstack/pull/4064
.. _`#4057`: https://github.com/apache/cloudstack/pull/4057
.. _`#3992`: https://github.com/apache/cloudstack/pull/3992
.. _`#4055`: https://github.com/apache/cloudstack/pull/4055
.. _`#4042`: https://github.com/apache/cloudstack/pull/4042
.. _`#4043`: https://github.com/apache/cloudstack/pull/4043
.. _`#4029`: https://github.com/apache/cloudstack/pull/4029
.. _`#4033`: https://github.com/apache/cloudstack/pull/4033
.. _`#4023`: https://github.com/apache/cloudstack/pull/4023
.. _`#3969`: https://github.com/apache/cloudstack/pull/3969
.. _`#4025`: https://github.com/apache/cloudstack/pull/4025
.. _`#4014`: https://github.com/apache/cloudstack/pull/4014
.. _`#4002`: https://github.com/apache/cloudstack/pull/4002
.. _`#3984`: https://github.com/apache/cloudstack/pull/3984
.. _`#3999`: https://github.com/apache/cloudstack/pull/3999
.. _`#4008`: https://github.com/apache/cloudstack/pull/4008
.. _`#3988`: https://github.com/apache/cloudstack/pull/3988
.. _`#4005`: https://github.com/apache/cloudstack/pull/4005
.. _`#3995`: https://github.com/apache/cloudstack/pull/3995
.. _`#3993`: https://github.com/apache/cloudstack/pull/3993
.. _`#3977`: https://github.com/apache/cloudstack/pull/3977
.. _`#3973`: https://github.com/apache/cloudstack/pull/3973
.. _`#3956`: https://github.com/apache/cloudstack/pull/3956
.. _`#3985`: https://github.com/apache/cloudstack/pull/3985
.. _`#3989`: https://github.com/apache/cloudstack/pull/3989
.. _`#3972`: https://github.com/apache/cloudstack/pull/3972
.. _`#3971`: https://github.com/apache/cloudstack/pull/3971
.. _`#3587`: https://github.com/apache/cloudstack/pull/3587
.. _`#3839`: https://github.com/apache/cloudstack/pull/3839
.. _`#3638`: https://github.com/apache/cloudstack/pull/3638
.. _`#3960`: https://github.com/apache/cloudstack/pull/3960
.. _`#3932`: https://github.com/apache/cloudstack/pull/3932
.. _`#3681`: https://github.com/apache/cloudstack/pull/3681
.. _`#3962`: https://github.com/apache/cloudstack/pull/3962
.. _`#3963`: https://github.com/apache/cloudstack/pull/3963
.. _`#3610`: https://github.com/apache/cloudstack/pull/3610
.. _`#3948`: https://github.com/apache/cloudstack/pull/3948
.. _`#3953`: https://github.com/apache/cloudstack/pull/3953
.. _`#3925`: https://github.com/apache/cloudstack/pull/3925
.. _`#2446`: https://github.com/apache/cloudstack/pull/2446
.. _`#3657`: https://github.com/apache/cloudstack/pull/3657
.. _`#3943`: https://github.com/apache/cloudstack/pull/3943
.. _`#3940`: https://github.com/apache/cloudstack/pull/3940
.. _`#3828`: https://github.com/apache/cloudstack/pull/3828
.. _`#3651`: https://github.com/apache/cloudstack/pull/3651
.. _`#3947`: https://github.com/apache/cloudstack/pull/3947
.. _`#3935`: https://github.com/apache/cloudstack/pull/3935
.. _`#3919`: https://github.com/apache/cloudstack/pull/3919
.. _`#3680`: https://github.com/apache/cloudstack/pull/3680
.. _`#3862`: https://github.com/apache/cloudstack/pull/3862
.. _`#3924`: https://github.com/apache/cloudstack/pull/3924
.. _`#3928`: https://github.com/apache/cloudstack/pull/3928
.. _`#3911`: https://github.com/apache/cloudstack/pull/3911
.. _`#3930`: https://github.com/apache/cloudstack/pull/3930
.. _`#3927`: https://github.com/apache/cloudstack/pull/3927
.. _`#3553`: https://github.com/apache/cloudstack/pull/3553
.. _`#3901`: https://github.com/apache/cloudstack/pull/3901
.. _`#3847`: https://github.com/apache/cloudstack/pull/3847
.. _`#3898`: https://github.com/apache/cloudstack/pull/3898
.. _`#3907`: https://github.com/apache/cloudstack/pull/3907
.. _`#3916`: https://github.com/apache/cloudstack/pull/3916
.. _`#3913`: https://github.com/apache/cloudstack/pull/3913
.. _`#3904`: https://github.com/apache/cloudstack/pull/3904
.. _`#3903`: https://github.com/apache/cloudstack/pull/3903
.. _`#3894`: https://github.com/apache/cloudstack/pull/3894
.. _`#3731`: https://github.com/apache/cloudstack/pull/3731
.. _`#3899`: https://github.com/apache/cloudstack/pull/3899
.. _`#3905`: https://github.com/apache/cloudstack/pull/3905
.. _`#3639`: https://github.com/apache/cloudstack/pull/3639
.. _`#3491`: https://github.com/apache/cloudstack/pull/3491
.. _`#3879`: https://github.com/apache/cloudstack/pull/3879
.. _`#3739`: https://github.com/apache/cloudstack/pull/3739
.. _`#3884`: https://github.com/apache/cloudstack/pull/3884
.. _`#3882`: https://github.com/apache/cloudstack/pull/3882
.. _`#3864`: https://github.com/apache/cloudstack/pull/3864
.. _`#3880`: https://github.com/apache/cloudstack/pull/3880
.. _`#3871`: https://github.com/apache/cloudstack/pull/3871
.. _`#3873`: https://github.com/apache/cloudstack/pull/3873
.. _`#3877`: https://github.com/apache/cloudstack/pull/3877
.. _`#3601`: https://github.com/apache/cloudstack/pull/3601
.. _`#3876`: https://github.com/apache/cloudstack/pull/3876
.. _`#3732`: https://github.com/apache/cloudstack/pull/3732
.. _`#3870`: https://github.com/apache/cloudstack/pull/3870
.. _`#3688`: https://github.com/apache/cloudstack/pull/3688
.. _`#3854`: https://github.com/apache/cloudstack/pull/3854
.. _`#3865`: https://github.com/apache/cloudstack/pull/3865
.. _`#3869`: https://github.com/apache/cloudstack/pull/3869
.. _`#3805`: https://github.com/apache/cloudstack/pull/3805
.. _`#3844`: https://github.com/apache/cloudstack/pull/3844
.. _`#3865`: https://github.com/apache/cloudstack/pull/3865
.. _`#3857`: https://github.com/apache/cloudstack/pull/3857
.. _`#3851`: https://github.com/apache/cloudstack/pull/3851
.. _`#3867`: https://github.com/apache/cloudstack/pull/3867
.. _`#3861`: https://github.com/apache/cloudstack/pull/3861
.. _`#3863`: https://github.com/apache/cloudstack/pull/3863
.. _`#3803`: https://github.com/apache/cloudstack/pull/3803
.. _`#3606`: https://github.com/apache/cloudstack/pull/3606
.. _`#3836`: https://github.com/apache/cloudstack/pull/3836
.. _`#3807`: https://github.com/apache/cloudstack/pull/3807
.. _`#3818`: https://github.com/apache/cloudstack/pull/3818
.. _`#3791`: https://github.com/apache/cloudstack/pull/3791
.. _`#3832`: https://github.com/apache/cloudstack/pull/3832
.. _`#3855`: https://github.com/apache/cloudstack/pull/3855
.. _`#3383`: https://github.com/apache/cloudstack/pull/3383
.. _`#3819`: https://github.com/apache/cloudstack/pull/3819
.. _`#3575`: https://github.com/apache/cloudstack/pull/3575
.. _`#3275`: https://github.com/apache/cloudstack/pull/3275
.. _`#3604`: https://github.com/apache/cloudstack/pull/3604
.. _`#3760`: https://github.com/apache/cloudstack/pull/3760
.. _`#3803`: https://github.com/apache/cloudstack/pull/3803
.. _`#3840`: https://github.com/apache/cloudstack/pull/3840
.. _`#3834`: https://github.com/apache/cloudstack/pull/3834
.. _`#3848`: https://github.com/apache/cloudstack/pull/3848
.. _`#3726`: https://github.com/apache/cloudstack/pull/3726
.. _`#3846`: https://github.com/apache/cloudstack/pull/3846
.. _`#3845`: https://github.com/apache/cloudstack/pull/3845
.. _`#3835`: https://github.com/apache/cloudstack/pull/3835
.. _`#3813`: https://github.com/apache/cloudstack/pull/3813
.. _`#3761`: https://github.com/apache/cloudstack/pull/3761
.. _`#3758`: https://github.com/apache/cloudstack/pull/3758
.. _`#3728`: https://github.com/apache/cloudstack/pull/3728
.. _`#3727`: https://github.com/apache/cloudstack/pull/3727
.. _`#3477`: https://github.com/apache/cloudstack/pull/3477
.. _`#3821`: https://github.com/apache/cloudstack/pull/3821
.. _`#3825`: https://github.com/apache/cloudstack/pull/3825
.. _`#3759`: https://github.com/apache/cloudstack/pull/3759
.. _`#3822`: https://github.com/apache/cloudstack/pull/3822
.. _`#3694`: https://github.com/apache/cloudstack/pull/3694
.. _`#3799`: https://github.com/apache/cloudstack/pull/3799
.. _`#3806`: https://github.com/apache/cloudstack/pull/3806
.. _`#3814`: https://github.com/apache/cloudstack/pull/3814
.. _`#3350`: https://github.com/apache/cloudstack/pull/3350
.. _`#3795`: https://github.com/apache/cloudstack/pull/3795
.. _`#3776`: https://github.com/apache/cloudstack/pull/3776
.. _`#3659`: https://github.com/apache/cloudstack/pull/3659
.. _`#3800`: https://github.com/apache/cloudstack/pull/3800
.. _`#3510`: https://github.com/apache/cloudstack/pull/3510
.. _`#3736`: https://github.com/apache/cloudstack/pull/3736
.. _`#3778`: https://github.com/apache/cloudstack/pull/3778
.. _`#3796`: https://github.com/apache/cloudstack/pull/3796
.. _`#3743`: https://github.com/apache/cloudstack/pull/3743
.. _`#3536`: https://github.com/apache/cloudstack/pull/3536
.. _`#3313`: https://github.com/apache/cloudstack/pull/3313
.. _`#3682`: https://github.com/apache/cloudstack/pull/3682
.. _`#3658`: https://github.com/apache/cloudstack/pull/3658
.. _`#3662`: https://github.com/apache/cloudstack/pull/3662
.. _`#3793`: https://github.com/apache/cloudstack/pull/3793
.. _`#3597`: https://github.com/apache/cloudstack/pull/3597
.. _`#3721`: https://github.com/apache/cloudstack/pull/3721
.. _`#3790`: https://github.com/apache/cloudstack/pull/3790
.. _`#3715`: https://github.com/apache/cloudstack/pull/3715
.. _`#3775`: https://github.com/apache/cloudstack/pull/3775
.. _`#3755`: https://github.com/apache/cloudstack/pull/3755
.. _`#3782`: https://github.com/apache/cloudstack/pull/3782
.. _`#3729`: https://github.com/apache/cloudstack/pull/3729
.. _`#3733`: https://github.com/apache/cloudstack/pull/3733
.. _`#3747`: https://github.com/apache/cloudstack/pull/3747
.. _`#3754`: https://github.com/apache/cloudstack/pull/3754
.. _`#3767`: https://github.com/apache/cloudstack/pull/3767
.. _`#3781`: https://github.com/apache/cloudstack/pull/3781
.. _`#3765`: https://github.com/apache/cloudstack/pull/3765
.. _`#3772`: https://github.com/apache/cloudstack/pull/3772
.. _`#3425`: https://github.com/apache/cloudstack/pull/3425
.. _`#3774`: https://github.com/apache/cloudstack/pull/3774
.. _`#3771`: https://github.com/apache/cloudstack/pull/3771
.. _`#3371`: https://github.com/apache/cloudstack/pull/3371
.. _`#3737`: https://github.com/apache/cloudstack/pull/3737
.. _`#3738`: https://github.com/apache/cloudstack/pull/3738
.. _`#3769`: https://github.com/apache/cloudstack/pull/3769
.. _`#3746`: https://github.com/apache/cloudstack/pull/3746
.. _`#3615`: https://github.com/apache/cloudstack/pull/3615
.. _`#3546`: https://github.com/apache/cloudstack/pull/3546
.. _`#3474`: https://github.com/apache/cloudstack/pull/3474
.. _`#3745`: https://github.com/apache/cloudstack/pull/3745
.. _`#3740`: https://github.com/apache/cloudstack/pull/3740
.. _`#3617`: https://github.com/apache/cloudstack/pull/3617
.. _`#3669`: https://github.com/apache/cloudstack/pull/3669
.. _`#3723`: https://github.com/apache/cloudstack/pull/3723
.. _`#3640`: https://github.com/apache/cloudstack/pull/3640
.. _`#3704`: https://github.com/apache/cloudstack/pull/3704
.. _`#3703`: https://github.com/apache/cloudstack/pull/3703
.. _`#3696`: https://github.com/apache/cloudstack/pull/3696
.. _`#3695`: https://github.com/apache/cloudstack/pull/3695
.. _`#3701`: https://github.com/apache/cloudstack/pull/3701
.. _`#3635`: https://github.com/apache/cloudstack/pull/3635
.. _`#3636`: https://github.com/apache/cloudstack/pull/3636
.. _`#3653`: https://github.com/apache/cloudstack/pull/3653
.. _`#3630`: https://github.com/apache/cloudstack/pull/3630
.. _`#3650`: https://github.com/apache/cloudstack/pull/3650
.. _`#3678`: https://github.com/apache/cloudstack/pull/3678
.. _`#3632`: https://github.com/apache/cloudstack/pull/3632
.. _`#3682`: https://github.com/apache/cloudstack/pull/3682
.. _`#3605`: https://github.com/apache/cloudstack/pull/3605
.. _`#3668`: https://github.com/apache/cloudstack/pull/3668
.. _`#3612`: https://github.com/apache/cloudstack/pull/3612
.. _`#3616`: https://github.com/apache/cloudstack/pull/3616
.. _`#3644`: https://github.com/apache/cloudstack/pull/3644
.. _`#3666`: https://github.com/apache/cloudstack/pull/3666
.. _`#3623`: https://github.com/apache/cloudstack/pull/3623
.. _`#3620`: https://github.com/apache/cloudstack/pull/3620
.. _`#3658`: https://github.com/apache/cloudstack/pull/3658
.. _`#3665`: https://github.com/apache/cloudstack/pull/3665
.. _`#3662`: https://github.com/apache/cloudstack/pull/3662
.. _`#3641`: https://github.com/apache/cloudstack/pull/3641
.. _`#3648`: https://github.com/apache/cloudstack/pull/3648
.. _`#3525`: https://github.com/apache/cloudstack/pull/3525
.. _`#3627`: https://github.com/apache/cloudstack/pull/3627
.. _`#3589`: https://github.com/apache/cloudstack/pull/3589
.. _`#3608`: https://github.com/apache/cloudstack/pull/3608
.. _`#3607`: https://github.com/apache/cloudstack/pull/3607
.. _`#3538`: https://github.com/apache/cloudstack/pull/3538
.. _`#3597`: https://github.com/apache/cloudstack/pull/3597
.. _`#3591`: https://github.com/apache/cloudstack/pull/3591
.. _`#3574`: https://github.com/apache/cloudstack/pull/3574
.. _`#3519`: https://github.com/apache/cloudstack/pull/3519
.. _`#3582`: https://github.com/apache/cloudstack/pull/3582
