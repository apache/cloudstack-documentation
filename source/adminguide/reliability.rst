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


HA for Management Server
------------------------

The CloudStack Management Server should be deployed in a multi-node
configuration such that it is not susceptible to individual server
failures. The Management Server itself (as distinct from the MySQL
database) is stateless and may be placed behind a load balancer.

Normal operation of Hosts is not impacted by an outage of all Management
Serves. All Guest Instances will continue to work.

When the Management Server is down, no new Instances can be created, and the
end User and admin UI, API, dynamic load distribution, and HA will cease
to work.

.. _management-server-load-balancing:

Management Server Load Balancing
--------------------------------

CloudStack can use a load balancer to provide a virtual IP for multiple
Management Servers. The administrator is responsible for creating the
load balancer rules for the Management Servers. The application requires
persistence or stickiness across multiple sessions. The following chart
lists the ports that should be load balanced and whether or not
persistence is required.

Even if persistence is not required, enabling it is permitted.

.. cssclass:: table-striped table-bordered table-hover

============== ======================== ================ =====================
Source Port    Destination Port         Protocol         Persistence Required?
============== ======================== ================ =====================
80 or 443      8080 (or 20400 with AJP) HTTP (or AJP)    Yes
8250           8250                     TCP              Yes
8096           8096                     HTTP             No
============== ======================== ================ =====================

In addition to above settings, the administrator is responsible for
setting the 'host' global config value from the management server IP to
load balancer virtual IP address. If the 'host' value is not set to the
VIP for Port 8250 and one of your management servers crashes, the UI is
still available but the system VMs will not be able to contact the
management server.


Multiple Management Servers Support on agents
---------------------------------------------

In a Cloudstack environment with multiple management servers, an agent can be
configured, based on an algorithm, to which management server to connect to.
This can be useful as an internal load balancer or for high availability.
An administrator is responsible for setting the list of management servers and
choosing a sorting algorithm using global settings.
The management server is responsible for propagating the settings to the
connected agents (running inside of the Secondary Storage
Virtual Machine, Console Proxy Virtual Machine or the KVM hosts).

The three global settings that need to be configured are the following:

- hosts: a comma separated list of management server IP addresses
- indirect.agent.lb.algorithm: The algorithm for the indirect agent LB
- indirect.agent.lb.check.interval: The preferred host check interval
  for the agent's background task that checks and switches to an agent's
  preferred host.

These settings can be configured from the global settings page in the UI or
using the updateConfiguration API call.

The indirect.agent.lb.algorithm setting supports following algorithm options:

- static: Use the list of management server IP addresses as provided.
- roundrobin: Evenly spread hosts across management servers, based on the
  host's id.
- shuffle: Pseudo Randomly sort the list (this is not recommended for
  production).

.. note:: 
   The 'static' and 'roundrobin' algorithms, strictly checks for the order as
   expected by them, however, the 'shuffle' algorithm just checks for content
   and not the order of the comma separate management server host addresses.

Any changes to the global settings - `indirect.agent.lb.algorithm` and
`host` does not require restarting of the management server(s) and the
agents. A change in these global settings will be propagated to all connected
agents.

The comma-separated management server list is propagated to agents in
following cases:
- An addition of an agent (including ssvm, cpvm system VMs).
- Connection or reconnection of an agent to a management server.
- After an administrator changes the 'host' and/or the
'indirect.agent.lb.algorithm' global settings.

On the agent side, the 'host' setting is saved in its properties file as:
`host=<comma separated addresses>@<algorithm name>`.

From the agent's perspective, the first address in the propagated list
will be considered the preferred host. A new background task can be
activated by configuring the `indirect.agent.lb.check.interval` which is
a cluster level global setting from CloudStack and administrators can also
override this by configuring the 'host.lb.check.interval' in the
`agent.properties` file.

When an agent gets a host and algorithm combination, the host specific
background check interval is also sent and is dynamically reconfigured
in the background task without need to restart agents.

To make things more clear, consider this example:
Suppose an environment which has 3 management servers: A, B and C and
3 KVM agents.

Setting 'host' = 'A,B,C', agents will receive lists depending on
'direct.agent.lb' value:

'static': Each agent will receive the list: 'A,B,C'
'roundrobin': First agent receives: 'A,B,C', second agent 
receives: 'B,C,A', third agent receives: 'C,B,A'
'shuffle': Each agent will receive a list in random order.

HA-Enabled Instances
--------------------

The User can specify an Instance as HA-enabled. By default, all
virtual router Instances and Elastic Load Balancing Instances are automatically
configured as HA-enabled. When an HA-enabled Instance crashes, CloudStack
detects the crash and restarts the Instance automatically within the same
Availability Zone. HA is never performed across different Availability
Zones. CloudStack has a conservative policy towards restarting Instances and
ensures that there will never be two equal Instances running at
the same time. The Management Server attempts to start the Instance on another
Host in the same cluster.

HA features work with iSCSI or NFS primary storage. HA with local
storage is not supported.

.. note::
   HA-Enabled Instances will be restarted when it is detected that the Instance is
   crashed beyond a shadow of a doubt. When the host it is running on is
   unreachable, either because of Network issue or because it is crashed,
   CloudStack can not be sure the disk image of the Instance is not still being
   accessed and will not restart the Instance.


Dedicated HA Hosts
------------------

One or more hosts can be designated for use only by HA-enabled Instances that
are restarting due to a host failure. Setting up a pool of such
dedicated HA hosts as the recovery destination for all HA-enabled Instances is
useful to:

-  Make it easier to determine which Instances have been restarted as part of
   the CloudStack high-availability function. If an Instance is running on a
   dedicated HA host, then it must be an HA-enabled Instance whose original
   host failed. (With one exception: It is possible for an administrator
   to manually migrate any Instance to a dedicated HA host.).

-  Keep HA-enabled Instances from restarting on hosts which may be reserved
   for other purposes.

The dedicated HA option is set through a special host tag when the host
is created. To allow the administrator to dedicate hosts to only
HA-enabled Instances, set the global configuration variable ha.tag to the
desired tag (for example, "ha\_host"), and restart the Management
Server. Enter the value in the Host Tags field when adding the host(s)
that you want to dedicate to HA-enabled Instances.

.. note:: 
   If you set ha.tag, be sure to actually use that tag on at least one 
   host in your cloud. If the tag specified in ha.tag is not set for 
   any host in the cloud, the HA-enabled Instances will fail to restart after
   a crash.


HA-Enabled Hosts
----------------

.. note::
   This feature is only applicable to KVM clusters. It is not supported
   on for instance VMware or Xen. For those hypervisor types, the Host HA
   is left to the VMware-cluster or Xen-pool respectively.

The User can specify a host as HA-enabled, In the event of a host
failure, attempts will be made to recover the failed host by first
issuing some OOBM commands. If the host recovery fails the host will be
fenced and placed into maintenance mode. To restore the host to normal 
operation, manual intervention would then be required.

Out of band management is a requirement of HA-Enabled hosts and has to be 
configured on all intended participating hosts.
(see `“Out of band management” <hosts.html#out-of-band-management>`_).

Host-HA has granular configuration on a host/cluster/zone level. In a large 
environment, some hosts from a cluster can be HA-enabled and some not, 

Host-HA uses a state machine design to manage the operations of recovering
and fencing hosts. The current status of a host is reported when querying a
specific host.

Timely health investigations are done on HA-Enabled hosts to monitor for
any failures. Specific thresholds can be set for failed investigations,
only when it’s exceeded, will the host transition to a different state.

Host-HA uses both health checks and activity checks to make decisions on 
recovering and fencing actions. Once determined that the host is in faulty 
state (health checks failed) it runs activity checks to figure out if there is 
any disk activity on the Instances running on the specific host.

The HA Resource Management Service manages the check/recovery cycle including
periodic execution, concurrency management, persistence, back pressure and 
clustering operations. Administrators associate a provider with a partition 
type (e.g. KVM HA Host provider to clusters) and may override the provider on a
per-partition (i.e. zone, cluster, or pod) basis. The service operates on all
resources of the type supported by the provider contained in a partition.
Administrators can also enable or disable HA operations globally or on a
per-partition basis.

Only one (1) HA provider per resource type may be specified for a partition.
Nested HA providers by resource type is not supported (e.g. a pod
specifying an HA resource provider for hosts and a containing cluster
specifying a HA resource provider for hosts). The service is designed to be
opt-in where by only resources with a defined provider and HA enabled will be
managed.

For each resource in an HA partition, the HA Resource Management Service
maintains and persists an "Finite State Machine" composed of the following
states:

- AVAILABLE - The feature is enabled and Host-HA is available.
- SUSPECT - There are health checks failing with the host.
- CHECKING - Activity checks are being performed.
- DEGRADED - The host is passing the activity check ratio and still providing
  service to the end User, but it cannot be managed from the CloudStack
  management server.
- RECOVERING - The Host-HA framework is trying to recover the host by issuing
  OOBM jobs.
- RECOVERED - The Host-HA framework has recovered the host successfully.
- FENCING - The Host-HA framework is trying to fence the host by issuing OOBM
  jobs.
- FENCED - The Host-HA framework has fenced the host successfully.
- DISABLED - The feature is disabled for the host.
- INELIGIBLE - The feature is enabled, but it cannot be managed successfully by
  the Host-HA framework. (OOBM is possibly not configured properly)

When HA is enabled for a partition, the HA state of all contained resources 
will be transitioned from DISABLED to AVAILABLE. Based on the state models, the
following failure scenarios and their responses will be handled by the HA 
resource management service:

- Activity check operation fails on the resource: Provide a semantic in the 
  activity check protocol to express that an error while performing the 
  activity check and a reason for the failure (e.g. unable to access the NFS 
  mount). If the maximum number of activity check attempts has not been 
  exceeded, the activity check will be retried.

- Slow activity check operation: After a configurable timeout, the HA resource
  management service abandons the check. The response to this condition would 
  be the same as a failure to recover the resource.

- Traffic flood due to a large number of resource recoveries: The HA resource 
  management service must limit the number of concurrent recovery operations 
  permitted to avoid overwhelming the management server with resource status 
  updates as recovery operations complete.

- Processor/memory starvation due to large number of activity check 
  operations: The HA resource management service must limit the number of 
  concurrent activity check operations permitted per management server to 
  prevent checks from starving other management server activities of scarce
  processor and/or memory resources.

- A SUSPECT, CHECKING, or RECOVERING resource passes a health check before the
  state action completes: The HA resource management service refreshes the HA
  state of the resource before transition. If it does not match the expected
  current state, the result of state action is ignored.

For further information around the inner workings of Host HA, refer
to the design document at 
`https://cwiki.apache.org/confluence/display/CLOUDSTACK/Host+HA 
<https://cwiki.apache.org/confluence/display/CLOUDSTACK/Host+HA>`_

Primary Storage Outage and Data Loss
------------------------------------

When a primary storage outage occurs the hypervisor immediately stops
all Instances stored on that storage device. Guests that are marked for HA
will be restarted as soon as practical when the primary storage comes
back on line. With NFS, the hypervisor may allow the Instances to
continue running depending on the nature of the issue. For example, an
NFS hang will cause the Guest Instances to be suspended until storage
connectivity is restored.Primary storage is not designed to be backed
up. Individual volumes in primary storage can be backed up using
Templates.


Secondary Storage Outage and Data Loss
--------------------------------------

For a Zone that has only one secondary storage server, a secondary
storage outage will have feature level impact to the system but will not
impact running Guest Instances. It may become impossible to create an Instance
with the selected Template for a User. A User may also not be able to save
Templates or examine/restore saved Templates. These features will
automatically be available when the secondary storage comes back online.

Secondary storage data loss will impact recently added User data
including Templates, Snapshots, and ISO Images. Secondary storage should
be backed up periodically. Multiple secondary storage servers can be
provisioned within each zone to increase the scalability of the system.


Database High Availability
--------------------------

To help ensure high availability of the databases that store the
internal data for CloudStack, you can set up database replication. This
covers both the main CloudStack database and the Usage database.
Replication is achieved using the MySQL connector parameters and two-way
replication. Tested with MySQL 5.1 and 5.5.


How to Set Up Database Replication
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Database replication in CloudStack is provided using the MySQL
replication capabilities. The steps to set up replication can be found
in the MySQL documentation (links are provided below). It is suggested
that you set up two-way replication, which involves two database nodes.
In this case, for example, you might have node1 and node2.

You can also set up chain replication, which involves more than two
nodes. In this case, you would first set up two-way replication with
node1 and node2. Next, set up one-way replication from node2 to node3.
Then set up one-way replication from node3 to node4, and so on for all
the additional nodes.

References:

-  `http://dev.mysql.com/doc/refman/5.0/en/replication-howto.html <http://dev.mysql.com/doc/refman/5.0/en/replication-howto.html>`_

-  `https://wikis.oracle.com/display/CommSuite/MySQL+High+Availability+and+Replication+Information+For+Calendar+Server <https://wikis.oracle.com/display/CommSuite/MySQL+High+Availability+and+Replication+Information+For+Calendar+Server>`_


Configuring Database High Availability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To control the database high availability behavior, use the following
configuration settings in the file
/etc/cloudstack/management/db.properties.

**Required Settings**

Be sure you have set the following in db.properties:

-  ``db.ha.enabled``: set to true if you want to use the replication
   feature.

   Example: ``db.ha.enabled=true``

-  ``db.cloud.replicas``: set to a comma-delimited set of replica hosts for the
   cloud database. This is the list of nodes set up with replication.
   The source node is not in the list, since it is already mentioned
   elsewhere in the properties file.

   Example: ``db.cloud.replicas=node2,node3,node4``

-  ``db.usage.replicas``: set to a comma-delimited set of replica hosts for the
   usage database. This is the list of nodes set up with replication.
   The source node is not in the list, since it is already mentioned
   elsewhere in the properties file.

   Example: ``db.usage.replicas=node2,node3,node4``

**Optional Settings**

The following settings must be present in db.properties, but you are not
required to change the default values unless you wish to do so for
tuning purposes:

-  ``db.cloud.secondsBeforeRetrySource``: The number of seconds the MySQL
   connector should wait before trying again to connect to the source
   after the source went down. Default is 1 hour. The retry might happen
   sooner if db.cloud.queriesBeforeRetrySource is reached first.

   Example: ``db.cloud.secondsBeforeRetrySource=3600``

-  ``db.cloud.queriesBeforeRetrySource``: The minimum number of queries to
   be sent to the database before trying again to connect to the source
   after the source went down. Default is 5000. The retry might happen
   sooner if db.cloud.secondsBeforeRetrySource is reached first.

   Example: ``db.cloud.queriesBeforeRetrySource=5000``

-  ``db.cloud.initialTimeout``: Initial time the MySQL connector should wait
   before trying again to connect to the source. Default is 3600.

   Example: ``db.cloud.initialTimeout=3600``


Limitations on Database High Availability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following limitations exist in the current implementation of this
feature.

-  Replica hosts can not be monitored through CloudStack. You will need to
   have a separate means of monitoring.

-  Events from the database side are not integrated with the CloudStack
   Management Server events system.

-  You must periodically perform manual clean-up of bin log files
   generated by replication on database nodes. If you do not clean up
   the log files, the disk can become full.
