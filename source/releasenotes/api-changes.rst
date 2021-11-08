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


Removed API Commands
--------------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``configureSimulator``                      | configure simulator                                                            |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``querySimulatorMock``                      | query simulator mock                                                           |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``cleanupSimulatorMock``                    | cleanup simulator mock                                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``configureSimulatorHAProviderState``       | configures simulator HA provider state for a host for probing and testing      |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSimulatorHAStateTransitions``         | list recent simulator HA state transitions for a host for probing and testing  |
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

API Changes Introduced in 4.15.0.0
===================================
For the complete list of API commands and params consult the `CloudStack Apidocs`_.

New API Commands
----------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``listVsphereStoragePolicyCompatiblePools`` | List storage pools compatible with a vSphere storage policy                    |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjectRolePermissions``              | Lists a project's project role permissions                                     |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importVsphereStoragePolicies``            | Import vSphere storage policies                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateSecondaryStorageData``             | migrates data objects from one secondary storage to destination image store(s) |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``unmanageVirtualMachine``                  | Unmanage a guest virtual machine.                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateImageStore``                        | Updates image store read-only status                                           |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteProjectRole``                       | Delete Project roles in CloudStack                                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteUserFromProject``                   | Deletes user from the project                                                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjectRoles``                        | Lists Project roles in CloudStack                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createProjectRole``                       | Creates a Project role                                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateProjectRole``                       | Creates a Project role                                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVsphereStoragePolicies``              | List vSphere storage policies                                                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createProjectRolePermission``             | Adds API permissions to a project role                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateProjectRolePermission``             | Updates a project role permission and/or order                                 |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addUserToProject``                        | Adds user to a project                                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importRole``                              | Imports a role based on provided map of rule permissions                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteProjectRolePermission``             | Deletes a project role permission in the project                               |
+---------------------------------------------+--------------------------------------------------------------------------------+


Removed API Commands
--------------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``listTemplateOvfProperties``               | List template OVF properties if available.                                     |
+---------------------------------------------+--------------------------------------------------------------------------------+


Parameters Changed API Commands
-------------------------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``copyIso``                                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis``                                                               |
|                                             | - ``deployasisdetails``                                                        |
|                                             | - ``downloaddetails``                                                          |
|                                             | - ``url``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachinesMetrics``              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``haenable`` (optional)                                                      |
|                                             | - ``securitygroupid`` (optional)                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listHosts``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuallocatedpercentage``                                                   |
|                                             | - ``cpuallocatedvalue``                                                        |
|                                             | - ``cpuallocatedwithoverprovisioning``                                         |
|                                             | - ``memoryallocatedbytes``                                                     |
|                                             | - ``memoryallocatedpercentage``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateStoragePool``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``name`` (optional)                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootSystemVm``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworks``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``networkofferingid`` (optional)                                             |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateHost``                              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``name`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuallocatedpercentage``                                                   |
|                                             | - ``cpuallocatedvalue``                                                        |
|                                             | - ``cpuallocatedwithoverprovisioning``                                         |
|                                             | - ``memoryallocatedbytes``                                                     |
|                                             | - ``memoryallocatedpercentage``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroySystemVm``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addSwift``                                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``disksizetotal``                                                            |
|                                             | - ``disksizeused``                                                             |
|                                             | - ``readonly``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleSystemVm``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopRouter``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjectInvitations``                  | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``userid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``userid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listLdapConfigurations``                  | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``listall`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSecondaryStagingStores``              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``disksizetotal``                                                            |
|                                             | - ``disksizeused``                                                             |
|                                             | - ``readonly``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startRouter``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForVirtualMachine``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listTemplates``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details`` (optional)                                                       |
|                                             | - ``showunique`` (optional)                                                    |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis``                                                               |
|                                             | - ``deployasisdetails``                                                        |
|                                             | - ``downloaddetails``                                                          |
|                                             | - ``url``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listPhysicalNetworks``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zonename``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createSecondaryStagingStore``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``disksizetotal``                                                            |
|                                             | - ``disksizeused``                                                             |
|                                             | - ``readonly``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootVirtualMachine``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``bootintosetup`` (optional)                                                 |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVPC``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``vpcofferingname``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopSystemVm``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listPrivateGateways``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVmNicIp``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startInternalLoadBalancerVM``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDiskOffering``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``bytesreadrate`` (optional)                                                 |
|                                             | - ``bytesreadratemax`` (optional)                                              |
|                                             | - ``bytesreadratemaxlength`` (optional)                                        |
|                                             | - ``byteswriterate`` (optional)                                                |
|                                             | - ``byteswriteratemax`` (optional)                                             |
|                                             | - ``byteswriteratemaxlength`` (optional)                                       |
|                                             | - ``cachemode`` (optional)                                                     |
|                                             | - ``iopsreadrate`` (optional)                                                  |
|                                             | - ``iopsreadratemax`` (optional)                                               |
|                                             | - ``iopsreadratemaxlength`` (optional)                                         |
|                                             | - ``iopswriterate`` (optional)                                                 |
|                                             | - ``iopswriteratemax`` (optional)                                              |
|                                             | - ``iopswriteratemaxlength`` (optional)                                        |
|                                             | - ``tags`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``vspherestoragepolicy``                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addAccountToProject``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``projectroleid`` (optional)                                                 |
|                                             | - ``roletype`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesClusters``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ipaddress``                                                                |
|                                             | - ``ipaddressid``                                                              |
|                                             | - ``virtualmachines``                                                          |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``virtualmachineids``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleKubernetesCluster``                  | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``id`` was 'optional' and is now 'required'                                  |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ipaddress``                                                                |
|                                             | - ``ipaddressid``                                                              |
|                                             | - ``virtualmachines``                                                          |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``virtualmachineids``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopNetScalerVpx``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updatePhysicalNetwork``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zonename``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createRolePermission``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``description``                                                              |
|                                             | - ``permission``                                                               |
|                                             | - ``rule``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSystemVms``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createProject``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``accountid`` (optional)                                                     |
|                                             | - ``userid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``owner``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForSystemVm``                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootRouter``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``findHostsForMigration``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuallocatedpercentage``                                                   |
|                                             | - ``cpuallocatedvalue``                                                        |
|                                             | - ``cpuallocatedwithoverprovisioning``                                         |
|                                             | - ``memoryallocatedbytes``                                                     |
|                                             | - ``memoryallocatedpercentage``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addNicToVirtualMachine``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listStaticRoutes``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``state`` (optional)                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listPublicIpAddresses``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``networkname``                                                              |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateIso``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis``                                                               |
|                                             | - ``deployasisdetails``                                                        |
|                                             | - ``downloaddetails``                                                          |
|                                             | - ``url``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listExternalLoadBalancers``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuallocatedpercentage``                                                   |
|                                             | - ``cpuallocatedvalue``                                                        |
|                                             | - ``cpuallocatedwithoverprovisioning``                                         |
|                                             | - ``memoryallocatedbytes``                                                     |
|                                             | - ``memoryallocatedpercentage``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDefaultNicForVirtualMachine``       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareTemplate``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis``                                                               |
|                                             | - ``deployasisdetails``                                                        |
|                                             | - ``downloaddetails``                                                          |
|                                             | - ``url``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopInternalLoadBalancerVM``              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restartNetwork``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``networkname``                                                              |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addImageStore``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``disksizetotal``                                                            |
|                                             | - ``disksizeused``                                                             |
|                                             | - ``readonly``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listRolePermissions``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``description``                                                              |
|                                             | - ``permission``                                                               |
|                                             | - ``rule``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworkACLs``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``copyTemplate``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis``                                                               |
|                                             | - ``deployasisdetails``                                                        |
|                                             | - ``downloaddetails``                                                          |
|                                             | - ``url``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createServiceOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``rootdisksize`` (optional)                                                  |
|                                             | - ``storagepolicy`` (optional)                                                 |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``rootdisksize``                                                             |
|                                             | - ``vspherestoragepolicy``                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNiciraNvpDeviceNetworks``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateTemplate``                          | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``templatetype`` (optional)                                                  |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis``                                                               |
|                                             | - ``deployasisdetails``                                                        |
|                                             | - ``downloaddetails``                                                          |
|                                             | - ``url``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listPaloAltoFirewallNetworks``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForRouter``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addSecondaryStorage``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``disksizetotal``                                                            |
|                                             | - ``disksizeused``                                                             |
|                                             | - ``readonly``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetwork``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVpnGateway``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createTemplate``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis``                                                               |
|                                             | - ``deployasisdetails``                                                        |
|                                             | - ``downloaddetails``                                                          |
|                                             | - ``url``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetPasswordForVirtualMachine``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``associateIpAddress``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``networkname``                                                              |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetworkACL``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetSSHKeyForVirtualMachine``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVPC``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``vpcofferingname``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listInternalLoadBalancerVMs``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSrxFirewallNetworks``                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``detachIso``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createRole``                              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``roleid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``type`` was 'required' and is now 'optional'                                |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isdefault``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``description``                                                              |
|                                             | - ``name``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareHostForMaintenance``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuallocatedpercentage``                                                   |
|                                             | - ``cpuallocatedvalue``                                                        |
|                                             | - ``cpuallocatedwithoverprovisioning``                                         |
|                                             | - ``memoryallocatedbytes``                                                     |
|                                             | - ``memoryallocatedpercentage``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachines``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``haenable`` (optional)                                                      |
|                                             | - ``securitygroupid`` (optional)                                               |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listDiskOfferings``                       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``vspherestoragepolicy``                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``upgradeKubernetesCluster``                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ipaddress``                                                                |
|                                             | - ``ipaddressid``                                                              |
|                                             | - ``virtualmachines``                                                          |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``virtualmachineids``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjects``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``username`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``owner``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``revertToVMSnapshot``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerIso``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis``                                                               |
|                                             | - ``deployasisdetails``                                                        |
|                                             | - ``downloaddetails``                                                          |
|                                             | - ``url``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVirtualMachine``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``bootintosetup`` (optional)                                                 |
|                                             | - ``nicnetworklist`` (optional)                                                |
|                                             | - ``properties`` (optional)                                                    |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``ovfproperties``                                                            |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostMaintenance``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuallocatedpercentage``                                                   |
|                                             | - ``cpuallocatedvalue``                                                        |
|                                             | - ``cpuallocatedwithoverprovisioning``                                         |
|                                             | - ``memoryallocatedbytes``                                                     |
|                                             | - ``memoryallocatedpercentage``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjectAccounts``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``projectroleid`` (optional)                                                 |
|                                             | - ``userid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``owner``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createDiskOffering``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``storagepolicy`` (optional)                                                 |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``vspherestoragepolicy``                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetwork``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVPCs``                                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``vpcofferingname``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachineWithVolume``         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restartVPC``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``vpcofferingname``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addHost``                                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuallocatedpercentage``                                                   |
|                                             | - ``cpuallocatedvalue``                                                        |
|                                             | - ``cpuallocatedwithoverprovisioning``                                         |
|                                             | - ``memoryallocatedbytes``                                                     |
|                                             | - ``memoryallocatedpercentage``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateProject``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``roletype`` (optional)                                                      |
|                                             | - ``swapowner`` (optional)                                                     |
|                                             | - ``userid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``owner``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listIsos``                                | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``showunique`` (optional)                                                    |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis``                                                               |
|                                             | - ``deployasisdetails``                                                        |
|                                             | - ``downloaddetails``                                                          |
|                                             | - ``url``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateCloudToUseObjectStore``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``disksizetotal``                                                            |
|                                             | - ``disksizeused``                                                             |
|                                             | - ``readonly``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateRole``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isdefault``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``description``                                                              |
|                                             | - ``name``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetscalerLoadBalancerNetworks``       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startSystemVm``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createKubernetesCluster``                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ipaddress``                                                                |
|                                             | - ``ipaddressid``                                                              |
|                                             | - ``virtualmachines``                                                          |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``virtualmachineids``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVMAffinityGroup``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVPC``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``vpcofferingname``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``getUploadParamsForTemplate``              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``ostypeid`` was 'required' and is now 'optional'                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateProjectInvitation``                 | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``userid`` (optional)                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateSystemVm``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVpnGateways``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listRoles``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isdefault``                                                                |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``description``                                                              |
|                                             | - ``name``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetworkACLItem``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listRouters``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBrocadeVcsDeviceNetworks``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSwifts``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``disksizetotal``                                                            |
|                                             | - ``disksizeused``                                                             |
|                                             | - ``readonly``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listUsageRecords``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ostypeid``                                                                 |
|                                             | - ``vpcid``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``suspendProject``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``owner``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateIpAddress``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``networkname``                                                              |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateNetwork``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerTemplate``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``ostypeid`` was 'required' and is now 'optional'                            |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deployasis``                                                               |
|                                             | - ``deployasisdetails``                                                        |
|                                             | - ``downloaddetails``                                                          |
|                                             | - ``url``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importUnmanagedInstance``                 | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forced`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addImageStoreS3``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``disksizetotal``                                                            |
|                                             | - ``disksizeused``                                                             |
|                                             | - ``readonly``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createPhysicalNetwork``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zonename``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listF5LoadBalancerNetworks``              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVMSnapshot``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``hypervisor``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``moveNetworkAclItem``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``attachIso``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVpnGateway``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVMSnapshot``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``hypervisor``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyRouter``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``podname``                                                                  |
|                                             | - ``templatename``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listImageStores``                         | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonly`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``disksizetotal``                                                            |
|                                             | - ``disksizeused``                                                             |
|                                             | - ``readonly``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``removeNicFromVirtualMachine``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``activateProject``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``owner``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``reconnectHost``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuallocatedpercentage``                                                   |
|                                             | - ``cpuallocatedvalue``                                                        |
|                                             | - ``cpuallocatedwithoverprovisioning``                                         |
|                                             | - ``memoryallocatedbytes``                                                     |
|                                             | - ``memoryallocatedpercentage``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startKubernetesCluster``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ipaddress``                                                                |
|                                             | - ``ipaddressid``                                                              |
|                                             | - ``virtualmachines``                                                          |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``virtualmachineids``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createPrivateGateway``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``aclname``                                                                  |
|                                             | - ``vpcname``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``uploadSslCert``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``enabledrevocationcheck`` (optional)                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addBaremetalHost``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpuallocatedpercentage``                                                   |
|                                             | - ``cpuallocatedvalue``                                                        |
|                                             | - ``cpuallocatedwithoverprovisioning``                                         |
|                                             | - ``memoryallocatedbytes``                                                     |
|                                             | - ``memoryallocatedpercentage``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listServiceOfferings``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``cpunumber`` (optional)                                                     |
|                                             | - ``cpuspeed`` (optional)                                                      |
|                                             | - ``memory`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``rootdisksize``                                                             |
|                                             | - ``vspherestoragepolicy``                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startVirtualMachine``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``bootintosetup`` (optional)                                                 |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateServiceOffering``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``rootdisksize``                                                             |
|                                             | - ``vspherestoragepolicy``                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopVirtualMachine``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``osdisplayname``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+

