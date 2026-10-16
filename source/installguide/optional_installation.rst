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


Additional Installation Options
===============================

The next few sections describe CloudStack features above and beyond the
basic deployment options.


Installing the Usage Server (Optional)
--------------------------------------

You can optionally install the Usage Server once the Management Server
is configured properly. The Usage Server takes data from the events in
the system and enables usage-based billing for Accounts.

When multiple Management Servers are present, the Usage Server may be
installed on any number of them. The Usage Servers will coordinate usage
processing. A site that is concerned about availability should install
Usage Servers on at least two Management Servers.


Requirements for Installing the Usage Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  The Management Server must be running when the Usage Server is
   installed.

-  The Usage Server must be installed on the same server as a Management
   Server.


Steps to Install the Usage Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Package repository should already being configured. Refer to 
   `Configure Package Repository <../installguide/management-server/_pkg_repo.html#configure-package-repository>`_

#. Install package cloudstack-usage

   On RHEL/CentOS systems, use:
   
   .. parsed-literal::

      # yum install cloudstack-usage

   On Debian/Ubuntu systems, use:

   .. parsed-literal::
      
      # apt install cloudstack-usage

#. Once installed, start the Usage Server with the following command.

   .. parsed-literal::

      # service cloudstack-usage start

#. Enable the service at boot

   On RHEL/CentOS systems, use:
   
   .. parsed-literal::
   
      # chkconfig cloudstack-usage on
      
   On Debian/Ubuntu systems, use:

   .. parsed-literal::

      # update-rc.d cloudstack-usage defaults

:ref:`working-with-usage` discusses further configuration of the Usage
Server.


SSL (Optional)
--------------

CloudStack provides HTTP access in its default installation. There are a
number of technologies and sites which choose to implement SSL/TLS. As a
result, we have left CloudStack to expose HTTP under the assumption that
a site will implement its typical practice.

CloudStack 4.9 and above uses embedded Jetty as its servlet container. For sites
that would like CloudStack to terminate the SSL session, HTTPS can be enabled
by configuring the https-related settings in CloudStack management server's
server.properties file at /etc/cloudstack/management/ location:

   .. parsed-literal::

      # For management server to pickup these configuration settings, the configured
      # keystore file should exists and be readable by the management server.
      https.enable=true
      https.port=8443
      https.keystore=/etc/cloudstack/management/cloud.jks
      https.keystore.password=vmops.com

For storing certificates, admins can create and configure a java keystore file
and configure the same in the server.properties file as illustrated above.


Health Checks and Monitoring (Optional)
---------------------------------------

CloudStack has a plugin for exporting metrics in the format that Prometheus can consume.
This is done by enabling the following configuration parameters in the Global Settings.

   .. parsed-literal::

      # cloudmonkey update configuration name=prometheus.exporter.enable      value=true
      # cloudmonkey update configuration name=prometheus.exporter.port        value=9595
      # cloudmonkey update configuration name=prometheus.exporter.allowed.ips value="127.0.0.1,192.168.0.10"

.. note:: 
   These settings are available to be configured via the CloudStack UI as well.
   CloudStack Management needs to be restarted for the changes to take effect.
   Replace the mock IP address 192.168.0.10 with the actual IP address of the Prometheus server.

.. warning::
   A list of addresses can be provided as a comma separated list. It does NOT accept CIDR notation.

Then, configure prometheus to start pulling metrics by adding the following configuration to ``/etc/prometheus/prometheus.yml``.

   .. parsed-literal::

      - job_name: 'management'
         static_configs:
            - targets: ['192.168.0.20:9595']

.. note::
   Replace the mock IP address 192.168.0.20 with the actual IP address of the Management server.
   Public dashboards are available in the Grafana repository for visualizing CloudStack Management metrics.


Database Replication (Optional)
-------------------------------

CloudStack supports database replication from one MySQL node to another.
This is achieved using standard MySQL replication. You may want to do
this as insurance against MySQL server or storage loss. MySQL
replication enables data from one MySQL database server (the source) to be
copied to one or more MySQL database servers (the replicas). The source is the
node that the Management Servers are configured to use. The replica is a
standby node that receives all write operations from the source and
applies them to a local, redundant copy of the database. The following
steps are a guide to implementing MySQL replication.

.. note:: 
   Creating a replica is not a backup solution. You should develop a backup 
   procedure for the MySQL data that is distinct from replication.

#. Ensure that this is a fresh install with no data in the source server.

#. Edit my.cnf on the source server and add the following in the [mysqld]
   section below datadir.

   .. parsed-literal::

      log_bin=mysql-bin
      server_id=1

   The server\_id must be unique with respect to other servers. The
   recommended way to achieve this is to give the source server an ID of 1 and
   each replica a sequential number greater than 1, so that the servers
   are numbered 1, 2, 3, etc.

#. Restart the MySQL service. On RHEL/CentOS systems, use:

   .. parsed-literal::

      # service mysqld restart

   On Debian/Ubuntu systems, use:

   .. parsed-literal::

      # service mysql restart

#. Create a replication Account on the source server and give it privileges. We
   will use the "cloud-repl" user with the password "password". This
   assumes that source and replica run on the 172.16.1.0/24 Network.

   .. sourcecode: bash
   .. parsed-literal::
      # mysql -u root
      mysql> create user 'cloud-repl'@'172.16.1.%' identified by 'password';
      mysql> grant replication replica on *.* TO 'cloud-repl'@'172.16.1.%';
      mysql> flush privileges;
      mysql> flush tables with read lock;

#. Leave the current MySQL session running.

#. In a new shell start a second MySQL session.

#. Retrieve the current position of the database.

   .. parsed-literal::

      # mysql -u root
      mysql> show source status;
      +------------------+----------+--------------+------------------+
      | File             | Position | Binlog_Do_DB | Binlog_Ignore_DB |
      +------------------+----------+--------------+------------------+
      | mysql-bin.000001 |      412 |              |                  |
      +------------------+----------+--------------+------------------+

#. Note the file and the position that are returned by your Instance.

#. Exit from this session.

#. Complete the source server setup. Returning to your first session on the
   source server, release the locks and exit MySQL.

   .. parsed-literal::

      mysql> unlock tables;

#. Install and configure the replica. On the replica server, run the
   following commands.

   .. parsed-literal::

      # yum install mysql-server
      # chkconfig mysqld on

#. Edit my.cnf and add the following lines in the [mysqld] section below
   datadir.

   .. parsed-literal::

      server_id=2
      innodb_rollback_on_timeout=1
      innodb_lock_wait_timeout=600

#. Restart MySQL. Use "mysqld" on RHEL/CentOS systems:

   .. parsed-literal::

      # service mysqld restart

   On Ubuntu/Debian systems use "mysql."

   .. parsed-literal::

      # service mysql restart

#. Instruct the replica to connect to and replicate from the source.
   Replace the IP address, password, log file, and position with the
   values you have used in the previous steps.

   .. parsed-literal::

      mysql> change source to
          -> source_host='172.16.1.217',
          -> source_user='cloud-repl',
          -> source_password='password',
          -> source_log_file='mysql-bin.000001',
          -> source_log_pos=412;

#. Then start replication on the replica.

   .. parsed-literal::

      mysql> start replica;

#. Optionally, open port 3306 on the replica as was done on the source
   earlier.

   This is not required for replication to work. But if you choose not
   to do this, you will need to do it when failover to the replica
   occurs.


Failover
~~~~~~~~

This will provide for a replicated database that can be used to
implement manual failover for the Management Servers. CloudStack
failover from one MySQL instance to another is performed by the
administrator. In the event of a database failure you should:

#. Stop the Management Servers (via service cloudstack-management stop).

#. Change the replica's configuration to be a source and restart it.

#. Ensure that the replica's port 3306 is open to the Management
   Servers.

#. Make a change so that the Management Server uses the new database.
   The simplest process here is to put the IP address of the new
   database server into each Management Server's
   /etc/cloudstack/management/db.properties.

#. Restart the Management Servers:

   .. parsed-literal::

      # service cloudstack-management start

