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

The CloudStack Extensions Framework allows developers and operators to write extensions using any programming language or script. From CloudStack’s perspective, an extension is simply an executable capable of handling specific actions and processing input payloads. CloudStack invokes the executable by passing the action name and the path to a JSON-formatted payload file as command-line arguments. The extension processes the payload, performs the required operations on an external system, and returns the result as a JSON response written to `stdout`.


Create a New Extension
^^^^^^^^^^^^^^^^^^^^^^

You must first register a new extension using the API or UI:

.. code-block:: bash

   cloudmonkey createExtension name=myext path=myext-executable

Arguments:

- ``name``: Unique name
- ``path``: Relative path to the executable. Root path will be `/usr/share/cloudstack-management/extensions/<extension_name>`

The path must be:

- Executable (``chmod +x``)
- Owned by the ``cloud:cloud`` user
- Present on all management servers (identical path and binary)

If no explicit path is provided during extension creation, CloudStack will scaffold a basic shell script at a default location with minimal required action handlers. This provides a starting point for customization and ensures the extension is immediately recognized and callable by the system.

CloudStack checks extension readiness periodically and shows its state in the UI/API.

Extension Structure
^^^^^^^^^^^^^^^^^^^

Your extension must support the following invocation structure:

.. code-block:: bash

   /path/to/executable <action> <payload_file> <timeout_seconds>

Arguments:

- ``<action>``: Action name (e.g., ``deploy``, ``start``, ``status``)
- ``<payload_file>``: Path to the input JSON file
- ``<timeout_seconds>``: Max duration CloudStack will wait for completion

Sample Invocation:

.. code-block:: bash

   /usr/share/cloudstack-management/extensions/myext/myext.py deploy /var/lib/cloudstack/management/extensions/myext/162345.json 60

Input Format (Payload)
^^^^^^^^^^^^^^^^^^^^^^

CloudStack provides input via a JSON file, which your executable must read and parse.

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
     "virtualmachinename": "i-2-100-VM"
   }

The schema varies depending on the resource and action. Use this to perform context-specific logic.

Output Format
^^^^^^^^^^^^^

Your extension should write a response JSON to ``stdout``. Example:

.. code-block:: json

   {
     "status": "success",
     "message": "Deployment completed"
   }

For custom actions, CloudStack will display the ``message`` in the UI if the output JSON includes ``"printmessage": "true"``.
The ``message`` field can be a string, a JSON object or a JSON array.

Action Lifecycle
^^^^^^^^^^^^^^^^

1. A CloudStack action (e.g., deploy VM) triggers a corresponding extension action.
2. CloudStack invokes the extension’s executable with appropriate parameters.
3. The extension processes the input and responds within the timeout.
4. CloudStack continues action workflow based on the result.

Console Access for Instances with Orchestrator Extensions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Orchestrator extensions can provide console access for instances either through **VNC** or a **direct URL**.
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
        "protocol": "vnc"
      }
    }

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


Custom Actions
^^^^^^^^^^^^^^

You can define new custom actions for users or admin-triggered workflows.

- Register via UI or ``addCustomAction`` API
- Define input parameters (name, type, required)
- Implement the handler for the custom action in your executable.

CloudStack UI will render forms dynamically based on these definitions.

Best Practices
^^^^^^^^^^^^^^

- Make executable/script idempotent and stateless
- Validate all inputs before acting
- Avoid hard dependencies on CloudStack internals
- Implement logging for troubleshooting
- Use exit code and ``stdout`` for signaling success/failure

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

For a clearer understanding of how to implement an extension, developers can refer to the base shell script scaffolded by CloudStack for orchestrator-type extensions. This script is located at:

/usr/share/cloudstack-common/scripts/vm/hypervisor/external/provisioner/provisioner.sh

It serves as a template with minimal required action handlers, making it a useful starting point for building new extensions.

Additionally, CloudStack includes in-built extensions for Proxmox and Hyper-V that demonstrate how to implement extensions in different languages - Bash and Python.
