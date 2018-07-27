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


API Changes Introduced in |release|
===================================

For the complete list of API commands and params consult the `CloudStack Apidocs`_.


New API Commands
----------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``provisionCertificate``                    | Issues and propagates client certificate on a connected host/agent using       |
|                                             | configured CA plugin                                                           |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listElastistorPool``                      | Lists the pools of elastistor                                                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteServicePackageOffering``            | Delete Service Package                                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listAnnotations``                         | Lists annotations.                                                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableHAForZone``                         | Enables HA for a zone                                                          |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableHAForCluster``                      | Enables HA cluster-wide                                                        |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNuageVspDomainTemplates``             | Lists Nuage VSP domain templates                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listElastistorInterface``                 | Lists the network Interfaces of elastistor                                     |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopNetScalerVpx``                        | Stops a NetScalervm.                                                           |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``disableHAForZone``                        | Disables HA for a zone                                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``revokeCertificate``                       | Revokes certificate using configured CA plugin                                 |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateSiocInfo``                          | Update SIOC info                                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``cloudianSsoLogin``                        | Generates single-sign-on login url for logged-in CloudStack user to access the |
|                                             | Cloudian Management Console                                                    |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``issueCertificate``                        | Issues a client certificate using configured or provided CA plugin             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetscalerControlCenter``              | list control center                                                            |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listCAProviders``                         | Lists available certificate authority providers in CloudStack                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``acquirePodIpAddress``                     | Allocates IP addresses in respective Pod of a Zone                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteManagementNetworkIpRange``          | Deletes a management network IP range. This action is only allowed when no IPs |
|                                             | in this range are allocated.                                                   |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addAnnotation``                           | add an annotation.                                                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deployNetscalerVpx``                      | Creates new NS Vpx                                                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listElastistorVolume``                    | Lists the volumes of elastistor                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``cloudianIsEnabled``                       | Checks if the Cloudian Connector is enabled                                    |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNuageVspGlobalDomainTemplate``        | Lists Nuage VSP domain templates                                               |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listHostHAResources``                     | Lists host HA resources                                                        |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableHAForHost``                         | Enables HA for a host                                                          |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerNetscalerServicePackage``         | Registers NCC Service Package                                                  |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listHostHAProviders``                     | Lists HA providers                                                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listCaCertificate``                       | Lists the CA public certificate(s) as support by the configured/provided CA    |
|                                             | plugin                                                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVPC``                              | moves a vpc to another physical network                                        |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``configureHAForHost``                      | Configures HA for a host                                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listRegisteredServicePackages``           | lists registered service packages                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``disableHAForCluster``                     | Disables HA cluster-wide                                                       |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``linkAccountToLdap``                       | link a cloudstack account to a group or OU in ldap                             |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``associateNuageVspDomainTemplate``         | associate a vpc with a domain template                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``moveUser``                                | Moves a user to another account                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``disableHAForHost``                        | Disables HA for a host                                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteNetscalerControlCenter``            | Delete Netscaler Control Center                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateNetwork``                          | moves a network to another physical network                                    |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``uploadTemplateDirectDownloadCertificate`` | Upload a certificate for HTTPS direct template download on KVM hosts           |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerNetscalerControlCenter``          | Adds a netscaler control center device                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createManagementNetworkIpRange``          | Creates a Management network IP range.                                         |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``removeAnnotation``                        | remove an annotation.                                                          |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``releasePodIpAddress``                     | Releases a Pod IP back to the Pod                                              |
+---------------------------------------------+--------------------------------------------------------------------------------+


Parameters Changed API Commands
-------------------------------

.. cssclass:: table-striped table-bordered table-hover

+---------------------------------------------+--------------------------------------------------------------------------------+
| Name                                        | Description                                                                    |
+=============================================+================================================================================+
| ``createPod``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forsystemvms``                                                             |
|                                             | - ``vlanid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``copyIso``                                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``childtemplates``                                                           |
|                                             | - ``directdownload``                                                           |
|                                             | - ``parenttemplateid``                                                         |
|                                             | - ``physicalsize``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listHosts``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``annotation``                                                               |
|                                             | - ``hostha``                                                                   |
|                                             | - ``lastannotated``                                                            |
|                                             | - ``username``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateStoragePool``                       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``allocatediops``                                                            |
|                                             | - ``provider``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``rebootSystemVm``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``guestvlan``                                                                |
|                                             | - ``publicvlan``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetworks``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``externalid``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateResourceLimit``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``resourcetypename``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateHost``                              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``annotation`` (optional)                                                    |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``annotation``                                                               |
|                                             | - ``hostha``                                                                   |
|                                             | - ``lastannotated``                                                            |
|                                             | - ``username``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``uploadVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid``                                                                |
|                                             | - ``clustername``                                                              |
|                                             | - ``physicalsize``                                                             |
|                                             | - ``podid``                                                                    |
|                                             | - ``podname``                                                                  |
|                                             | - ``utilization``                                                              |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``destroySystemVm``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``guestvlan``                                                                |
|                                             | - ``publicvlan``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``scaleSystemVm``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``guestvlan``                                                                |
|                                             | - ``publicvlan``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listLdapConfigurations``                  | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listTemplates``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``parenttemplateid`` (optional)                                              |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``childtemplates``                                                           |
|                                             | - ``directdownload``                                                           |
|                                             | - ``parenttemplateid``                                                         |
|                                             | - ``physicalsize``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createLoadBalancerRule``                  | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zonename``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetworkOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``tags`` (optional)                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``stopSystemVm``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``guestvlan``                                                                |
|                                             | - ``publicvlan``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetworkOffering``                   | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forvpc`` (optional)                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumesMetrics``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid`` (optional)                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSslCerts``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``name``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listPods``                                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forsystemvms``                                                             |
|                                             | - ``vlanid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSnapshots``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listConfigurations``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSystemVms``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``guestvlan``                                                                |
|                                             | - ``publicvlan``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``detachVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid``                                                                |
|                                             | - ``clustername``                                                              |
|                                             | - ``physicalsize``                                                             |
|                                             | - ``podid``                                                                    |
|                                             | - ``podname``                                                                  |
|                                             | - ``utilization``                                                              |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``changeServiceForSystemVm``                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``guestvlan``                                                                |
|                                             | - ``publicvlan``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshot``                          | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``asyncbackup`` (optional)                                                   |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNics``                                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``extradhcpoption``                                                          |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createSnapshotFromVMSnapshot``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listStoragePools``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``allocatediops``                                                            |
|                                             | - ``provider``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addNicToVirtualMachine``                  | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``dhcpoptions`` (optional)                                                   |
|                                             | - ``macaddress`` (optional)                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listExternalLoadBalancers``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``annotation``                                                               |
|                                             | - ``hostha``                                                                   |
|                                             | - ``lastannotated``                                                            |
|                                             | - ``username``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateIso``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``childtemplates``                                                           |
|                                             | - ``directdownload``                                                           |
|                                             | - ``parenttemplateid``                                                         |
|                                             | - ``physicalsize``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareTemplate``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``childtemplates``                                                           |
|                                             | - ``directdownload``                                                           |
|                                             | - ``parenttemplateid``                                                         |
|                                             | - ``physicalsize``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``copyTemplate``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``childtemplates``                                                           |
|                                             | - ``directdownload``                                                           |
|                                             | - ``parenttemplateid``                                                         |
|                                             | - ``physicalsize``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNiciraNvpDeviceNetworks``             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``externalid``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``resizeVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid``                                                                |
|                                             | - ``clustername``                                                              |
|                                             | - ``physicalsize``                                                             |
|                                             | - ``podid``                                                                    |
|                                             | - ``podname``                                                                  |
|                                             | - ``utilization``                                                              |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateTemplate``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``childtemplates``                                                           |
|                                             | - ``directdownload``                                                           |
|                                             | - ``parenttemplateid``                                                         |
|                                             | - ``physicalsize``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVlanIpRange``                       | **Request:**                                                                   |
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
| ``listPaloAltoFirewallNetworks``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``externalid``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteLdapConfiguration``                 | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             | - ``port`` (optional)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid``                                                                |
|                                             | - ``clustername``                                                              |
|                                             | - ``physicalsize``                                                             |
|                                             | - ``podid``                                                                    |
|                                             | - ``podname``                                                                  |
|                                             | - ``utilization``                                                              |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateVirtualMachine``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``dhcpoptionsnetworklist`` (optional)                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listDomains``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``details`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateNetwork``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``externalid``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deleteTemplate``                          | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forced`` (optional)                                                        |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createTemplate``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``childtemplates``                                                           |
|                                             | - ``directdownload``                                                           |
|                                             | - ``parenttemplateid``                                                         |
|                                             | - ``physicalsize``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updatePortForwardingRule``                | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``privateendport`` (optional)                                                |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``linkDomainToLdap``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ldapdomain`` (required)                                                    |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``ldapdomain``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listSrxFirewallNetworks``                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``externalid``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``prepareHostForMaintenance``               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``annotation``                                                               |
|                                             | - ``hostha``                                                                   |
|                                             | - ``lastannotated``                                                            |
|                                             | - ``username``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerIso``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``directdownload`` (optional)                                                |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``childtemplates``                                                           |
|                                             | - ``directdownload``                                                           |
|                                             | - ``parenttemplateid``                                                         |
|                                             | - ``physicalsize``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``deployVirtualMachine``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``datadiskofferinglist`` (optional)                                          |
|                                             | - ``dhcpoptionsnetworklist`` (optional)                                        |
|                                             | - ``macaddress`` (optional)                                                    |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVlanIpRanges``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forsystemvms``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelHostMaintenance``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``annotation``                                                               |
|                                             | - ``hostha``                                                                   |
|                                             | - ``lastannotated``                                                            |
|                                             | - ``username``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listVolumes``                             | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid`` (optional)                                                     |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid``                                                                |
|                                             | - ``clustername``                                                              |
|                                             | - ``physicalsize``                                                             |
|                                             | - ``podid``                                                                    |
|                                             | - ``podname``                                                                  |
|                                             | - ``utilization``                                                              |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``lockUser``                                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``usersource``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createNetwork``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``bypassvlanoverlapcheck`` (optional)                                        |
|                                             | - ``externalid`` (optional)                                                    |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``externalid``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateUser``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``usersource``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addHost``                                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``annotation``                                                               |
|                                             | - ``hostha``                                                                   |
|                                             | - ``lastannotated``                                                            |
|                                             | - ``username``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``attachVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid``                                                                |
|                                             | - ``clustername``                                                              |
|                                             | - ``physicalsize``                                                             |
|                                             | - ``podid``                                                                    |
|                                             | - ``podname``                                                                  |
|                                             | - ``utilization``                                                              |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listUsers``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``usersource``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listResourceLimits``                      | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``resourcetypename`` (optional)                                              |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``resourcetypename``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``disableUser``                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``usersource``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listIsos``                                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``childtemplates``                                                           |
|                                             | - ``directdownload``                                                           |
|                                             | - ``parenttemplateid``                                                         |
|                                             | - ``physicalsize``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listNetscalerLoadBalancerNetworks``       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``externalid``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``startSystemVm``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``guestvlan``                                                                |
|                                             | - ``publicvlan``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateVolume``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid``                                                                |
|                                             | - ``clustername``                                                              |
|                                             | - ``physicalsize``                                                             |
|                                             | - ``podid``                                                                    |
|                                             | - ``podname``                                                                  |
|                                             | - ``utilization``                                                              |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listEvents``                              | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``startid`` (optional)                                                       |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addLdapConfiguration``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateConfiguration``                     | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``domainid`` (optional)                                                      |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``dedicatePublicIpRange``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forsystemvms``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``revertSnapshot``                          | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``migrateSystemVm``                         | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``guestvlan``                                                                |
|                                             | - ``publicvlan``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateResourceCount``                     | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``resourcetypename``                                                         |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listBrocadeVcsDeviceNetworks``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``externalid``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listUsageRecords``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``includetags`` (optional)                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableUser``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``usersource``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``registerTemplate``                        | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``directdownload`` (optional)                                                |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``childtemplates``                                                           |
|                                             | - ``directdownload``                                                           |
|                                             | - ``parenttemplateid``                                                         |
|                                             | - ``physicalsize``                                                             |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createStoragePool``                       | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``allocatediops``                                                            |
|                                             | - ``provider``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``findStoragePoolsForMigration``            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``allocatediops``                                                            |
|                                             | - ``provider``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createVolume``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``clusterid``                                                                |
|                                             | - ``clustername``                                                              |
|                                             | - ``physicalsize``                                                             |
|                                             | - ``podid``                                                                    |
|                                             | - ``podname``                                                                  |
|                                             | - ``utilization``                                                              |
|                                             | - ``virtualsize``                                                              |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listF5LoadBalancerNetworks``              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``externalid``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updatePod``                               | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``forsystemvms``                                                             |
|                                             | - ``vlanid``                                                                   |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``enableStorageMaintenance``                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``allocatediops``                                                            |
|                                             | - ``provider``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``createUser``                              | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``usersource``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateRolePermission``                    | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``permission`` (optional)                                                    |
|                                             | - ``ruleid`` (optional)                                                        |
|                                             |                                                                                |
|                                             | *Changed Parameters:*                                                          |
|                                             |                                                                                |
|                                             | - ``ruleorder`` was 'required' and is now 'optional'                           |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``cancelStorageMaintenance``                | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``allocatediops``                                                            |
|                                             | - ``provider``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``updateLoadBalancerRule``                  | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``protocol`` (optional)                                                      |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zonename``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``reconnectHost``                           | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``annotation``                                                               |
|                                             | - ``hostha``                                                                   |
|                                             | - ``lastannotated``                                                            |
|                                             | - ``username``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``getUser``                                 | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``usersource``                                                               |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listLoadBalancerRules``                   | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``zonename``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``uploadSslCert``                           | **Request:**                                                                   |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``name`` (required)                                                          |
|                                             |                                                                                |
|                                             | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``name``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``addBaremetalHost``                        | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``annotation``                                                               |
|                                             | - ``hostha``                                                                   |
|                                             | - ``lastannotated``                                                            |
|                                             | - ``username``                                                                 |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+
| ``listCapacity``                            | **Response:**                                                                  |
|                                             |                                                                                |
|                                             | *New Parameters:*                                                              |
|                                             |                                                                                |
|                                             | - ``capacityallocated``                                                        |
|                                             | - ``name``                                                                     |
|                                             |                                                                                |
+---------------------------------------------+--------------------------------------------------------------------------------+

