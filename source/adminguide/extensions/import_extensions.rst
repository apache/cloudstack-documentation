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

Importing Extensions using manifest files
=========================================

CloudStack provides functionality to import extensions using manifest files. This allows administrators to quickly set up and configure built-in extensions without manually creating them through the UI or API.
Either the ``importExtension`` API call can be used by providing a manifest file link, or the UI can be used to import extensions by providing the manifest file link directly.
CloudStack supports importing extensions from Git repositories or direct archive links. The manifest file must reference a source that provides:

- A Git repository with archive download capability (e.g., GitHub), or
- A direct URL to a downloadable archive (e.g., ``.zip``, ``.tar.gz``)

The archive must contain the required entrypoint file and any other needed scripts/files at the correct paths.

   |import-extension.png|


Git Repository Layout and Required Files
----------------------------------------

For an extension to be installed by CloudStack, two files are required:

1. ``manifest.yaml``
2. An entrypoint binary or script referenced from the manifest.

``manifest.yaml`` (required)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Must be located at the root of the repository.
- Must follow the extension schema (``apiVersion``, ``kind``, ``metadata``, ``spec``, etc.).
- Must reference a valid entrypoint file under ``spec.entrypoint.path``.

Example layout::

    cloudstack-orchestrator-extension/
     ├── manifest.yaml      # Required — must be at the root
     └── orchestrator.py    # Required — entrypoint binary/script

Entrypoint Binary or Script (required)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The entrypoint file must exist at the exact relative path specified::

    entrypoint:
      language: python
      path: orchestrator.py
      targetDir: /usr/share/cloudstack-management/extensions/orchestrator

Resulting installation path::

    /usr/share/cloudstack-management/extensions/orchestrator/orchestrator.py

---

Manifest Structure Overview
---------------------------

The ``manifest.yaml`` file describes how CloudStack should install, register, and run the extension.

At a high level, a manifest contains::

    apiVersion
    kind
    metadata
    source
    spec
    enabled
    customActions

---

Required Fields
---------------

apiVersion and kind
~~~~~~~~~~~~~~~~~~~

- ``apiVersion``: API version for the extension manifest.
- ``kind``: Extension type — for compute lifecycle handlers, this must be ``OrchestratorExtension``.

---

Metadata
--------

Provides human-readable information stored in the Registry and shown in the UI.

+--------------+----------+---------------------------------------------+
| Field        | Required | Description                                 |
+==============+==========+=============================================+
| name         | Yes      | Internal identifier                         |
+--------------+----------+---------------------------------------------+
| displayName  | Yes      | UI-visible name                             |
+--------------+----------+---------------------------------------------+
| description  | Yes      | Short explanation                           |
+--------------+----------+---------------------------------------------+
| version      | Yes      | Semantic version                            |
+--------------+----------+---------------------------------------------+
| maintainer   | Yes      | Contact information                         |
+--------------+----------+---------------------------------------------+
| homepage     | Optional | Project URL                                 |
+--------------+----------+---------------------------------------------+

Example::

    metadata:
      name: orchestrator
      displayName: Orchestrator Extension
      description: >
        Example orchestrator extension for CloudStack.
      version: 0.1.0
      maintainer: "Your Name <your.email@example.com>"
      homepage: "https://github.com/user/cloudstack-orchestrator-extension"

---

Source
------

Defines where CloudStack fetches extension files from::

    source:
      type: git
      url: "https://github.com/user/cloudstack-orchestrator-extension"
      refs: "main"

---

Spec
----

Spec Type::

    spec:
      type: Orchestrator

Compatibility (required)
~~~~~~~~~~~~~~~~~~~~~~~~

Defines supported CloudStack versions::

    spec:
      compatibility:
        cloudstack:
          minVersion: 4.23.0

Entrypoint (required)
~~~~~~~~~~~~~~~~~~~~~

Specifies installation and execution settings::

    spec:
      entrypoint:
        path: orchestrator.py
        targetDir: /usr/share/cloudstack-management/extensions/orchestrator

Execution path::

    <targetDir>/<path>

Orchestrator Options (optional)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    spec:
      orchestrator:
        requiresPrepareVm: false

Details (optional)
~~~~~~~~~~~~~~~~~~

Free-form metadata passed through without interpretation::

    spec:
      details:
        key1: value1
        key2: value2

---

Global Enabled Flag
-------------------

Controls whether the extension becomes active after installation::

    enabled: true

---

Custom Actions
--------------

Extensions may expose UI actions.

If not required::

    customActions: []

Example::

    customActions:
      - name: BackupInstance
        displayName: "Backup Instance"
        description: "Trigger a backup using the external orchestrator."
        resourcetype: VirtualMachine
        enabled: true
        timeout: 600
        allowedroletypes: [Admin, DomainAdmin, User]
        successmessage: "Successfully completed {{actionName}} for {{resourceName}} with {{extensionName}}"
        errormessage: "Failed to complete {{actionName}} for {{resourceName}} with {{extensionName}}"
        details:
          vendor: "external-backup-system"
          retentionPolicy: "daily"

---

Parameters
----------

Shown to the user when executing an action.

If unused::

    parameters: []

Example::

    parameters:
      - name: backup_type
        type: STRING
        required: true
        validationformat: NONE
        valueoptions: "full,incremental"

      - name: retain_days
        type: NUMBER
        required: false
        validationformat: DECIMAL

Supported Parameter Types
~~~~~~~~~~~~~~~~~~~~~~~~~

- BOOLEAN
- DATE
- NUMBER
- STRING

Validation Formats
~~~~~~~~~~~~~~~~~~

+------------+--------------------------------------+
| Type       | Formats                              |
+============+======================================+
| NUMBER     | ``NONE``, ``DECIMAL``                |
+------------+--------------------------------------+
| STRING     | ``NONE``, ``EMAIL``, ``PASSWORD``,   |
|            | ``URL``, ``UUID``                    |
+------------+--------------------------------------+
| BOOLEAN    | No additional formats                |
+------------+--------------------------------------+
| DATE       | No additional formats                |
+------------+--------------------------------------+

---

Example Parameter Block
-----------------------

::

    parameters:
      - name: backup_type
        type: STRING
        required: true
        validationformat: NONE
        valueoptions: "full,incremental"

      - name: retain_days
        type: NUMBER
        validationformat: DECIMAL

      - name: notify
        type: BOOLEAN

.. Images


.. |import-extension.png| image:: /_static/images/import-extension.png
