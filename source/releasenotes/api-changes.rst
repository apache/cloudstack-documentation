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

API Changes Introduced in 4.14.0.0
===================================
For the complete list of API commands and params consult the `CloudStack Apidocs`_.

New API Commands
----------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``startRollingMaintenance``                 | Start rolling maintenance                                                      |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createBackupSchedule``                    | Creates a user-defined VM backup schedule                                      |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupOfferings``                     | Lists backup offerings                                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createBackup``                            | Create VM backup                                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopKubernetesCluster``                   | Stops a running Kubernetes cluster                                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesClusters``                  | Lists Kubernetes clusters                                                      |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleKubernetesCluster``                  | Scales a created, running or stopped Kubernetes cluster                        |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVolume``                           | Destroys a Volume.                                                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteBackupOffering``                    | Deletes a backup offering                                                      |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateSecurityGroup``                     | Updates a security group                                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``getRouterHealthCheckResults``             | Starts a router.                                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackups``                             | Lists VM backups                                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupProviders``                     | Lists Backup and Recovery providers                                            |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteKubernetesSupportedVersion``        | Deletes a Kubernetes cluster                                                   |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreBackup``                           | Restores an existing stopped or deleted VM using a VM backup                   |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addKubernetesSupportedVersion``           | Add a supported Kubernetes version                                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteKubernetesCluster``                 | Deletes a Kubernetes cluster                                                   |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``getKubernetesClusterConfig``              | Get Kubernetes cluster config                                                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateKubernetesSupportedVersion``        | Update a supported Kubernetes version                                          |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``upgradeKubernetesCluster``                | Upgrades a running Kubernetes cluster                                          |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteBackupSchedule``                    | Deletes the backup schedule of a VM                                            |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupProviderOfferings``             | Lists external backup offerings of the provider                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createKubernetesCluster``                 | Creates a Kubernetes cluster                                                   |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importBackupOffering``                    | Imports a backup offering using a backup provider                              |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``removeVirtualMachineFromBackupOffering``  | Removes a VM from any existing backup offering                                 |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesSupportedVersions``         | Lists container clusters                                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVolume``                           | Recovers a Destroy volume.                                                     |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listUnmanagedInstances``                  | Lists unmanaged virtual machines for a given cluster.                          |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importUnmanagedInstance``                 | Import unmanaged virtual machine from a given cluster.                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``getDiagnosticsData``                      | Get diagnostics and files from system VMs                                      |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startKubernetesCluster``                  | Starts a stopped Kubernetes cluster                                            |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupSchedule``                      | List backup schedule of a VM                                                   |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreVolumeFromBackupAndAttachToVM``    | Restore and attach a backed up volume to VM                                    |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateBackupSchedule``                    | Updates a user-defined VM backup schedule                                      |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteBackup``                            | Delete VM backup                                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVirtualMachineToBackupOffering``    | Assigns a VM to a backup offering                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+


Parameters Changed API Commands
-------------------------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``listHosts``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuloadaverage``                                                           |
|                                             | - ``ueficapability``                                                           |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``averageload``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importLdapUsers``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``conflictingusersource``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listHostsMetrics``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuloadaverage``                                                           |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateHost``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuloadaverage``                                                           |
|                                             | - ``ueficapability``                                                           |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``averageload``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopRouter``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``healthchecksfailed``                                                       |
|                                             | - ``healthcheckresults(*)``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForVirtualMachine``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startRouter``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``healthchecksfailed``                                                       |
|                                             | - ``healthcheckresults(*)``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumesMetrics``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``state`` (optional)                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVmNicIp``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startInternalLoadBalancerVM``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``healthchecksfailed``                                                       |
|                                             | - ``healthcheckresults(*)``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``searchLdap``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``conflictingusersource``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopNetScalerVpx``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``healthchecksfailed``                                                       |
|                                             | - ``healthcheckresults(*)``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listCapabilities``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``allowuserexpungerecovervolume``                                            |
|                                             | - ``kubernetesclusterexperimentalfeaturesenabled``                             |
|                                             | - ``kubernetesserviceenabled``                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listLdapUsers``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``userfilter`` (optional)                                                    |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``conflictingusersource``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootRouter``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``healthchecksfailed``                                                       |
|                                             | - ``healthcheckresults(*)``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNics``                                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``adaptertype``                                                              |
|                                             | - ``ipaddresses``                                                              |
|                                             | - ``isolatedpvlan``                                                            |
|                                             | - ``isolatedpvlantype``                                                        |
|                                             | - ``vlanid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addNicToVirtualMachine``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listExternalLoadBalancers``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuloadaverage``                                                           |
|                                             | - ``ueficapability``                                                           |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``averageload``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDefaultNicForVirtualMachine``       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopInternalLoadBalancerVM``              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``healthchecksfailed``                                                       |
|                                             | - ``healthcheckresults(*)``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createServiceOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cachemode`` (optional)                                                     |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cacheMode``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForRouter``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``healthchecksfailed``                                                       |
|                                             | - ``healthcheckresults(*)``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetPasswordForVirtualMachine``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``associateIpAddress``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ipaddress`` (optional)                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetSSHKeyForVirtualMachine``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listInternalLoadBalancerVMs``             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fetchhealthcheckresults`` (optional)                                       |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``healthchecksfailed``                                                       |
|                                             | - ``healthcheckresults(*)``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``detachIso``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareHostForMaintenance``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuloadaverage``                                                           |
|                                             | - ``ueficapability``                                                           |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``averageload``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachines``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``revertToVMSnapshot``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVirtualMachine``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``bootmode`` (optional)                                                      |
|                                             | - ``boottype`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostMaintenance``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuloadaverage``                                                           |
|                                             | - ``ueficapability``                                                           |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``averageload``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createDiskOffering``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cachemode`` (optional)                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumes``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``state`` (optional)                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetwork``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isolatedpvlantype`` (optional)                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachineWithVolume``         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addHost``                                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuloadaverage``                                                           |
|                                             | - ``ueficapability``                                                           |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``averageload``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVMAffinityGroup``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listRouters``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fetchhealthcheckresults`` (optional)                                       |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``healthchecksfailed``                                                       |
|                                             | - ``healthcheckresults(*)``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``attachIso``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyRouter``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``healthchecksfailed``                                                       |
|                                             | - ``healthcheckresults(*)``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``removeNicFromVirtualMachine``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``reconnectHost``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuloadaverage``                                                           |
|                                             | - ``ueficapability``                                                           |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``averageload``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createPrivateGateway``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``bypassvlanoverlapcheck`` (optional)                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addBaremetalHost``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuloadaverage``                                                           |
|                                             | - ``ueficapability``                                                           |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``averageload``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listServiceOfferings``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cacheMode``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startVirtualMachine``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopVirtualMachine``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``bootmode``                                                                 |
|                                             | - ``boottype``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateServiceOffering``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cacheMode``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
