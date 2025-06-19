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
   

Troubleshooting Extensions
--------------------------

Validate the Extension Entry Point
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   - Ensure that the entry point path is correctly defined and accessible on all management servers.

   - The script or binary must be executable and have appropriate permissions.

   - If the binary differs across management servers, the extension will be marked as Not Ready.

   - Entry points are stored at: `/usr/share/cloudstack-management/extensions/<extension_name>`

   - CloudStack runs a background task at regular intervals to verify entry point readiness. If the entry point is not ready, its state will appear as Not Ready in the UI or API responses.

   - Alerts are generated if an entry point is not ready.

   - The check interval can be configured using the cloudstack.extensions.entrypoint.check.interval property in global.properties. The default is 5 minutes.

Verify Payload Handling
^^^^^^^^^^^^^^^^^^^^^^^

   - Ensure the extension binary can correctly read and parse the incoming JSON payload.

   - Payload files are placed at: `/var/lib/cloudstack/management/extensions/<extension_name>/`

   - These payload files are automatically cleaned up after 24 hours.

   - Improper parsing of the payload is a common cause of failure—log any parsing errors in your extension binary for debugging.

Refer to Base Extension Scripts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   - For guidance on implementing supported actions, refer to the base scripts present for each extension type.

   - For Orchestrator-type extensions, see: `/usr/share/cloudstack-common/scripts/vm/hypervisor/external/provisioner/provisioner.sh`

   - These scripts provide examples of how to handle standard actions like start, stop, status, etc.

Check Logs for Errors
^^^^^^^^^^^^^^^^^^^^^

   - If the extension does not respond or returns an error, check the management server logs.

   - Logs include details of:

        1. Invocation of the extension binary

        2. Payload hand-off

        3. Output parsing

   - Any exceptions or exit code issues.
