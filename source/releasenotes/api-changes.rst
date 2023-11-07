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

API Changes in |release| since 4.18.0.0
===================================
For the complete list of API commands and params consult the `CloudStack Apidocs`_.

Parameters Changed in API Commands
-------------------------------

.. cssclass:: table-striped table-bordered table-hover

+------------------------------------------------------------+--------------------------------------------------------------------------------+
| Name                                                       | Description                                                                    |
+============================================================+================================================================================+
| ``listStoragePools``                                       | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``status`` (optional)                                                        |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startVirtualMachine``                                    | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``considerLastHost`` was available for Users but now only for ROOT admins    |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addGuestOs``                                             | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``display`` (optional)                                                       |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``details`` was 'required' and is now 'optional'                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateGuestOs``                                          | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``display`` (optional)                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listOsTypes``                                            | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``display`` (optional)                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createAutoScaleVmProfile``                               | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid`` (optional)                                                    |
|                                                            | - ``userdatadetails`` (optional)                                               |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            | - ``userdatadetails``                                                          |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateAutoScaleVmProfile``                               | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid`` (optional)                                                    |
|                                                            | - ``userdatadetails`` (optional)                                               |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            | - ``userdatadetails``                                                          |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listAutoScaleVmProfiles``                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            | - ``userdatadetails``                                                          |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+

API Changes Introduced in 4.18.0.0
===================================
For the complete list of API commands and params consult the `CloudStack Apidocs`_.

New API Commands
----------------

.. cssclass:: table-striped table-bordered table-hover

+------------------------------------------------------------+--------------------------------------------------------------------------------+
| Name                                                       | Description                                                                    |
+============================================================+================================================================================+
| ``listTungstenFabricTag``                                  | Lists Tungsten-Fabric tags                                                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricLBHealthMonitor``                      | list Tungsten-Fabric LB health monitor                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``getLoadBalancerSslCertificate``                          | get load balancer certificate                                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricApplicationPolicySet``                 | list Tungsten-Fabric application policy set                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listUserData``                                           | List registered userdatas                                                      |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``applyTungstenFabricTag``                                 | apply Tungsten-Fabric tag                                                      |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricFirewallPolicy``                     | create Tungsten-Fabric firewall policy                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricPolicy``                             | create Tungsten-Fabric policy                                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeTungstenFabricPolicyRule``                         | remove Tungsten-Fabric policy                                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricProvider``                           | Create Tungsten-Fabric provider in cloudstack                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricLogicalRouter``                        | list Tungsten-Fabric logical router                                            |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteTungstenFabricAddressGroup``                       | delete Tungsten-Fabric address group                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteTungstenFabricLogicalRouter``                      | delete Tungsten-Fabric logical router                                          |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricLogicalRouter``                      | create Tungsten-Fabric logical router                                          |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricFirewallRule``                       | create Tungsten-Fabric firewall                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricManagementNetwork``                  | create Tungsten-Fabric management Network                                      |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricFirewallRule``                         | list Tungsten-Fabric firewall rule                                             |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricAddressGroup``                         | list Tungsten-Fabric address group                                             |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricServiceGroup``                         | list Tungsten-Fabric service group                                             |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``isAccountAllowedToCreateOfferingsWithTags``              | Return true if the specified account is allowed to create offerings with tags. |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricTagType``                            | create Tungsten-Fabric tag type                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVolume``                                           | Changes ownership of a Volume from one account to another.                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteUserData``                                         | Deletes a userdata                                                             |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaTariffDelete``                                      | Marks a quota tariff as removed.                                               |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteTungstenFabricServiceGroup``                       | delete Tungsten-Fabric service group                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``validateUserTwoFactorAuthenticationCode``                | Checks the 2FA code for the User.                                              |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``synchronizeTungstenFabricData``                          | Synchronize Tungsten-Fabric data                                               |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteTungstenFabricPolicy``                             | delete Tungsten-Fabric policy                                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricPolicyRule``                           | list Tungsten-Fabric policy                                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``resetUserDataForVirtualMachine``                         | Resets the UserData for Instance. The Instance must be in a                    |
|                                                            | "Stopped" state. [async]                                                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricNetwork``                              | list Tungsten-Fabric Network                                                   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``setupUserTwoFactorAuthentication``                       | Setup the 2FA for the User.                                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``linkUserDataToTemplate``                                 | Link or unlink a userdata to a Template.                                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricProviders``                            | Lists Tungsten-Fabric providers                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteTungstenFabricTag``                                | delete Tungsten-Fabric tag                                                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricServiceGroup``                       | create Tungsten-Fabric service group                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteTungstenFabricApplicationPolicySet``               | delete Tungsten-Fabric application policy set                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeTungstenFabricPolicy``                             | remove Tungsten-Fabric policy                                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addTungstenFabricNetworkGatewayToLogicalRouter``         | add Tungsten-Fabric Network gateway to logical router                          |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricNic``                                  | list Tungsten-Fabric nic                                                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``applyTungstenFabricPolicy``                              | apply Tungsten-Fabric policy                                                   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricPublicNetwork``                      | create Tungsten-Fabric public Network                                          |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricFirewallPolicy``                       | list Tungsten-Fabric firewall policy                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricApplicationPolicySet``               | create Tungsten-Fabric application policy set                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricAddressGroup``                       | create Tungsten-Fabric address group                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumesUsageHistory``                                | Lists volume stats                                                             |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createConsoleEndpoint``                                  | Create a console endpoint to connect to an Instance console                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteTungstenFabricFirewallPolicy``                     | delete Tungsten-Fabric firewall policy                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateTungstenFabricLBHealthMonitor``                    | update Tungsten-Fabric loadbalancer health monitor                             |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateCondition``                                        | Updates a condition for Instance auto scaling                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeTungstenFabricTag``                                | remove Tungsten-Fabric tag                                                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricPolicy``                               | list Tungsten-Fabric policy                                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricVm``                                   | list Tungsten-Fabric Instance                                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addTungstenFabricPolicyRule``                            | add Tungsten-Fabric policy rule                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteTungstenFabricTagType``                            | delete Tungsten-Fabric tag type                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeTungstenFabricNetworkGatewayFromLogicalRouter``    | remove Tungsten-Fabric Network gateway from logical router                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaTariffCreate``                                      | Creates a quota tariff for a resource.                                         |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTungstenFabricTag``                                | create Tungsten-Fabric tag                                                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteTungstenFabricFirewallRule``                       | delete Tungsten-Fabric firewall rule                                           |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSystemVmsUsageHistory``                              | Lists System Instance stats                                                    |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerUserData``                                       | Register a new userdata.                                                       |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTungstenFabricTagType``                              | Lists Tungsten-Fabric tags                                                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``configTungstenFabricService``                            | config Tungsten-Fabric service                                                 |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listConfigurationGroups``                                | Lists all configuration groups (primarily used for UI).                        |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listUserTwoFactorAuthenticatorProviders``                | Lists User two factor authenticator providers                                  |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
'

Removed API Commands
--------------------

.. cssclass:: table-striped table-bordered table-hover

+------------------------------------------------------------+--------------------------------------------------------------------------------+
| Name                                                       | Description                                                                    |
+============================================================+================================================================================+
| ``addExternalFirewall``                                    | Adds an external firewall appliance                                            |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSrxFirewalls``                                       | lists SRX firewall devices in a physical Network                               |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteExternalFirewall``                                 | Deletes an external firewall appliance.                                        |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addSrxFirewall``                                         | Adds a SRX firewall device                                                     |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteSrxFirewall``                                      | delete a SRX firewall device                                                   |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listExternalFirewalls``                                  | List external firewall appliances.                                             |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSrxFirewallNetworks``                                | lists Network that are using SRX firewall device                               |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``configureSrxFirewall``                                   | Configures a SRX firewall device                                               |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
'

Parameters Changed API Commands
-------------------------------

.. cssclass:: table-striped table-bordered table-hover

+------------------------------------------------------------+--------------------------------------------------------------------------------+
| Name                                                       | Description                                                                    |
+============================================================+================================================================================+
| ``createPod``                                              | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``startip`` was 'required' and is now 'optional'                             |
|                                                            | - ``netmask`` was 'required' and is now 'optional'                             |
|                                                            | - ``gateway`` was 'required' and is now 'optional'                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``copyIso``                                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdataparams``                                                           |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachinesMetrics``                             | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid`` (optional)                                            |
|                                                            | - ``clusterid`` (optional)                                                     |
|                                                            | - ``hostid`` (optional)                                                        |
|                                                            | - ``podid`` (optional)                                                         |
|                                                            | - ``storageid`` (optional)                                                     |
|                                                            | - ``userdata`` (optional)                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listHosts``                                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptionsupported``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootSystemVm``                                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworks``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``privatemtu``                                                               |
|                                                            | - ``publicmtu``                                                                |
|                                                            | - ``supportsvmautoscaling``                                                    |
|                                                            | - ``tungstenvirtualrouteruuid``                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerSSHKeyPair``                                     | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``project``                                                                  |
|                                                            | - ``projectid``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``restoreVirtualMachine``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateHost``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptionsupported``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVPCOfferings``                                       | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``domainid`` (optional)                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``uploadVolume``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``vmtype``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``destroySystemVm``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleSystemVm``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopRouter``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForVirtualMachine``                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startRouter``                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listTemplates``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdataparams``                                                           |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``resetConfiguration``                                     | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``component``                                                                |
|                                                            | - ``defaultvalue``                                                             |
|                                                            | - ``displaytext``                                                              |
|                                                            | - ``group``                                                                    |
|                                                            | - ``options``                                                                  |
|                                                            | - ``parent``                                                                   |
|                                                            | - ``subgroup``                                                                 |
|                                                            | - ``type``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createAutoScalePolicy``                                  | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``name`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``name``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootVirtualMachine``                                   | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetworkOffering``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``fortungsten``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVPC``                                              | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``publicmtu`` (optional)                                                     |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``dns1``                                                                     |
|                                                            | - ``dns2``                                                                     |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``publicmtu``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopSystemVm``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetworkOffering``                                  | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``fortungsten`` (optional)                                                   |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``fortungsten``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumesMetrics``                                     | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``listsystemvms`` (optional)                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVmNicIp``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startInternalLoadBalancerVM``                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDiskOffering``                                     | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``encrypt``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaTariffList``                                        | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``enddate`` (optional)                                                       |
|                                                            | - ``listall`` (optional)                                                       |
|                                                            | - ``name`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``activationRule``                                                           |
|                                                            | - ``endDate``                                                                  |
|                                                            | - ``name``                                                                     |
|                                                            | - ``removed``                                                                  |
|                                                            | - ``usageTypeDescription``                                                     |
|                                                            | - ``uuid``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesClusters``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``created``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createAutoScaleVmGroup``                                 | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``name`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            | - ``associatednetworkname``                                                    |
|                                                            | - ``availablevirtualmachinecount``                                             |
|                                                            | - ``created``                                                                  |
|                                                            | - ``lbprovider``                                                               |
|                                                            | - ``name``                                                                     |
|                                                            | - ``privateport``                                                              |
|                                                            | - ``publicip``                                                                 |
|                                                            | - ``publicipid``                                                               |
|                                                            | - ``publicport``                                                               |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listConfigurations``                                     | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``group`` (optional)                                                         |
|                                                            | - ``parent`` (optional)                                                        |
|                                                            | - ``subgroup`` (optional)                                                      |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``component``                                                                |
|                                                            | - ``defaultvalue``                                                             |
|                                                            | - ``displaytext``                                                              |
|                                                            | - ``group``                                                                    |
|                                                            | - ``options``                                                                  |
|                                                            | - ``parent``                                                                   |
|                                                            | - ``subgroup``                                                                 |
|                                                            | - ``type``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaTariffUpdate``                                      | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``name`` (required)                                                          |
|                                                            | - ``activationrule`` (optional)                                                |
|                                                            | - ``description`` (optional)                                                   |
|                                                            | - ``enddate`` (optional)                                                       |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``usagetype`` was 'required' and is now 'optional'                           |
|                                                            | - ``startdate`` was 'required' and is now 'optional'                           |
|                                                            | - ``value`` was 'required' and is now 'optional'                               |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``activationRule``                                                           |
|                                                            | - ``endDate``                                                                  |
|                                                            | - ``name``                                                                     |
|                                                            | - ``removed``                                                                  |
|                                                            | - ``usageTypeDescription``                                                     |
|                                                            | - ``uuid``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleKubernetesCluster``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``created``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopNetScalerVpx``                                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listCapabilities``                                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``instancesdisksstatsretentionenabled``                                      |
|                                                            | - ``instancesdisksstatsretentiontime``                                         |
|                                                            | - ``instancesstatsretentiontime``                                              |
|                                                            | - ``instancesstatsuseronly``                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listConditions``                                         | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``projectid`` (optional)                                                     |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``counterid``                                                                |
|                                                            | - ``countername``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVolume``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``vmtype``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``disableAutoScaleVmGroup``                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            | - ``associatednetworkname``                                                    |
|                                                            | - ``availablevirtualmachinecount``                                             |
|                                                            | - ``created``                                                                  |
|                                                            | - ``lbprovider``                                                               |
|                                                            | - ``name``                                                                     |
|                                                            | - ``privateport``                                                              |
|                                                            | - ``publicip``                                                                 |
|                                                            | - ``publicipid``                                                               |
|                                                            | - ``publicport``                                                               |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSystemVms``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``detachVolume``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``vmtype``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForSystemVm``                               | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNics``                                               | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``mtu``                                                                      |
|                                                            | - ``vpcid``                                                                    |
|                                                            | - ``vpcname``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootRouter``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addNicToVirtualMachine``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateIso``                                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdataparams``                                                           |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateDefaultNicForVirtualMachine``                      | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareTemplate``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdataparams``                                                           |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopInternalLoadBalancerVM``                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``samlSso``                                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``is2faenabled``                                                             |
|                                                            | - ``is2faverified``                                                            |
|                                                            | - ``issuerfor2fa``                                                             |
|                                                            | - ``providerfor2fa``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``login``                                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``is2faenabled``                                                             |
|                                                            | - ``is2faverified``                                                            |
|                                                            | - ``issuerfor2fa``                                                             |
|                                                            | - ``providerfor2fa``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``copyTemplate``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdataparams``                                                           |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createServiceOffering``                                  | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptroot`` (optional)                                                   |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptroot``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNiciraNvpDeviceNetworks``                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``privatemtu``                                                               |
|                                                            | - ``publicmtu``                                                                |
|                                                            | - ``supportsvmautoscaling``                                                    |
|                                                            | - ``tungstenvirtualrouteruuid``                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``assignVirtualMachine``                                   | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``resizeVolume``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``vmtype``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateTemplate``                                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdataparams``                                                           |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listPaloAltoFirewallNetworks``                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``privatemtu``                                                               |
|                                                            | - ``publicmtu``                                                                |
|                                                            | - ``supportsvmautoscaling``                                                    |
|                                                            | - ``tungstenvirtualrouteruuid``                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``changeOfferingForVolume``                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``vmtype``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForRouter``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVolume``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``vmtype``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVirtualMachine``                                   | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdatadetails`` (optional)                                               |
|                                                            | - ``userdataid`` (optional)                                                    |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetwork``                                          | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``dns1`` (optional)                                                          |
|                                                            | - ``dns2`` (optional)                                                          |
|                                                            | - ``ip6dns1`` (optional)                                                       |
|                                                            | - ``ip6dns2`` (optional)                                                       |
|                                                            | - ``privatemtu`` (optional)                                                    |
|                                                            | - ``publicmtu`` (optional)                                                     |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``privatemtu``                                                               |
|                                                            | - ``publicmtu``                                                                |
|                                                            | - ``supportsvmautoscaling``                                                    |
|                                                            | - ``tungstenvirtualrouteruuid``                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachine``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createTemplate``                                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdataparams``                                                           |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``resetPasswordForVirtualMachine``                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``resetSSHKeyForVirtualMachine``                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addKubernetesSupportedVersion``                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``created``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createVPC``                                              | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``dns1`` (optional)                                                          |
|                                                            | - ``dns2`` (optional)                                                          |
|                                                            | - ``ip6dns1`` (optional)                                                       |
|                                                            | - ``ip6dns2`` (optional)                                                       |
|                                                            | - ``publicmtu`` (optional)                                                     |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``dns1``                                                                     |
|                                                            | - ``dns2``                                                                     |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``publicmtu``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listInternalLoadBalancerVMs``                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateKubernetesSupportedVersion``                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``created``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``detachIso``                                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareHostForMaintenance``                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptionsupported``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateAutoScaleVmGroup``                                 | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``name`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            | - ``associatednetworkname``                                                    |
|                                                            | - ``availablevirtualmachinecount``                                             |
|                                                            | - ``created``                                                                  |
|                                                            | - ``lbprovider``                                                               |
|                                                            | - ``name``                                                                     |
|                                                            | - ``privateport``                                                              |
|                                                            | - ``publicip``                                                                 |
|                                                            | - ``publicipid``                                                               |
|                                                            | - ``publicport``                                                               |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateAutoScaleVmProfile``                               | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``expungevmgraceperiod`` (optional)                                          |
|                                                            | - ``otherdeployparams`` (optional)                                             |
|                                                            | - ``serviceofferingid`` (optional)                                             |
|                                                            | - ``userdata`` (optional)                                                      |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``destroyvmgraceperiod``                                                     |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``expungevmgraceperiod``                                                     |
|                                                            | - ``userdata``                                                                 |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``destroyvmgraceperiod``                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``enableAutoScaleVmGroup``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            | - ``associatednetworkname``                                                    |
|                                                            | - ``availablevirtualmachinecount``                                             |
|                                                            | - ``created``                                                                  |
|                                                            | - ``lbprovider``                                                               |
|                                                            | - ``name``                                                                     |
|                                                            | - ``privateport``                                                              |
|                                                            | - ``publicip``                                                                 |
|                                                            | - ``publicipid``                                                               |
|                                                            | - ``publicport``                                                               |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVirtualMachines``                                    | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid`` (optional)                                            |
|                                                            | - ``userdata`` (optional)                                                      |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listDiskOfferings``                                      | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encrypt`` (optional)                                                       |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``encrypt``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``upgradeKubernetesCluster``                               | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``created``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createCondition``                                        | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``projectid`` (optional)                                                     |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``counterid``                                                                |
|                                                            | - ``countername``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``revertToVMSnapshot``                                     | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerIso``                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdataparams``                                                           |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVirtualMachine``                                   | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``iodriverpolicy`` (optional)                                                |
|                                                            | - ``iothreadsenabled`` (optional)                                              |
|                                                            | - ``userdatadetails`` (optional)                                               |
|                                                            | - ``userdataid`` (optional)                                                    |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateZone``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``allowuserspecifyvrmtu``                                                    |
|                                                            | - ``routerprivateinterfacemaxmtu``                                             |
|                                                            | - ``routerpublicinterfacemaxmtu``                                              |
|                                                            | - ``type``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostMaintenance``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptionsupported``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateAutoScalePolicy``                                  | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``name`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``name``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createDiskOffering``                                     | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encrypt`` (optional)                                                       |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``details``                                                                  |
|                                                            | - ``encrypt``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumes``                                            | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``listsystemvms`` (optional)                                                 |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``vmtype``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``lockUser``                                               | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``is2faenabled``                                                             |
|                                                            | - ``is2famandated``                                                            |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetwork``                                          | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``dns1`` (optional)                                                          |
|                                                            | - ``dns2`` (optional)                                                          |
|                                                            | - ``ip6dns1`` (optional)                                                       |
|                                                            | - ``ip6dns2`` (optional)                                                       |
|                                                            | - ``privatemtu`` (optional)                                                    |
|                                                            | - ``publicmtu`` (optional)                                                     |
|                                                            | - ``tungstenvirtualrouteruuid`` (optional)                                     |
|                                                            |                                                                                |
|                                                            | *Changed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``displaytext`` was 'required' and is now 'optional'                         |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``privatemtu``                                                               |
|                                                            | - ``publicmtu``                                                                |
|                                                            | - ``supportsvmautoscaling``                                                    |
|                                                            | - ``tungstenvirtualrouteruuid``                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworkOfferings``                                   | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``fortungsten``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listVPCs``                                               | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``dns1``                                                                     |
|                                                            | - ``dns2``                                                                     |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``publicmtu``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVirtualMachineWithVolume``                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateUser``                                             | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``mandate2fa`` (optional)                                                    |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``is2faenabled``                                                             |
|                                                            | - ``is2famandated``                                                            |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``attachVolume``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``vmtype``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addHost``                                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptionsupported``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listUsers``                                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``is2faenabled``                                                             |
|                                                            | - ``is2famandated``                                                            |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``disableUser``                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``is2faenabled``                                                             |
|                                                            | - ``is2famandated``                                                            |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listIsos``                                               | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdataparams``                                                           |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listAutoScalePolicies``                                  | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``name`` (optional)                                                          |
|                                                            | - ``projectid`` (optional)                                                     |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``name``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listZones``                                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``allowuserspecifyvrmtu``                                                    |
|                                                            | - ``routerprivateinterfacemaxmtu``                                             |
|                                                            | - ``routerpublicinterfacemaxmtu``                                              |
|                                                            | - ``type``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetscalerLoadBalancerNetworks``                      | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``privatemtu``                                                               |
|                                                            | - ``publicmtu``                                                                |
|                                                            | - ``supportsvmautoscaling``                                                    |
|                                                            | - ``tungstenvirtualrouteruuid``                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startSystemVm``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createKubernetesCluster``                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``created``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``declareHostAsDegraded``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptionsupported``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVolume``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``vmtype``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVMAffinityGroup``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVPC``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``dns1``                                                                     |
|                                                            | - ``dns2``                                                                     |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``publicmtu``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateConfiguration``                                    | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``component``                                                                |
|                                                            | - ``defaultvalue``                                                             |
|                                                            | - ``displaytext``                                                              |
|                                                            | - ``group``                                                                    |
|                                                            | - ``options``                                                                  |
|                                                            | - ``parent``                                                                   |
|                                                            | - ``subgroup``                                                                 |
|                                                            | - ``type``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVirtualMachine``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listCounters``                                           | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider`` (optional)                                                      |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateSystemVm``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listAutoScaleVmProfiles``                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``expungevmgraceperiod``                                                     |
|                                                            | - ``userdata``                                                                 |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``destroyvmgraceperiod``                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostAsDegraded``                                   | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptionsupported``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listRouters``                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listBrocadeVcsDeviceNetworks``                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``privatemtu``                                                               |
|                                                            | - ``publicmtu``                                                                |
|                                                            | - ``supportsvmautoscaling``                                                    |
|                                                            | - ``tungstenvirtualrouteruuid``                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listKubernetesSupportedVersions``                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``created``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``recoverVolume``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``vmtype``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``enableUser``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``is2faenabled``                                                             |
|                                                            | - ``is2famandated``                                                            |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateNetwork``                                         | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``ip6dns1``                                                                  |
|                                                            | - ``ip6dns2``                                                                  |
|                                                            | - ``privatemtu``                                                               |
|                                                            | - ``publicmtu``                                                                |
|                                                            | - ``supportsvmautoscaling``                                                    |
|                                                            | - ``tungstenvirtualrouteruuid``                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``registerTemplate``                                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdataparams``                                                           |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createZone``                                             | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``isedge`` (optional)                                                        |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``allowuserspecifyvrmtu``                                                    |
|                                                            | - ``routerprivateinterfacemaxmtu``                                             |
|                                                            | - ``routerpublicinterfacemaxmtu``                                              |
|                                                            | - ``type``                                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``importUnmanagedInstance``                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listAutoScaleVmGroups``                                  | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``name`` (optional)                                                          |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``associatednetworkid``                                                      |
|                                                            | - ``associatednetworkname``                                                    |
|                                                            | - ``availablevirtualmachinecount``                                             |
|                                                            | - ``created``                                                                  |
|                                                            | - ``lbprovider``                                                               |
|                                                            | - ``name``                                                                     |
|                                                            | - ``privateport``                                                              |
|                                                            | - ``publicip``                                                                 |
|                                                            | - ``publicipid``                                                               |
|                                                            | - ``publicport``                                                               |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createVolume``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``vmtype``                                                                   |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``attachIso``                                              | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createUser``                                             | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``is2faenabled``                                                             |
|                                                            | - ``is2famandated``                                                            |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listSSHKeyPairs``                                        | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``project``                                                                  |
|                                                            | - ``projectid``                                                                |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyRouter``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``quotaSummary``                                           | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``quotaenabled``                                                             |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createCounter``                                          | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider`` (required)                                                      |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``provider``                                                                 |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``removeNicFromVirtualMachine``                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteAutoScaleVmGroup``                                 | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``cleanup`` (optional)                                                       |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``createAutoScaleVmProfile``                               | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``account`` (optional)                                                       |
|                                                            | - ``domainid`` (optional)                                                      |
|                                                            | - ``expungevmgraceperiod`` (optional)                                          |
|                                                            | - ``projectid`` (optional)                                                     |
|                                                            | - ``userdata`` (optional)                                                      |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``destroyvmgraceperiod``                                                     |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``expungevmgraceperiod``                                                     |
|                                                            | - ``userdata``                                                                 |
|                                                            |                                                                                |
|                                                            | *Removed Parameters:*                                                          |
|                                                            |                                                                                |
|                                                            | - ``destroyvmgraceperiod``                                                     |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``reconnectHost``                                          | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptionsupported``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startKubernetesCluster``                                 | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``created``                                                                  |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``getUser``                                                | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``is2faenabled``                                                             |
|                                                            | - ``is2famandated``                                                            |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteBackup``                                           | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``forced`` (optional)                                                        |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``addBaremetalHost``                                       | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptionsupported``                                                      |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``destroyVirtualMachine``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``listServiceOfferings``                                   | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptroot`` (optional)                                                   |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptroot``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``startVirtualMachine``                                    | **Request:**                                                                   |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``considerlasthost`` (optional)                                              |
|                                                            |                                                                                |
|                                                            | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``stopVirtualMachine``                                     | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``autoscalevmgroupid``                                                       |
|                                                            | - ``autoscalevmgroupname``                                                     |
|                                                            | - ``hostcontrolstate``                                                         |
|                                                            | - ``userdata``                                                                 |
|                                                            | - ``userdatadetails``                                                          |
|                                                            | - ``userdataid``                                                               |
|                                                            | - ``userdataname``                                                             |
|                                                            | - ``userdatapolicy``                                                           |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
| ``updateServiceOffering``                                  | **Response:**                                                                  |
|                                                            |                                                                                |
|                                                            | *New Parameters:*                                                              |
|                                                            |                                                                                |
|                                                            | - ``encryptroot``                                                              |
|                                                            |                                                                                |
+------------------------------------------------------------+--------------------------------------------------------------------------------+
"
