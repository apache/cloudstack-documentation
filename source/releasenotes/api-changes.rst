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

API Changes Introduced in 4.20.0.0
==================================
For the complete list of API commands and params consult the `CloudStack Apidocs`_.

New API Commands
----------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``changeBgpPeersForNetwork``                | Change the BGP peers for a network.                                            |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableRole``                              | Enables a role                                                                 |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateSharedFileSystem``                  | Update a Shared FileSystem                                                     |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateIpv4SubnetForZone``                 | Updates an existing IPv4 subnet for a zone.                                    |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listASNumbers``                           | List Autonomous Systems Numbers                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateRoutingFirewallRule``               | Updates Routing firewall rule with specified ID                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaListEmailConfiguration``             | List quota email template configurations                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteBackupRepository``                  | delete a backup repository                                                     |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeBgpPeersForVpc``                    | Change the BGP peers for a VPC.                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createSharedFileSystem``                  | Create a new Shared File System of specified size and disk offering, attached  |
|                                             | to the given network                                                           |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaPresetVariablesList``                | List the preset variables available for using in the Quota tariff activation   |
|                                             | rules given the usage type.                                                    |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addNsxController``                        | Add NSX Controller to CloudStack                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``purgeExpungedResources``                  | Purge expunged resources                                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteNsxController``                     | delete NSX Controller to CloudStack                                            |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listWebhooks``                            | Lists Webhooks                                                                 |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``executeWebhookDelivery``                  | Executes a Webhook delivery                                                    |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverSharedFileSystem``                 | Recover a Shared FileSystem by id                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listIpv4SubnetsForGuestNetwork``          | Lists IPv4 subnets for guest networks.                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``releaseIpv4SubnetForZone``                | Releases an existing dedicated IPv4 subnet for a zone.                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createIpv4SubnetForZone``                 | Creates a IPv4 subnet for a zone.                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworkProtocols``                    | Lists details of network protocols                                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createASNRange``                          | Creates a range of Autonomous Systems for BGP Dynamic Routing                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteBgpPeer``                           | Deletes an existing Bgp Peer.                                                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateBgpPeer``                           | Updates an existing Bgp Peer.                                                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteIpv4SubnetForGuestNetwork``         | Deletes an existing IPv4 subnet for guest network.                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createRoutingFirewallRule``               | Creates a routing firewall rule in the given network in ROUTED mode            |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``releaseASNumber``                         | Releases an AS Number back to the pool                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listWebhookDeliveries``                   | Lists Webhook deliveries                                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restartSharedFileSystem``                 | Restart a Shared FileSystem                                                    |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``forgotPassword``                          | Sends an email to the user with a token to reset the password using            |
|                                             | resetPassword command.                                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listASNRanges``                           | List Autonomous Systems Number Ranges                                          |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetPassword``                           | Resets the password for the user using the token generated via forgotPassword  |
|                                             | command.                                                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``disableRole``                             | Disables a role                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBackupRepositories``                  | Lists all backup repositories                                                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createBgpPeer``                           | Creates a Bgp Peer for a zone.                                                 |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``dedicateBgpPeer``                         | Dedicates an existing Bgp Peer to an account or a domain.                      |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createIpv4SubnetForGuestNetwork``         | Creates a IPv4 subnet for guest networks.                                      |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroySharedFileSystem``                 | Destroy a Shared FileSystem by id                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteASNRange``                          | deletes a range of Autonomous Systems for BGP Dynamic Routing                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listRoutingFirewallRules``                | Lists all Routing firewall rules                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listIpv4SubnetsForZone``                  | Lists IPv4 subnets for zone.                                                   |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startSharedFileSystem``                   | Start a Shared FileSystem                                                      |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addBackupRepository``                     | Adds a backup repository to store NAS backups                                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopSharedFileSystem``                    | Stop a Shared FileSystem                                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteRoutingFirewallRule``               | Deletes a routing firewall rule                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBgpPeers``                            | Lists Bgp Peers.                                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNsxControllers``                      | list all NSX controllers added to CloudStack                                   |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``releaseBgpPeer``                          | Releases an existing dedicated Bgp Peer.                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteIpv4SubnetForZone``                 | Deletes an existing IPv4 subnet for a zone.                                    |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteWebhookDelivery``                   | Deletes Webhook delivery                                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeSharedFileSystemServiceOffering``   | Change Service offering of a Shared FileSystem                                 |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaConfigureEmail``                     | Configure a quota email template                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``dedicateIpv4SubnetForZone``               | Dedicates an existing IPv4 subnet for a zone to an account or a domain.        |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSharedFileSystems``                   | List Shared FileSystems                                                        |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteWebhook``                           | Deletes a Webhook                                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateWebhook``                           | Updates a Webhook                                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeSharedFileSystemDiskOffering``      | Change Disk offering of a Shared FileSystem                                    |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``expungeSharedFileSystem``                 | Expunge a Shared FileSystem by id                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createWebhook``                           | Creates a Webhook                                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``extractSnapshot``                         | Returns a download URL for extracting a snapshot. It must be in the Backed Up  |
|                                             | state.                                                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSharedFileSystemProviders``           | Lists all available shared filesystem providers.                               |
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
|                                             | - ``fornsx`` (optional)                                                        |
|                                             | - ``networkmode`` (optional)                                                   |
|                                             | - ``nsxsupportlb`` (optional)                                                  |
|                                             | - ``routingmode`` (optional)                                                   |
|                                             | - ``specifyasnumber`` (optional)                                               |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``supportedservices`` was 'required' and is now 'optional'                   |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx``                                                                   |
|                                             | - ``networkmode``                                                              |
|                                             | - ``routingmode``                                                              |
|                                             | - ``specifyasnumber``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``ldapCreateAccount``                       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``copyIso``                                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateResourceLimit``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tag`` (optional)                                                           |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tag``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateHost``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             | - ``explicithosttags``                                                         |
|                                             | - ``implicithosttags``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listClusters``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listStoragePoolObjects``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``snapshotname``                                                             |
|                                             | - ``templatename``                                                             |
|                                             | - ``volumename``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVPC``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVmNicIp``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDiskOffering``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``suitableforvirtualmachine``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaTariffUpdate``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``position`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``position``                                                                 |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``uuid``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listCapabilities``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``allowuserforcestopvm``                                                     |
|                                             | - ``sharedfsvmmincpucount``                                                    |
|                                             | - ``sharedfsvmminramsize``                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``checkVolume``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDomain``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``detachVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``findHostsForMigration``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``explicithosttags``                                                         |
|                                             | - ``implicithosttags``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addNicToVirtualMachine``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listPublicIpAddresses``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forsystemvms`` (optional)                                                  |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forsystemvms``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDefaultNicForVirtualMachine``       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``copyTemplate``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNiciraNvpDeviceNetworks``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resizeVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeOfferingForVolume``                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetwork``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listUsageTypes``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``name``                                                                     |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``usagetypeid``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetPasswordForVirtualMachine``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVPC``                               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber`` (optional)                                                      |
|                                             | - ``bgppeerids`` (optional)                                                    |
|                                             | - ``cidrsize`` (optional)                                                      |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``cidr`` was 'required' and is now 'optional'                                |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``detachIso``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareHostForMaintenance``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             | - ``explicithosttags``                                                         |
|                                             | - ``implicithosttags``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachines``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listDiskOfferings``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``virtualmachineid`` (optional)                                              |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``suitableforvirtualmachine``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjects``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createAccount``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``revertToVMSnapshot``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerIso``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostMaintenance``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             | - ``explicithosttags``                                                         |
|                                             | - ``implicithosttags``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateZone``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnrange``                                                                 |
|                                             | - ``ismultiarch``                                                              |
|                                             | - ``isnsxenabled``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVlanIpRanges``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listProjectAccounts``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createDiskOffering``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``suitableforvirtualmachine``                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachineWithVolume``         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``attachVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addHost``                                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             | - ``explicithosttags``                                                         |
|                                             | - ``implicithosttags``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateProject``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listZones``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnrange``                                                                 |
|                                             | - ``ismultiarch``                                                              |
|                                             | - ``isnsxenabled``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetscalerLoadBalancerNetworks``       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVolume``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVPC``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``dedicatePublicIpRange``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostAsDegraded``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             | - ``explicithosttags``                                                         |
|                                             | - ``implicithosttags``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBrocadeVcsDeviceNetworks``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importRole``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``state``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaTariffCreate``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``position`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``position``                                                                 |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``uuid``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``suspendProject``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createZone``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnrange``                                                                 |
|                                             | - ``ismultiarch``                                                              |
|                                             | - ``isnsxenabled``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listDomainChildren``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importUnmanagedInstance``                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``attachIso``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``generateUsageRecords``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``enddate`` was 'required' and is now 'optional'                             |
|                                             | - ``startdate`` was 'required' and is now 'optional'                           |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listAccounts``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tag`` (optional)                                                           |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``activateProject``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteVnfTemplate``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``issystem`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addBaremetalHost``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             | - ``explicithosttags``                                                         |
|                                             | - ``implicithosttags``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVirtualMachine``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startVirtualMachine``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listHosts``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             | - ``explicithosttags``                                                         |
|                                             | - ``implicithosttags``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``moveDomain``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworks``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listAffinityGroups``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``dedicatedresources``                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``reserveIpAddress``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forsystemvms``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVPCOfferings``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx``                                                                   |
|                                             | - ``networkmode``                                                              |
|                                             | - ``routingmode``                                                              |
|                                             | - ``specifyasnumber``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``uploadVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``lockAccount``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForVirtualMachine``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listTemplates``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createAffinityGroup``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``dedicatedresources``                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVnfTemplates``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVnfAppliance``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetworkOffering``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx``                                                                   |
|                                             | - ``networkmode``                                                              |
|                                             | - ``routingmode``                                                              |
|                                             | - ``specifyasnumber``                                                          |
|                                             | - ``supportsinternallb``                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetworkOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx`` (optional)                                                        |
|                                             | - ``networkmode`` (optional)                                                   |
|                                             | - ``nsxsupportlb`` (optional)                                                  |
|                                             | - ``nsxsupportsinternallb`` (optional)                                         |
|                                             | - ``routingmode`` (optional)                                                   |
|                                             | - ``specifyasnumber`` (optional)                                               |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx``                                                                   |
|                                             | - ``networkmode``                                                              |
|                                             | - ``routingmode``                                                              |
|                                             | - ``specifyasnumber``                                                          |
|                                             | - ``supportsinternallb``                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaTariffList``                         | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id`` (optional)                                                            |
|                                             | - ``listonlyremoved`` (optional)                                               |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``position``                                                                 |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``uuid``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVolume``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createProject``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``markDefaultZoneForAccount``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listImageStoreObjects``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``snapshotname``                                                             |
|                                             | - ``templatename``                                                             |
|                                             | - ``volumename``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateIso``                               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareTemplate``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createDomain``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createServiceOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``purgeresources`` (optional)                                                |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``purgeresources``                                                           |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateTemplate``                          | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             | - ``templatetag`` (optional)                                                   |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVlanIpRange``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx`` (optional)                                                        |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listPaloAltoFirewallNetworks``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVolume``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection`` (optional)                                              |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVirtualMachine``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection`` (optional)                                              |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateAccount``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``disableAccount``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listDomains``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tag`` (optional)                                                           |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetUserDataForVirtualMachine``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteTemplate``                          | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``issystem`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createTemplate``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``associateIpAddress``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forsystemvms``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resetSSHKeyForVirtualMachine``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addKubernetesSupportedVersion``           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``linkUserDataToTemplate``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createRole``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``state``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateCluster``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listHostTags``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``isimplicit``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVirtualMachine``                    | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumes``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetwork``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber`` (optional)                                                      |
|                                             | - ``bgppeerids`` (optional)                                                    |
|                                             | - ``cidrsize`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworkOfferings``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``routingmode`` (optional)                                                   |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx``                                                                   |
|                                             | - ``networkmode``                                                              |
|                                             | - ``routingmode``                                                              |
|                                             | - ``specifyasnumber``                                                          |
|                                             | - ``supportsinternallb``                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVPCs``                                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVlanIpRange``                       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listResourceLimits``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tag`` (optional)                                                           |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tag``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listIsos``                                | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateRole``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``state``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerVnfTemplate``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``declareHostAsDegraded``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             | - ``explicithosttags``                                                         |
|                                             | - ``implicithosttags``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVMAffinityGroup``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``getUploadParamsForTemplate``              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateResourceCount``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tag`` (optional)                                                           |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tag``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listRoles``                               | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``state`` (optional)                                                         |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``state``                                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVolume``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateIpAddress``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forsystemvms``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateNetwork``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asnumber``                                                                 |
|                                             | - ``asnumberid``                                                               |
|                                             | - ``bgppeers``                                                                 |
|                                             | - ``ip4routes``                                                                |
|                                             | - ``ip4routing``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerTemplate``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVnfAppliances``                       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``removeSecondaryStorageSelector``          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``displaytext``                                                              |
|                                             | - ``success``                                                                  |
|                                             |                                                                                |
|                                             | *Removed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``id``                                                                       |
|                                             | - ``created``                                                                  |
|                                             | - ``description``                                                              |
|                                             | - ``heuristicrule``                                                            |
|                                             | - ``name``                                                                     |
|                                             | - ``removed``                                                                  |
|                                             | - ``type``                                                                     |
|                                             | - ``zoneid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addCluster``                              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``removeNicFromVirtualMachine``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableAccount``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``taggedresources``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``reconnectHost``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             | - ``explicithosttags``                                                         |
|                                             | - ``implicithosttags``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVnfTemplate``                       | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch`` (optional)                                                          |
|                                             | - ``templatetag`` (optional)                                                   |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``arch``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVPCOffering``                       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``fornsx``                                                                   |
|                                             | - ``networkmode``                                                              |
|                                             | - ``routingmode``                                                              |
|                                             | - ``specifyasnumber``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listServiceOfferings``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``templateid`` (optional)                                                    |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``purgeresources``                                                           |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``importVm``                                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listCapacity``                            | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tag`` (optional)                                                           |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tag``                                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopVirtualMachine``                      | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``deleteprotection``                                                         |
|                                             | - ``vmtype``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateServiceOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``purgeresources`` (optional)                                                |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``purgeresources``                                                           |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+


