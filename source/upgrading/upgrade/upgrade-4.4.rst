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


.. |version_to_upgrade| replace:: 4.4.x

Upgrade Instruction from |version_to_upgrade|
=============================================

This section will guide you from CloudStack |version_to_upgrade| to CloudStack 
|release|.

Any steps that are hypervisor-specific will be called out with a note.

We recommend reading through this section once or twice before beginning
your upgrade procedure, and working through it on a test system before
working on a production system.

.. note:: 
    The following upgrade instructions should be performed regardless of
    hypervisor type.

Upgrade Steps:

#. Backup CloudStack database (MySQL)
#. Install new systemvm Template
#. Add package repository for MySQL connector
#. Upgrade CloudStack management server(s)
#. Update hypervisors specific dependencies


Packages repository
-------------------

Most users of CloudStack manage the installation and upgrades of
CloudStack with one of Linux's predominant package systems, RPM or
APT. This guide assumes you'll be using RPM and Yum (for Red Hat
Enterprise Linux or CentOS), or APT and Debian packages (for Ubuntu).

Create RPM or Debian packages (as appropriate) and a repository from
the |release| source, or check the Apache CloudStack downloads page at
http://cloudstack.apache.org/downloads.html
for package repositories supplied by community members. You will need
them for :ref:`ubuntu44` or :ref:`rhel44` and :ref:`kvm44` hosts upgrade. 

Instructions for creating packages from the CloudStack source are in the 
`CloudStack Installation Guide`_.

.. include:: _sysvm_templates.rst

.. include:: _java_version.rst


Database Preparation
--------------------

Backup current database

#. Stop your management server or servers. Run this on all management
   server hosts:

   .. parsed-literal::

      $ sudo service cloudstack-management stop

#. If you are running a usage server or usage servers, stop those as well:

   .. parsed-literal::

      $ sudo service cloudstack-usage stop

#. Make a backup of your MySQL database. If you run into any issues or
   need to roll back the upgrade, this will assist in debugging or
   restoring your existing environment. You'll be prompted for your
   password.

   .. parsed-literal::

      $ mysqldump -u root -p cloud > cloud-backup_$(date +%Y-%m-%d-%H%M%S)
      $ mysqldump -u root -p cloud_usage > cloud_usage-backup_$(date +%Y-%m-%d-%H%M%S)


.. _ubuntu44:

Management Server on Ubuntu
---------------------------

If you are using Ubuntu, follow this procedure to upgrade your packages. If 
not, skip to step :ref:`rhel44`.

.. include:: _timezone.rst

.. note:: 
   **Community Packages:** This section assumes you're using the community
   supplied packages for CloudStack. If you've created your own packages and
   APT repository, substitute your own URL for the ones used in these examples.

The first order of business will be to change the sources list for
each system with CloudStack packages. This means all management
servers, and any hosts that have the KVM agent. (No changes should
be necessary for hosts that are running VMware or Xen.)


.. _apt-repo44:


CloudStack apt repository
^^^^^^^^^^^^^^^^^^^^^^^^^

   Start by opening ``/etc/apt/sources.list.d/cloudstack.list`` on
   any systems that have CloudStack packages installed.

   This file should have one line, which contains:

   .. parsed-literal::

      deb http://download.cloudstack.org/ubuntu precise 4.4

   We'll change it to point to the new package repository:

   .. parsed-literal::

      deb http://download.cloudstack.org/ubuntu precise 4.9

   Setup the public key for the above repository:

   .. parsed-literal::

      wget -qO - http://download.cloudstack.org/release.asc | sudo apt-key add -

   If you're using your own package repository, change this line to
   read as appropriate for your |version| repository.

#. Now update your apt package list:

   .. parsed-literal::

      $ sudo apt-get update

#. Now that you have the repository configured, it's time to upgrade
    the ``cloudstack-management`` package.

   .. parsed-literal::

      $ sudo apt-get upgrade cloudstack-management

#. If you use CloudStack usage server

    .. parsed-literal::

        $ sudo apt-get upgrade cloudstack-usage


.. _rhel44:

Management Server on CentOS/RHEL
--------------------------------

If you are using CentOS or RHEL, follow this procedure to upgrade your 
packages. If not, skip to hypervisors section :ref:`upg_hyp_44`.

.. include:: _timezone.rst

.. note:: 
   **Community Packages:** This section assumes you're using the community
   supplied packages for CloudStack. If you've created your own packages and
   yum repository, substitute your own URL for the ones used in these examples.

.. include:: _mysql_connector.rst


.. _rpm-repo44:

CloudStack RPM repository
^^^^^^^^^^^^^^^^^^^^^^^^^^

The first order of business will be to change the yum repository
for each system with CloudStack packages. This means all
management servers, and any hosts that have the KVM agent.

(No changes should be necessary for hosts that are running VMware
or Xen.)

Start by opening ``/etc/yum.repos.d/cloudstack.repo`` on any
systems that have CloudStack packages installed.

This file should have content similar to the following:

.. parsed-literal::

   [apache-cloudstack]
   name=Apache CloudStack
   baseurl=http://download.cloudstack.org/rhel/4.4/
   enabled=1
   gpgcheck=0

If you are using the community provided package repository, change
the base url to ``http://download.cloudstack.org/centos/$releasever/4.9/``.

Setup the GPG public key if you wish to enable ``gpgcheck=1``:

.. parsed-literal::

   rpm --import http://download.cloudstack.org/RPM-GPG-KEY


If you're using your own package repository, change this line to
read as appropriate for your |version| repository.

#. Remove the deprecated dependency for awsapi.

   .. parsed-literal::

      $ sudo rpm -e --nodeps cloudstack-awsapi

#. Now that you have the repository configured, it's time to upgrade the 
    ``cloudstack-management``.

   .. parsed-literal::

      $ sudo yum upgrade cloudstack-management

#. If you use CloudStack usage server

   .. parsed-literal::

      $ sudo yum upgrade cloudstack-usage

.. _upg_hyp_44:

Hypervisor: XenServer
---------------------

**(XenServer only)** Copy vhd-utils file on CloudStack management servers.
Copy the file `vhd-utils <http://download.cloudstack.org/tools/vhd-util>`_
to ``/usr/share/cloudstack-common/scripts/vm/hypervisor/xenserver``.

.. parsed-literal::

   wget -P /usr/share/cloudstack-common/scripts/vm/hypervisor/xenserver \
   http://download.cloudstack.org/tools/vhd-util

.. include:: _xenserver_upg.rst


Hypervisor: VMware
------------------

.. warning::
    For VMware hypervisor CloudStack management server packages must be
    build using "noredist". Refer to :ref:`building-noredist`

**(VMware only)** Additional steps are required for each VMware cluster.
These steps will not affect running guests in the cloud. These steps
are required only for clouds using VMware clusters:

#. Stop the Management Server:

   .. parsed-literal::

      $ sudo service cloudstack-management stop

#. Generate the encrypted equivalent of your vCenter password:

   .. parsed-literal::

      $ java -classpath /usr/share/cloudstack-common/lib/jasypt-1.9.2.jar org.jasypt.intf.cli.JasyptPBEStringEncryptionCLI encrypt.sh input="_your_vCenter_password_" password="`cat /etc/cloudstack/management/key`" verbose=false

   Store the output from this step, we need to add this in
   cluster\_details table and vmware\_data\_center tables in place of
   the plain text password

#. Find the ID of the row of cluster\_details table that you have to
   update:

   .. parsed-literal::

      $ mysql -u <username> -p<password>

   .. parsed-literal::

      select * from cloud.cluster_details;

#. Update the plain text password with the encrypted one

   .. parsed-literal::

      update cloud.cluster_details set value = '_ciphertext_from_step_1_' where id = _id_from_step_2_;

#. Confirm that the table is updated:

   .. parsed-literal::

      select * from cloud.cluster_details;

#. Find the ID of the correct row of vmware\_data\_center that you
    want to update

   .. parsed-literal::

      select * from cloud.vmware_data_center;

#. update the plain text password with the encrypted one:

   .. parsed-literal::

      update cloud.vmware_data_center set password = '_ciphertext_from_step_1_'
      where id = _id_from_step_5_;

#. Confirm that the table is updated:

   .. parsed-literal::

      select * from cloud.vmware_data_center;


.. _kvm44:

Hypervisor: KVM
---------------

KVM on Ubuntu
^^^^^^^^^^^^^

(KVM only) Additional steps are required for each KVM host. These
steps will not affect running guests in the cloud. These steps are
required only for clouds using KVM as hosts and only on the KVM
hosts.

#. Configure the :ref:`APT repo <apt-repo44>` as detailed above.

#. Stop the running agent.

   .. parsed-literal::

      $ sudo service cloudstack-agent stop

#. Update the agent software.

   .. parsed-literal::

      $ sudo apt-get upgrade cloudstack-agent

#. Verify that the file ``/etc/cloudstack/agent/environment.properties`` has a 
    line that reads:

   .. parsed-literal::

      paths.script=/usr/share/cloudstack-common

   If not, add the line.

#. Start the agent.

   .. parsed-literal::

      $ sudo service cloudstack-agent start


KVM on CentOS/RHEL
^^^^^^^^^^^^^^^^^^
For KVM hosts, upgrade the ``cloudstack-agent`` package

#. Configure the :ref:`rpm-repo44` as detailed above.

   .. parsed-literal::

      $ sudo yum upgrade cloudstack-agent

#. Verify that the file ``/etc/cloudstack/agent/environment.properties`` has a 
   line that reads:

   .. parsed-literal::

      paths.script=/usr/share/cloudstack-common

   If not, add the line.

#. Restart the agent:

   .. parsed-literal::

      $ sudo service cloudstack-agent stop
      $ sudo service cloudstack-agent start


Restart management services
---------------------------
#. If upgrading fresh installation of 4.4.0

   If you are upgrading fresh installation of CloudStack 4.4.0, the following MySQL
   command must be executed before restarting the management server. If the system
   was running pre 4.4 and then upgraded to 4.4.0, the MySQL command is not required.
   Refer to: `CLOUDSTACK-7813 <https://issues.apache.org/jira/browse/CLOUDSTACK-7813>`_

   .. sourcecode:: mysql

      use cloud;
      ALTER TABLE `snapshot_policy` ADD `display` TINYINT( 1 ) NOT NULL DEFAULT '1';

#. Now it's time to start the management server

   .. parsed-literal::

      $ sudo service cloudstack-management start

#. If you use it, start the usage server

   .. parsed-literal::

      $ sudo service cloudstack-usage start


.. _upg-sysvm44:

.. include:: _sysvm_restart.rst
