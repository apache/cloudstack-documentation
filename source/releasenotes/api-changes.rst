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

API Changes Introduced in 4.21.0.0
==================================

For the complete list of API commands and params consult the `CloudStack Apidocs`_.

New API Commands
----------------

.. cssclass:: table-striped table-bordered table-hover

+------------------------------------------------------------+--------------------------------------------------------------------------------+
| Name                                                       | Description                                                                    |
+============================================================+================================================================================+
| ``removeNodesFromKubernetesCluster``                       | Removes external nodes from a CKS cluster.                                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeGuiTheme``                                         | Removes an existing GUI theme.                                                 |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateOsCategory``                                       | Updates an OS category                                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``runCustomAction``                                        | Run the custom action                                                          |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addNodesToKubernetesCluster``                            | Add nodes as workers to an existing CKS cluster.                               |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``configureStorageAccess``                                 | Configure the storage access groups on zone/pod/cluster/host and storage,      |
|                                                            | accordingly connections to the storage pools                                   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createGpuCard``                                          | Creates a GPU card definition in the system                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVgpuProfiles``                                       | Lists all available vGPU profiles                                              |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateGuiTheme``                                         | Updates an existing GUI theme.                                                 |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``manageGpuDevice``                                        | Manages a GPU device                                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteOsCategory``                                       | Deletes an OS category                                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelMaintenance``                                      | Cancels maintenance of the management server                                   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateGpuCard``                                          | Updates a GPU card definition in the system                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateCustomAction``                                     | Update the custom action                                                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listGuiThemes``                                          | Lists GUI themes.                                                              |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteCniConfiguration``                                 | Deletes a CNI Configuration                                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createExtension``                                        | Create an extension                                                            |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteCustomAction``                                     | Delete the custom action                                                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addNetrisProvider``                                      | Add Netris Provider to CloudStack                                              |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteGpuDevice``                                        | Deletes a vGPU profile from the system                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listStorageAccessGroups``                                | Lists storage access groups                                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaCreditsList``                                       | Lists quota credits of an account.                                             |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``unmanageGpuDevice``                                      | Unmanage a GPU device                                                          |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addCustomAction``                                        | Add a custom action for an extension                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareForMaintenance``                                  | Prepares management server for maintenance by preventing new jobs from being   |
|                                                            | accepted after completion of active jobs and migrating the agents              |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateGpuDevice``                                        | Updates an existing GPU device                                                 |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createVMFromBackup``                                     | Creates and automatically starts a VM from a backup.                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listGpuDevices``                                         | Lists all available GPU devices                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addOsCategory``                                          | Adds a new OS category                                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaValidateActivationRule``                            | Validates if the given activation rule is valid for the informed usage type.   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVgpuProfile``                                      | Updates a vGPU profile in the system                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerExtension``                                      | Register an extension with a resource                                          |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listGpuCards``                                           | Lists all available GPU cards                                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteVgpuProfile``                                      | Deletes a vGPU profile from the system                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteExtension``                                        | Delete the extensions                                                          |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createVgpuProfile``                                      | Creates a vGPU profile in the system                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetrisProviders``                                    | list all Netris providers added to CloudStack                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listConsoleSessions``                                    | Lists console sessions.                                                        |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listCniConfiguration``                                   | List user data for CNI plugins                                                 |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createGpuDevice``                                        | Creates a GPU device manually on a host                                        |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``unregisterExtension``                                    | Unregister an extension with a resource                                        |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createGuiTheme``                                         | Creates a customized GUI theme for a set of Common Names (fixed or wildcard),  |
|                                                            | a set of domain UUIDs, and/or a set of account UUIDs.                          |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerCniConfiguration``                               | Register a CNI Configuration to be used with CKS cluster                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listCustomActions``                                      | Lists the custom actions                                                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateExtension``                                        | Update the extension                                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeManagementServer``                                 | Removes a Management Server.                                                   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``discoverGpuDevices``                                     | Discovers available GPU devices on a host                                      |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteNetrisProvider``                                   | delete Netris Provider to CloudStack                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteGpuCard``                                          | Deletes a GPU card definition from the system                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listExtensions``                                         | Lists extensions                                                               |
+------------------------------------------------------------+--------------------------------------------------------------------------------+


Parameters Changed API Commands
-------------------------------

.. cssclass:: table-striped table-bordered table-hover

+------------------------------------------------------------+--------------------------------------------------------------------------------+
| Name                                                       | Description                                                                    |
+============================================================+================================================================================+
| ``createVPCOffering``                                      | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider`` (optional)                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``ldapCreateAccount``                                      | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``copyIso``                                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVsphereStoragePolicyCompatiblePools``                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``usediops``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootSystemVm``                                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``jobid``                                                                    |
|                                                            | - ``jobstatus``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateGuestOs``                                          | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``oscategoryid`` (optional)                                                  |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``osdisplayname`` was 'required' and is now 'optional'                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreVirtualMachine``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateHost``                                             | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``externaldetails`` (optional)                                               |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``clusterstorageaccessgroups``                                               |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``managementservername``                                                     |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``virtualmachineid``                                                         |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``destroySystemVm``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``jobid``                                                                    |
|                                                            | - ``jobstatus``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleSystemVm``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``jobid``                                                                    |
|                                                            | - ``jobstatus``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listClusters``                                           | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            | - ``storageaccessgroup`` (optional)                                            |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listClustersMetrics``                                    | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            | - ``storageaccessgroup`` (optional)                                            |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createBackupSchedule``                                   | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``maxbackups`` (optional)                                                    |
|                                                            | - ``quiescevm`` (optional)                                                     |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``description``                                                              |
|                                                            | - ``intervaltype``                                                             |
|                                                            | - ``name``                                                                     |
|                                                            | - ``vmbackupofferingremoved``                                                  |
|                                                            | - ``vmdetails``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startRouter``                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listObjectStoragePools``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageallocated``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createBackup``                                           | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``description`` (optional)                                                   |
|                                                            | - ``name`` (optional)                                                          |
|                                                            | - ``quiescevm`` (optional)                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopSystemVm``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``jobid``                                                                    |
|                                                            | - ``jobstatus``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVmNicIp``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startInternalLoadBalancerVM``                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesClusters``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``cniconfigname``                                                            |
|                                                            | - ``cniconfigurationid``                                                       |
|                                                            | - ``controlofferingid``                                                        |
|                                                            | - ``controlofferingname``                                                      |
|                                                            | - ``etcdips``                                                                  |
|                                                            | - ``etcdnodes``                                                                |
|                                                            | - ``etcdofferingid``                                                           |
|                                                            | - ``etcdofferingname``                                                         |
|                                                            | - ``workerofferingid``                                                         |
|                                                            | - ``workerofferingname``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listCapabilities``                                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``dynamicscalingenabled``                                                    |
|                                                            | - ``extensionspath``                                                           |
|                                                            | - ``instanceleaseenabled``                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listManagementServersMetrics``                           | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``peers`` (optional)                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createStaticRoute``                                      | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``nexthop`` (optional)                                                       |
|                                                            | - ``vpcid`` (optional)                                                         |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``gatewayid`` was 'required' and is now 'optional'                           |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``nexthop``                                                                  |
|                                                            | - ``vpcgatewayid``                                                             |
|                                                            | - ``vpcgatewayip``                                                             |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``gatewayid``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDomain``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshotPolicy``                                   | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageids`` (optional)                                                    |
|                                                            | - ``usestoragereplication`` (optional)                                         |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storage``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSystemVms``                                          | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``jobid``                                                                    |
|                                                            | - ``jobstatus``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshot``                                         | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageids`` (optional)                                                    |
|                                                            | - ``usestoragereplication`` (optional)                                         |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``chainsize``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listStoragePoolsMetrics``                                | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroup`` (optional)                                            |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listStoragePools``                                       | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroup`` (optional)                                            |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``usediops``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``findHostsForMigration``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``id``                                                                       |
|                                                            | - ``averageload``                                                              |
|                                                            | - ``capabilities``                                                             |
|                                                            | - ``clusterid``                                                                |
|                                                            | - ``clustername``                                                              |
|                                                            | - ``clustertype``                                                              |
|                                                            | - ``cpuallocated``                                                             |
|                                                            | - ``cpuallocatedpercentage``                                                   |
|                                                            | - ``cpuallocatedvalue``                                                        |
|                                                            | - ``cpuallocatedwithoverprovisioning``                                         |
|                                                            | - ``cpunumber``                                                                |
|                                                            | - ``cpuspeed``                                                                 |
|                                                            | - ``cpuused``                                                                  |
|                                                            | - ``cpuwithoverprovisioning``                                                  |
|                                                            | - ``created``                                                                  |
|                                                            | - ``disconnected``                                                             |
|                                                            | - ``disksizeallocated``                                                        |
|                                                            | - ``disksizetotal``                                                            |
|                                                            | - ``events``                                                                   |
|                                                            | - ``explicithosttags``                                                         |
|                                                            | - ``hahost``                                                                   |
|                                                            | - ``hasenoughcapacity``                                                        |
|                                                            | - ``hosttags``                                                                 |
|                                                            | - ``hypervisor``                                                               |
|                                                            | - ``hypervisorversion``                                                        |
|                                                            | - ``implicithosttags``                                                         |
|                                                            | - ``ipaddress``                                                                |
|                                                            | - ``islocalstorageactive``                                                     |
|                                                            | - ``lastpinged``                                                               |
|                                                            | - ``managementserverid``                                                       |
|                                                            | - ``memoryallocated``                                                          |
|                                                            | - ``memoryallocatedbytes``                                                     |
|                                                            | - ``memoryallocatedpercentage``                                                |
|                                                            | - ``memorytotal``                                                              |
|                                                            | - ``memoryused``                                                               |
|                                                            | - ``memorywithoverprovisioning``                                               |
|                                                            | - ``name``                                                                     |
|                                                            | - ``networkkbsread``                                                           |
|                                                            | - ``networkkbswrite``                                                          |
|                                                            | - ``oscategoryid``                                                             |
|                                                            | - ``oscategoryname``                                                           |
|                                                            | - ``podid``                                                                    |
|                                                            | - ``podname``                                                                  |
|                                                            | - ``removed``                                                                  |
|                                                            | - ``resourcestate``                                                            |
|                                                            | - ``state``                                                                    |
|                                                            | - ``suitableformigration``                                                     |
|                                                            | - ``type``                                                                     |
|                                                            | - ``version``                                                                  |
|                                                            | - ``zoneid``                                                                   |
|                                                            | - ``zonename``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``isAccountAllowedToCreateOfferingsWithTags``              | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``id`` was 'optional' and is now 'required'                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addNicToVirtualMachine``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listStaticRoutes``                                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``nexthop``                                                                  |
|                                                            | - ``vpcgatewayid``                                                             |
|                                                            | - ``vpcgatewayip``                                                             |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``gatewayid``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listPublicIpAddresses``                                  | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``forprovider`` (optional)                                                   |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``forprovider``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDefaultNicForVirtualMachine``                      | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listAsyncJobs``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``managementservername``                                                     |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``jobstatus``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``login``                                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``managementserverid``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``copyTemplate``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNiciraNvpDeviceNetworks``                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``specifyvlan``                                                              |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``associatednetwork``                                                        |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``resizeVolume``                                           | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``automigrate`` (optional)                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``triggerShutdown``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``agents``                                                                   |
|                                                            | - ``agentscount``                                                              |
|                                                            | - ``maintenanceinitiated``                                                     |
|                                                            | - ``state``                                                                    |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetwork``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``specifyvlan``                                                              |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``associatednetwork``                                                        |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackups``                                            | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupofferingid`` (optional)                                              |
|                                                            | - ``listvmdetails`` (optional)                                                 |
|                                                            | - ``name`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``description``                                                              |
|                                                            | - ``intervaltype``                                                             |
|                                                            | - ``name``                                                                     |
|                                                            | - ``vmbackupofferingremoved``                                                  |
|                                                            | - ``vmdetails``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachine``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``resetPasswordForVirtualMachine``                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createVPC``                                              | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userouteripresolver`` (optional)                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``detachIso``                                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareHostForMaintenance``                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``clusterstorageaccessgroups``                                               |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``managementservername``                                                     |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``virtualmachineid``                                                         |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachines``                                    | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            | - ``extensionid`` (optional)                                                   |
|                                                            | - ``gpuenabled`` (optional)                                                    |
|                                                            | - ``leased`` (optional)                                                        |
|                                                            | - ``userdataid`` (optional)                                                    |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``upgradeKubernetesCluster``                               | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``cniconfigname``                                                            |
|                                                            | - ``cniconfigurationid``                                                       |
|                                                            | - ``controlofferingid``                                                        |
|                                                            | - ``controlofferingname``                                                      |
|                                                            | - ``etcdips``                                                                  |
|                                                            | - ``etcdnodes``                                                                |
|                                                            | - ``etcdofferingid``                                                           |
|                                                            | - ``etcdofferingname``                                                         |
|                                                            | - ``workerofferingid``                                                         |
|                                                            | - ``workerofferingname``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjects``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createAccount``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``revertToVMSnapshot``                                     | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerIso``                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateZone``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``provider``                                                                 |
|                                                            | - ``routedmodeenabled``                                                        |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVlanIpRanges``                                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider``                                                                 |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``fornsx``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostMaintenance``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``clusterstorageaccessgroups``                                               |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``managementservername``                                                     |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``virtualmachineid``                                                         |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjectAccounts``                                    | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachineWithVolume``                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateUser``                                             | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess`` (optional)                                                  |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addHost``                                                | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``externaldetails`` (optional)                                               |
|                                                            | - ``storageaccessgroups`` (optional)                                           |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``clusterstorageaccessgroups``                                               |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``managementservername``                                                     |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``virtualmachineid``                                                         |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateProject``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerUserKeys``                                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listZones``                                              | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroup`` (optional)                                            |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``provider``                                                                 |
|                                                            | - ``routedmodeenabled``                                                        |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteBackupSchedule``                                   | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``id`` (optional)                                                            |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``virtualmachineid`` was 'required' and is now 'optional'                    |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupProviderOfferings``                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetscalerLoadBalancerNetworks``                      | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``specifyvlan``                                                              |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``associatednetwork``                                                        |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``importBackupOffering``                                   | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listEvents``                                             | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``state`` (optional)                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``dedicatePublicIpRange``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider``                                                                 |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``fornsx``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVirtualMachine``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``revertSnapshot``                                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``chainsize``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateSystemVm``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``jobid``                                                                    |
|                                                            | - ``jobstatus``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostAsDegraded``                                   | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``clusterstorageaccessgroups``                                               |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``managementservername``                                                     |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``virtualmachineid``                                                         |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listBrocadeVcsDeviceNetworks``                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``specifyvlan``                                                              |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``associatednetwork``                                                        |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``enableUser``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``suspendProject``                                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createZone``                                             | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroups`` (optional)                                           |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``provider``                                                                 |
|                                                            | - ``routedmodeenabled``                                                        |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listDomainChildren``                                     | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``importUnmanagedInstance``                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updatePod``                                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``attachIso``                                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createUser``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createVpnGateway``                                       | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``ipaddressid`` (optional)                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listAccounts``                                           | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess`` (optional)                                                  |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyRouter``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``activateProject``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateBackupSchedule``                                   | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``maxbackups`` (optional)                                                    |
|                                                            | - ``quiescevm`` (optional)                                                     |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``description``                                                              |
|                                                            | - ``intervaltype``                                                             |
|                                                            | - ``name``                                                                     |
|                                                            | - ``vmbackupofferingremoved``                                                  |
|                                                            | - ``vmdetails``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addBaremetalHost``                                       | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``externaldetails`` (optional)                                               |
|                                                            | - ``storageaccessgroups`` (optional)                                           |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``clusterstorageaccessgroups``                                               |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``managementservername``                                                     |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``virtualmachineid``                                                         |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVirtualMachine``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startVirtualMachine``                                    | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createPod``                                              | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroups`` (optional)                                           |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachinesMetrics``                             | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            | - ``extensionid`` (optional)                                                   |
|                                                            | - ``gpuenabled`` (optional)                                                    |
|                                                            | - ``leased`` (optional)                                                        |
|                                                            | - ``userdataid`` (optional)                                                    |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listHosts``                                              | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            | - ``managementserverid`` (optional)                                            |
|                                                            | - ``storageaccessgroup`` (optional)                                            |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``clusterstorageaccessgroups``                                               |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``managementservername``                                                     |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``virtualmachineid``                                                         |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateStoragePool``                                      | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``usediops``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupRepositories``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``mountopts``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``moveDomain``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworks``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``specifyvlan``                                                              |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``associatednetwork``                                                        |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listHostsMetrics``                                       | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            | - ``managementserverid`` (optional)                                            |
|                                                            | - ``storageaccessgroup`` (optional)                                            |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``cpuloadaverage``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelShutdown``                                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``agents``                                                                   |
|                                                            | - ``agentscount``                                                              |
|                                                            | - ``maintenanceinitiated``                                                     |
|                                                            | - ``state``                                                                    |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``reserveIpAddress``                                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``forprovider``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSnapshotPolicies``                                   | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storage``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateObjectStoragePool``                                | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``size`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageallocated``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopRouter``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``lockAccount``                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForVirtualMachine``                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTemplates``                                          | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid`` (optional)                                                   |
|                                                            | - ``forcks`` (optional)                                                        |
|                                                            | - ``isready`` (optional)                                                       |
|                                                            | - ``oscategoryid`` (optional)                                                  |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createBucket``                                           | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``quota`` was 'optional' and is now 'required'                               |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``oauthlogin``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``managementserverid``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootVirtualMachine``                                   | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupOfferings``                                    | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVnfTemplates``                                       | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid`` (optional)                                                   |
|                                                            | - ``forcks`` (optional)                                                        |
|                                                            | - ``isready`` (optional)                                                       |
|                                                            | - ``oscategoryid`` (optional)                                                  |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVnfAppliance``                                     | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``datadisksdetails`` (optional)                                              |
|                                                            | - ``externaldetails`` (optional)                                               |
|                                                            | - ``leaseduration`` (optional)                                                 |
|                                                            | - ``leaseexpiryaction`` (optional)                                             |
|                                                            | - ``snapshotid`` (optional)                                                    |
|                                                            | - ``volumeid`` (optional)                                                      |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``templateid`` was 'required' and is now 'optional'                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetworkOffering``                                  | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider`` (optional)                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listPods``                                               | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroup`` (optional)                                            |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSnapshots``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``chainsize``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``readyForShutdown``                                       | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``managementserverid`` was 'optional' and is now 'required'                  |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``agents``                                                                   |
|                                                            | - ``agentscount``                                                              |
|                                                            | - ``maintenanceinitiated``                                                     |
|                                                            | - ``state``                                                                    |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleKubernetesCluster``                                 | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``nodeofferings`` (optional)                                                 |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``cniconfigname``                                                            |
|                                                            | - ``cniconfigurationid``                                                       |
|                                                            | - ``controlofferingid``                                                        |
|                                                            | - ``controlofferingname``                                                      |
|                                                            | - ``etcdips``                                                                  |
|                                                            | - ``etcdnodes``                                                                |
|                                                            | - ``etcdofferingid``                                                           |
|                                                            | - ``etcdofferingname``                                                         |
|                                                            | - ``workerofferingid``                                                         |
|                                                            | - ``workerofferingname``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopNetScalerVpx``                                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addBackupRepository``                                    | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``mountopts``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createProject``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``markDefaultZoneForAccount``                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForSystemVm``                               | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``jobid``                                                                    |
|                                                            | - ``jobstatus``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootRouter``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshotFromVMSnapshot``                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``chainsize``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateIso``                                              | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``forceupdateostype`` (optional)                                             |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareTemplate``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateBackupOffering``                                   | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopInternalLoadBalancerVM``                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``samlSso``                                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``managementserverid``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createDomain``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateStorageCapabilities``                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``usediops``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createServiceOffering``                                  | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``externaldetails`` (optional)                                               |
|                                                            | - ``gpucount`` (optional)                                                      |
|                                                            | - ``gpudisplay`` (optional)                                                    |
|                                                            | - ``leaseduration`` (optional)                                                 |
|                                                            | - ``leaseexpiryaction`` (optional)                                             |
|                                                            | - ``vgpuprofileid`` (optional)                                                 |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``gpudisplay``                                                               |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVirtualMachine``                                   | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVmsForImport``                                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``bootmode``                                                                 |
|                                                            | - ``boottype``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addObjectStoragePool``                                   | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``size`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageallocated``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateTemplate``                                         | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``forceupdateostype`` (optional)                                             |
|                                                            | - ``forcks`` (optional)                                                        |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createVlanIpRange``                                      | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider`` (optional)                                                      |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``fornsx``                                                                   |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider``                                                                 |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``fornsx``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listPaloAltoFirewallNetworks``                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``specifyvlan``                                                              |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``associatednetwork``                                                        |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listManagementServers``                                  | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``peers`` (optional)                                                         |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``agents``                                                                   |
|                                                            | - ``agentscount``                                                              |
|                                                            | - ``ipaddress``                                                                |
|                                                            | - ``lastagents``                                                               |
|                                                            | - ``peers``                                                                    |
|                                                            | - ``pendingjobscount``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForRouter``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVirtualMachine``                                   | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``leaseduration`` (optional)                                                 |
|                                                            | - ``leaseexpiryaction`` (optional)                                             |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateAccount``                                          | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess`` (optional)                                                  |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listDomains``                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``disableAccount``                                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``resetUserDataForVirtualMachine``                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``archiveSnapshot``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``chainsize``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTemplate``                                         | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updatePortForwardingRule``                               | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``cidrlist`` (optional)                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``associateIpAddress``                                     | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``forprovider``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``resetSSHKeyForVirtualMachine``                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addKubernetesSupportedVersion``                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``linkUserDataToTemplate``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listInternalLoadBalancerVMs``                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateKubernetesSupportedVersion``                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateCluster``                                          | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``externaldetails`` (optional)                                               |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVmwareDcVms``                                        | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostname`` (optional)                                                      |
|                                                            | - ``instancename`` (optional)                                                  |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``bootmode``                                                                 |
|                                                            | - ``boottype``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``getUserKeys``                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVirtualMachine``                                   | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``datadisksdetails`` (optional)                                              |
|                                                            | - ``externaldetails`` (optional)                                               |
|                                                            | - ``leaseduration`` (optional)                                                 |
|                                                            | - ``leaseexpiryaction`` (optional)                                             |
|                                                            | - ``snapshotid`` (optional)                                                    |
|                                                            | - ``volumeid`` (optional)                                                      |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``templateid`` was 'required' and is now 'optional'                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``lockUser``                                               | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetwork``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``specifyvlan``                                                              |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``associatednetwork``                                                        |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``copySnapshot``                                           | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageids`` (optional)                                                    |
|                                                            | - ``usestoragereplication`` (optional)                                         |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``chainsize``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listUsers``                                              | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess`` (optional)                                                  |
|                                                            | - ``usersource`` (optional)                                                    |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVlanIpRange``                                      | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider``                                                                 |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``fornsx``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``disableUser``                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listIsos``                                               | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``oscategoryid`` (optional)                                                  |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startSystemVm``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``jobid``                                                                    |
|                                                            | - ``jobstatus``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerVnfTemplate``                                    | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid`` (optional)                                                   |
|                                                            | - ``externaldetails`` (optional)                                               |
|                                                            | - ``forcks`` (optional)                                                        |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``declareHostAsDegraded``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``clusterstorageaccessgroups``                                               |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``managementservername``                                                     |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``virtualmachineid``                                                         |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createKubernetesCluster``                                | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``asnumber`` (optional)                                                      |
|                                                            | - ``cniconfigdetails`` (optional)                                              |
|                                                            | - ``cniconfigurationid`` (optional)                                            |
|                                                            | - ``etcdnodes`` (optional)                                                     |
|                                                            | - ``hypervisor`` (optional)                                                    |
|                                                            | - ``nodeofferings`` (optional)                                                 |
|                                                            | - ``nodetemplates`` (optional)                                                 |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``cniconfigname``                                                            |
|                                                            | - ``cniconfigurationid``                                                       |
|                                                            | - ``controlofferingid``                                                        |
|                                                            | - ``controlofferingname``                                                      |
|                                                            | - ``etcdips``                                                                  |
|                                                            | - ``etcdnodes``                                                                |
|                                                            | - ``etcdofferingid``                                                           |
|                                                            | - ``etcdofferingname``                                                         |
|                                                            | - ``workerofferingid``                                                         |
|                                                            | - ``workerofferingname``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVMAffinityGroup``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaCredits``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``credit``                                                                   |
|                                                            | - ``creditedon``                                                               |
|                                                            | - ``creditoruserid``                                                           |
|                                                            | - ``creditorusername``                                                         |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``credits``                                                                  |
|                                                            | - ``updated_by``                                                               |
|                                                            | - ``updated_on``                                                               |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``getUploadParamsForTemplate``                             | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``forcks`` (optional)                                                        |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``syncStoragePool``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``usediops``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listRouters``                                            | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesSupportedVersions``                        | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listZonesMetrics``                                       | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroup`` (optional)                                            |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateIpAddress``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``forprovider``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateNetwork``                                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``specifyvlan``                                                              |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``associatednetwork``                                                        |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listUnmanagedInstances``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``bootmode``                                                                 |
|                                                            | - ``boottype``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerTemplate``                                       | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid`` (optional)                                                   |
|                                                            | - ``externaldetails`` (optional)                                               |
|                                                            | - ``forcks`` (optional)                                                        |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVnfAppliances``                                      | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            | - ``extensionid`` (optional)                                                   |
|                                                            | - ``gpuenabled`` (optional)                                                    |
|                                                            | - ``leased`` (optional)                                                        |
|                                                            | - ``userdataid`` (optional)                                                    |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``findStoragePoolsForMigration``                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``usediops``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createStoragePool``                                      | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroups`` (optional)                                           |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``usediops``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``enableStorageMaintenance``                               | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``usediops``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelStorageMaintenance``                               | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``usediops``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateSnapshotPolicy``                                   | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storage``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``queryAsyncJobResult``                                    | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``managementservername``                                                     |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``jobstatus``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareForShutdown``                                     | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``agents``                                                                   |
|                                                            | - ``agentscount``                                                              |
|                                                            | - ``maintenanceinitiated``                                                     |
|                                                            | - ``state``                                                                    |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addCluster``                                             | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid`` (optional)                                                   |
|                                                            | - ``externaldetails`` (optional)                                               |
|                                                            | - ``storageaccessgroups`` (optional)                                           |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeNicFromVirtualMachine``                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``enableAccount``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            | - ``backupavailable``                                                          |
|                                                            | - ``backuplimit``                                                              |
|                                                            | - ``backupstorageavailable``                                                   |
|                                                            | - ``backupstoragelimit``                                                       |
|                                                            | - ``backupstoragetotal``                                                       |
|                                                            | - ``backuptotal``                                                              |
|                                                            | - ``bucketavailable``                                                          |
|                                                            | - ``bucketlimit``                                                              |
|                                                            | - ``buckettotal``                                                              |
|                                                            | - ``gpuavailable``                                                             |
|                                                            | - ``gpulimit``                                                                 |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``objectstorageavailable``                                                   |
|                                                            | - ``objectstoragelimit``                                                       |
|                                                            | - ``objectstoragetotal``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startKubernetesCluster``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``cniconfigname``                                                            |
|                                                            | - ``cniconfigurationid``                                                       |
|                                                            | - ``controlofferingid``                                                        |
|                                                            | - ``controlofferingname``                                                      |
|                                                            | - ``etcdips``                                                                  |
|                                                            | - ``etcdnodes``                                                                |
|                                                            | - ``etcdofferingid``                                                           |
|                                                            | - ``etcdofferingname``                                                         |
|                                                            | - ``workerofferingid``                                                         |
|                                                            | - ``workerofferingname``                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``reconnectHost``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``clusterstorageaccessgroups``                                               |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``gputotal``                                                                 |
|                                                            | - ``gpuused``                                                                  |
|                                                            | - ``managementservername``                                                     |
|                                                            | - ``podstorageaccessgroups``                                                   |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``virtualmachineid``                                                         |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupSchedule``                                     | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``id``                                                                       |
|                                                            | - ``maxbackups``                                                               |
|                                                            | - ``quiescevm``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``getUser``                                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``apikeyaccess``                                                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createManagementNetworkIpRange``                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``storageaccessgroups``                                                      |
|                                                            | - ``zonestorageaccessgroups``                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVnfTemplate``                                      | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``forceupdateostype`` (optional)                                             |
|                                                            | - ``forcks`` (optional)                                                        |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``extensionid``                                                              |
|                                                            | - ``extensionname``                                                            |
|                                                            | - ``forcks``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listServiceOfferings``                                   | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``gpuenabled`` (optional)                                                    |
|                                                            | - ``vgpuprofileid`` (optional)                                                 |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``gpudisplay``                                                               |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listOsCategories``                                       | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch`` (optional)                                                          |
|                                                            | - ``isfeatured`` (optional)                                                    |
|                                                            | - ``isiso`` (optional)                                                         |
|                                                            | - ``isvnf`` (optional)                                                         |
|                                                            | - ``showicon`` (optional)                                                      |
|                                                            | - ``zoneid`` (optional)                                                        |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``created``                                                                  |
|                                                            | - ``icon``                                                                     |
|                                                            | - ``isfeatured``                                                               |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``importVm``                                               | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``importinstancehostid`` (optional)                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateServiceOffering``                                  | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``externaldetails`` (optional)                                               |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``gpudisplay``                                                               |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopVirtualMachine``                                     | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``arch``                                                                     |
|                                                            | - ``gpucardid``                                                                |
|                                                            | - ``gpucardname``                                                              |
|                                                            | - ``gpucount``                                                                 |
|                                                            | - ``leaseduration``                                                            |
|                                                            | - ``leaseexpiryaction``                                                        |
|                                                            | - ``leaseexpirydate``                                                          |
|                                                            | - ``maxheads``                                                                 |
|                                                            | - ``maxresolutionx``                                                           |
|                                                            | - ``maxresolutiony``                                                           |
|                                                            | - ``vgpuprofileid``                                                            |
|                                                            | - ``vgpuprofilename``                                                          |
|                                                            | - ``videoram``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+


