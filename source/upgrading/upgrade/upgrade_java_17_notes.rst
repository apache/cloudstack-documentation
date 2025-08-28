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

.. CloudStack Release Notes documentation main file, created by
   sphinx-quickstart on Fri Feb  7 16:00:59 2014.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

|menu_acs_logo|


Upgrading CloudStack
====================

Java version upgraded to Java 17
---------------------------------

As of Apache CloudStack 4.20, support for running with Java 17 has been added.
In later versions, support for Java 11 will be removed.

If you are running CloudStack with Java 17, for CloudStack versions 4.20 and later:
  * Verify /etc/default/cloudstack-management is consistent with https://github.com/apache/cloudstack/blob/main/packaging/systemd/cloudstack-management.default; Specifically, ensure that the following is present in the JAVA_OPTS:

  .. code-block:: bash

   --add-opens=java.base/java.lang=ALL-UNNAMED --add-exports=java.base/sun.security.x509=ALL-UNNAMED

  * Verify /etc/default/cloudstack-usage is also consistent with the same file in the repository.
  * Perform the same check for /etc/default/cloudstack-agent on the hypervisor hosts.

.. include:: _java_version.rst