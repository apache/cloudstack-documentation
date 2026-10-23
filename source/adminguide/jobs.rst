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


.. _working-with-jobs:

Working with Asynchronous Jobs
==============================

Every API command that takes time to complete, such as starting an Instance, migrating it
or taking a snapshot, runs as an asynchronous job: the command returns a job ID at once and
the work goes on in the background on one of the management servers. The result is fetched
with ``queryAsyncJobResult`` (see the :ref:`Developers Guide <async-commands>`). Since
version 24.0 the jobs themselves can be listed and inspected, with their events and the
resource they act on, and a running job can be cancelled, including the work it has started
on the hypervisor.

A job is in one of four states:

.. cssclass:: table-striped table-bordered table-hover

=============== ====== ======================================================================
Status          Value  Meaning
=============== ====== ======================================================================
In progress     0      The job is waiting or running. While its cancellation has been
                       requested and not yet carried out, the UI shows it as *Cancelling*.
Succeeded       1      The job completed; its result is the response of the command.
Failed          2      The job failed; the result carries the error.
Cancelled       3      The job was cancelled and its work was stopped or undone.
=============== ====== ======================================================================

A cancelled job's result has the shape of a failure: result code 530 and an error text that
names who cancelled it and through which management server, for example ``Cancelled by admin
via mgmt2``.


Listing Jobs
------------

#. Log in to the CloudStack UI.

#. In the left navigation, click Activity, then Jobs. The jobs of the account are listed;
   administrators see the jobs of every account.

By default only pending jobs are shown. The status filter switches to the jobs that are
*Cancelling*, *Succeeded*, *Failed* or *Cancelled*, or to all jobs, and for completed jobs
a period filter (last hour, day or week) limits the listing. The filter dialog narrows the
list by domain, account and resource type. Each row shows the command, the status, the
resource the job acted on (as a link where the resource still exists), the management
server, the creation and completion times and the result; the result column is truncated
and can be copied in full from the row.

Click a job to open its details: the command, the user and account that submitted it, the
resource, the management servers that initiated, executed and completed it, the times, the
full result, and, while its cancellation is in progress, the reason recorded for the cancel.
The Events tab of the job lists the events it raised, and the Cancel action is available to
administrators.

Jobs are also listed on the resource they act on: the Jobs tab of an Instance, a Volume, a
Volume Snapshot and an Instance Snapshot shows that resource's jobs, and the Jobs tab of a
Management Server shows the jobs that server executed. The same status and period filters
apply there.

Completed jobs are kept for ``job.expire.minutes`` (default one day) and then purged, so the
listing of succeeded, failed and cancelled jobs covers that window.

With the API, ``listAsyncJobs`` takes these parameters in addition to the usual account,
domain, keyword and paging ones:

.. cssclass:: table-striped table-bordered table-hover

.. list-table::
   :header-rows: 1
   :widths: 22 78

   * - Parameter
     - Description
   * - ``id``
     - The ID of a single job, returned whatever its status.
   * - ``jobstatus``
     - Comma-separated statuses to list, as names (``IN_PROGRESS``, ``SUCCEEDED``, ``FAILED``,
       ``CANCELLED``) or numbers (0-3). Only pending jobs are listed by default.
   * - ``cancelrequested``
     - ``true`` lists only the jobs whose cancellation has been requested.
   * - ``startdate``, ``enddate``
     - Jobs created on or after, or on or before, the given date.
   * - ``duration``
     - Jobs started or completed within that many hours up to now.
   * - ``resourceid``, ``resourcetype``
     - The resource the job acts on, as the job's instance.
   * - ``managementserverid``
     - The management server that executed the job.

The response carries, for each job, the command, the status and result, the resource
(``jobinstancetype``, ``jobinstanceid``, ``jobinstancename``), the management servers
(``initmanagementservername``, ``executingmanagementservername``,
``completemanagementservername``), ``cancellable`` (whether ``cancelAsyncJob`` applies to the
job's command), ``cancelrequested`` and, while the cancel is in progress, ``cancelreason``.


Jobs and Events
---------------

The events an asynchronous command raises are linked to its job: the *Scheduled* and
*Started* events the API server writes when the job is submitted, and the *Completed* event
written when it ends. The Events tab of a job shows them, and ``listEvents`` takes a ``jobid``
parameter to fetch them; the Events view can be filtered by job ID as well. A cancel request
raises a ``JOB.CANCEL`` event on the job, whether it was carried out or refused, that names
the user who asked and the management server that took the request.


Cancelling a Job
----------------

An administrator can cancel a job that is in progress, from the Jobs list, the job's details
or the resource's Jobs tab, or with ``cancelAsyncJob jobid=<id>``. Cancelling means more than
marking the job: the work the job has started on the hypervisor is stopped where the
hypervisor allows it, what the job had already done is undone, and the job ends *Cancelled*.
Where the work cannot be stopped, the request is refused with the reason, and the job is
left to finish as it would have.

A cancel is accepted only when every step the job currently runs can be stopped, so the
outcome is known before anything is changed:

#. The command must be cancellable. The UI disables Cancel for the jobs of other commands,
   and ``listApis`` and ``listAsyncJobs`` report ``cancellable`` so that an API client knows
   in advance. A job whose command is not cancellable can still be cancelled while all its
   work is still waiting in the Instance's queue and nothing has started; that frees the
   queue for the Instance's other jobs.

#. The job must still be in progress.

#. The hypervisor must be able to stop the work the job has in flight. The management server
   asks the host or agent before changing anything.

#. The stop must actually succeed. A task that completed first, or that the hypervisor
   could not stop, leaves the job to finish normally.

The commands that are cancellable, and the work each hypervisor can stop:

.. cssclass:: table-striped table-bordered table-hover

.. list-table::
   :header-rows: 1
   :widths: 34 22 22 22

   * - Command
     - VMware
     - XenServer/XCP-ng
     - KVM
   * - ``startVirtualMachine`` (first start)
     - template clone or copy
     - template copy
     - no
   * - ``migrateVirtualMachine``, ``migrateVirtualMachineWithVolume``
     - live migration
     - live migration
     - live migration
   * - ``migrateVolume``
     - volume copy
     - volume copy
     - live migration only
   * - ``createVolume`` (from a snapshot)
     - copy on the SSVM
     - copy on the host
     - no
   * - ``createSnapshot``
     - backup on the SSVM
     - backup on the host
     - no
   * - ``createVMSnapshot``
     - vCenter snapshot
     - XenAPI snapshot
     - no
   * - stop, reboot, destroy, attach, detach, delete and revert commands
     - no
     - no
     - no

Power operations, attach and detach, deletes and reverts are listed as cancellable so that a
request can be made, but no hypervisor can stop them once they run: vCenter reports its power
tasks as not cancelable, XenServer runs them as synchronous calls, and KVM has nothing to
abort, so such a request is refused unless it arrives before the work started. On KVM, a
cancelled migration aborts the libvirt job; snapshots and copies on KVM cannot be stopped.

When a cancel is accepted:

-  The job is marked as cancel requested and keeps running until its work is stopped; the
   listing shows it as *Cancelling* with the reason.

-  The management server executing the job stops the commands it holds for it; with several
   management servers, each one stops what it holds, so a migration whose work runs on
   another server is stopped there too.

-  The job's work is undone as after a failure: a cancelled migration leaves the Instance or
   volume where it was and removes what was created on the target, a cancelled snapshot or
   Instance snapshot is removed, a cancelled volume creation expunges the volume. On VMware,
   an Instance whose snapshot task was stopped has its disks consolidated.

-  The job ends *Cancelled*. A job whose work completed before the cancel took effect ends
   *Succeeded* with ``cancelrequested`` set, so the records always match what happened.

Refusals and what they mean:

-  ``Cannot cancel, job <id> is not cancellable.`` The command does not support cancellation.

-  ``Cannot cancel job-N, its work cannot be stopped at this point: <reason> (host <name>)``
   The command supports it, but the step now running cannot be stopped; the reason is what
   the hypervisor reported, for example ``vCenter reports task PowerOffVM_Task(...) as not
   cancelable`` or ``no vCenter task or transfer is running for StopCommand``. Try again
   later, or let the job finish.

-  ``Cannot cancel job-N, the operation it is running could not be stopped.`` The stop was
   attempted and the hypervisor did not stop the work; the job finishes normally.

-  ``Cannot cancel, job-N is not running. Current job status is <status>.`` The job had
   already ended.

.. note::
   Usage records are written by the operations themselves, not by the job status, so a
   cancelled job leaves them matching what happened: a job that ends *Cancelled* has had its
   work undone, and the usage record its allocation opened is closed; a job whose work
   completed despite the request ends *Succeeded* with the normal events. If a cancel is
   refused because the hypervisor finished the work first, nothing needs reconciling.


Usage Server Jobs
-----------------

The runs of the Usage Server are listed on the Usage Jobs tab of a Management Server (see
:ref:`listing-usage-jobs`) and with ``listUsageJobs``.


Global Settings
---------------

.. cssclass:: table-striped table-bordered table-hover

========================= ===========================================================================
Setting                   Description
========================= ===========================================================================
job.expire.minutes        Time in minutes for which completed jobs are kept and listed. Default 1440.
job.cancelled.interval    Interval in seconds at which every management server checks for jobs whose
                          cancellation was requested and stops the work it holds for them. Default 1.
========================= ===========================================================================
