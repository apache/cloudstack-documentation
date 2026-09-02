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

Writing Extensions for CloudStack
=================================

The CloudStack Extensions Framework allows developers and operators to write extensions using any programming language or script. From CloudStack’s perspective, an extension is an executable capable of handling CloudStack actions and integrating with an external system.

Extension Types
^^^^^^^^^^^^^^^

CloudStack currently supports two extension types:

- ``Orchestrator`` for external instance lifecycle management. These extensions are registered with ``Cluster`` resources.

- ``NetworkOrchestrator`` for external guest network and VPC service orchestration. These extensions are registered with ``PhysicalNetwork`` resources.

Both types share the same extension lifecycle in the UI and API, but their invocation model and supported resource mappings differ.


Create a New Extension
^^^^^^^^^^^^^^^^^^^^^^

You must first register a new extension using the API or UI:

.. code-block:: bash

  cloudmonkey createExtension name=myext type=Orchestrator path=myext-executable

Arguments:

- ``name``: Unique name
- ``type``: ``Orchestrator`` or ``NetworkOrchestrator``
- ``path``: Relative path to the executable. Root path will be `/usr/share/cloudstack-management/extensions/<extension_name>`

The path must be:

- Executable (``chmod +x``)
- Owned by the ``cloud:cloud`` user
- Present on all management servers (identical path and binary)

If no explicit path is provided during extension creation, CloudStack will scaffold a basic shell script at a default location with minimal required action handlers. This provides a starting point for customization and ensures the extension is immediately recognized and callable by the system.

CloudStack checks extension readiness periodically and shows its state in the UI/API.

For ``NetworkOrchestrator`` extensions, define supported services in the extension detail ``network.services`` and optionally declare per-service capabilities in ``network.service.capabilities``. CloudStack uses these values when exposing supported providers and validating network and VPC offerings.

Register Extension With a Resource
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

After creating an extension, register it with the CloudStack resource it serves:

- ``Orchestrator`` extensions are registered with ``Cluster`` resources.

- ``NetworkOrchestrator`` extensions are registered with ``PhysicalNetwork`` resources.

Resource-level details supplied during registration are useful for endpoints, credentials, host lists, interface mappings, or other device-specific settings. These registration details can later be changed with the ``updateRegisteredExtension`` API without removing the existing mapping.

When a ``NetworkOrchestrator`` extension is registered with a physical network, CloudStack creates a network service provider using the extension name. Network and VPC offerings can then use that provider name.

Invocation Model
^^^^^^^^^^^^^^^^

Orchestrator Invocation
~~~~~~~~~~~~~~~~~~~~~~~

Orchestrator extensions must support the following invocation structure:

.. code-block:: bash

   /path/to/executable <action> <payload_file> <timeout_seconds>

Arguments:

- ``<action>``: Action name (e.g., ``deploy``, ``start``, ``status``)
- ``<payload_file>``: Path to the input JSON file
- ``<timeout_seconds>``: Max duration CloudStack will wait for completion

Sample Invocation:

.. code-block:: bash

   /usr/share/cloudstack-management/extensions/myext/myext.py deploy /var/lib/cloudstack/management/extensions/myext/162345.json 60

NetworkOrchestrator Invocation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

NetworkOrchestrator extensions also use the payload-file invocation model:

.. code-block:: bash

  /path/to/<extension_name>.sh <command> <payload_file> <timeout_seconds>

CloudStack resolves the executable in this order:

- ``<extensionPath>/<extensionName>.sh``

- ``<extensionPath>`` itself, if it is an executable file

Depending on the declared services, CloudStack can invoke commands such as ``ensure-network-device``, ``implement-network``, ``shutdown-network``, ``destroy-network``, ``restore-network``, ``implement-vpc``, ``shutdown-vpc``, ``update-vpc-source-nat-ip``, ``assign-ip``, ``release-ip``, ``add-static-nat``, ``delete-static-nat``, ``add-port-forward``, ``delete-port-forward``, ``apply-fw-rules``, ``apply-network-acl``, ``add-dhcp-entry``, ``remove-dhcp-entry``, ``config-dhcp-subnet``, ``remove-dhcp-subnet``, ``set-dhcp-options``, ``add-dns-entry``, ``config-dns-subnet``, ``remove-dns-subnet``, ``save-vm-data``, ``save-password``, ``save-userdata``, ``save-sshkey``, ``save-hypervisor-hostname``, ``apply-lb-rules``, and ``custom-action``.

The command name determines the operation. The payload file carries registration details, stored network or VPC state, and command-specific fields.

Input Format (Payload)
^^^^^^^^^^^^^^^^^^^^^^

For Orchestrator extensions, CloudStack provides input via a JSON file, which your executable must read and parse.

Example:

.. code-block:: json

   {
     "externaldetails": {
       "resourcemap": {
         ...
       },
       "virtualmachine": {
         "exttemplateid": "1"
       },
       "host": {
         ...
       },
       "extension": {
         ...
       }
     },
     "virtualmachineid": "...",
     "cloudstack.vm.details": {
       "id": 100,
       "name": "i-2-100-VM",
       ...
     },
     "virtualmachinename": "i-2-100-VM",
     "caller": {
       "roleid": "6b86674b-7e61-11f0-ba77-1e00c8000158",
       "rolename": "Root Admin",
       "name": "admin",
       "roletype": "Admin",
       "id": "93567ed9-7e61-11f0-ba77-1e00c8000158",
       "type": "ADMIN"
     }
   }

The schema varies depending on the resource and action. Use this to perform context-specific logic.

For NetworkOrchestrator extensions, CloudStack writes a JSON payload file and passes its path as the second argument. For standard network and VPC commands, the payload has this envelope:

.. code-block:: json

   {
     "physical-network-extension-details": {},
     "network-extension-details": {},
     "payload": {}
   }

``physical-network-extension-details`` contains the registration details stored against the physical network, enriched with values such as the physical network name. ``network-extension-details`` contains the per-network or per-VPC state saved by the extension, including the output previously returned by ``ensure-network-device``. ``payload`` contains the command-specific fields.

Frequently used payload fields include ``network_id``, ``vpc_id``, ``vlan``, ``gateway``, ``cidr``, ``extension_ip``, ``public_ip``, ``public_cidr``, ``public_vlan``, ``public_gateway``, ``private_ip``, ``nic_uuid``, ``dns``, and ``domain``.

For ``custom-action``, CloudStack still uses a payload file, but the command-specific values are placed at the top level instead of under ``payload``. The request includes keys such as ``action``, ``action-params``, ``physical-network-extension-details``, and ``network-extension-details``.

Output Format
^^^^^^^^^^^^^

Orchestrator extensions should write a response JSON to ``stdout``. Example:

.. code-block:: json

   {
     "status": "success",
     "message": "Deployment completed"
   }

For custom actions, CloudStack will display the ``message`` in the UI if the output JSON includes ``"printmessage": "true"``.
The ``message`` field can be a string, a JSON object or a JSON array.

For NetworkOrchestrator extensions, all commands must exit with code ``0`` on success and a non-zero code on failure. ``ensure-network-device`` is special: it must write a single-line JSON object to ``stdout`` and CloudStack persists that JSON for later calls. ``custom-action`` may also return output on ``stdout``. Other commands should not rely on ``stdout`` for normal operation because CloudStack ignores it apart from debug logging.

Declaring Network Services and Capabilities
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``NetworkOrchestrator`` extensions should declare their supported services in the extension detail ``network.services`` as a comma-separated list. Example values include ``SourceNat``, ``StaticNat``, ``PortForwarding``, ``Firewall``, ``Lb``, ``Dhcp``, ``Dns``, ``UserData``, ``NetworkACL``, ``Gateway``, ``Vpn``, and ``CustomAction``.

Use ``network.service.capabilities`` to provide a JSON object describing capability values for the declared services. CloudStack uses these capabilities when listing supported providers and validating network or VPC offerings.

For example, ``Firewall`` capabilities can declare values such as ``SupportedProtocols``, ``SupportedEgressProtocols``, and ``SupportedTrafficDirection``; ``Lb`` can declare ``SupportedLBAlgorithms`` and ``SupportedProtocols``; and ``SourceNat`` can declare ``SupportedSourceNatTypes``.

CloudStack Setup for NetworkOrchestrator
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

After creating a ``NetworkOrchestrator`` extension, the usual setup flow is:

1. Deploy the executable to the path returned by ``listExtensions`` on every management server.
2. Register the extension with a ``PhysicalNetwork`` using ``registerExtension`` and pass any device-specific details required by the script.
3. Enable the generated network service provider on that physical network.
4. Create network or VPC offerings that map supported services to the extension name.
5. When registration details need to change, update them with ``updateRegisteredExtension`` instead of deleting and recreating the mapping.

Service-to-Command Mapping
^^^^^^^^^^^^^^^^^^^^^^^^^^

NetworkOrchestrator scripts only need to implement the commands for the services they advertise in ``network.services``.

- ``SourceNat`` and ``Gateway`` trigger ``assign-ip`` and ``release-ip``.
- ``StaticNat`` triggers ``add-static-nat`` and ``delete-static-nat``.
- ``PortForwarding`` triggers ``add-port-forward`` and ``delete-port-forward``.
- ``Firewall`` triggers ``apply-fw-rules``.
- ``Lb`` triggers ``apply-lb-rules``.
- ``NetworkACL`` triggers ``apply-network-acl``.
- ``Dhcp`` triggers ``add-dhcp-entry``, ``remove-dhcp-entry``, ``config-dhcp-subnet``, ``remove-dhcp-subnet``, and ``set-dhcp-options``.
- ``Dns`` triggers ``add-dns-entry``, ``config-dns-subnet``, and ``remove-dns-subnet``.
- ``UserData`` triggers ``save-vm-data``, ``save-password``, ``save-userdata``, ``save-sshkey``, and ``save-hypervisor-hostname``.
- Network lifecycle operations always include ``ensure-network-device``, ``implement-network``, ``shutdown-network``, ``destroy-network``, and ``restore-network``.
- VPC lifecycle operations include ``ensure-network-device``, ``implement-vpc``, ``shutdown-vpc``, and ``update-vpc-source-nat-ip``.
- Operator-triggered actions use ``custom-action``.

VPC and Extension IP Notes
^^^^^^^^^^^^^^^^^^^^^^^^^^

For VPC-backed networks, CloudStack includes ``vpc_id`` in tier-level payloads and invokes VPC-level lifecycle commands without a ``network_id``. Use that value when the implementation needs to keep all tiers of a VPC on the same device.

``extension_ip`` is the IP address the external device presents on the guest side. When the extension provides ``SourceNat`` or ``Gateway``, it typically matches the network gateway. When the extension only provides services such as ``Dhcp``, ``Dns``, or ``UserData``, CloudStack can allocate a dedicated guest-side IP for the device and pass it as ``extension_ip``.

Action Lifecycle
^^^^^^^^^^^^^^^^

1. A CloudStack action (e.g., deploy VM) triggers a corresponding extension action.
2. CloudStack invokes the extension’s executable using the protocol defined by the extension type.
3. The extension processes the input and responds within the timeout.
4. CloudStack continues action workflow based on the result.

Console Access for Instances with Orchestrator Extensions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Orchestrator extensions can provide console access for instances either through **VNC** or a **URL**.
To enable this, the extension must implement the ``getconsole`` action and return output in one of the following JSON formats:

VNC-based console:

.. code-block:: json

    {
      "status": "success",
      ...
      "console": {
        "host": "pve-node1.internal",
        "port": "5901",
        "password": "PVEVNC:6329C6AA::ZPcs5MT....d9",
        "passwordonetimeuseonly": true
        "protocol": "vnc"
      }
    }

``passwordonetimeuseonly`` is optional. It can be set to ``true`` if the system returns a one-time-use VNC ticket.

For VNC-based access, the returned details are forwarded to the Console Proxy VM (CPVM) in the same zone as the instance. The specified **host** and **port** must be reachable from the CPVM.  

Direct URL-based console:

.. code-block:: json

    {
      "status": "success",
      ...
      "console": {
        "url": "CONSOLE_URL",
        "protocol": "direct"
      }
    }


.. note::
   For URL–based console access, CloudStack does not report the acquired or client IP address.
   In this mode, security and access control must be handled by the server providing the console.

   Protocol value of ``direct`` can be used for URL–based console access.

Custom Actions
^^^^^^^^^^^^^^

You can define new custom actions for users or admin-triggered workflows.

- Register via UI or ``addCustomAction`` API
- Choose a resource type that matches the extension type: ``VirtualMachine`` for Orchestrator, ``Network`` or ``Vpc`` for NetworkOrchestrator
- Define input parameters (name, type, required)
- Implement the handler for the custom action in your executable.

For NetworkOrchestrator extensions, advertise the ``CustomAction`` service in ``network.services`` if the extension should receive custom actions for network or VPC resources.

For network extension custom actions, the script should read the payload file passed on the command line and parse the top-level keys rather than looking for a nested ``payload`` object.

CloudStack UI will render forms dynamically based on these definitions.

Best Practices
^^^^^^^^^^^^^^

- Make executable/script idempotent and stateless
- Validate all inputs before acting
- Avoid hard dependencies on CloudStack internals
- Implement logging for troubleshooting
- Use exit code and ``stdout`` for signaling success/failure
- Keep ``network.services`` and ``network.service.capabilities`` aligned with the services your NetworkOrchestrator implementation actually handles
- Use resource registration details for environment-specific settings and rotate them with ``updateRegisteredExtension`` instead of recreating mappings when possible
- Keep non-``ensure-network-device`` commands quiet on ``stdout`` unless the command contract explicitly returns output, such as ``custom-action``

Extension Examples
^^^^^^^^^^^^^^^^^^

**Bash Example**

.. code-block:: bash

   #!/bin/bash
   ACTION=$1
   FILE=$2
   TIMEOUT=$3

   if [ "$ACTION" == "deploy" ]; then
       echo '{ "success": true, "result": { "message": "OK" } }'
   else
       echo '{ "success": false, "result": { "message": "Unsupported action" } }'
   fi

**Python Example**

.. code-block:: python

   import sys, json

   action = sys.argv[1]
   payload_file = sys.argv[2]

   with open(payload_file) as f:
       data = json.load(f)

   if action == "deploy":
       print(json.dumps({"success": True, "result": {"message": "Deployed"}}))
   else:
       print(json.dumps({"success": False, "result": {"message": "Unknown action"}}))

For a clearer understanding of how to implement an Orchestrator extension, developers can refer to the base shell script scaffolded by CloudStack for orchestrator-type extensions. This script is located at:

/usr/share/cloudstack-common/scripts/vm/hypervisor/external/provisioner/provisioner.sh

It serves as a template with minimal required action handlers, making it a useful starting point for building new extensions.

For NetworkOrchestrator extensions, refer to the Network Extension Script Protocol in the CloudStack source tree and the reference implementation in `cloudstack-extensions <https://github.com/apache/cloudstack-extensions/tree/network-namespace/Network-Namespace>`_.

Additionally, CloudStack includes in-built extensions for Proxmox and Hyper-V that demonstrate how to implement extensions in different languages - Bash and Python.
