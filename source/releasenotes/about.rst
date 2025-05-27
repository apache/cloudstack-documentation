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

Apache CloudStack |release| is a 4.20 LTS minor release with over 150 fixes
and improvements since the 4.20.0.0 release. Some of the highlights include:

• Improve listing of Vmware Datacenter VMs for migration to KVM
• Improvements to multi-architecture support in CloudStack
• vTPM support for KVM and VMware
• Support for XenServer 8.4 / XCP-ng 8.3
• Added support for VMware 80u2 and 80u3
• Updated Sysyem VM template to Debian 12.10
• Linstore improvements
• NAS B&R improvements


The full list of new features can be found in the project release notes at
https://docs.cloudstack.apache.org/en/4.20.1.0/releasenotes/changes.html

Log4j Upgrade
=============

Up until 4.19.x.x, the logging library used for the project was Log4j 1.29. 
The 4.20.0.0 version has updated the library to Log4j2. The new Log4j2 configuration file format is not backwards 
compatible with the old one. The 4.20.0.0 packages will come with the default configuration files updated. 
Users that have made customizations to their files must update their configuration files to match with the new format, 
the `official Log4j documentation`_ might help you migrate your custom configurations.

JRE Upgrade
============

Up until 4.19.x.x, the JRE used for ACS was JRE 11. In 4.20.0.0, JRE has been upgraded to JRE 17 as JRE 11 has reached EOL. 
This means that Centos7 (EL7) is no longer supported.

.. _official Log4j documentation: https://logging.apache.org/log4j/2.x/migrate-from-log4j1.html

Events Message Bus Change
=========================
On upgrading from 4.19.x or lower, existing AMQP or Kafka intergration
configurations should be moved from folder
``/etc/cloudstack/management/META-INF/cloudstack/core`` to
``/etc/cloudstack/management/META-INF/cloudstack/event``
