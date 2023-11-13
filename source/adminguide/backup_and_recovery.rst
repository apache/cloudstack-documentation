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

About Backup And Recovery
--------------------------

CloudStack version 4.14 introduces a new Backup and Recovery (B&R) framework that
provides CloudStack with users the ability to back up their Guest Instances for recovery
purposes via 3rd party backup solutions.  The framework abstracts the API commands
required for common backup and recovery
operations, from the vendor specific commands needed to perform those actions and provides
a plugin model to enable any solution which provides backup and recovery 'like'
features to be integrated.

The following providers are currently supported:

- VMware with Veeam Backup and Recovery
- KVM with DELL EMC Networker

See the Veeam Backup and Recovery plugin documentation for plugin specific information.
:ref:`Veeam Backup and Recovery Plugin`

See the DELL EMC Networker Backup and Recovery plugin documentation for plugin specific information.
:ref:`DELL EMC Networker Backup and Recovery Plugin`


Backup and Recovery Concepts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Backup and recovery has been designed to support two modes:

- ‘SLA’ based backups

- Adhoc and user scheduled backups

'SLA' based backups are ones where the Cloud provider (ie the root admin) controls the time, and frequency of a backup scheme.
A user signs up for a 'Gold' offering, which might give them a RPO of 12 hours and the last 14 backups kept; however the user would not be
allowed to perform additional backups nor set the exact time that these backups took place.  The user might be charged
a fix rate for these backups regardless of the size of the backups.

To use an SLA based backup policy the user adds their Instances to the offering/policy.  The job then runs at its predetermined times and 'includes' the
Instance when it runs. A user can remove the Instance from the offering/policy and it will no longer be included in the job when it runs.

Adhoc and user scheduled backups follow the same idea as Volume Snapshots, however they leverage the backup solution
rather than secondary storage.  These could likely be billed on backup storage consumed or protected capacity (the full virtual
size of the Instance(s) being backed up.

Adhoc and user scheduled backups are created and managed in the same fashion as Volume Snapshots are.


Configuring Backup and Recovery
--------------------------------

The cloud administrator can use global configuration variables to
control the behavior of B&R feature. To set these variables, go through
the Global Settings area of the CloudStack UI.

.. cssclass:: table-striped table-bordered table-hover

================================= ========================
Configuration                     Description
================================= ========================
backup.framework.enabled          Setting to enable or disable the feature. Default: false.
backup.framework.provider.plugin  The backup provider (plugin) name. For example: 'dummy', 'veeam' and 'networker'. This is a zone specific setting. Default: dummy.
backup.framework.sync.interval    Background sync task internal in seconds that performs metrics/usage stats collection, backup reconciliation and backup scheduling. Default: 300.
================================= ========================

Plugin specific settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each backup and recovery plugin is likely to have settings specific to that plugin.  Refer to the CloudStack documentation
for your plugin for details on how to configure those settings.


Backup Offerings
------------------

Admins can import an external provider's backup offerings using UI or API for a
particular zone, as well as manage a backup offering's lifecyle. Admins can also
specify if a backup offering allows user-defined backup schedules and ad-hoc
backups. Users can list and consume the imported backup offerings, only root admins can import or
delete offerings.

Supported APIs:
~~~~~~~~~~~~~~~~

- **listBackupProviders**: lists available backup provider plugins
- **listBackupProviderOfferings**: lists external backup policy/offering from a provider
- **importBackupOffering**: allows importing of an external backup policy/offering to CloudStack as a backup offering
- **listBackupOfferings**: lists CloudStack's backup offerings (searching via keyword, and pagination supported)
- **deleteBackupOffering**: deletes a backup offering by its ID

Importing Backup Offerings
-----------------------------

See plugin specific documentation to create 'Backup provider offerings'

To import a backup provider offering;

#. (As root) navigate to Service Offerings, click on the 'select offering' dropdown box and select 'Backup Offerings'
#. Click on Import Backup Offering
#. Enter your user-friendly name and description and select the applicable zone.  The External ID will then be populated with the
   Template jobs which CloudStack retrieves from the connected provider.

   |B&R-backup_offering_policy.png|  |B&R-backup_offering.png|

Creating Instance Backups
-------------------------

SLA/Policy Based backups
~~~~~~~~~~~~~~~~~~~~~~~~~

With the backup and recovery feature enabled for a zone, users simply add and
remove an Instance from a backup offering.

|B&R-assignOffering.png|

Adhoc and Scheduled Backups
~~~~~~~~~~~~~~~~~~~~~~~~~~~

For backup offerings that allow ad-hoc user backups and user-defined backup
schedules, user will be allowed to define a backup schedule for an Instance that is
assigned to a backup offering using UI and API. An Instance with backup will not be
allowed to add/remove volumes similar to Instance Snapshots.

To trigger an adhoc backup of an Instance, navigate to the Instance and click on the 'Create Backup'
icon.

|B&R-createBackup.png|

To setup a recurring backup schedule, navigate to the Instance and click on the 'Backup Schedule'
icon.

|B&R-BackupSchedule.png|

Then set the time and frequency of the backups, click 'Configure' and then 'Close'

|B&R-BackupScheduleEntry.png|

Restoring Instance Backups
--------------------------

Users will need to stop an Instance to restore to any existing Instance backup, restoration
of an expunged Instance will not restore nics and recovery any network which may/may
not exist. User may however restore a specific volume from an Instance backup and attach
that volume to a specified Instance.

Supported APIs:
~~~~~~~~~~~~~~~~

- **assignVirtualMachineToBackupOffering**: adds an Instance to a backup offering.
- **removeVirtualMachineFromBackupOffering**: removes an Instance from a backup offering, if forced `true` parameter is passed this may also
  remove any and all the backups of an Instance associated with a backup offering.
- **createBackupSchedule**: creates a backup schedule for an Instance.
- **updateBackupSchedule**: updates backup schedule.
- **listBackupSchedule**: returns backup schedule of an Instance if defined.
- **deleteBackupSchedule**: deletes backup schedule of an Instance.
- **createBackup**: creates an adhoc backup for an Instance.
- **deleteBackup**: deletes an Instance backup (not support for per restore point for Veeam).
- **listBackups**: lists backups.
- **restoreBackup**: restore a previous Instance backup in-place of a stopped or destroyed Instance.
- **restoreVolumeFromBackupAndAttachToVM**: restore and attach a backed-up volume (of an Instance backup) to a specified Instance.


.. |B&R-assignOffering.png| image:: /_static/images/B&R-assignOffering.png
   :alt: Assigning an SLA/Policy to an Instance.
   :width: 400 px
.. |B&R-backup_offering_policy.png| image:: /_static/images/B&R-backup_offering_policy.png
   :alt: Importing an SLA/Policy offering.
   :width: 300 px
.. |B&R-backup_offering.png| image:: /_static/images/B&R-backup_offering.png
   :alt: Importing a Template backup offering.
   :width: 300 px
.. |B&R-createBackup.png| image:: /_static/images/B&R-createBackup.png
   :alt: Triggering an adhoc backup for an Instance.
   :width: 400 px
.. |B&R-BackupSchedule.png| image:: /_static/images/B&R-BackupSchedule.png
   :alt: Creating a backup schedule for an Instance.
   :width: 400 px
.. |B&R-BackupScheduleEntry.png| image:: /_static/images/B&R-BackupScheduleEntry.png
   :alt: Creating a backup schedule for an Instance.
   :width: 400px
