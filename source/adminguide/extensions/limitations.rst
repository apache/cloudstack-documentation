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
   

Limitations
===========

Although the external Instances behave a lot like CloudStack managed
Instances in many ways, there are some limitations. Some of these
limitations are due to the framework itself, while others can be addressed
by adding custom actions in the scripts written for the built-in extensions.

**Some general features/actions not supported at the framework level:**

   - Data volumes.

   - User Data and Metadata services.

   - SSH key injection.

   - Affinity Groups.

   - Migrate Instance.

   - Host Capacity and Utilization Stats.

   - Add Nics to Instance post deployment.

   - Console access to the in-built Hyper-V orchestrator Instances.

**Actions which can be implemented using Custom Actions in built-in extensions:**

   - Reinstall Instance.

   - Backup and Restore.

   - Recurring Snapshots.

   - Change Service Offering.

   - Resize Volume.

   - Attach ISO.
