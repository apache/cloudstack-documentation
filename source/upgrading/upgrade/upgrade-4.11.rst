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


.. |version_to_upgrade| replace:: 4.11.x

Upgrade Instruction from |version_to_upgrade|
=============================================

This section will guide you from CloudStack |version_to_upgrade| to latest
CloudStack |release|.

Any steps that are hypervisor-specific will be called out with a note.

We recommend reading through this section once or twice before beginning
your upgrade procedure, and working through it on a test system before
working on a production system.

.. note::
    The following upgrade instructions should be performed regardless of
    hypervisor type.

Overview of Upgrade Steps:
----------------------------

#. Check any customisations and integrations
#. Upload the |sysvm64-version| System VM template if not already using it.
#. Stop all running management servers
#. Backup CloudStack database (MySQL)
#. Upgrade 1st CloudStack management server
#. Update hypervisors specific dependencies
#. Restart 1st management server
#. Check that your upgraded environment works as expected
#. Upgrade and restart the remaining management servers



.. include:: _customisation_warnings.rst

.. warning::
    If you are not already using the |sysvm64-version| System VM template you will need to 
    upgrade your System VM template prior to performing the upgrade of the 
    CloudStack packages.

.. include:: _sysvm_templates.rst

.. include:: _java_version.rst

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
them for :ref:`ubuntu411` or :ref:`rhel411` and :ref:`kvm411` hosts upgrade.

Instructions for creating packages from the CloudStack source are in the
`CloudStack Installation Guide`_.

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

      $ mysqldump -u root -p -R cloud > cloud-backup_$(date +%Y-%m-%d-%H%M%S)
      $ mysqldump -u root -p cloud_usage > cloud_usage-backup_$(date +%Y-%m-%d-%H%M%S)


.. _ubuntu411:
.. _apt-repo411:

Management Server
-----------------

.. include:: _timezone.rst

Ubuntu
######


If you are using Ubuntu, follow this procedure to upgrade your packages. If
not, skip to step :ref:`rhel411`.

.. note::
   **Community Packages:** This section assumes you're using the community
   supplied packages for CloudStack. If you've created your own packages and
   APT repository, substitute your own URL for the ones used in these examples.

The first order of business will be to change the sources list for
each system with CloudStack packages. This means all management
servers, and any hosts that have the KVM agent. (No changes should
be necessary for hosts that are running VMware or Xen.)

Start by opening ``/etc/apt/sources.list.d/cloudstack.list`` on
any systems that have CloudStack packages installed.

This file should have one line, which contains:

.. parsed-literal::

   deb http://download.cloudstack.org/ubuntu precise 4.11

We'll change it to point to the new package repository:

.. parsed-literal::

   deb http://download.cloudstack.org/ubuntu precise |version|

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


.. _rhel411:
.. _rpm-repo411:

CentOS/RHEL
##############

If you are using CentOS or RHEL, follow this procedure to upgrade your
packages. If not, skip to hypervisors section :ref:`upg_hyp_411`.

.. note::
   **Community Packages:** This section assumes you're using the community
   supplied packages for CloudStack. If you've created your own packages and
   yum repository, substitute your own URL for the ones used in these examples.

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
   baseurl=http://download.cloudstack.org/centos/7/4.11/
   enabled=1
   gpgcheck=0

If you are using the community provided package repository, change the base url to:

.. parsed-literal::

   http://download.cloudstack.org/centos/$releasever/|version|/

Setup the GPG public key if you wish to enable ``gpgcheck=1``:

.. parsed-literal::

   rpm --import http://download.cloudstack.org/RPM-GPG-KEY



If you're using your own package repository, change this line to
read as appropriate for your |version| repository.

#. Now that you have the repository configured, it's time to upgrade the
   ``cloudstack-management``.

   .. parsed-literal::

      $ sudo yum upgrade cloudstack-management

#. If you use CloudStack usage server

   .. parsed-literal::

      $ sudo yum upgrade cloudstack-usage

.. _upg_hyp_411:

Upgrade Hypervisors
-------------------

Hypervisor: XenServer
#####################

No additional steps are required wrt for XenServer Hypervisor for this upgrade.


Hypervisor: VMware
###################

.. warning::
   For VMware hypervisor CloudStack management server packages must be
   build using "noredist". Refer to :ref:`building-noredist`.


No additional steps are requried for the VMware Hypervisor for this upgrade.


.. _kvm411:

Hypervisor: KVM
#################

KVM on Ubuntu
""""""""""""""

(KVM only) Additional steps are required for each KVM host. These
steps will not affect running guests in the cloud. These steps are
required only for clouds using KVM as hosts and only on the KVM
hosts.

#. Configure the :ref:`APT repo <apt-repo411>` as detailed above.

#. Stop the running agent.

   .. parsed-literal::

      $ sudo service cloudstack-agent stop

#. Update the agent software.

   .. parsed-literal::

      $ sudo apt-get upgrade cloudstack-agent

#. Start the agent.

   .. parsed-literal::

      $ sudo service cloudstack-agent start


KVM on CentOS/RHEL
"""""""""""""""""""

For KVM hosts, upgrade the ``cloudstack-agent`` package

#. Configure the :ref:`rpm-repo411` as detailed above.

   .. parsed-literal::

      $ sudo yum install -y epel-release
      $ sudo yum install -y python36-libvirt
      $ sudo yum upgrade cloudstack-agent

#. Restart the agent:

   .. parsed-literal::

      $ sudo service cloudstack-agent stop
      $ sudo service cloudstack-agent start


Restart management services
---------------------------

#. Now it's time to start the management server

   .. parsed-literal::

      $ sudo service cloudstack-management start

#. If you use it, start the usage server

   .. parsed-literal::

      $ sudo service cloudstack-usage start


.. include:: _sysvm_restart.rst
