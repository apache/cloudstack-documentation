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


General Upgrade Notes
=====================


Java version upgraded to Java 11
---------------------------------

As of Apache CloudStack 4.14, Java version required is 11 for the
management-server, cloudstack-usage, KVM agent and system-VMs.


.. include:: _java_version.rst

UI Deprecation and Removal Notice
---------------------------------

The current jQuery-based CloudStack UI is `deprecated
<http://markmail.org/message/vxnskmwhfaagnm4r/>`_ in this release of CloudStack
and will be removed in the next release of Apache CloudStack.

Migrating to dynamic roles feature
----------------------------------

As of Apache CloudStack 4.9, dynamic roles feature can be enabled after an
upgrade. Dynamic roles feature is enabled by default on new installations.

Please read more about :ref:`using-dynamics-roles`
feature and process of migrating to using this after an upgrade.

Agent and KVM Host Security
---------------------------

Starting 4.11, a new CA framework has been introduced that is used to secure
agent and management server connections. Starting 4.11.1, KVM hosts in UP
state that are not secured (i.e. the KVM host agent and libvirtd don't have
CA framework provisioned X509 certificates) will show up as 'Unsecure'. A new
button in the UI is available as well as an API to secure and onboard such
hosts.

Please read more about :ref:`host-security` and the process of migrating existing KVM hosts and agents to use the new security
feature.

OVS plug-in
-----------

OVS plug-in functionality is disrupted if ovsdaemon crashes

A critical functionality issue came out with `CLOUDSTACK-6779 <https://issues.apache.org/jira/browse/CLOUDSTACK-6779>`_. On XenServer it
is observed that on VIF unplug Ovs-Vswitchd is crashing resulting in loosing all
the openflow rules added to the bridge. Ovs daemon gets started and creates a
bridge but configure openflow rules are lost resulting in the disruption of
connectivity for the Instances on the host.


Active-Directory Authentication (LDAP)
--------------------------------------

If using Active-Directory (LDAP/LDAPs) as User authentication; Upgrading to
4.3 and later require changes in Global Settings. After upgrading CloudStack
to 4.3 or latest, following Global Settings must be change:

.. cssclass:: table-striped table-bordered table-hover

======================= ============== ==============
Global Settings         Default        New
======================= ============== ==============
ldap.user.object        inetOrgPerson  user
ldap.username.attribute uid            sAMAccountName
======================= ============== ==============


SystemVM 32bit deprecated
-------------------------

32bit versions of System VM Templates are in the process of being deprecated. Upgrade instructions from this Release Notes use 64bit Templates.

Explicit JDBC driver declaration
--------------------------------

While upgrading, on some environments the following may be required to be
added in CloudStack's db.properties file:

   # Add these to your db.properties file

   db.cloud.driver=jdbc:mysql

   db.usage.driver=jdbc:mysql


MySQL 8.0 sql mode change
-------------------------

MySQL mode (sql_mode) has changed in CloudStack db.properties to 
"STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,
ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION".

This gets automatically applies to the MySQL session used by CloudStack management server.

If the admin uses MySQL directly and wants to query tables it is advised to change the sql_mode in the corresponding session or globally.

Eg. mysql> set global sql_mode="STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,
                             "> ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION";
    Query OK, 0 rows affected (0.00 sec)

    mysql> set sql_mode="STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,
                     "> ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION";
    Query OK, 0 rows affected (0.00 sec)