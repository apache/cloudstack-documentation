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

.. _Veeam Backup and Recovery Plugin:

Veeam Backup and Recovery Plugin
=================================

About the Veeam Backup and Recovery Plugin
-------------------------------------------

There are a couple of important concepts to understand before working with the Veeam plugin.

#. Veeams API does not allow for the creation of backup jobs.  Therefore, a backup job must be created which will act
   as a template for all 'backups' which are based on it.

#. The backup job templates will be zone specific as they will contain the backup destination, and this will be different
   in each zone (unless you have extreamly fat links between zones).


Installing Veeam Backup and Recovery for use with CloudStack
-------------------------------------------------------------




Plugin specific settings:
------------------------
(all settings can be global or per-zone)

.. cssclass:: table-striped table-bordered table-hover

==================================== ========================
Configuration                         Description
==================================== ========================
backup.plugin.veeam.url              Veeam B&R server URL. Default: http://localhost:9399/api/.
backup.plugin.veeam.username         Veeam B&R server username. Default: administrator.
backup.plugin.veeam.password         Veeam B&R server password. Default: P@ssword123.
backup.plugin.veeam.validate.ssl     Whether to validate Veeam B&R server (SSL/TLS) connection while making API requests. Default: false.
backup.plugin.veeam.request.timeout  Veeam B&R API request timeout in seconds. Default: 300.
==================================== ========================


