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


Synchronization and Download
============================

In clustered Apache CloudStack management server deployments, extension files
must remain consistent across all management nodes. This release introduces
built-in support for:

* Synchronizing extension files across management servers
* Downloading extension files as an archive
* Secure file sharing via Secondary Storage (SSVM) when direct access to a
  management server is not possible

These capabilities are available via new APIs and UI actions.

Share Endpoint Configuration
----------------------------

Extension download and synchronization workflows rely on the management
server's **share endpoint**, which enables controlled file sharing.

The share endpoint is configured in ``server.properties`` and allows
administrators to enable or disable file sharing, define the base directory,
configure cache behavior, and secure download links.

Share Endpoint Properties
~~~~~~~~~~~~~~~~~~~~~~~~~

.. cssclass:: table-striped table-bordered table-hover

+----------------------+----------------------------------------------+---------------------------------------------+
| Property             | Default Value                                | Description                                 |
+======================+==============================================+=============================================+
| share.enabled        | true                                         | Enables or disables the file sharing        |
|                      |                                              | feature. Must be ``true`` for extension     |
|                      |                                              | downloads to function.                      |
+----------------------+----------------------------------------------+---------------------------------------------+
| share.base.dir       | <HOME_DIRECTORY_OF_CLOUD_USER>/share         | Base directory from which files can be      |
|                      |                                              | shared. If not explicitly set, the default  |
|                      |                                              | directory under the CloudStack user home    |
|                      |                                              | is used.                                    |
+----------------------+----------------------------------------------+---------------------------------------------+
| share.cache.control  | public,max-age=86400,immutable               | Cache-Control header value applied to       |
|                      |                                              | shared files. Controls browser/client       |
|                      |                                              | caching behavior.                           |
+----------------------+----------------------------------------------+---------------------------------------------+
| share.secret         | change-me                                    | Secret key used to generate HMAC-signed     |
|                      |                                              | download links. It is strongly recommended  |
|                      |                                              | to change this value in production. If not  |
|                      |                                              | set, links will not be signed.              |
+----------------------+----------------------------------------------+---------------------------------------------+

Notes:

* ``share.enabled`` must be ``true`` for extension downloads to function.
* If ``share.secret`` is configured, generated links are signed using HMAC.
* It is strongly recommended to replace the default ``share.secret`` value
  in production environments.
* If ``share.secret`` is not configured, download links will not be signed.

Extension Synchronization
^^^^^^^^^^^^^^^^^^^^^^^^^

In a multi-node management server cluster, extension files are stored locally
on each management server. If an extension is installed or modified on one
node, it must be synchronized to peers.

syncExtension API
~~~~~~~~~~~~~~~~~

The ``syncExtension`` API triggers synchronization of a selected extension
across all management servers in the cluster.

How It Works
~~~~~~~~~~~~

1. The source management server:

   * Calculates checksums for all files in the extension directory.
   * Packages the extension directory (or selected files) into a ``.tgz`` archive.

2. The server sends a ``DownloadAndSyncExtensionFilesCommand`` to peer
   management servers.

3. Each peer management server:

   * Downloads the archive.
   * Stages it temporarily.
   * Extracts the files into the extension directory.
   * Validates checksums.
   * Cleans up temporary files.

Checksum Validation
~~~~~~~~~~~~~~~~~~~

Checksums are calculated for all files in the extension directory and compared
during synchronization. This ensures:

* File integrity
* Detection of missing or modified files
* Cluster-wide consistency

UI Support
~~~~~~~~~~

In the CloudStack UI:

1. Navigate to **Extensions**
2. Select an extension
3. Click **Sync Extension**

This triggers synchronization across all management servers.

Downloading Extension Files
^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can download an extension’s files as an archive for backup, inspection,
or migration.

downloadExtension API
~~~~~~~~~~~~~~~~~~~~~

The ``downloadExtension`` API allows administrators to download the complete
extension directory as a ``.zip`` archive.

How It Works
~~~~~~~~~~~~

1. The management server creates a ``.zip`` archive of the extension directory.
2. A secure share URL is generated.
3. The administrator downloads the archive using the signed URL.

Secure Share URL
~~~~~~~~~~~~~~~~

Download URLs are:

* Signed using HMAC
* Time-bound (expire automatically)
* Cleaned up after expiry

The validity interval is controlled via the global configuration:

.. code-block:: text

   extension.share.link.validity.interval

This defines how long (in seconds) the signed URL remains valid before
automatic cleanup.

Download via Secondary Storage (SSVM)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In some environments, a management server may not be directly accessible from
the administrator’s network.

To support this scenario:

* The archive can be staged on Secondary Storage.
* The signed URL points to the SSVM endpoint.
* The file is served via Secondary Storage instead of directly from the
  management server.

Global Configuration
~~~~~~~~~~~~~~~~~~~~

To force downloads via Secondary Storage:

.. code-block:: text

   extension.share.download.use.secondary.storage = true

When set to ``true``, extension downloads are always served via Secondary
Storage (SSVM).

When set to ``false`` (default), downloads are served directly from the
selected management server.

Global Configuration Parameters
--------------------------------

.. cssclass:: table-striped table-bordered table-hover

+------------------------------------------------+---------------+-----------------------------------------+
| Name                                           | Default Value | Description                             |
+================================================+===============+=========================================+
| extension.share.download.use.secondary.storage | false         | If ``true``, forces extension downloads |
|                                                |               | via Secondary Storage (SSVM).           |
+------------------------------------------------+---------------+-----------------------------------------+
| extension.share.link.validity.interval         | 3600          | Validity duration (in seconds) of the   |
|                                                |               | signed download URL.                    |
+------------------------------------------------+---------------+-----------------------------------------+

Events and Logging
------------------

The following improvements are included:

* Dedicated events for sync and download operations
* Improved logging for archive creation, transfer, extraction, and cleanup
* Automatic cleanup of temporary share files after expiry

These changes improve traceability and operational visibility.

Archive Formats
---------------

.. cssclass:: table-striped table-bordered table-hover

+---------------+----------+
| Operation     | Format   |
+===============+==========+
| Synchronize   | ``.tgz`` |
+---------------+----------+
| Download      | ``.zip`` |
+---------------+----------+

The use of ``.tgz`` for synchronization ensures efficient transfer between
management servers, while ``.zip`` is used for administrator downloads for
broad compatibility.

Typical Workflows
^^^^^^^^^^^^^^^^^

Synchronize Extension Across Cluster
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Install or update the extension on one management server.
2. Call the ``syncExtension`` API or use **Sync Extension** in the UI.
3. Verify synchronization across all nodes.

Download Extension for Backup or Migration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Call the ``downloadExtension`` API or use **Download Extension** in the UI.
2. Use the generated signed URL.
3. Download the ``.zip`` archive before the URL expires.

Best Practices
^^^^^^^^^^^^^^

* Always synchronize extensions after modifying files on a single management
  server in a clustered setup.
* Use Secondary Storage download mode when management servers are behind
  private networks.
* Monitor management server logs for sync failures due to permission or
  filesystem issues.
* Adjust ``extension.share.link.validity.interval`` according to your
  operational security requirements.
