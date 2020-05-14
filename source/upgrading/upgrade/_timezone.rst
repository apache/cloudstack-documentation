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

.. sub-section included in upgrade notes.

Time zone requirements
######################

As of CloudStack 4.14,  you must explicitly configure time zone either in the MySQL server or JDBC driver (db.properties).
In previous CloudStack versions, UTC time zone was assumed by default (all event's have UTC time stamps), so
the same UTC time zone should now be explicitly configured.

You can do this by editing the /etc/cloudstack/management/db.properties file and adding "serverTimezone=UTC"
to the "db.cloud.url.params=" and "db.usage.url.params=" lines.  Example lines, from a clean 4.14 installation, are given below:

.. parsed-literal::

   db.cloud.url.params=prepStmtCacheSize=517&cachePrepStmts=true&sessionVariables=sql_mode='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION'&serverTimezone=UTC
   db.usage.url.params=serverTimezone=UTC

