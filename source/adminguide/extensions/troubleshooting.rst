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
==========================

Validate the Extension Path
^^^^^^^^^^^^^^^^^^^^^^^^^^^

   - Ensure that the path is correctly defined and accessible on all management servers. The executable must be owned by the `cloud` user and group, and have appropriate permissions to be executed by `cloud:cloud`.

   - The script or binary must be executable and have appropriate permissions.

   - If the binary differs across management servers, the extension will be marked as Not Ready.

   - Ensure files are stored at: `/usr/share/cloudstack-management/extensions/<extension_name>`

   - For NetworkOrchestrator extensions, ensure the configured path resolves either to an executable file or to a directory that contains an executable named `<extension_name>.sh`.

   - CloudStack runs a background task at regular intervals to verify path readiness. If the path is not ready, its state will appear as Not Ready in the UI or API responses.

   - Alerts are generated if the extension path is not ready.

   - The check interval can be configured using the global configuration - `extension.path.state.check.interval`. The default is 5 minutes.

Verify Payload Handling
^^^^^^^^^^^^^^^^^^^^^^^

   - Ensure the extension binary can correctly read and parse the incoming JSON payload.

   - Payload files are placed at: `/var/lib/cloudstack/management/extensions/<extension_name>/`

   - These payload files are automatically cleaned up after 24 hours.

   - Improper parsing of the payload is a common cause of failure—log any parsing errors in your extension binary for debugging.

   - NetworkOrchestrator extensions use command-specific CLI arguments in addition to JSON strings such as ``--physical-network-extension-details`` and ``--network-extension-details``. Verify that the script accepts the expected command names and argument format for the services it implements.

Check Resource Registration and Provider State
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   - Orchestrator extensions must be registered with a ``Cluster`` resource. NetworkOrchestrator extensions must be registered with a ``PhysicalNetwork`` resource.

   - If resource-specific configuration changes are needed after registration, use the UI or the ``updateRegisteredExtension`` API instead of unregistering and recreating the mapping.

   - For NetworkOrchestrator extensions, confirm that a network service provider with the same name as the extension exists on the target physical network and is in the expected state before creating network or VPC offerings.

Verify Declared Network Services
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   - NetworkOrchestrator extensions should declare supported services in the extension detail ``network.services``.

   - Per-service capabilities should be declared in ``network.service.capabilities``.

   - If the expected provider services do not appear while creating a network or VPC offering, verify that these details were saved correctly and that any JSON value was quoted correctly when creating or updating the extension.

   - Common declared services include ``SourceNat``, ``StaticNat``, ``PortForwarding``, ``Firewall``, ``Lb``, ``Dhcp``, ``Dns``, ``UserData``, ``NetworkACL``, and ``CustomAction``. Additional services such as ``Gateway`` or ``Vpn`` can also be declared when supported by the implementation.

Refer to Base Extension Scripts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   - For guidance on implementing supported actions, refer to the base scripts present for each extension type.

   - For Orchestrator-type extensions, see: `/usr/share/cloudstack-common/scripts/vm/hypervisor/external/provisioner/provisioner.sh`

   - For NetworkOrchestrator-type extensions, refer to the Network Extension Script Protocol in the CloudStack source tree and the reference implementation in `cloudstack-extensions <https://github.com/apache/cloudstack-extensions/tree/network-namespace/Network-Namespace>`_.

   - These scripts provide examples of how to handle standard actions like start, stop, status, etc.

Check Logs for Errors
^^^^^^^^^^^^^^^^^^^^^

   - If the extension does not respond or returns an error, check the management server logs.

   - Logs include details of:

        1. Invocation of the extension binary

        2. Payload hand-off

        3. Output parsing

         4. Provider and service resolution for network and VPC operations

   - Any exceptions or exit code issues.
