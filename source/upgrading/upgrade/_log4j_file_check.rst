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

.. note::

   During upgrades from versions prior to 4.20, the logging configuration file may not be migrated automatically to the new Log4j2 format - especially if the original log4j configuration file was manually customized or modified.

   It is strongly recommended to verify **before starting the Management Server** that the configuration file under `/etc/cloudstack/management` and `/etc/cloudstack/usage` (e.g., `log4j-cloud.xml`) uses the Log4j2 format.

   If the file still uses legacy Log4j (version 1) syntax or structure, **manually replace or update** the configuration using the default Log4j2 configuration supplied with the latest package.

   Failure to update may result in missing or incomplete log generation after upgrade.
