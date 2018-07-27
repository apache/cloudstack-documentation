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
Serves. All guest VMs will continue to work.

When the Management Server is down, no new VMs can be created, and the
end user and admin UI, API, dynamic load distribution, and HA will cease
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


HA-Enabled Virtual Machines
---------------------------

The user can specify a virtual machine as HA-enabled. By default, all
virtual router VMs and Elastic Load Balancing VMs are automatically
configured as HA-enabled. When an HA-enabled VM crashes, CloudStack
detects the crash and restarts the VM automatically within the same
Availability Zone. HA is never performed across different Availability
Zones. CloudStack has a conservative policy towards restarting VMs and
ensures that there will never be two instances of the same VM running at
the same time. The Management Server attempts to start the VM on another
Host in the same cluster.

HA features work with iSCSI or NFS primary storage. HA with local
storage is not supported.


HA for Hosts
------------

The user can specify a virtual machine as HA-enabled. By default, all
virtual router VMs and Elastic Load Balancing VMs are automatically
configured as HA-enabled. When an HA-enabled VM crashes, CloudStack
detects the crash and restarts the VM automatically within the same
Availability Zone. HA is never performed across different Availability
Zones. CloudStack has a conservative policy towards restarting VMs and
ensures that there will never be two instances of the same VM running at
the same time. The Management Server attempts to start the VM on another
Host in the same cluster.

HA features work with iSCSI or NFS primary storage. HA with local
storage is not supported.


Dedicated HA Hosts
~~~~~~~~~~~~~~~~~~

One or more hosts can be designated for use only by HA-enabled VMs that
are restarting due to a host failure. Setting up a pool of such
dedicated HA hosts as the recovery destination for all HA-enabled VMs is
useful to:

-  Make it easier to determine which VMs have been restarted as part of
   the CloudStack high-availability function. If a VM is running on a
   dedicated HA host, then it must be an HA-enabled VM whose original
   host failed. (With one exception: It is possible for an administrator
   to manually migrate any VM to a dedicated HA host.).

-  Keep HA-enabled VMs from restarting on hosts which may be reserved
   for other purposes.

The dedicated HA option is set through a special host tag when the host
is created. To allow the administrator to dedicate hosts to only
HA-enabled VMs, set the global configuration variable ha.tag to the
desired tag (for example, "ha\_host"), and restart the Management
Server. Enter the value in the Host Tags field when adding the host(s)
that you want to dedicate to HA-enabled VMs.

.. note:: 
   If you set ha.tag, be sure to actually use that tag on at least one 
   host in your cloud. If the tag specified in ha.tag is not set for 
   any host in the cloud, the HA-enabled VMs will fail to restart after 
   a crash.


Primary Storage Outage and Data Loss
------------------------------------

When a primary storage outage occurs the hypervisor immediately stops
all VMs stored on that storage device. Guests that are marked for HA
will be restarted as soon as practical when the primary storage comes
back on line. With NFS, the hypervisor may allow the virtual machines to
continue running depending on the nature of the issue. For example, an
NFS hang will cause the guest VMs to be suspended until storage
connectivity is restored.Primary storage is not designed to be backed
up. Individual volumes in primary storage can be backed up using
snapshots.


Secondary Storage Outage and Data Loss
--------------------------------------

For a Zone that has only one secondary storage server, a secondary
storage outage will have feature level impact to the system but will not
impact running guest VMs. It may become impossible to create a VM with
the selected template for a user. A user may also not be able to save
snapshots or examine/restore saved snapshots. These features will
automatically be available when the secondary storage comes back online.

Secondary storage data loss will impact recently added user data
including templates, snapshots, and ISO images. Secondary storage should
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

-  ``db.cloud.slaves``: set to a comma-delimited set of slave hosts for the
   cloud database. This is the list of nodes set up with replication.
   The master node is not in the list, since it is already mentioned
   elsewhere in the properties file.

   Example: ``db.cloud.slaves=node2,node3,node4``

-  ``db.usage.slaves``: set to a comma-delimited set of slave hosts for the
   usage database. This is the list of nodes set up with replication.
   The master node is not in the list, since it is already mentioned
   elsewhere in the properties file.

   Example: ``db.usage.slaves=node2,node3,node4``

**Optional Settings**

The following settings must be present in db.properties, but you are not
required to change the default values unless you wish to do so for
tuning purposes:

-  ``db.cloud.secondsBeforeRetryMaster``: The number of seconds the MySQL
   connector should wait before trying again to connect to the master
   after the master went down. Default is 1 hour. The retry might happen
   sooner if db.cloud.queriesBeforeRetryMaster is reached first.

   Example: ``db.cloud.secondsBeforeRetryMaster=3600``

-  ``db.cloud.queriesBeforeRetryMaster``: The minimum number of queries to
   be sent to the database before trying again to connect to the master
   after the master went down. Default is 5000. The retry might happen
   sooner if db.cloud.secondsBeforeRetryMaster is reached first.

   Example: ``db.cloud.queriesBeforeRetryMaster=5000``

-  ``db.cloud.initialTimeout``: Initial time the MySQL connector should wait
   before trying again to connect to the master. Default is 3600.

   Example: ``db.cloud.initialTimeout=3600``


Limitations on Database High Availability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following limitations exist in the current implementation of this
feature.

-  Slave hosts can not be monitored through CloudStack. You will need to
   have a separate means of monitoring.

-  Events from the database side are not integrated with the CloudStack
   Management Server events system.

-  You must periodically perform manual clean-up of bin log files
   generated by replication on database nodes. If you do not clean up
   the log files, the disk can become full.
