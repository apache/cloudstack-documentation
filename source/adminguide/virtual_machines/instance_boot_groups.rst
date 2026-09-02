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

An **Instance Boot Group** lets a User or Administrator group a set of Instances
and Instance Groups together so that they can be started, stopped, and
rebooted as a single, ordered unit. This is useful for multi-tier
applications where some Instances depend on others being up and reachable
before they should boot, for example a database tier that must be running
before an application tier starts, which in turn must be running before a
web tier starts.

An Instance Boot Group is owned by an account, just like an Instance, and is
managed from **Compute > Instance Boot Groups** in the CloudStack UI.

.. note:: An Instance Boot Group is a different concept from an Instance
   Group (**Compute > Instance Groups**), which is a simple, unordered label
   used to organize Instances. An Instance Group can itself be added as a
   member of an Instance Boot Group.

Members and Boot Order
~~~~~~~~~~~~~~~~~~~~~~~

A **member** of an Instance Boot Group is either a single Instance or an
existing Instance Group. Each member is assigned a **Boot Order**, a
non-negative integer.

- All members that share the same Boot Order value form a **tier**, and boot
  (or shut down) together, concurrently.
- Tiers are processed strictly in order: when starting a group, tier 0 is
  processed before tier 1, tier 1 before tier 2, and so on. When stopping a
  group, tiers are processed in the reverse order.
- An Instance or Instance Group can be a member of only one Instance Boot
  Group at a time.
- An Instance that is part of a VNF appliance, or that already belongs to an
  AutoScale VM group, cannot be added to an Instance Boot Group.
- The maximum number of members allowed in a single Instance Boot Group is
  controlled by the domain-scoped configuration
  ``instance.boot.group.max.members`` (default: 10).

Readiness Rules
~~~~~~~~~~~~~~~~

By default, CloudStack does not define any readiness rules for the members of
an Instance Boot Group, so it considers a member of the group "ready"
as soon as its Instance (or, for an Instance Group member, all of its
Instances) reaches the Running state. For many applications this is not
enough. For example, a database Instance may be Running but not yet
accepting connections.

A **Readiness Rule** lets you define what "ready" really means for a member,
beyond the Instance's power state. When an Instance Boot Group is started,
CloudStack waits for a tier's readiness rules to report success before
moving on to start the next tier.

Readiness Rules can be attached directly to an Instance member or to an
Instance Group member. A rule attached to an Instance Group is automatically
**inherited** by every Instance currently in that group, and is evaluated
individually against each of them.

The following Readiness Rule types are supported:

.. cssclass:: table-striped table-bordered table-hover

======================= ============================= ==========================================================================================
Rule Type               Applies to                    Description
======================= ============================= ==========================================================================================
Ping                     Instance, Instance Group     Checks that the Instance responds to an ICMP ping, issued from the Virtual Router on the
                                                      Instance's default network. Requires a running Virtual Router on that network.
PortCheck                Instance, Instance Group     Checks that a TCP port on the Instance can be connected to, from the Virtual Router on the
                                                      Instance's default network. Requires the ``port`` detail (1-65535) and, optionally, the
                                                      ``protocol`` detail (only ``tcp`` is supported).
GuestAgentLiveness       Instance, Instance Group     Checks that the QEMU guest agent inside the Instance responds to a liveness ping.
                                                      Supported on **KVM only**. Requires installing the ``qemu-guest-agent`` package on the
                                                      guest Instances.
MemberQuorum             Instance Group only          Considers the group ready once a threshold of its member Instances are ready, instead of
                                                      requiring all of them. Requires the ``thresholdtype`` detail (``COUNT`` or ``PERCENTAGE``)
                                                      and the ``thresholdvalue`` detail.
======================= ============================= ==========================================================================================

.. note:: ``Ping``, ``GuestAgentLiveness``, and ``MemberQuorum`` are singleton
   rules, i.e., only one of each can be attached to a given member. Multiple
   ``PortCheck`` rules can be attached to the same member, one per port.

.. note:: ``Ping`` and ``PortCheck`` rules require the target Instance to
   have a default network with a Virtual Router (they cannot be used on an
   L2 network).

If a member has no Readiness Rules of its own and inherits none from an
owning Instance Group, its readiness is simply its Instance's power state
(Running or not).

Configuring Instance Boot Group Behaviour
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following global configuration parameters control how readiness is
checked while an Instance Boot Group is starting. All of them, except the
poll interval and the concurrency setting, can be overridden per Instance
Boot Group when it is created or updated.

.. cssclass:: table-striped table-bordered table-hover

========================================================= ==========================================================================================
Configuration                                             Description
========================================================= ==========================================================================================
instance.boot.group.readiness.timeout.seconds             Timeout, in seconds, for a single readiness check attempt. **Default: 300**
                                                          (overridable per Instance Boot Group)
instance.boot.group.readiness.max.retry.attempts          Maximum number of readiness check attempts for a member before the tier, and the
                                                          Instance Boot Group start, is considered to have failed. **Default: 5**
                                                          (overridable per Instance Boot Group)
instance.boot.group.readiness.initial.delay.seconds       Delay, in seconds, after an Instance is started before its first readiness check
                                                          attempt is made. **Default: 30** (overridable per Instance Boot Group)
instance.boot.group.readiness.reboot.on.retry             Whether a member Instance should be rebooted before each new readiness check retry,
                                                          instead of simply being re-checked. **Default: false** (overridable per Instance Boot
                                                          Group)
instance.boot.group.readiness.poll.interval.seconds       Interval, in seconds, between readiness check attempts. **Default: 10** (global only)
instance.boot.group.readiness.check.concurrency           Maximum number of members within a tier whose readiness is checked concurrently.
                                                          **Default: 10** (global only)
instance.boot.group.max.members                           Maximum number of members allowed in a single Instance Boot Group. This is a
                                                          domain-scoped setting. **Default: 10**
========================================================= ==========================================================================================

Creating an Instance Boot Group
---------------------------------

#. Log in to the CloudStack UI.
#. In the left navigation bar, click **Compute**, then **Instance Boot Groups**.
#. Click **Add Instance Boot Group**.
#. Provide a name and, optionally, a description.
#. Optionally, expand the readiness settings to override the default
   readiness timeout, maximum retry attempts, initial delay, or
   reboot-on-retry behaviour for this Instance Boot Group only.
#. Click **OK**.

Using the API:

.. code:: bash

   cmk create instancebootgroup name=web-app-stack description="DB, App and Web tiers"

Adding and Managing Members
------------------------------

Once an Instance Boot Group has been created, Instances or Instance Groups
can be added to it as members, each with its own Boot Order.

Adding a Member
~~~~~~~~~~~~~~~~

#. Open the Instance Boot Group and go to the **Members** tab.
#. Click **Add Member**.
#. Choose whether the member is an Instance or an Instance Group, then
   select it from the list.
#. Enter the Boot Order for the new member.
#. Click **OK**.

Using the API:

.. code:: bash

   # Add an Instance as a member of tier 0 (starts first)
   cmk add membertoinstancebootgroup id=<boot-group-id> virtualmachineid=<vm-id> order=0

   # Add an Instance Group as a member of tier 1 (starts after tier 0)
   cmk add membertoinstancebootgroup id=<boot-group-id> instancegroupid=<instance-group-id> order=1

Changing a Member's Boot Order
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

From the **Members** tab, use the **Boot Order** action on a member row to
move it to a different tier. Any other members between the old and new
position are automatically shifted to keep the ordering consistent.

Using the API:

.. code:: bash

   cmk update instancebootgroupmember id=<member-id> order=2

Removing a Member
~~~~~~~~~~~~~~~~~~

Removing a member from an Instance Boot Group only removes it from the
group (and deletes any Readiness Rules attached to it); the Instance or
Instance Group itself, and its running state, are not affected.

.. code:: bash

   cmk remove instancebootgroupmember id=<member-id>

Listing Members and Their Status
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The **Members** tab lists all members of an Instance Boot Group sorted by
Boot Order, along with a readiness status badge (Ready, NotReady, Error, or
Unknown) for each. An Instance Group member row can be expanded to see the
readiness of each Instance inside it.

.. code:: bash

   cmk list instancebootgroupmembers bootgroupid=<boot-group-id> details=readiness,children

.. note:: Computing readiness details is not free, so it is only returned
   when explicitly requested (``details=readiness``). Add
   ``ignoreinstancestate=true`` to see the last cached rule result even
   while the Instance is stopped; by default, a stopped Instance is always
   reported NotReady regardless of the cached result.

Configuring Readiness Rules for a Member
-------------------------------------------

#. From the **Members** tab, use the **Manage Readiness Rules** action on
   the member you want to configure.
#. Click **Add Rule**, choose a Rule Type, and fill in the fields relevant
   to that type (for example, the port and protocol for a ``PortCheck``
   rule, or the threshold type and value for a ``MemberQuorum`` rule on an
   Instance Group).
#. Click **OK**.

Rules inherited from an owning Instance Group are shown read-only, tagged
**Inherited**; they must be removed from the Instance Group member instead.

.. note:: When adding a ``GuestAgentLiveness`` rule, make sure the QEMU
   guest agent is installed, running, and responsive inside the guest
   Instance, the rule can only report Ready once the agent answers.

Using the API:

.. code:: bash

   # A TCP port check on an Instance
   cmk create instancebootgroupreadinessrule bootgroupid=<boot-group-id> \
       virtualmachineid=<vm-id> ruletype=PortCheck \
       details[0].port=1433 details[0].protocol=tcp

   # A member quorum rule on an Instance Group (ready once 75% of its Instances are ready)
   cmk create instancebootgroupreadinessrule bootgroupid=<boot-group-id> \
       instancegroupid=<instance-group-id> ruletype=MemberQuorum \
       details[0].thresholdtype=PERCENTAGE details[0].thresholdvalue=75

   cmk list instancebootgroupreadinessrules bootgroupid=<boot-group-id>

   cmk update instancebootgroupreadinessrule id=<rule-id> enabled=false

   cmk delete instancebootgroupreadinessrule id=<rule-id>

.. note:: The rule type of an existing Readiness Rule cannot be changed;
   only its name, enabled state, and details can be updated. Delete and
   re-create the rule to change its type.

Starting, Stopping, and Rebooting an Instance Boot Group
-------------------------------------------------------------

Instance Boot Groups are started, stopped, and rebooted as a whole from the
**Instance Boot Groups** list or detail view, or via the API. These are
asynchronous operations.

- **Start**: tiers are started in ascending Boot Order. All members of a
  tier are started concurrently, and CloudStack waits for the tier to
  become ready based on its members' Readiness Rules before starting
  the next tier. If a member does not become ready within the configured
  number of retry attempts, or fails to start, the whole start operation is
  halted. Instances that were already started before the failure are left
  running; they are not automatically stopped again.
- **Stop**: tiers are stopped in descending Boot Order, the reverse of
  start. Readiness Rules are not checked while stopping, and a failure to
  stop one member does not prevent CloudStack from continuing to stop the
  remaining tiers.
- **Reboot**: equivalent to a stop followed by a start, i.e. the whole
  group is stopped in descending order and then started again in ascending,
  readiness-gated order.

Using the API:

.. code:: bash

   cmk start instancebootgroup id=<boot-group-id>

   cmk stop instancebootgroup id=<boot-group-id> forced=true

   cmk reboot instancebootgroup id=<boot-group-id>

Deleting an Instance Boot Group
------------------------------------

Deleting an Instance Boot Group removes its members and any Readiness
Rules attached to them; the Instances and Instance Groups themselves are
left untouched and continue running or stopped as they were.

.. code:: bash

   cmk delete instancebootgroup id=<boot-group-id>

Instance Boot Group Events
---------------------------------

The following events are logged for auditing and monitoring Instance Boot
Group activity:

.. cssclass:: table-striped table-bordered table-hover

================================================= ======================================================
Event Type                                         Description
================================================= ======================================================
INSTANCE.BOOT.GROUP.CREATE                         An Instance Boot Group was created
INSTANCE.BOOT.GROUP.UPDATE                         An Instance Boot Group was updated
INSTANCE.BOOT.GROUP.DELETE                         An Instance Boot Group was deleted
INSTANCE.BOOT.GROUP.START                          An Instance Boot Group was started
INSTANCE.BOOT.GROUP.STOP                           An Instance Boot Group was stopped
INSTANCE.BOOT.GROUP.REBOOT                         An Instance Boot Group was rebooted
INSTANCE.BOOT.GROUP.MEMBER.ADD                     A member was added to an Instance Boot Group
INSTANCE.BOOT.GROUP.MEMBER.REMOVE                  A member was removed from an Instance Boot Group
INSTANCE.BOOT.GROUP.READINESS.RULE.CREATE          A Readiness Rule was created
INSTANCE.BOOT.GROUP.READINESS.RULE.UPDATE          A Readiness Rule was updated
INSTANCE.BOOT.GROUP.READINESS.RULE.DELETE          A Readiness Rule was deleted
================================================= ======================================================

Limitations
-----------

#. An Instance or Instance Group can belong to at most one Instance Boot
   Group at a time.
#. Instances that are part of a VNF appliance, or already belong to an
   AutoScale VM group, cannot be added to an Instance Boot Group.
#. The ``GuestAgentLiveness`` Readiness Rule requires the QEMU guest agent
   and is supported on KVM Instances only. It requires installing the
   ``qemu-guest-agent`` package on the guest Instances.
#. ``Ping`` and ``PortCheck`` Readiness Rules require a running Virtual
   Router on the Instance's default network, and cannot be used on Instances
   connected only to an L2 network.
#. If starting an Instance Boot Group is halted because a tier fails to
   become ready, any Instances already started in earlier tiers are left
   running. The operation is not automatically rolled back.
