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


Resource alerts let you get told when a resource goes over (or under) a
value you pick. For example, "CPU of this Instance is above 80%" or
"this storage pool is more than 90% full".

You create a rule. CloudStack checks the rule every minute. When the
condition is true, an alert is fired. The alert is saved in the alert
history and can be sent out by webhook, email and the event bus.

Rules can be set on:

-  Instances
-  Volumes
-  Hosts
-  Storage pools

A rule can watch one resource, or all resources of that type that the
rule owner can see.

Instance and Volume rules only cover user Instances and their volumes.
System VMs, virtual routers and their volumes are not included.

Resource alerts can be managed using both API and UI. CloudStack provides
the following APIs:

   .. cssclass:: table-striped table-bordered table-hover

   ======================== =================================
   API                      Description
   ======================== =================================
   createResourceAlertRule  Creates a resource alert rule
   listResourceAlertRules   Lists resource alert rules
   updateResourceAlertRule  Updates a resource alert rule
   deleteResourceAlertRule  Deletes a resource alert rule
   listResourceAlerts       Lists fired resource alerts
   ======================== =================================

In the UI, rules are under *Monitoring > Resource Alerts*.

|resource-alert-rules.png|


Who can create rules
~~~~~~~~~~~~~~~~~~~~

Every account role can create rules, but each one only sees and manages
its own.

-  **User**: rules on their own Instances and Volumes.

-  **Domain Admin**: rules on Instances and Volumes in their domain. A
   domain admin can also create a rule for another account in the
   domain.

-  **Root Admin**: rules on any resource, including Hosts and Storage
   pools. Only the root admin can turn on email for a rule.

A rule on "all resources" follows the same limits. For a user it covers
only their own resources. For a domain admin it covers the domain. For
the root admin it covers the whole cloud.

Users and domain admins cannot see or change rules that belong to
someone else.


Creating a rule
~~~~~~~~~~~~~~~

#. Go to *Monitoring > Resource Alerts* and click *New Resource Alert*.

#. Fill in the form:

   -  **Name**: a name for the rule.

   -  **Domain** and **Account**: shown to admins. Pick them to create the
      rule for another account. Leave empty to create it for yourself.

   -  **Resource type**: Virtual Machine, Volume, Host or Storage Pool.

   -  **Resource**: one resource, or *All resources*.

   -  **Metric**: what to watch. The list depends on the resource type.

   -  **Condition** and **Threshold**: for example *Is above* and *80*.

   -  **Severity**: Critical, High, Medium or Low.

   -  **Message**: optional text that is added to the alert.

   -  **Email**: root admin only. Also send the alert by email.

   -  **Cooldown (seconds)**: how long to wait before the same rule
      alerts again for the same resource. Leave empty to use
      ``resourcealert.repeat.interval.default``.

   -  **Webhooks**: optional. Webhooks the alert is sent to. Only webhooks
      the rule owner can use are listed.

#. Click *OK*.

|resource-alert-create.png|

The rule details page shows the rule and the webhooks it sends to. It can
be edited, disabled or deleted from there.

A disabled rule is not checked and fires no alerts, but it keeps its alert
history. Enable it again to start checking. This is useful during planned
maintenance. A disabled rule on one resource does not stop your *All
resources* rule for that resource.

|resource-alert-details.png|

Metrics
~~~~~~~

   .. cssclass:: table-striped table-bordered table-hover

   =============== ==========================================================
   Resource type   Metrics
   =============== ==========================================================
   Virtual Machine CPU Utilization %, Memory Utilization %, Disk Read IOPS,
                   Disk Write IOPS, Disk Read KB/s, Disk Write KB/s,
                   Network In KB/s, Network Out KB/s
   Volume          Volume Used (GB), Volume Used %
   Host            CPU Utilization %, Memory Utilization %, Load Average,
                   Network In KB/s, Network Out KB/s
   Storage Pool    Storage Utilization %, Storage Used IOPS
   =============== ==========================================================

Values come from the stats CloudStack already collects. If a resource does
not report a metric, the rule is skipped for it and no alert is fired. For
example, NFS storage pools do not report IOPS, and Instance memory needs
the guest to report it.

Volume Used is the space the volume takes on the storage, not its disk
size. Volume Used % is that space out of the disk size.

Disk metrics are only on Instances. CloudStack does not collect disk
reads and writes per volume by default, so a rule on a Volume cannot use
them.

For metrics that are a percentage, the threshold cannot be more than 100.


How alerts are fired
~~~~~~~~~~~~~~~~~~~~

-  Rules are checked every ``resourcealert.evaluation.interval`` seconds.

-  When a rule's condition is true, an alert is fired. After that, the
   same rule does not alert again for the same resource until the
   cooldown is over. The check still runs every interval, the cooldown
   only controls how often an alert goes out.

-  With more than one management server, only one of them checks the
   rules. Alerts are not doubled.

-  If you have a rule on one resource for a metric, your *All resources*
   rule for the same metric skips that resource. Rules of other accounts
   are not affected.

-  To keep a resource out of *All resources* rules, add the tag
   ``resource.alert.opt.out`` with the value ``true`` to it. Rules on that
   one resource still work.

-  When a resource or an account is removed, its rules are removed too.


Alert history
~~~~~~~~~~~~~

Fired alerts can be seen in two places:

-  The *Alert History* tab of a rule.

   |resource-alert-history.png|

-  The *Alerts* tab on the Instance, Volume, Host or Storage pool page. It
   lists the alerts for that resource from the rules you can see.

   |resource-alerts-tab.png|

Old alerts are removed after ``resourcealert.history.retention.days``
days. Deleting a rule also deletes its alert history.


Where alerts are sent
~~~~~~~~~~~~~~~~~~~~~

Every alert is saved in the alert history. It can also be sent to:

-  **Webhooks**: to the webhooks picked on the rule. The payload is JSON
   with the rule, the resource, the metric, the value, the threshold and
   the severity. The event type is ``RESOURCE.ALERT``, so webhook filters
   can include or exclude it. The deliveries show in the webhook's
   *Recent deliveries* tab and can be sent again from there. See the
   Webhooks section above for setting up webhooks.

   Example payload:

   .. code:: json

      {
        "event": "RESOURCE.ALERT",
        "id": "2695b7b3-7500-4a0f-93ab-dae8b405cae2",
        "ruleid": "e6a44e57-a087-4d53-bf29-ac092ee69fa0",
        "rulename": "web-01 high CPU",
        "resourcetype": "VirtualMachine",
        "resourceid": "3e5f346d-7dd8-4a05-af64-9c356d4fce34",
        "resourcename": "web-01",
        "metric": "CPU_UTILIZATION",
        "condition": "GT",
        "threshold": 80.0,
        "value": 86.9,
        "severity": "HIGH",
        "message": null,
        "timestamp": "2026-09-29T16:11:03.940Z"
      }

-  **Email**: when *Email* is on for the rule. The email goes to the
   addresses in ``alert.email.addresses`` and uses the same mail server
   settings as other CloudStack alerts (``alert.smtp.host``,
   ``alert.smtp.port`` and so on).

-  **Event bus**: every alert is published as an alert event with type
   ``RESOURCE.ALERT``, when an event bus such as RabbitMQ or Kafka is
   set up. See the Notification section above for setting up the event bus.

Creating, updating and deleting rules also creates the events
``RESOURCE.ALERT.RULE.CREATE``, ``RESOURCE.ALERT.RULE.UPDATE`` and
``RESOURCE.ALERT.RULE.DELETE``.


Settings
~~~~~~~~

   .. cssclass:: table-striped table-bordered table-hover

   ======================================== ======= ======================================================
   Setting                                  Default Description
   ======================================== ======= ======================================================
   resourcealert.evaluation.interval        60      Seconds between rule checks. Needs a management
                                                    server restart.
   resourcealert.repeat.interval.default    600     Cooldown in seconds for rules that don't set one.
   resourcealert.history.retention.days     30      Days to keep fired alerts. 0 keeps them forever.
   resourcealert.per.user.limit             20      Most rules an account can own, admin accounts
                                                    included. 0 is unlimited. Can be set per account.
   ======================================== ======= ======================================================


.. Images


.. |resource-alert-rules.png| image:: /_static/images/resource-alert-rules.png
.. |resource-alert-create.png| image:: /_static/images/resource-alert-create.png
.. |resource-alert-details.png| image:: /_static/images/resource-alert-details.png
.. |resource-alert-history.png| image:: /_static/images/resource-alert-history.png
.. |resource-alerts-tab.png| image:: /_static/images/resource-alerts-tab.png
