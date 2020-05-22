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

API Changes Introduced in 4.13.0.0
===================================
For the complete list of API commands and params consult the `CloudStack Apidocs`_.


New API Commands
----------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``listTemplateOvfProperties``               | List template OVF properties if available.                                     |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listDetailOptions``                       | Lists all possible details and their options for a resource type such as a VM  |
|                                             | or a template                                                                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``revokeTemplateDirectDownloadCertificate`` | Revoke a certificate alias from a KVM host                                     |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``getUploadParamsForIso``                   | upload an existing ISO into the CloudStack cloud.                              |
+---------------------------------------------+--------------------------------------------------------------------------------+


Removed API Commands
--------------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``listNuageVspDomainTemplates``             | Lists Nuage VSP domain templates                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNuageUnderlayVlanIpRanges``           | enable Nuage underlay on vlan ip range                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``disableNuageUnderlayVlanIpRange``         | disable Nuage underlay on vlan ip range                                        |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addNuageVspDevice``                       | Adds a Nuage VSP device                                                        |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteNuageVspDevice``                    | delete a nuage vsp device                                                      |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableNuageUnderlayVlanIpRange``          | enable Nuage underlay on vlan ip range                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNuageVspDevices``                     | Lists Nuage VSP devices                                                        |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNuageVspGlobalDomainTemplate``        | Lists Nuage VSP domain templates                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``associateNuageVspDomainTemplate``         | associate a vpc with a domain template                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNuageVspDevice``                    | Update a Nuage VSP device                                                      |
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
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``zoneid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domain``                                                                   |
|                                             | - ``domainid``                                                                 |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``ldapCreateAccount``                       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainpath``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworks``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVPCOfferings``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zoneid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domain``                                                                   |
|                                             | - ``domainid``                                                                 |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``uploadVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``diskioread``                                                               |
|                                             | - ``diskiowrite``                                                              |
|                                             | - ``diskkbsread``                                                              |
|                                             | - ``diskkbswrite``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``lockAccount``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainpath``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForVirtualMachine``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetworkOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``zoneid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domain``                                                                   |
|                                             | - ``domainid``                                                                 |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetworkOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``zoneid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domain``                                                                   |
|                                             | - ``domainid``                                                                 |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumesMetrics``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``diskiopstotal``                                                            |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVmNicIp``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDiskOffering``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``zoneid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSnapshots``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``tags(*)``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listCapabilities``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``allowuserviewalldomainaccounts``                                           |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshotPolicy``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tags`` (optional)                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``detachVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``diskioread``                                                               |
|                                             | - ``diskiowrite``                                                              |
|                                             | - ``diskkbsread``                                                              |
|                                             | - ``diskkbswrite``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``markDefaultZoneForAccount``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainpath``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshot``                          | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tags`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``tags(*)``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshotFromVMSnapshot``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``tags(*)``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addNicToVirtualMachine``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listPublicIpAddresses``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``networkid`` (optional)                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDefaultNicForVirtualMachine``       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createServiceOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``customized`` (optional)                                                    |
|                                             | - ``maxcpunumber`` (optional)                                                  |
|                                             | - ``maxmemory`` (optional)                                                     |
|                                             | - ``mincpunumber`` (optional)                                                  |
|                                             | - ``minmemory`` (optional)                                                     |
|                                             | - ``zoneid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNiciraNvpDeviceNetworks``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resizeVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``diskioread``                                                               |
|                                             | - ``diskiowrite``                                                              |
|                                             | - ``diskkbsread``                                                              |
|                                             | - ``diskkbswrite``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listPaloAltoFirewallNetworks``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``diskioread``                                                               |
|                                             | - ``diskiowrite``                                                              |
|                                             | - ``diskkbsread``                                                              |
|                                             | - ``diskkbswrite``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateAccount``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainpath``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``disableAccount``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainpath``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetwork``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``hideipaddressusage`` (optional)                                            |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``archiveSnapshot``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``tags(*)``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetPasswordForVirtualMachine``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetSSHKeyForVirtualMachine``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSrxFirewallNetworks``                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``detachIso``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachines``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listDiskOfferings``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zoneid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjects``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createAccount``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainpath``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``revertToVMSnapshot``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVirtualMachine``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid`` (optional)                                                     |
|                                             | - ``copyimagetags`` (optional)                                                 |
|                                             | - ``ovfproperties`` (optional)                                                 |
|                                             | - ``podid`` (optional)                                                         |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateZone``                              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``sortkey`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createDiskOffering``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zoneid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumes``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``diskioread``                                                               |
|                                             | - ``diskiowrite``                                                              |
|                                             | - ``diskkbsread``                                                              |
|                                             | - ``diskkbswrite``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetwork``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``hideipaddressusage`` (optional)                                            |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworkOfferings``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domain``                                                                   |
|                                             | - ``domainid``                                                                 |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachineWithVolume``         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``attachVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``diskioread``                                                               |
|                                             | - ``diskiowrite``                                                              |
|                                             | - ``diskkbsread``                                                              |
|                                             | - ``diskkbswrite``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetscalerLoadBalancerNetworks``       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVolume``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``diskioread``                                                               |
|                                             | - ``diskiowrite``                                                              |
|                                             | - ``diskkbsread``                                                              |
|                                             | - ``diskkbswrite``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVMAffinityGroup``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``revertSnapshot``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``tags(*)``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBrocadeVcsDeviceNetworks``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listUsageRecords``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``oldformat`` (optional)                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateNetwork``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``uploadTemplateDirectDownloadCertificate`` | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zoneid`` (required)                                                        |
|                                             | - ``hostid`` (optional)                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``diskioread``                                                               |
|                                             | - ``diskiowrite``                                                              |
|                                             | - ``diskkbsread``                                                              |
|                                             | - ``diskkbswrite``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listF5LoadBalancerNetworks``              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details``                                                                  |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``attachIso``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listAccounts``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details`` (optional)                                                       |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainpath``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``removeNicFromVirtualMachine``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableAccount``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainpath``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVPCOffering``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``sortkey`` (optional)                                                       |
|                                             | - ``zoneid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domain``                                                                   |
|                                             | - ``domainid``                                                                 |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listServiceOfferings``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zoneid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startVirtualMachine``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid`` (optional)                                                     |
|                                             | - ``podid`` (optional)                                                         |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopVirtualMachine``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``readonlyuidetails``                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateServiceOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``zoneid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zone``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+


