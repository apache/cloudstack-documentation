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
   
.. _working-with-usage:

Working with Usage
==================

The Usage Server is an optional, separately-installed part of CloudStack
that provides aggregated usage records which you can use to create
billing integration for CloudStack. The Usage Server works by taking
data from the events log and creating summary usage records that you can
access using the listUsageRecords API call.

The usage records show the amount of resources, such as VM run time or
template storage space, consumed by guest instances.

The Usage Server runs at least once per day. It can be configured to run
multiple times per day.


Configuring the Usage Server
----------------------------

To configure the usage server:

#. Be sure the Usage Server has been installed. This requires extra
   steps beyond just installing the CloudStack software. See Installing
   the Usage Server (Optional) in the Advanced Installation Guide.

#. Log in to the CloudStack UI as administrator.

#. Click Global Settings.

#. In Search, type usage. Find the configuration parameter that controls
   the behavior you want to set. See the table below for a description
   of the available parameters.

#. In Actions, click the Edit icon.

#. Type the desired value and click the Save icon.

#. Restart the Management Server (as usual with any global configuration
   change) and also the Usage Server:

   .. code:: bash

      # service cloudstack-management restart
      # service cloudstack-usage restart

The following table shows the global configuration settings that control
the behavior of the Usage Server.

Parameter Name  Description

enable.usage.server  Whether the Usage Server is active.

usage.aggregation.timezone

Time zone of usage records. Set this if the usage records and daily job
execution are in different time zones. For example, with the following
settings, the usage job will run at PST 00:15 and generate usage records
for the 24 hours from 00:00:00 GMT to 23:59:59 GMT:

.. code:: bash

   usage.stats.job.exec.time = 00:15   
   usage.execution.timezone = PST
   usage.aggregation.timezone = GMT

Valid values for the time zone are specified in the :ref:`time-zones` section

Default: GMT

usage.execution.timezone

The time zone of usage.stats.job.exec.time. Valid values for the time
zone are specified in the :ref:`time-zones` section

Default: The time zone of the management server.

usage.sanity.check.interval

The number of days between sanity checks. Set this in order to
periodically search for records with erroneous data before issuing
customer invoices. For example, this checks for VM usage records created
after the VM was destroyed, and similar checks for templates, volumes,
and so on. It also checks for usage times longer than the aggregation
range. If any issue is found, the alert
ALERT\_TYPE\_USAGE\_SANITY\_RESULT = 21 is sent.

usage.stats.job.aggregation.range

The time period in minutes between Usage Server processing jobs. For
example, if you set it to 1440, the Usage Server will run once per day.
If you set it to 600, it will run every ten hours. In general, when a
Usage Server job runs, it processes all events generated since usage was
last run.

There is special handling for the case of 1440 (once per day). In this
case the Usage Server does not necessarily process all records since
Usage was last run. CloudStack assumes that you require processing once
per day for the previous, complete day’s records. For example, if the
current day is October 7, then it is assumed you would like to process
records for October 6, from midnight to midnight. CloudStack assumes
this “midnight to midnight” is relative to the usage.execution.timezone.

Default: 1440

usage.stats.job.exec.time

The time when the Usage Server processing will start. It is specified in
24-hour format (HH:MM) in the time zone of the server, which should be
GMT. For example, to start the Usage job at 10:30 GMT, enter “10:30”.

If usage.stats.job.aggregation.range is also set, and its value is not
1440, then its value will be added to usage.stats.job.exec.time to get
the time to run the Usage Server job again. This is repeated until 24
hours have elapsed, and the next day's processing begins again at
usage.stats.job.exec.time.

Default: 00:15.

For example, suppose that your server is in GMT, your user population is
predominantly in the East Coast of the United States, and you would like
to process usage records every night at 2 AM local (EST) time. Choose
these settings:

-  enable.usage.server = true

-  usage.execution.timezone = America/New\_York

-  usage.stats.job.exec.time = 07:00. This will run the Usage job at
   2:00 AM EST. Note that this will shift by an hour as the East Coast
   of the U.S. enters and exits Daylight Savings Time.

-  usage.stats.job.aggregation.range = 1440

With this configuration, the Usage job will run every night at 2 AM EST
and will process records for the previous day’s midnight-midnight as
defined by the EST (America/New\_York) time zone.

.. note:: 
   Because the special value 1440 has been used for
   usage.stats.job.aggregation.range, the Usage Server will ignore the data
   between midnight and 2 AM. That data will be included in the next day's
   run.


Setting Usage Limits
--------------------

CloudStack provides several administrator control points for capping
resource usage by users. Some of these limits are global configuration
parameters. Others are applied at the ROOT domain and may be overridden
on a per-account basis.


Globally Configured Limits
~~~~~~~~~~~~~~~~~~~~~~~~~~

In a zone, the guest virtual network has a 24 bit CIDR by default. This
limits the guest virtual network to 254 running instances. It can be
adjusted as needed, but this must be done before any instances are
created in the zone. For example, 10.1.1.0/22 would provide for ~1000
addresses.

The following table lists limits set in the Global Configuration:

.. cssclass:: table-striped table-bordered table-hover

+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter Name            | Definition                                                                                                                                                                                                                                                                                       |
+===========================+==================================================================================================================================================================================================================================================================================================+
| max.account.public.ips    | Number of public IP addresses that can be owned by an account                                                                                                                                                                                                                                    |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| max.account.snapshots     | Number of snapshots that can exist for an account                                                                                                                                                                                                                                                |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| max.account.templates     | Number of templates that can exist for an account                                                                                                                                                                                                                                                |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| max.account.user.vms      | Number of virtual machine instances that can exist for an account                                                                                                                                                                                                                                |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| max.account.volumes       | Number of disk volumes that can exist for an account                                                                                                                                                                                                                                             |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| max.template.iso.size     | Maximum size for a downloaded template or ISO in GB                                                                                                                                                                                                                                              |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| max.volume.size.gb        | Maximum size for a volume in GB                                                                                                                                                                                                                                                                  |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| network.throttling.rate   | Default data transfer rate in megabits per second allowed per user (supported on XenServer)                                                                                                                                                                                                      |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| snapshot.max.hourly       | Maximum recurring hourly snapshots to be retained for a volume. If the limit is reached, early snapshots from the start of the hour are deleted so that newer ones can be saved. This limit does not apply to manual snapshots. If set to 0, recurring hourly snapshots can not be scheduled     |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| snapshot.max.daily        | Maximum recurring daily snapshots to be retained for a volume. If the limit is reached, snapshots from the start of the day are deleted so that newer ones can be saved. This limit does not apply to manual snapshots. If set to 0, recurring daily snapshots can not be scheduled              |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| snapshot.max.weekly       | Maximum recurring weekly snapshots to be retained for a volume. If the limit is reached, snapshots from the beginning of the week are deleted so that newer ones can be saved. This limit does not apply to manual snapshots. If set to 0, recurring weekly snapshots can not be scheduled       |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| snapshot.max.monthly      | Maximum recurring monthly snapshots to be retained for a volume. If the limit is reached, snapshots from the beginning of the month are deleted so that newer ones can be saved. This limit does not apply to manual snapshots. If set to 0, recurring monthly snapshots can not be scheduled.   |
+---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

To modify global configuration parameters, use the global configuration
screen in the CloudStack UI. See Setting Global Configuration Parameters


Limiting Resource Usage
~~~~~~~~~~~~~~~~~~~~~~~

CloudStack allows you to control resource usage based on the types of
resources, such as CPU, RAM, Primary storage, and Secondary storage. A
new set of resource types has been added to the existing pool of
resources to support the new customization model—need-basis usage, such
as large VM or small VM. The new resource types are now broadly
classified as CPU, RAM, Primary storage, and Secondary storage. The root
administrator is able to impose resource usage limit by the following
resource types for Domain, Project, and Accounts.

-  CPUs

-  Memory (RAM)

-  Primary Storage (Volumes)

-  Secondary Storage (Snapshots, Templates, ISOs)

To control the behaviour of this feature, the following configuration
parameters have been added:

.. cssclass:: table-striped table-bordered table-hover

=================================== =================================================================
Parameter Name                      Description
=================================== =================================================================
max.account.cpus                    Maximum number of CPU cores that can be used for an account.
                                    Default is 40.
max.account.ram (MB)                Maximum RAM that can be used for an account.
                                    Default is 40960.
max.account.primary.storage (GB)    Maximum primary storage space that can be used for an account.
                                    Default is 200.
max.account.secondary.storage (GB)  Maximum secondary storage space that can be used for an account.
                                    Default is 400.
max.project.cpus                    Maximum number of CPU cores that can be used for an account.
                                    Default is 40.
max.project.ram (MB)                Maximum RAM that can be used for an account.
                                    Default is 40960.
max.project.primary.storage (GB)    Maximum primary storage space that can be used for an account.
                                    Default is 200.
max.project.secondary.storage (GB)  Maximum secondary storage space that can be used for an account.
                                    Default is 400.
=================================== =================================================================


User Permission
~~~~~~~~~~~~~~~

The root administrator, domain administrators and users are able to list
resources. Ensure that proper logs are maintained in the ``vmops.log``
and ``api.log`` files.

-  The root admin will have the privilege to list and update resource
   limits.

-  The domain administrators are allowed to list and change these
   resource limits only for the sub-domains and accounts under their own
   domain or the sub-domains.

-  The end users will the privilege to list resource limits. Use the
   listResourceLimits API.


Limit Usage Considerations
~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Primary or Secondary storage space refers to the stated size of the
   volume and not the physical size— the actual consumed size on disk in
   case of thin provisioning.

-  If the admin reduces the resource limit for an account and set it to
   less than the resources that are currently being consumed, the
   existing VMs/templates/volumes are not destroyed. Limits are imposed
   only if the user under that account tries to execute a new operation
   using any of these resources. For example, the existing behavior in
   the case of a VM are:

   -  migrateVirtualMachine: The users under that account will be able
      to migrate the running VM into any other host without facing any
      limit issue.

   -  recoverVirtualMachine: Destroyed VMs cannot be recovered.

-  For any resource type, if a domain has limit X, sub-domains or
   accounts under that domain can have there own limits. However, the
   sum of resource allocated to a sub-domain or accounts under the
   domain at any point of time should not exceed the value X.

   For example, if a domain has the CPU limit of 40 and the sub-domain
   D1 and account A1 can have limits of 30 each, but at any point of
   time the resource allocated to D1 and A1 should not exceed the limit
   of 40.

-  If any operation needs to pass through two of more resource limit
   check, then the lower of 2 limits will be enforced, For example: if
   an account has the VM limit of 10 and CPU limit of 20, and a user
   under that account requests 5 VMs of 4 CPUs each. The user can deploy
   5 more VMs because VM limit is 10. However, the user cannot deploy
   any more instances because the CPU limit has been exhausted.


Limiting Resource Usage in a Domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack allows the configuration of limits on a domain basis. With a
domain limit in place, all users still have their account limits. They
are additionally limited, as a group, to not exceed the resource limits
set on their domain. Domain limits aggregate the usage of all accounts
in the domain as well as all the accounts in all the sub-domains of that
domain. Limits set at the root domain level apply to the sum of resource
usage by the accounts in all the domains and sub-domains below that root
domain.

To set a domain limit:

#. Log in to the CloudStack UI.

#. In the left navigation tree, click Domains.

#. Select the domain you want to modify. The current domain limits are
   displayed.

   A value of -1 shows that there is no limit in place.

#. Click the Edit button |editbutton.png|

#. Edit the following as per your requirement:

   -  Parameter Name

   -  Description

   -  Instance Limits

      The number of instances that can be used in a domain.

   -  Public IP Limits

      The number of public IP addresses that can be used in a domain.

   -  Volume Limits

      The number of disk volumes that can be created in a domain.

   -  Snapshot Limits

      The number of snapshots that can be created in a domain.

   -  Template Limits

      The number of templates that can be registered in a domain.

   -  VPC limits

      The number of VPCs that can be created in a domain.

   -  CPU limits

      The number of CPU cores that can be used for a domain.

   -  Memory limits (MB)

      The number of RAM that can be used for a domain.

   -  Primary Storage limits (GB)

      The primary storage space that can be used for a domain.

   -  Secondary Storage limits (GB)

      The secondary storage space that can be used for a domain.

#. Click Apply.


Default Account Resource Limits
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can limit resource use by accounts. The default limits are set by
using Global configuration parameters, and they affect all accounts
within a cloud. The relevant parameters are those beginning with
max.account, for example: max.account.snapshots.

To override a default limit for a particular account, set a per-account
resource limit.

#. Log in to the CloudStack UI.

#. In the left navigation tree, click Accounts.

#. Select the account you want to modify. The current limits are
   displayed.

   A value of -1 shows that there is no limit in place.

#. Click the Edit button. |editbutton.png|

#. Edit the following as per your requirement:

   -  Parameter Name

   -  Description

   -  Instance Limits

      The number of instances that can be used in an account.

      The default is 20.

   -  Public IP Limits

      The number of public IP addresses that can be used in an account.

      The default is 20.

   -  Volume Limits

      The number of disk volumes that can be created in an account.

      The default is 20.

   -  Snapshot Limits

      The number of snapshots that can be created in an account.

      The default is 20.

   -  Template Limits

      The number of templates that can be registered in an account.

      The default is 20.

   -  VPC limits

      The number of VPCs that can be created in an account.

      The default is 20.

   -  CPU limits

      The number of CPU cores that can be used for an account.

      The default is 40.

   -  Memory limits (MB)

      The number of RAM that can be used for an account.

      The default is 40960.

   -  Primary Storage limits (GB)

      The primary storage space that can be used for an account.

      The default is 200.

   -  Secondary Storage limits (GB)

      The secondary storage space that can be used for an account.

      The default is 400.

#. Click Apply.


Usage Record Format
-------------------

Virtual Machine Usage Record Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For running and allocated virtual machine usage, the following fields
exist in a usage record:

-  account – name of the account

-  accountid – ID of the account

-  domainid – ID of the domain in which this account resides

-  zoneid – Zone where the usage occurred

-  description – A string describing what the usage record is tracking

-  usage – String representation of the usage, including the units of
   usage (e.g. 'Hrs' for VM running time)

-  usagetype – A number representing the usage type (see Usage Types)

-  rawusage – A number representing the actual usage in hours

-  virtualMachineId – The ID of the virtual machine

-  name – The name of the virtual machine

-  offeringid – The ID of the service offering

-  templateid – The ID of the template or the ID of the parent template.
   The parent template value is present when the current template was
   created from a volume.

-  usageid – Virtual machine

-  type – Hypervisor

-  startdate, enddate – The range of time for which the usage is
   aggregated; see Dates in the Usage Record


Network Usage Record Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~

For network usage (bytes sent/received), the following fields exist in a
usage record.

-  account – name of the account

-  accountid – ID of the account

-  domainid – ID of the domain in which this account resides

-  zoneid – Zone where the usage occurred

-  description – A string describing what the usage record is tracking

-  usagetype – A number representing the usage type (see Usage Types)

-  rawusage – A number representing the actual usage in hours

-  usageid – Device ID (virtual router ID or external device ID)

-  type – Device type (domain router, external load balancer, etc.)

-  startdate, enddate – The range of time for which the usage is
   aggregated; see Dates in the Usage Record


IP Address Usage Record Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For IP address usage the following fields exist in a usage record.

-  account - name of the account

-  accountid - ID of the account

-  domainid - ID of the domain in which this account resides

-  zoneid - Zone where the usage occurred

-  description - A string describing what the usage record is tracking

-  usage - String representation of the usage, including the units of
   usage

-  usagetype - A number representing the usage type (see Usage Types)

-  rawusage - A number representing the actual usage in hours

-  usageid - IP address ID

-  startdate, enddate - The range of time for which the usage is
   aggregated; see Dates in the Usage Record

-  issourcenat - Whether source NAT is enabled for the IP address

-  iselastic - True if the IP address is elastic.


Disk Volume Usage Record Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For disk volumes, the following fields exist in a usage record.

-  account – name of the account

-  accountid – ID of the account

-  domainid – ID of the domain in which this account resides

-  zoneid – Zone where the usage occurred

-  description – A string describing what the usage record is tracking

-  usage – String representation of the usage, including the units of
   usage (e.g. 'Hrs' for hours)

-  usagetype – A number representing the usage type (see Usage Types)

-  rawusage – A number representing the actual usage in hours

-  usageid – The volume ID

-  offeringid – The ID of the disk offering

-  type – Hypervisor

-  templateid – ROOT template ID

-  size – The amount of storage allocated

-  startdate, enddate – The range of time for which the usage is
   aggregated; see Dates in the Usage Record


Template, ISO, and Snapshot Usage Record Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  account – name of the account

-  accountid – ID of the account

-  domainid – ID of the domain in which this account resides

-  zoneid – Zone where the usage occurred

-  description – A string describing what the usage record is tracking

-  usage – String representation of the usage, including the units of
   usage (e.g. 'Hrs' for hours)

-  usagetype – A number representing the usage type (see Usage Types)

-  rawusage – A number representing the actual usage in hours

-  usageid – The ID of the the template, ISO, or snapshot

-  offeringid – The ID of the disk offering

-  templateid – – Included only for templates (usage type 7). Source
   template ID.

-  size – Size of the template, ISO, or snapshot

-  startdate, enddate – The range of time for which the usage is
   aggregated; see Dates in the Usage Record


Load Balancer Policy or Port Forwarding Rule Usage Record Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  account - name of the account

-  accountid - ID of the account

-  domainid - ID of the domain in which this account resides

-  zoneid - Zone where the usage occurred

-  description - A string describing what the usage record is tracking

-  usage - String representation of the usage, including the units of
   usage (e.g. 'Hrs' for hours)

-  usagetype - A number representing the usage type (see Usage Types)

-  rawusage - A number representing the actual usage in hours

-  usageid - ID of the load balancer policy or port forwarding rule

-  usagetype - A number representing the usage type (see Usage Types)

-  startdate, enddate - The range of time for which the usage is
   aggregated; see Dates in the Usage Record


Network Offering Usage Record Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  account – name of the account

-  accountid – ID of the account

-  domainid – ID of the domain in which this account resides

-  zoneid – Zone where the usage occurred

-  description – A string describing what the usage record is tracking

-  usage – String representation of the usage, including the units of
   usage (e.g. 'Hrs' for hours)

-  usagetype – A number representing the usage type (see Usage Types)

-  rawusage – A number representing the actual usage in hours

-  usageid – ID of the network offering

-  usagetype – A number representing the usage type (see Usage Types)

-  offeringid – Network offering ID

-  virtualMachineId – The ID of the virtual machine

-  virtualMachineId – The ID of the virtual machine

-  startdate, enddate – The range of time for which the usage is
   aggregated; see Dates in the Usage Record


VPN User Usage Record Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  account – name of the account

-  accountid – ID of the account

-  domainid – ID of the domain in which this account resides

-  zoneid – Zone where the usage occurred

-  description – A string describing what the usage record is tracking

-  usage – String representation of the usage, including the units of
   usage (e.g. 'Hrs' for hours)

-  usagetype – A number representing the usage type (see Usage Types)

-  rawusage – A number representing the actual usage in hours

-  usageid – VPN user ID

-  usagetype – A number representing the usage type (see Usage Types)

-  startdate, enddate – The range of time for which the usage is
   aggregated; see Dates in the Usage Record


Usage Types
-----------

The following table shows all usage types.

.. cssclass:: table-striped table-bordered table-hover

+------------------+-----------------------------------+-----------------------+
| Type ID          | Type Name                         | Description           |
+==================+===================================+=======================+
| 1                | RUNNING\_VM                       | Tracks the total      |
|                  |                                   | running time of a VM  |
|                  |                                   | per usage record      |
|                  |                                   | period. If the VM is  |
|                  |                                   | upgraded during the   |
|                  |                                   | usage period, you     |
|                  |                                   | will get a separate   |
|                  |                                   | Usage Record for the  |
|                  |                                   | new upgraded VM.      |
+------------------+-----------------------------------+-----------------------+
| 2                | ALLOCATED\_VM                     | Tracks the total time |
|                  |                                   | the VM has been       |
|                  |                                   | created to the time   |
|                  |                                   | when it has been      |
|                  |                                   | destroyed. This usage |
|                  |                                   | type is also useful   |
|                  |                                   | in determining usage  |
|                  |                                   | for specific          |
|                  |                                   | templates such as     |
|                  |                                   | Windows-based         |
|                  |                                   | templates.            |
+------------------+-----------------------------------+-----------------------+
| 3                | IP\_ADDRESS                       | Tracks the public IP  |
|                  |                                   | address owned by the  |
|                  |                                   | account.              |
+------------------+-----------------------------------+-----------------------+
| 4                | NETWORK\_BYTES\_SENT              | Tracks the total      |
|                  |                                   | number of bytes sent  |
|                  |                                   | by all the VMs for an |
|                  |                                   | account. Cloud.com    |
|                  |                                   | does not currently    |
|                  |                                   | track network traffic |
|                  |                                   | per VM.               |
+------------------+-----------------------------------+-----------------------+
| 5                | NETWORK\_BYTES\_RECEIVED          | Tracks the total      |
|                  |                                   | number of bytes       |
|                  |                                   | received by all the   |
|                  |                                   | VMs for an account.   |
|                  |                                   | Cloud.com does not    |
|                  |                                   | currently track       |
|                  |                                   | network traffic per   |
|                  |                                   | VM.                   |
+------------------+-----------------------------------+-----------------------+
| 6                | VOLUME                            | Tracks the total time |
|                  |                                   | a disk volume has     |
|                  |                                   | been created to the   |
|                  |                                   | time when it has been |
|                  |                                   | destroyed.            |
+------------------+-----------------------------------+-----------------------+
| 7                | TEMPLATE                          | Tracks the total time |
|                  |                                   | a template (either    |
|                  |                                   | created from a        |
|                  |                                   | snapshot or uploaded  |
|                  |                                   | to the cloud) has     |
|                  |                                   | been created to the   |
|                  |                                   | time it has been      |
|                  |                                   | destroyed. The size   |
|                  |                                   | of the template is    |
|                  |                                   | also returned.        |
+------------------+-----------------------------------+-----------------------+
| 8                | ISO                               | Tracks the total time |
|                  |                                   | an ISO has been       |
|                  |                                   | uploaded to the time  |
|                  |                                   | it has been removed   |
|                  |                                   | from the cloud. The   |
|                  |                                   | size of the ISO is    |
|                  |                                   | also returned.        |
+------------------+-----------------------------------+-----------------------+
| 9                | SNAPSHOT                          | Tracks the total time |
|                  |                                   | from when a snapshot  |
|                  |                                   | has been created to   |
|                  |                                   | the time it have been |
|                  |                                   | destroyed.            |
+------------------+-----------------------------------+-----------------------+
| 11               | LOAD\_BALANCER\_POLICY            | Tracks the total time |
|                  |                                   | a load balancer       |
|                  |                                   | policy has been       |
|                  |                                   | created to the time   |
|                  |                                   | it has been removed.  |
|                  |                                   | Cloud.com does not    |
|                  |                                   | track whether a VM    |
|                  |                                   | has been assigned to  |
|                  |                                   | a policy.             |
+------------------+-----------------------------------+-----------------------+
| 12               | PORT\_FORWARDING\_RULE            | Tracks the time from  |
|                  |                                   | when a port           |
|                  |                                   | forwarding rule was   |
|                  |                                   | created until the     |
|                  |                                   | time it was removed.  |
+------------------+-----------------------------------+-----------------------+
| 13               | NETWORK\_OFFERING                 | The time from when a  |
|                  |                                   | network offering was  |
|                  |                                   | assigned to a VM      |
|                  |                                   | until it is removed.  |
+------------------+-----------------------------------+-----------------------+
| 14               | VPN\_USERS                        | The time from when a  |
|                  |                                   | VPN user is created   |
|                  |                                   | until it is removed.  |
+------------------+-----------------------------------+-----------------------+


Example response from listUsageRecords
--------------------------------------

All CloudStack API requests are submitted in the form of a HTTP GET/POST
with an associated command and any parameters. A request is composed of
the following whether in HTTP or HTTPS:

::

   <listusagerecordsresponse>
      <count>1816</count>
      <usagerecord>
         <account>user5</account>
         <accountid>10004</accountid>
         <domainid>1</domainid>
         <zoneid>1</zoneid>
         <description>i-3-4-WC running time (ServiceOffering: 1) (Template: 3)</description>
         <usage>2.95288 Hrs</usage>
         <usagetype>1</usagetype>
         <rawusage>2.95288</rawusage>
         <virtualmachineid>4</virtualmachineid>
         <name>i-3-4-WC</name>
         <offeringid>1</offeringid>
         <templateid>3</templateid>
         <usageid>245554</usageid>
         <type>XenServer</type>
         <startdate>2009-09-15T00:00:00-0700</startdate>
         <enddate>2009-09-18T16:14:26-0700</enddate>
      </usagerecord>

      … (1,815 more usage records)
   </listusagerecordsresponse>


Dates in the Usage Record
-------------------------

Usage records include a start date and an end date. These dates define
the period of time for which the raw usage number was calculated. If
daily aggregation is used, the start date is midnight on the day in
question and the end date is 23:59:59 on the day in question (with one
exception; see below). A virtual machine could have been deployed at
noon on that day, stopped at 6pm on that day, then started up again at
11pm. When usage is calculated on that day, there will be 7 hours of
running VM usage (usage type 1) and 12 hours of allocated VM usage
(usage type 2). If the same virtual machine runs for the entire next
day, there will 24 hours of both running VM usage (type 1) and allocated
VM usage (type 2).

Note: The start date is not the time a virtual machine was started, and
the end date is not the time when a virtual machine was stopped. The
start and end dates give the time range within which usage was
calculated.

For network usage, the start date and end date again define the range in
which the number of bytes transferred was calculated. If a user
downloads 10 MB and uploads 1 MB in one day, there will be two records,
one showing the 10 megabytes received and one showing the 1 megabyte
sent.

There is one case where the start date and end date do not correspond to
midnight and 11:59:59pm when daily aggregation is used. This occurs only
for network usage records. When the usage server has more than one day's
worth of unprocessed data, the old data will be included in the
aggregation period. The start date in the usage record will show the
date and time of the earliest event. For other types of usage, such as
IP addresses and VMs, the old unprocessed data is not included in daily
aggregation.


.. |editbutton.png| image:: /_static/images/edit-icon.png
   :alt: edits the settings.
