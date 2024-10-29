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


What's New in |release|
=======================

Apache CloudStack 4.20.0.0 is the initial 4.20 LTS release with 190+ new
features, improvements and bug fixes since 4.19, including 15 major
new features. Some of the highlights include:

• Webhooks
• Dynamic and Static Routing
• Ceph RGW Object Store Support
• NSX integration
• Shared Filesystem
• Multi-arch Zones


The full list of new features can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.20.0.0/releasenotes/changes.html

Log4j Upgrade
=============

Up until 4.19.x.x, the logging library used for the project was Log4j 1.29. 
The 4.20.0.0 version has updated the library to Log4j2. The new Log4j2 configuration file format is not backwards 
compatible with the old one. The 4.20.0.0 packages will come with the default configuration files updated. 
Users that have made customizations to their files must update their configuration files to match with the new format, 
the `official Log4j documentation` might help you migrate your custom configurations.

JRE Upgrade
============

Up until 4.19.x.x, the JRE used for ACS was JRE 11. In 4.20.0.0, the JRE was upgraded to JRE 17 as JRE 11 has reached EOL. 
This means that Centos7 (EL7) is no longer supported.

.. _official Log4j documentation_: https://logging.apache.org/log4j/2.x/migrate-from-log4j1.html
