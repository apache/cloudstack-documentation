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

.. _KVM with Veeam Backup and Replication:

KVM with Veeam Backup and Replication
=====================================

About the KVM with Veeam Backup and Replication
-----------------------------------------------
Starting with 4.23.0 release, support has been added for integrating
KVM-based CloudStack environments with Veeam Backup & Replication. This
integration allows CloudStack-managed KVM virtual machines to be discovered
and protected by Veeam, enabling organizations to use Veeam's backup
infrastructure for data protection and recovery.

The integration exposes a compatibility layer that allows Veeam to interact
with CloudStack in a manner similar to environments managed by platforms such
as oVirt. Through this interface, Veeam can discover infrastructure resources
such as datacenters, clusters, hosts, and virtual machines, and perform
backup and restore operations using its standard workflows.

At present, backup and restore operations are supported only for the
following storage types:

- NFS
- Local storage
- SharedMountPoint

Backup and restore operations are currently supported for user instances
only. Similar to other backup providers in CloudStack, system VMs (for
example, VR, CPVM, SSVM, and other infrastructure VMs) are not considered
by this integration.

With this capability, administrators can:

- Configure CloudStack as a virtualization manager within Veeam.
- Discover KVM hosts and virtual machines managed by CloudStack.
- Perform VM backups and restores directly from the Veeam Backup & Replication console.
- Leverage Veeam features such as scheduled backups, retention policies, and recovery operations.

It is important to note that backup and restore operations are managed
entirely from the Veeam side. CloudStack does not currently provide a native
user interface or self-service capability for triggering or managing backups.
This is because CloudStack does not communicate directly with the Veeam UHAPI
manager for backup orchestration.

As a result, self-service backup and restore functionality within CloudStack
is not available in this release. All backup configuration, execution, and
recovery workflows must be initiated and managed through the Veeam Backup &
Replication platform.

This integration provides a foundation for using enterprise-grade backup
tooling with CloudStack-managed KVM environments while maintaining
compatibility with Veeam's existing workflows and management interfaces.

Configuring CloudStack as Hypervisor Manager in Veeam Backup & Replication
---------------------------------------------------------------------------

To allow **Veeam Backup & Replication** to discover and protect virtual machines
running on **Apache CloudStack** KVM environments, the CloudStack Veeam Control
Service must first be enabled and configured. Once configured, CloudStack can
be added as a hypervisor manager within Veeam.

1. Configure the CloudStack Veeam Control Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack exposes a control service that allows Veeam to communicate with the
CloudStack-managed KVM infrastructure. This service must be enabled and
configured using CloudStack global configuration parameters.

Update the following global configuration values in CloudStack:

+------------------------------------------------+-------------------------------------------------------------+
| Configuration Key                              | Description                                                 |
+================================================+=============================================================+
| integration.veeam.control.enabled              | Enables the CloudStack Veeam Control Service.               |
+------------------------------------------------+-------------------------------------------------------------+
| integration.veeam.control.bind.address         | IP address on which the control service listens.            |
+------------------------------------------------+-------------------------------------------------------------+
| integration.veeam.control.port                 | Port used by the service.                                   |
+------------------------------------------------+-------------------------------------------------------------+
| integration.veeam.control.api.username         | Username used by Veeam to authenticate with the service.    |
+------------------------------------------------+-------------------------------------------------------------+
| integration.veeam.control.api.password         | Password used by Veeam to authenticate with the service.    |
+------------------------------------------------+-------------------------------------------------------------+
| integration.veeam.control.allowed.client.cidrs | Comma-separated list of CIDR blocks representing clients    |
|                                                | allowed to access the API. If empty, all clients will be    |
|                                                | allowed. Example: 192.168.1.1/24,192.168.2.100/32           |
+------------------------------------------------+-------------------------------------------------------------+

These parameters can be configured from the **Global Settings** section of the
CloudStack UI or using the CloudStack API.

After updating the desired values, **restart the CloudStack management
server(s)** for the changes to take effect.

The CloudStack environment must have SSL enabled on the management server so
that it can be added in Veeam as a KVM hypervisor manager.

For instructions on enabling HTTPS/SSL on the management server, see:
`SSL (Optional) <installguide/optional_installation.html#ssl-optional>`_.

2. Verify the CloudStack Veeam Control Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once the management server has restarted, verify that the service is accessible.

You can test the service using ``curl`` from a machine that can reach the
CloudStack management server.

Example::

    curl -k -u <username>:<password> \
    https://<cloudstack-management-ip>:<port>/<context-path>/api

If the service is configured correctly, the request should return a valid
response from the CloudStack Veeam control API.

This confirms that the API endpoints required by Veeam are reachable.

3. Add CloudStack in Veeam Backup & Replication
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
   **CloudStack KVM** is not currently available as a native hypervisor manager type in Veeam Backup & Replication.
   For testing purposes, the **oVirt KVM** hypervisor manager can be used to connect to CloudStack environments.
   When adding a new manager in Veeam, select **oVirt KVM** as the type and provide the CloudStack management server details.

   This workaround is for testing only until native support for CloudStack KVM is introduced in a future Veeam Backup & Replication release.
   There is no upgrade path for CloudStack environments added as **oVirt KVM** managers.
   After native CloudStack KVM support becomes available, the existing manager must be removed and re-added using the native CloudStack KVM manager type.

After confirming that the CloudStack control service is operational, CloudStack
can be added as a hypervisor manager in Veeam.

1. Open the **Veeam Backup & Replication Console**.
2. Navigate to **Inventory**.
3. Select **CloudStack KVM**.
4. Click **Add Manager**.
5. Enter the CloudStack server details:

   - **Server address**: CloudStack management server address.
   - **Port**: The configured control service port.
   - **Credentials**: The username and password configured earlier in
     CloudStack (``integration.veeam.control.api.username`` and
     ``integration.veeam.control.api.password``).

6. Complete the wizard to add the manager.

Once the manager is successfully added, Veeam will connect to CloudStack,
discover the infrastructure resources, and make the virtual machines available
for backup and restore operations.

Backup Proxy or Worker VM for Veeam Backup and Replication
----------------------------------------------------------

A **worker VM** (also referred to as a backup proxy by Veeam) is required by
**Veeam Backup & Replication** to perform backup and restore operations in a
CloudStack KVM environment.

The worker VM is responsible for:

* Performing data transfer during backup and restore operations.
* Communicating with the **CloudStack Veeam Control Service** to discover
  infrastructure resources and coordinate backup activities.
* Interacting with the KVM hypervisor hosts to read or write VM disk data.

Because of these responsibilities, the worker VM must be deployed in a network
that has connectivity to both:

* The **CloudStack management server** running the Veeam Control Service.
* The **KVM hypervisor hosts** that store and run the virtual machines.

One approach is to create a **shared network** within the **management traffic
range** configured in CloudStack. The worker VM can then be deployed on this
network so that it can communicate with both the management server and the
hypervisor hosts.

The following considerations should be taken into account when deploying the
worker VM:

* The **service account** configured for the CloudStack Veeam Control Service
  should have permission to deploy and access virtual machines in the selected
  network.
* The worker VM should use an appropriate **compute offering** depending on the
  resources allocated for the backup proxy in Veeam Backup & Replication.
* If multiple backup proxies are required for scaling backup operations,
  additional worker VMs can be deployed using similar network and compute
  configurations.

.. note::
   If worker VM deployment fails, especially due to network connectivity
   issues, worker VMs may remain in a **Stopped** state in CloudStack.
   To clean up undesired worker VMs, in **Veeam Backup & Replication** go to
   **Backup Infrastructure** > **Backup Proxies** and use the **Delete**
   operation.

The sizing of worker VMs, job concurrency, and deployment of multiple proxies
should follow the recommendations provided in the Veeam documentation. A
compute offering corresponding to the compute resources configured for the
worker VM must exist in CloudStack. This can be a custom offering, and
CloudStack will try to use one matching the configured vCPU and memory.

Refer to the official Veeam documentation for further details:

https://helpcenter.veeam.com/


Instance Backup using Veeam Backup and Replication
--------------------------------------------------

For a KVM instance to be accessible for backup in **Veeam Backup & Replication (Veeam B&R)**,
the instance must be visible and accessible to the **service account** configured for the
CloudStack Veeam Control Service.

Once CloudStack has been added as a hypervisor manager in Veeam B&R, instances managed by
CloudStack will appear in the Veeam inventory. Backup jobs can then be created and managed
in the same way as with other supported hypervisor managers.

Backup jobs in Veeam B&R may be configured as:

* **Manual backups** triggered on demand.
* **Scheduled backups** configured with a recurring schedule.
* **Policy-based backups** depending on the configuration defined in Veeam.

CloudStack itself **does not track or manage backup jobs** initiated by Veeam B&R. All job
configuration, scheduling, monitoring, and retention management are handled entirely from
the Veeam Backup & Replication platform.

Using Tags for Backup Jobs
~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack instance tags can be used to organize and select virtual machines for backup
jobs within Veeam B&R.

For a CloudStack instance tag to be recognized by Veeam, the tag key must be prefixed with
``veeam_tag``.

Example:

::

   key   = veeam_tag_environment
   value = production

In this example, Veeam B&R will interpret the tag simply as:

::

   production

Only the **value portion** of the CloudStack tag is considered by Veeam when creating or
selecting tags for backup jobs. The key prefix (``veeam_tag``) is used only to identify
tags intended for Veeam integration.

This mechanism allows administrators to control which instances are grouped together for
backup operations by assigning appropriate tags within CloudStack.

Instance Metadata in Backups
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

During backup operations, Veeam B&R stores important **instance metadata** in addition to
the VM disk data. This metadata may include details such as instance configuration and
environment-specific information required to reconstruct the instance.

When a backup is restored back into the **same CloudStack environment**, the CloudStack
Veeam integration plugin uses this stored metadata to recreate the instance with the
appropriate configuration where possible.


Instance Restore using Veeam Backup and Replication
---------------------------------------------------

Restore operations for instances backed up through **Veeam Backup & Replication (Veeam B&R)** are initiated from the Veeam console. The restore workflow recreates the virtual machine in CloudStack using the metadata and disk data stored during backup.

The restore process works as follows:

* A **new instance is deployed in CloudStack** as part of the restore workflow. Restore operations do not overwrite an existing instance.
* Initially, a **blank instance** is created by the CloudStack Veeam integration plugin.
* After the instance is created, **volumes and network interfaces are attached sequentially** based on the metadata stored in the backup.
* The VM disks are then restored from the backup data into the attached volumes.

All restore-related operations are executed using the **service account configured for the CloudStack Veeam Control Service**. Because of this, the service account must have sufficient permissions to perform the following actions:

* Deploy new instances.
* Attach volumes.
* Access and attach networks selected during the restore process.

If the service account does not have access to the networks selected in the **Veeam restore wizard**, the restore operation may fail.

The plugin reconstructs the instance networking configuration using the metadata saved during backup. This ensures that the restored instance closely resembles the original instance configuration where possible.

Compute Offering Selection
~~~~~~~~~~~~~~~~~~~~~~~~~~

During restore, the CloudStack Veeam integration plugin determines an appropriate **compute offering** for the restored instance based on the compute characteristics stored in the backup metadata. This typically includes parameters such as CPU and memory.

The plugin attempts to match these characteristics with an available compute offering in the CloudStack environment. If an exact match is not found, the closest suitable compute offering may be selected.

Network Reconstruction
~~~~~~~~~~~~~~~~~~~~~~

**Networks** are attached to the restored instance in the same order and configuration as recorded in the backup metadata.

If one or more original networks cannot be attached during restore (for example, due to permission or capacity constraints), the instance is created without those networks and the restore process continues. Administrators can manually attach the missing networks after restore. To better handle such scenarios, it is recommended to restore instances without powering them on immediately.

Volume Reconstruction
~~~~~~~~~~~~~~~~~~~~~

**Volumes** are created and restored from the backup data and then attached to the instance.

Restored volumes are always assigned an available custom disk offering. If needed, administrators can manually change the disk offering after the restore operation completes.


Assigning Restored Instances to Original Owners
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

By default, restored instances are deployed using the **service account** configured for the CloudStack Veeam Control Service. This ensures that restore operations can proceed even if the original account or network access constraints would otherwise prevent deployment.

If it is desired that the restored instance should instead be **assigned to the original account based on the instance metadata stored in the backup**, the following global configuration can be enabled:

::

   integration.veeam.control.instance.restore.assign.owner = true

When this configuration is enabled, the plugin will attempt to deploy the restored instance under the **original account ownership** and apply network access based on that account’s permissions.

This configuration is **dynamic**, meaning it can be updated without restarting the management server and adjusted based on operational requirements.

Restore Limitations
~~~~~~~~~~~~~~~~~~~

* Restore operations always result in **deployment of a new instance** rather than restoring an existing instance in place.
* All restore operations must be initiated from **Veeam Backup & Replication**.
* CloudStack does not maintain state or visibility of backup or restore jobs executed through Veeam.

