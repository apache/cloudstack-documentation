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

API Changes Introduced in 4.23.0.0
==================================

For the complete list of API commands and params consult the `CloudStack API Documentation`_.

New API Commands
-----------------

.. cssclass:: table-striped table-bordered table-hover

+------------------------------------------------------------+--------------------------------------------------------------------------------+
| Name                                                       | Description                                                                    |
+============================================================+================================================================================+
| ``addDnsServer``                                           | Adds a new external DNS server                                                 |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addWebhookFilter``                                       | Adds a Webhook filter                                                          |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``associateDnsZoneToNetwork``                              | Associates a DNS Zone with a Network for VM auto-registration                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cloneBackupOffering``                                    | Clones a backup offering from an existing offering                             |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cloneDiskOffering``                                      | Clones a disk offering. All parameters from createDiskOffering are available.  |
|                                                            | If not specified, values will be copied from the source offering.              |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cloneNetworkOffering``                                   | Clones a network offering. All parameters are copied from the source offering  |
|                                                            | unless explicitly overridden.                                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cloneServiceOffering``                                   | Clones a service offering. All parameters from createServiceOffering are       |
|                                                            | available. If not specified, values will be copied from the source offering.   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cloneVPCOffering``                                       | Clones an existing VPC offering. All parameters are copied from the source     |
|                                                            | offering unless explicitly overridden.                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createBackupOffering``                                   | Creates a backup offering                                                      |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createDnsRecord``                                        | Creates a DNS record directly on the provider                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createDnsZone``                                          | Creates a new DNS Zone on a specific server                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createHSMProfile``                                       | Creates a new HSM profile                                                      |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createImageTransfer``                                    | Create image transfer for a disk in backup. This API is intended for testing   |
|                                                            | only and is disabled by default.                                               |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createKMSKey``                                           | Creates a new KMS key (Key Encryption Key) for encryption                      |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createResourceSchedule``                                 | Create Resource Schedule                                                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteDnsRecord``                                        | Deletes a DNS record from the external provider                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteDnsServer``                                        | Removes a DNS server integration                                               |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteDnsZone``                                          | Removes a DNS Zone from CloudStack and the external provider                   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteHSMProfile``                                       | Deletes an HSM profile                                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteKMSKey``                                           | Deletes a KMS key (only if not in use)                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteResourceSchedule``                                 | Delete Resource Schedule                                                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteUserKeys``                                         | Deletes a keypair from a user                                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteVirtualMachineCheckpoint``                         | Delete a VM checkpoint. This API is intended for testing only and is disabled  |
|                                                            | by default.                                                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteWebhookFilter``                                    | Deletes Webhook filter                                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``disassociateDnsZoneFromNetwork``                         | Removes the association between a DNS Zone and a Network                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``downloadValidationScreenshot``                           | Download validation screenshot of given backup.                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``finalizeBackup``                                         | Finalize a VM backup session. This API is intended for testing only and is     |
|                                                            | disabled by default.                                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``finalizeImageTransfer``                                  | Finalize an image transfer. This API is intended for testing only and is       |
|                                                            | disabled by default.                                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``finishBackupChain``                                      | Finish the backup chain of VM. Currently only has effect on VMs with KBOSS     |
|                                                            | backup offerings.                                                              |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``importNetworkACL``                                       | Imports Network ACL rules.                                                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupServiceJobs``                                  | List backup service jobs                                                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listDnsProviders``                                       | Lists available DNS plugin providers                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listDnsRecords``                                         | Lists DNS records from the external provider                                   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listDnsServers``                                         | Lists DNS servers owned by the account.                                        |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listDnsZones``                                           | Lists DNS zones.                                                               |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listHSMProfiles``                                        | Lists HSM profiles                                                             |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listImageTransfers``                                     | List image transfers for a backup. This API is intended for testing only and is|
|                                                            | disabled by default.                                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listKMSKeys``                                            | Lists KMS keys available to the caller                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listResourceSchedule``                                   | List Resource Schedules                                                        |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listUserKeyRules``                                       | Lists the rules defined for a API key pair.                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listUserKeys``                                           | Lists the API key pairs (API and secret keys) of a user.                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachineCheckpoints``                          | List checkpoints for a VM. This API is intended for testing only and is        |
|                                                            | disabled by default.                                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listWebhookFilters``                                     | Lists Webhook filters                                                          |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVolumesToKMS``                                    | Migrates encrypted volumes to KMS                                              |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaResourceStatement``                                 | Generates a detailed Quota statement for a specific resource.                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``rotateKMSKey``                                           | Rotates KMS key (KEK) by creating new version and scheduling gradual re-       |
|                                                            | encryption                                                                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startBackup``                                            | Start a VM backup session using pull mode backup-begin on the KVM host. This   |
|                                                            | API is intended for testing only and is disabled by default.                   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``unlinkDomainFromLdap``                                   | remove the linkage of a Domain to a group or OU in ldap                        |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDnsServer``                                        | Update DNS server                                                              |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDnsZone``                                          | Updates a DNS Zone's metadata                                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateHSMProfile``                                       | Updates an HSM profile                                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateKMSKey``                                           | Updates KMS key name, description, or enabled status                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateKubernetesClusterAffinityGroups``                  | Updates the affinity group mappings for a stopped Kubernetes cluster           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateRegisteredExtension``                              | Update details for an extension registered with a resource                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateResourceSchedule``                                 | Update Resource Schedule                                                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVmNic``                                            | Updates the specified VM NIC                                                   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+

Parameters Changed API Commands
-------------------------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``addIpToNic``                              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``description`` (optional)                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addSecondaryStorage``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createBackup``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isolated`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createBackupSchedule``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isolated`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createExtension``                         | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``reservedresourcedetails`` (optional)                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createGuiTheme``                          | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``loginbasedomain`` (optional)                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createKubernetesCluster``                 | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``nodeaffinitygroups`` (optional)                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetwork``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``keepmacaddressonpublicnic`` (optional)                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createUser``                              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``passwordchangerequired`` (optional)                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVMFromBackup``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``quickrestore`` (optional)                                                  |
|                                             | - ``rootdiskkmskeyid`` (optional)                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVPC``                               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``keepmacaddressonpublicnic`` (optional)                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVPCOffering``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``conservemode`` (optional)                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVolume``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``kmskeyid`` (optional)                                                      |
|                                             | - ``storageid`` (optional)                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVirtualMachine``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``rootdiskkmskeyid`` (optional)                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``detachIso``                               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id`` (optional)                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importBackupOffering``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importVm``                                | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osid`` (optional)                                                          |
|                                             | - ``usevddk`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``linkDomainToLdap``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``ldapdomain`` was 'optional' and is now 'required'                          |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``name``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listAsyncJobs``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``resourceid`` (optional)                                                    |
|                                             | - ``resourcetype`` (optional)                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackups``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``status`` (optional)                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listCapabilities``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listExtensions``                          | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``type`` (optional)                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listHosts``                               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``version`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listHostsMetrics``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``version`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listManagementServers``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``version`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listManagementServersMetrics``            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``version`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listOauthProvider``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domain`` (optional)                                                        |
|                                             | - ``domainid`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listOsTypes``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ids`` (optional)                                                           |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumes``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``kmskeyid`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumesMetrics``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``kmskeyid`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``provisionCertificate``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forced`` (optional)                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``queryAsyncJobResult``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``resourceid`` (optional)                                                    |
|                                             | - ``resourcetype`` (optional)                                                  |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``jobid`` was 'required' and is now 'optional'                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaBalance``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``projectid`` (optional)                                                     |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``account`` was 'required' and is now 'optional'                             |
|                                             | - ``domainid`` was 'required' and is now 'optional'                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaCredits``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``accountid`` (optional)                                                     |
|                                             | - ``projectid`` (optional)                                                     |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``account`` was 'required' and is now 'optional'                             |
|                                             | - ``domainid`` was 'required' and is now 'optional'                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaCreditsList``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``projectid`` (optional)                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaStatement``                          | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isrecursive`` (optional)                                                   |
|                                             | - ``projectid`` (optional)                                                     |
|                                             | - ``showresources`` (optional)                                                 |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``account`` was 'required' and is now 'optional'                             |
|                                             | - ``domainid`` was 'required' and is now 'optional'                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaSummary``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``accountid`` (optional)                                                     |
|                                             | - ``accountstatetoshow`` (optional)                                            |
|                                             | - ``projectid`` (optional)                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerOauthProvider``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``authorizeurl`` (optional)                                                  |
|                                             | - ``domain`` (optional)                                                        |
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``tokenurl`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerUserKeys``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``description`` (optional)                                                   |
|                                             | - ``enddate`` (optional)                                                       |
|                                             | - ``name`` (optional)                                                          |
|                                             | - ``rules`` (optional)                                                         |
|                                             | - ``startdate`` (optional)                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetConfiguration``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``managementserverid`` (optional)                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreBackup``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``hostid`` (optional)                                                        |
|                                             | - ``quickrestore`` (optional)                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreVolumeFromBackupAndAttachToVM``    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``hostid`` (optional)                                                        |
|                                             | - ``quickrestore`` (optional)                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateBackupOffering``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateBackupSchedule``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isolated`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateConfiguration``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``managementserverid`` (optional)                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateExtension``                         | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``reservedresourcedetails`` (optional)                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateGuiTheme``                          | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``loginbasedomain`` (optional)                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateHost``                              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``guestosrule`` (optional)                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetwork``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``keepmacaddressonpublicnic`` (optional)                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateOauthProvider``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``authorizeurl`` (optional)                                                  |
|                                             | - ``domain`` (optional)                                                        |
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``tokenurl`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateUser``                              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``passwordchangerequired`` (optional)                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVPC``                               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``keepmacaddressonpublicnic`` (optional)                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVirtualMachine``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cleanupextraconfig`` (optional)                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``verifyOAuthCodeAndGetUser``               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domain`` (optional)                                                        |
|                                             | - ``domainid`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
