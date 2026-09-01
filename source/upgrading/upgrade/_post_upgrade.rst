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

Post Upgrade Procedures
------------------------

After upgrading CloudStack packages, new system properties and settings may be 
introduced in the release. CloudStack will not overwrite or replace your existing
configuration files. The latest configuration file are named with .rpmnew or .dpkg-dist 
extention depends on your package manager. 

It is strongly recommended to review and apply these new changes manually by comparing 
them to your previously installed version.


The locations of the essential configuration properties files are as follows:

.. parsed-literal::

   /etc/default/cloudstack-management
   /etc/default/cloudstack-usage
   /etc/cloudstack/management/db.properties
   /etc/cloudstack/management/config.json
   /etc/cloudstack/management/server.properties
   /etc/cloudstack/management/environment.properties
   /etc/cloudstack/management/java.security.ciphers





