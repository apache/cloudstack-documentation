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

API Changes Introduced in 4.16.0.0
===================================
For the complete list of API commands and params consult the `CloudStack Apidocs`_.

New API Commands
----------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``listResourceIcon``                        | Lists the resource icon for the specified resource(s)                          |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updatePodManagementNetworkIpRange``       | Updates a management network IP range. Only allowed when no IPs are allocated. |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteResourceIcon``                      | deletes the resource icon from the specified resource(s)                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateBackupOffering``                    | Updates a backup offering.                                                     |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateStorageCapabilities``               | Syncs capabilities of storage pools                                            |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``uploadResourceIcon``                      | Uploads an icon for the specified resource(s)                                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVlanIpRange``                       | Updates a VLAN IP range.                                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``declareHostAsDegraded``                   | Declare host as 'Degraded'. Host must be on 'Disconnected' or 'Alert' state.   |
|                                             | The ADMIN must be sure that there are no VMs running on the respective host    |
|                                             | otherwise this command might corrupted VMs that were running on the 'Degraded' |
|                                             | host.                                                                          |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateAnnotationVisibility``              | update an annotation visibility.                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostAsDegraded``                    | Cancel host status from 'Degraded'. Host will transit back to status           |
|                                             | 'Enabled'.                                                                     |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``syncStoragePool``                         | Sync storage pool with management server (currently supported for Datastore    |
|                                             | Cluster in VMware and syncs the datastores in it)                              |
+---------------------------------------------+--------------------------------------------------------------------------------+


Parameters Changed API Commands
-------------------------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``createVPCOffering``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``enable`` (optional)                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``ldapCreateAccount``                       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createPod``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ipranges(*)``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``copyIso``                                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachinesMetrics``              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootSystemVm``                          | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forced`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isdynamicallyscalable``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworks``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerSSHKeyPair``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``uploadVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsstoragesnapshot``                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroySystemVm``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isdynamicallyscalable``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listAnnotations``                         | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``annotationfilter`` (optional)                                              |
|                                             | - ``userid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``adminsonly``                                                               |
|                                             | - ``entityname``                                                               |
|                                             | - ``username``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleSystemVm``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isdynamicallyscalable``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVpnCustomerGateway``                | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ikeversion`` (optional)                                                    |
|                                             | - ``splitconnections`` (optional)                                              |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ikeversion``                                                               |
|                                             | - ``splitconnections``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``lockAccount``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjectRolePermissions``              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``projectid``                                                                |
|                                             | - ``projectroleid``                                                            |
|                                             | - ``projectrolename``                                                          |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``displaytext``                                                              |
|                                             | - ``success``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForVirtualMachine``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listTemplates``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootVirtualMachine``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forced`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopSystemVm``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isdynamicallyscalable``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVPC``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``network``                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``network(*)``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetworkOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``enable`` (optional)                                                        |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``supportedservices`` was 'required' and is now 'optional'                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVmNicIp``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listPods``                                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ipranges(*)``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetVpnConnection``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ikeversion``                                                               |
|                                             | - ``splitconnections``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesClusters``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``autoscalingenabled``                                                       |
|                                             | - ``controlnodes``                                                             |
|                                             | - ``maxsize``                                                                  |
|                                             | - ``minsize``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleKubernetesCluster``                  | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``autoscalingenabled`` (optional)                                            |
|                                             | - ``maxsize`` (optional)                                                       |
|                                             | - ``minsize`` (optional)                                                       |
|                                             | - ``nodeids`` (optional)                                                       |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``autoscalingenabled``                                                       |
|                                             | - ``controlnodes``                                                             |
|                                             | - ``maxsize``                                                                  |
|                                             | - ``minsize``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listCapabilities``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``defaultuipagesize``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVolume``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsstoragesnapshot``                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDomain``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``domaindetails``                                                            |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSystemVms``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isdynamicallyscalable``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createProject``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``account``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``detachVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsstoragesnapshot``                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``markDefaultZoneForAccount``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForSystemVm``                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isdynamicallyscalable``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootRouter``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forced`` (optional)                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addNicToVirtualMachine``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateIso``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDefaultNicForVirtualMachine``       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareTemplate``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createDomain``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``domaindetails``                                                            |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restartNetwork``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``displaytext``                                                              |
|                                             | - ``success``                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``account``                                                                  |
|                                             | - ``allocated``                                                                |
|                                             | - ``associatednetworkid``                                                      |
|                                             | - ``associatednetworkname``                                                    |
|                                             | - ``domain``                                                                   |
|                                             | - ``domainid``                                                                 |
|                                             | - ``fordisplay``                                                               |
|                                             | - ``forvirtualnetwork``                                                        |
|                                             | - ``ipaddress``                                                                |
|                                             | - ``isportable``                                                               |
|                                             | - ``issourcenat``                                                              |
|                                             | - ``isstaticnat``                                                              |
|                                             | - ``issystem``                                                                 |
|                                             | - ``networkid``                                                                |
|                                             | - ``networkname``                                                              |
|                                             | - ``physicalnetworkid``                                                        |
|                                             | - ``project``                                                                  |
|                                             | - ``projectid``                                                                |
|                                             | - ``purpose``                                                                  |
|                                             | - ``state``                                                                    |
|                                             | - ``virtualmachinedisplayname``                                                |
|                                             | - ``virtualmachineid``                                                         |
|                                             | - ``virtualmachinename``                                                       |
|                                             | - ``vlanid``                                                                   |
|                                             | - ``vlanname``                                                                 |
|                                             | - ``vmipaddress``                                                              |
|                                             | - ``vpcid``                                                                    |
|                                             | - ``vpcname``                                                                  |
|                                             | - ``zoneid``                                                                   |
|                                             | - ``zonename``                                                                 |
|                                             | - ``tags(*)``                                                                  |
|                                             | - ``jobid``                                                                    |
|                                             | - ``jobstatus``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createServiceOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``dynamicscalingenabled`` (optional)                                         |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``dynamicscalingenabled``                                                    |
|                                             | - ``storagetags``                                                              |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``tags``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``copyTemplate``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNiciraNvpDeviceNetworks``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resizeVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsstoragesnapshot``                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateTemplate``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVpnConnection``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ikeversion``                                                               |
|                                             | - ``splitconnections``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listPaloAltoFirewallNetworks``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVolume``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``name`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsstoragesnapshot``                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateAccount``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listDomains``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``domaindetails``                                                            |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``disableAccount``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetwork``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachine``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``autoselect`` (optional)                                                    |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createTemplate``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetPasswordForVirtualMachine``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVpnCustomerGateways``                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ikeversion``                                                               |
|                                             | - ``splitconnections``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetSSHKeyForVirtualMachine``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addKubernetesSupportedVersion``           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsautoscaling``                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVPC``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``network``                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``network(*)``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSrxFirewallNetworks``                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateKubernetesSupportedVersion``        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsautoscaling``                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``detachIso``                               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forced`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachines``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid`` (optional)                                                     |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``upgradeKubernetesCluster``                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``autoscalingenabled``                                                       |
|                                             | - ``controlnodes``                                                             |
|                                             | - ``maxsize``                                                                  |
|                                             | - ``minsize``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjects``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``account``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createAccount``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``revertToVMSnapshot``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addAnnotation``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``adminsonly`` (optional)                                                    |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``adminsonly``                                                               |
|                                             | - ``entityname``                                                               |
|                                             | - ``username``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerIso``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVirtualMachine``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``dynamicscalingenabled`` (optional)                                         |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateZone``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjectAccounts``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``account``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createDiskOffering``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumes``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsstoragesnapshot``                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``lockUser``                                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetwork``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``routerip`` (optional)                                                      |
|                                             | - ``routeripv6`` (optional)                                                    |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVPCs``                                | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``network``                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``network(*)``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachineWithVolume``         | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``hostid`` was 'required' and is now 'optional'                              |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateUser``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restartVPC``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``success``                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``account``                                                                  |
|                                             | - ``cidr``                                                                     |
|                                             | - ``created``                                                                  |
|                                             | - ``distributedvpcrouter``                                                     |
|                                             | - ``domain``                                                                   |
|                                             | - ``domainid``                                                                 |
|                                             | - ``fordisplay``                                                               |
|                                             | - ``name``                                                                     |
|                                             | - ``networkdomain``                                                            |
|                                             | - ``project``                                                                  |
|                                             | - ``projectid``                                                                |
|                                             | - ``redundantvpcrouter``                                                       |
|                                             | - ``regionlevelvpc``                                                           |
|                                             | - ``restartrequired``                                                          |
|                                             | - ``state``                                                                    |
|                                             | - ``vpcofferingid``                                                            |
|                                             | - ``vpcofferingname``                                                          |
|                                             | - ``zoneid``                                                                   |
|                                             | - ``zonename``                                                                 |
|                                             | - ``network(*)``                                                               |
|                                             | - ``service(*)``                                                               |
|                                             | - ``tags(*)``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``attachVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsstoragesnapshot``                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addHost``                                 | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``password`` was 'required' and is now 'optional'                            |
|                                             | - ``username`` was 'required' and is now 'optional'                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateProject``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``account``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listUsers``                               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVpnConnections``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ikeversion``                                                               |
|                                             | - ``splitconnections``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``disableUser``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listIsos``                                | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listZones``                               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetscalerLoadBalancerNetworks``       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startSystemVm``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isdynamicallyscalable``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createKubernetesCluster``                 | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``controlnodes`` (optional)                                                  |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``autoscalingenabled``                                                       |
|                                             | - ``controlnodes``                                                             |
|                                             | - ``maxsize``                                                                  |
|                                             | - ``minsize``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVolume``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsstoragesnapshot``                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVMAffinityGroup``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetApiLimit``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``displaytext``                                                              |
|                                             | - ``success``                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``account``                                                                  |
|                                             | - ``accountid``                                                                |
|                                             | - ``apiAllowed``                                                               |
|                                             | - ``apiIssued``                                                                |
|                                             | - ``expireAfter``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVPC``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``network``                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``network(*)``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``getUploadParamsForTemplate``              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis`` (optional)                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateSystemVm``                         | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``autoselect`` (optional)                                                    |
|                                             | - ``storageid`` (optional)                                                     |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``hostid`` was 'required' and is now 'optional'                              |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isdynamicallyscalable``                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listRouters``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``healthchecksfailed`` (optional)                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVpnConnection``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ikeversion``                                                               |
|                                             | - ``splitconnections``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBrocadeVcsDeviceNetworks``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesSupportedVersions``         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsautoscaling``                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listUsageRecords``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isrecursive`` (optional)                                                   |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``oscategoryid``                                                             |
|                                             | - ``oscategoryname``                                                           |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVolume``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsstoragesnapshot``                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableUser``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listZonesMetrics``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``suspendProject``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``account``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateNetwork``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listUnmanagedInstances``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``hostname``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerTemplate``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis`` (optional)                                                    |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createZone``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listDomainChildren``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``domaindetails``                                                            |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importUnmanagedInstance``                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listF5LoadBalancerNetworks``              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``supportsstoragesnapshot``                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVMSnapshot``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``virtualmachinename``                                                       |
|                                             | - ``zonename``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updatePod``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ipranges(*)``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``attachIso``                               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forced`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createUser``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVMSnapshot``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``virtualmachinename``                                                       |
|                                             | - ``zonename``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSSHKeyPairs``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listAccounts``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showicon`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``removeNicFromVirtualMachine``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``activateProject``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``account``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableAccount``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``created``                                                                  |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startKubernetesCluster``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``autoscalingenabled``                                                       |
|                                             | - ``controlnodes``                                                             |
|                                             | - ``maxsize``                                                                  |
|                                             | - ``minsize``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteProject``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cleanup`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``getUser``                                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVpnCustomerGateway``                | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ikeversion`` (optional)                                                    |
|                                             | - ``splitconnections`` (optional)                                              |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ikeversion``                                                               |
|                                             | - ``splitconnections``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createManagementNetworkIpRange``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ipranges(*)``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``removeAnnotation``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``adminsonly``                                                               |
|                                             | - ``entityname``                                                               |
|                                             | - ``username``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addBaremetalHost``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``password`` was 'required' and is now 'optional'                            |
|                                             | - ``username`` was 'required' and is now 'optional'                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listServiceOfferings``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``dynamicscalingenabled``                                                    |
|                                             | - ``storagetags``                                                              |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``tags``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVirtualMachineToBackupOffering``    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``displaytext``                                                              |
|                                             | - ``success``                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``account``                                                                  |
|                                             | - ``accountid``                                                                |
|                                             | - ``backupofferingid``                                                         |
|                                             | - ``backupofferingname``                                                       |
|                                             | - ``created``                                                                  |
|                                             | - ``domain``                                                                   |
|                                             | - ``domainid``                                                                 |
|                                             | - ``externalid``                                                               |
|                                             | - ``size``                                                                     |
|                                             | - ``status``                                                                   |
|                                             | - ``type``                                                                     |
|                                             | - ``virtualmachineid``                                                         |
|                                             | - ``virtualmachinename``                                                       |
|                                             | - ``virtualsize``                                                              |
|                                             | - ``volumes``                                                                  |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startVirtualMachine``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopVirtualMachine``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``icon``                                                                     |
|                                             | - ``lastupdated``                                                              |
|                                             | - ``pooltype``                                                                 |
|                                             | - ``readonlydetails``                                                          |
|                                             | - ``receivedbytes``                                                            |
|                                             | - ``sentbytes``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateServiceOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``hosttags`` (optional)                                                      |
|                                             | - ``storagetags`` (optional)                                                   |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``dynamicscalingenabled``                                                    |
|                                             | - ``storagetags``                                                              |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``tags``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+

