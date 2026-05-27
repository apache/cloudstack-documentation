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

API Changes Introduced in 4.22.0.0
==================================

For the complete list of API commands and params consult the `CloudStack Apidocs`_.

Parameters Changed API Commands
-------------------------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``listVsphereStoragePolicyCompatiblePools`` | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``capacitybytes``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``removeNodesFromKubernetesCluster``        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``csienabled``                                                               |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateHost``                              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cleanupexternaldetails`` (optional)                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createBackupSchedule``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isbackupvmexpunged``                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addNodesToKubernetesCluster``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``csienabled``                                                               |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesClusters``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``csienabled``                                                               |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listCapabilities``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``additionalconfigenabled``                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshotPolicy``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``volumename``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listStoragePools``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``capacitybytes``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteLdapConfiguration``                 | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id`` (optional)                                                            |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``hostname`` was 'required' and is now 'optional'                            |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackups``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isbackupvmexpunged``                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``upgradeKubernetesCluster``                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``csienabled``                                                               |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupProviderOfferings``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``crosszoneinstancecreation``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importBackupOffering``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``crosszoneinstancecreation``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateBackupSchedule``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isbackupvmexpunged``                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateStoragePool``                       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``capacitybytes``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupRepositories``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``crosszoneinstancecreation``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworks``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``name`` (optional)                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSnapshotPolicies``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``account`` (optional)                                                       |
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``isrecursive`` (optional)                                                   |
|                                             | - ``listall`` (optional)                                                       |
|                                             | - ``projectid`` (optional)                                                     |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``volumename``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listLdapConfigurations``                  | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id`` (optional)                                                            |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupOfferings``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``crosszoneinstancecreation``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleKubernetesCluster``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``csienabled``                                                               |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addBackupRepository``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``crosszoneinstancecreation`` (optional)                                     |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``crosszoneinstancecreation``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``assignCertToLoadBalancer``                | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forced`` (optional)                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``unmanageVirtualMachine``                  | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forced`` (optional)                                                        |
|                                             | - ``hostid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``hostid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateBackupOffering``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``crosszoneinstancecreation``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateStorageCapabilities``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``capacitybytes``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachinesUsageHistory``         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``stats(*)``                                                                 |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``stats``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createKubernetesCluster``                 | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``enablecsi`` (optional)                                                     |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``csienabled``                                                               |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addLdapConfiguration``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``getUploadParamsForTemplate``              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``templatetype`` (optional)                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``syncStoragePool``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``capacitybytes``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listInfrastructure``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backuprepositories``                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``findStoragePoolsForMigration``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``capacitybytes``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createStoragePool``                       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``capacitybytes``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSystemVmsUsageHistory``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``stats(*)``                                                                 |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``stats``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableStorageMaintenance``                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``capacitybytes``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelStorageMaintenance``                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``capacitybytes``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateSnapshotPolicy``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``volumename``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateLoadBalancerRule``                  | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cidrlist`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startKubernetesCluster``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``csienabled``                                                               |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupSchedule``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``account`` (optional)                                                       |
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``id`` (optional)                                                            |
|                                             | - ``isrecursive`` (optional)                                                   |
|                                             | - ``listall`` (optional)                                                       |
|                                             | - ``projectid`` (optional)                                                     |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``virtualmachineid`` was 'required' and is now 'optional'                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importVm``                                | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``extraparams`` (optional)                                                   |
|                                             | - ``forceconverttopool`` (optional)                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateServiceOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cleanupexternaldetails`` (optional)                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
