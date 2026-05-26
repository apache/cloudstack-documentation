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
   

Disable Omit Stack Trace
------------------------

The JVM, by default stops printing some stack traces in the logs. To enable printing full stack traces at all times:

#. Edit the following configuration file for the respective service to disable there and restart it:

   - For cloudstack-management.service in the Management Server:

      .. code:: bash

         /etc/default/cloudstack-management

   - For cloudstack-usage.service in the Usage Server:

      .. code:: bash

         /etc/default/cloudstack-usage

   - For cloudstack-agent.service in the KVM Host:

      .. code:: bash

         /etc/default/cloudstack-agent

   - For cloud.service in the SSVM:

      .. code:: bash

         /usr/local/cloud/systemvm/_run.sh

#. Add the command-line parameter -XX:-OmitStackTraceInFastThrow to disable the omit stack trace flag in the JVM so that all
   the stack traces are always printed on the logs. This flag is enabled by default in the JVM to omit the stack traces
   for certain exceptions that are thrown frequently. Printing of the stack traces might impact performance, and is not
   recommended for production, so it's better to disable this flag for troubleshooting or debugging purposes when required.

   .. code:: bash

      JAVA_OPTS="... -XX:-OmitStackTraceInFastThrow"
