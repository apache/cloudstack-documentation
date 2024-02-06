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

API Changes Introduced in 4.19.0.0
==================================
For the complete list of API commands and params consult the `CloudStack Apidocs`_.

New API Commands
----------------

.. cssclass:: table-striped table-bordered table-hover

+--------------------------------------------------+--------------------------------------------------------------------------------+
| Name                                             | Description                                                                    |
+==================================================+================================================================================+
| ``listOauthProvider``                            | List OAuth providers registered                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``verifyOAuthCodeAndGetUser``                    | Verify the OAuth Code and fetch the corresponding user from provider           |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listClusterDrsPlan``                           | List DRS plans for a clusters                                                  |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listStoragePoolObjects``                       | Lists objects at specified path on a storage pool.                             |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listObjectStoragePools``                       | Lists object storage pools.                                                    |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVMSchedule``                               | List VM Schedules.                                                             |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeVirtualMachinesFromKubernetesCluster``   | Remove VMs from an ExternalManaged kubernetes cluster. Not applicable for      |
|                                                  | CloudManaged kubernetes clusters.                                              |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createVMSchedule``                             | Create VM Schedule                                                             |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``generateClusterDrsPlan``                       | Generate DRS plan for a cluster                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createSecondaryStorageSelector``               | Creates a secondary storage selector, described by the heuristic rule.         |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``triggerShutdown``                              | Triggers an automatic safe shutdown of CloudStack by not accepting new jobs    |
|                                                  | and shutting down when all pending jobbs have been completed. Triggers an      |
|                                                  | immediate shutdown if forced                                                   |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeQuarantinedIp``                          | Removes a public IP address from quarantine. Only IPs in active quarantine can |
|                                                  | be removed.                                                                    |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteBucket``                                 | Deletes an empty Bucket.                                                       |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteObjectStoragePool``                      | Deletes an Object Storage Pool                                                 |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateSecondaryStorageSelector``               | Updates an existing secondary storage selector.                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerOauthProvider``                        | Register the OAuth2 provider in CloudStack                                     |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteVnfTemplate``                            | Deletes a VNF template from the system. All virtual machines using the deleted |
|                                                  | template will not be affected.                                                 |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateOauthProvider``                          | Updates the registered OAuth provider details                                  |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVMSchedule``                             | Update VM Schedule.                                                            |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``moveDomain``                                   | Moves a domain and its children to a new parent domain.                        |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteOauthProvider``                          | Deletes the registered OAuth provider                                          |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelShutdown``                               | Cancels a triggered shutdown                                                   |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteVMSchedule``                             | Delete VM Schedule.                                                            |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateObjectStoragePool``                      | Updates object storage pool                                                    |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createBucket``                                 | Creates a bucket in the specified object storage pool.                         |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``oauthlogin``                                   | Logs a user into the CloudStack after successful verification of OAuth secret  |
|                                                  | code from the particular provider.A successful login attempt will generate a   |
|                                                  | JSESSIONID cookie value that can be passed in subsequent Query command calls   |
|                                                  | until the "logout" command has been issued or the session has expired.         |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``getHypervisorGuestOsNames``                    | Gets the guest OS names in the hypervisor                                      |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``addVirtualMachinesToKubernetesCluster``        | Add VMs to an ExternalManaged kubernetes cluster. Not applicable for           |
|                                                  | CloudManaged kubernetes clusters.                                              |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVnfTemplates``                             | List all public, private, and privileged VNF templates.                        |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVnfAppliance``                           | Creates and automatically starts a VNF appliance based on a service offering,  |
|                                                  | disk offering, and template.                                                   |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateResourceToAnotherSecondaryStorage``     | migrates resources from one secondary storage to destination image store       |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``readyForShutdown``                             | Returns the status of CloudStack, whether a shutdown has been triggered and if |
|                                                  | ready to shutdown                                                              |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSecondaryStorageSelectors``                | Lists the secondary storage selectors and their rules.                         |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listImageStoreObjects``                        | Lists objects at specified path on an image store.                             |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listBuckets``                                  | Lists all Buckets.                                                             |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVmsForImport``                             | Lists virtual machines on a unmanaged host                                     |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``addObjectStoragePool``                         | Adds a object storage pool                                                     |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``executeClusterDrsPlan``                        | Execute DRS for a cluster. If there is another plan in progress for the same   |
|                                                  | cluster, this command will fail.                                               |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVmwareDcVms``                              | Lists the VMs in a VMware Datacenter                                           |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``copySnapshot``                                 | Copies a snapshot from one zone to another.                                    |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerVnfTemplate``                          | Registers an existing VNF template into the CloudStack cloud.                  |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateBucket``                                 | Updates Bucket properties                                                      |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``downloadImageStoreObject``                     | Download object at a specified path on an image store.                         |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listQuarantinedIps``                           | List public IP addresses in quarantine.                                        |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeSecondaryStorageSelector``               | Removes an existing secondary storage selector.                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareForShutdown``                           | Prepares CloudStack for a safe manual shutdown by preventing new jobs from     |
|                                                  | being accepted                                                                 |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateQuarantinedIp``                          | Updates the quarantine end date for the given public IP address.               |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVnfTemplate``                            | Updates a template to VNF template or attributes of a VNF template.            |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``importVm``                                     | Import virtual machine from a unmanaged host into CloudStack                   |
+--------------------------------------------------+--------------------------------------------------------------------------------+


Parameters Changed API Commands
-------------------------------

.. cssclass:: table-striped table-bordered table-hover

+--------------------------------------------------+--------------------------------------------------------------------------------+
| Name                                             | Description                                                                    |
+==================================================+================================================================================+
| ``createVPCOffering``                            | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachinesMetrics``                   | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``isvnf`` (optional)                                                         |
|                                                  | - ``retrieveonlyresourcecount`` (optional)                                     |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listHosts``                                    | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVsphereStoragePolicyCompatiblePools``      | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateStoragePool``                            | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``details`` (optional)                                                       |
|                                                  | - ``istagarule`` (optional)                                                    |
|                                                  | - ``url`` (optional)                                                           |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootSystemVm``                               | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``serviceofferingid``                                                        |
|                                                  | - ``serviceofferingname``                                                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworks``                                 | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``retrieveonlyresourcecount`` (optional)                                     |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``domainpath``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateGuestOs``                                | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``forDisplay`` (optional)                                                    |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``details`` was 'required' and is now 'optional'                             |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``fordisplay``                                                               |
|                                                  | - ``name``                                                                     |
|                                                  | - ``oscategoryname``                                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listHostsMetrics``                             | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``systeminstances``                                                          |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreVirtualMachine``                        | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``reserveIpAddress``                             | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``hasrules``                                                                 |
|                                                  | - ``virtualmachinetype``                                                       |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateHost``                                   | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule`` (optional)                                                    |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``destroySystemVm``                              | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``serviceofferingid``                                                        |
|                                                  | - ``serviceofferingname``                                                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleSystemVm``                                | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``serviceofferingid``                                                        |
|                                                  | - ``serviceofferingname``                                                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSnapshotPolicies``                         | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``zone``                                                                     |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForVirtualMachine``               | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTemplates``                                | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``imagestoreid`` (optional)                                                  |
|                                                  | - ``isvnf`` (optional)                                                         |
|                                                  | - ``storageid`` (optional)                                                     |
|                                                  | - ``templatetype`` (optional)                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listGuestOsMapping``                           | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``osdisplayname`` (optional)                                                 |
|                                                  | - ``osnameforhypervisor`` (optional)                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootVirtualMachine``                         | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``addGuestOsMapping``                            | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``forced`` (optional)                                                        |
|                                                  | - ``osmappingcheckenabled`` (optional)                                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVPC``                                    | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``sourcenatipaddress`` (optional)                                            |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopSystemVm``                                 | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``serviceofferingid``                                                        |
|                                                  | - ``serviceofferingname``                                                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetworkOffering``                        | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumesMetrics``                           | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``retrieveonlyresourcecount`` (optional)                                     |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVmNicIp``                                | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSnapshots``                                | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``imagestoreid`` (optional)                                                  |
|                                                  | - ``locationtype`` (optional)                                                  |
|                                                  | - ``showunique`` (optional)                                                    |
|                                                  | - ``storageid`` (optional)                                                     |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``datastoreid``                                                              |
|                                                  | - ``datastorename``                                                            |
|                                                  | - ``datastorestate``                                                           |
|                                                  | - ``datastoretype``                                                            |
|                                                  | - ``downloaddetails``                                                          |
|                                                  | - ``status``                                                                   |
|                                                  | - ``zonename``                                                                 |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesClusters``                       | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``clustertype`` (optional)                                                   |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``clustertype``                                                              |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleKubernetesCluster``                       | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``clustertype``                                                              |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listCapabilities``                             | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``customhypervisordisplayname``                                              |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshotPolicy``                         | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``zoneids`` (optional)                                                       |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``zone``                                                                     |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSystemVms``                                | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``serviceofferingid``                                                        |
|                                                  | - ``serviceofferingname``                                                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createProject``                                | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForSystemVm``                     | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``serviceofferingid``                                                        |
|                                                  | - ``serviceofferingname``                                                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshot``                               | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``zoneids`` (optional)                                                       |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``datastoreid``                                                              |
|                                                  | - ``datastorename``                                                            |
|                                                  | - ``datastorestate``                                                           |
|                                                  | - ``datastoretype``                                                            |
|                                                  | - ``downloaddetails``                                                          |
|                                                  | - ``status``                                                                   |
|                                                  | - ``zonename``                                                                 |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listStoragePoolsMetrics``                      | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``hostid`` (optional)                                                        |
|                                                  | - ``status`` (optional)                                                        |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNics``                                     | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``publicip``                                                                 |
|                                                  | - ``publicipid``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshotFromVMSnapshot``                 | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``datastoreid``                                                              |
|                                                  | - ``datastorename``                                                            |
|                                                  | - ``datastorestate``                                                           |
|                                                  | - ``datastoretype``                                                            |
|                                                  | - ``downloaddetails``                                                          |
|                                                  | - ``status``                                                                   |
|                                                  | - ``zonename``                                                                 |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listStoragePools``                             | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``hostid`` (optional)                                                        |
|                                                  | - ``status`` (optional)                                                        |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``addNicToVirtualMachine``                       | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listPublicIpAddresses``                        | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``retrieveonlyresourcecount`` (optional)                                     |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``hasrules``                                                                 |
|                                                  | - ``virtualmachinetype``                                                       |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDefaultNicForVirtualMachine``            | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listAsyncJobs``                                | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``managementserverid`` (optional)                                            |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``account``                                                                  |
|                                                  | - ``domainid``                                                                 |
|                                                  | - ``domainpath``                                                               |
|                                                  | - ``managementserverid``                                                       |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateStorageCapabilities``                    | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createServiceOffering``                        | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNiciraNvpDeviceNetworks``                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``domainpath``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVirtualMachine``                         | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listPaloAltoFirewallNetworks``                 | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``domainpath``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listManagementServers``                        | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``serviceip``                                                                |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVirtualMachine``                         | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetwork``                                | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``sourcenatipaddress`` (optional)                                            |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``domainpath``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``resetUserDataForVirtualMachine``               | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``archiveSnapshot``                              | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``datastoreid``                                                              |
|                                                  | - ``datastorename``                                                            |
|                                                  | - ``datastorestate``                                                           |
|                                                  | - ``datastoretype``                                                            |
|                                                  | - ``downloaddetails``                                                          |
|                                                  | - ``status``                                                                   |
|                                                  | - ``zonename``                                                                 |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachine``                        | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTemplate``                               | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``account`` (optional)                                                       |
|                                                  | - ``domainid`` (optional)                                                      |
|                                                  | - ``zoneid`` (optional)                                                        |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``resetPasswordForVirtualMachine``               | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``password`` (optional)                                                      |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``associateIpAddress``                           | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``hasrules``                                                                 |
|                                                  | - ``virtualmachinetype``                                                       |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``resetSSHKeyForVirtualMachine``                 | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``addKubernetesSupportedVersion``                | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``directdownload`` (optional)                                                |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``directdownload``                                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteKubernetesCluster``                      | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``cleanup`` (optional)                                                       |
|                                                  | - ``expunge`` (optional)                                                       |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createVPC``                                    | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``sourcenatipaddress`` (optional)                                            |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listOsTypes``                                  | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``fordisplay`` (optional)                                                    |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``fordisplay``                                                               |
|                                                  | - ``name``                                                                     |
|                                                  | - ``oscategoryname``                                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateKubernetesSupportedVersion``             | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``directdownload``                                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``detachIso``                                    | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareHostForMaintenance``                    | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createRole``                                   | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``ispublic`` (optional)                                                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateAutoScaleVmProfile``                     | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``userdatadetails`` (optional)                                               |
|                                                  | - ``userdataid`` (optional)                                                    |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``userdatadetails``                                                          |
|                                                  | - ``userdataid``                                                               |
|                                                  | - ``userdataname``                                                             |
|                                                  | - ``userdatapolicy``                                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteSnapshot``                               | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``zoneid`` (optional)                                                        |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachines``                          | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``isvnf`` (optional)                                                         |
|                                                  | - ``retrieveonlyresourcecount`` (optional)                                     |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateGuestOsMapping``                         | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``osmappingcheckenabled`` (optional)                                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listDiskOfferings``                            | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``account`` (optional)                                                       |
|                                                  | - ``projectid`` (optional)                                                     |
|                                                  | - ``storagetype`` (optional)                                                   |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``upgradeKubernetesCluster``                     | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``clustertype``                                                              |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``revertToVMSnapshot``                           | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``addGuestOs``                                   | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``forDisplay`` (optional)                                                    |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``details`` was 'required' and is now 'optional'                             |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``fordisplay``                                                               |
|                                                  | - ``name``                                                                     |
|                                                  | - ``oscategoryname``                                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerIso``                                  | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVirtualMachine``                         | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``nicmultiqueuenumber`` (optional)                                           |
|                                                  | - ``nicpackedvirtqueuesenabled`` (optional)                                    |
|                                                  | - ``password`` (optional)                                                      |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostMaintenance``                        | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createDiskOffering``                           | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumes``                                  | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``retrieveonlyresourcecount`` (optional)                                     |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetwork``                                | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``sourcenatipaddress`` (optional)                                            |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``domainpath``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachineWithVolume``              | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``autoselect`` (optional)                                                    |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``addHost``                                      | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateProject``                                | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``name`` (optional)                                                          |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listIsos``                                     | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``imagestoreid`` (optional)                                                  |
|                                                  | - ``storageid`` (optional)                                                     |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateRole``                                   | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``ispublic`` (optional)                                                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listZones``                                    | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``ids`` (optional)                                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetscalerLoadBalancerNetworks``            | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``domainpath``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``startSystemVm``                                | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``serviceofferingid``                                                        |
|                                                  | - ``serviceofferingname``                                                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createKubernetesCluster``                      | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``clustertype`` (optional)                                                   |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``description`` was 'required' and is now 'optional'                         |
|                                                  | - ``kubernetesversionid`` was 'required' and is now 'optional'                 |
|                                                  | - ``size`` was 'required' and is now 'optional'                                |
|                                                  | - ``serviceofferingid`` was 'required' and is now 'optional'                   |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``clustertype``                                                              |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``declareHostAsDegraded``                        | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listEvents``                                   | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``archived`` (optional)                                                      |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``archived``                                                                 |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVMAffinityGroup``                        | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVirtualMachine``                        | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``getUploadParamsForTemplate``                   | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``revertSnapshot``                               | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``datastoreid``                                                              |
|                                                  | - ``datastorename``                                                            |
|                                                  | - ``datastorestate``                                                           |
|                                                  | - ``datastoretype``                                                            |
|                                                  | - ``downloaddetails``                                                          |
|                                                  | - ``status``                                                                   |
|                                                  | - ``zonename``                                                                 |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateSystemVm``                              | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``serviceofferingid``                                                        |
|                                                  | - ``serviceofferingname``                                                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listAutoScaleVmProfiles``                      | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``userdatadetails``                                                          |
|                                                  | - ``userdataid``                                                               |
|                                                  | - ``userdataname``                                                             |
|                                                  | - ``userdatapolicy``                                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostAsDegraded``                         | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``syncStoragePool``                              | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listBrocadeVcsDeviceNetworks``                 | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``domainpath``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``importRole``                                   | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``ispublic`` (optional)                                                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesSupportedVersions``              | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``directdownload``                                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listInfrastructure``                           | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``objectstores``                                                             |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listZonesMetrics``                             | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``ids`` (optional)                                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateIpAddress``                              | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``hasrules``                                                                 |
|                                                  | - ``virtualmachinetype``                                                       |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateNetwork``                               | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``domainpath``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listUnmanagedInstances``                       | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``clustername``                                                              |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerTemplate``                             | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype`` (optional)                                                  |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createStoragePool``                            | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule`` (optional)                                                    |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``findStoragePoolsForMigration``                 | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``importUnmanagedInstance``                      | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``attachIso``                                    | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``disassociateIpAddress``                        | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``ipaddress`` (optional)                                                     |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``id`` was 'required' and is now 'optional'                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``enableStorageMaintenance``                     | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelStorageMaintenance``                     | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateSnapshotPolicy``                         | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``zone``                                                                     |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``queryAsyncJobResult``                          | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``account``                                                                  |
|                                                  | - ``domainid``                                                                 |
|                                                  | - ``domainpath``                                                               |
|                                                  | - ``managementserverid``                                                       |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeNicFromVirtualMachine``                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``getUploadParamsForIso``                        | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createAutoScaleVmProfile``                     | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``userdatadetails`` (optional)                                               |
|                                                  | - ``userdataid`` (optional)                                                    |
|                                                  |                                                                                |
|                                                  | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``userdatadetails``                                                          |
|                                                  | - ``userdataid``                                                               |
|                                                  | - ``userdataname``                                                             |
|                                                  | - ``userdatapolicy``                                                           |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``startKubernetesCluster``                       | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``clustertype``                                                              |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``reconnectHost``                                | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``addBaremetalHost``                             | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``istagarule``                                                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVirtualMachine``                        | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``listServiceOfferings``                         | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``account`` (optional)                                                       |
|                                                  | - ``projectid`` (optional)                                                     |
|                                                  | - ``storagetype`` (optional)                                                   |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``startVirtualMachine``                          | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopVirtualMachine``                           | **Response:**                                                                  |
|                                                  |                                                                                |
|                                                  | *New Parameters:*                                                              |
|                                                  |                                                                                |
|                                                  | - ``templatetype``                                                             |
|                                                  | - ``vnfdetails``                                                               |
|                                                  | - ``vnfnics``                                                                  |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetworkACLList``                         | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *Changed Parameters:*                                                          |
|                                                  |                                                                                |
|                                                  | - ``vpcid`` was 'required' and is now 'optional'                               |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+

Default Value Changed for the Parameters of the API commands
------------------------------------------------------------

.. cssclass:: table-striped table-bordered table-hover

+--------------------------------------------------+--------------------------------------------------------------------------------+
| Name                                             | Description                                                                    |
+==================================================+================================================================================+
| ``deleteTemplate``                               | **Request:**                                                                   |
|                                                  |                                                                                |
|                                                  | *Changed Parameter Values:*                                                    |
|                                                  |                                                                                |
|                                                  | - ``force`` - default value was 'true' and is now 'false'                      |
|                                                  |                                                                                |
+--------------------------------------------------+--------------------------------------------------------------------------------+
