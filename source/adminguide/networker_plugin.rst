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

.. _DELL EMC Networker Backup and Recovery Plugin:

DELL EMC Networker Backup and Recovery Plugin
=============================================

About the DELL EMC Networker Backup and Recovery Plugin
---------------------------------------------------------

Administrators must make sure that the following requirements and prerequisites are met in order for the plugin
to work as expected.

EMC Networker Server

#. A fairly recent .rpm or .deb Linux distribution that is supported by DELL EMC Networker for the installed version.
#. Network connectivity between the Cloudstack Management Servers in your zone and DELL EMC Networker Server
#. Administration access to the DELL EMC Networker management consoles
#. Unrestricted access to API port (running default at: 9090/tcp)
#. A proper timezone set. Identical to the Hypervisors
#. Proper DNS resolution of the Clients

KVM Hypervisor(s)

#. A BASH shell at minimum version 4.4.19
#. DELL EMC Networker must be installed and running
#. Hypervisor must be associated with the DELL EMC Networker server as CLIENT
#. In order to get backup for a VM running in a specific Hypervisor
   State and Resource State must be UP and ENABLED respectively.
#. A proper timezone set. Identical to the EMC Networker Server
#. Proper DNS resolution of the EMC Networker server

Virtual Machines

#. It is HIGHLY recommended to run qemu-guest-agent on the Machines you are planning to backup.
#. There has been no testing regarding KVM Primary Storage snapshots and possible problems with EMC DELL Networker plugin
#. In case you are using KVM Primary Storage snapshots, you have EMC Networker and you want to proceed with the
   installation of this plugin proceed with extreme caution.

General Concepts

#. DELL EMC Networker POLICIES are presented as Backup Provider Offerings to Cloudstack.
   At that level we can set the Protection Period (aka Expiration) to specify when old backups
   will expire. Restricted data zones can also be defined in POLICIES to create fine grain permissions.
#. DELL EMC Networker has no ability to initiate backup tasks for KVM Virtual Machines at the moment.
   The implementation is based on manual save sets initiated by the Cloudstack Networker plugin.
#. The tag -CSBKP- in the comment of the POLICY indicates that this policy is available to Cloudstack
   Other POLICIES used in your infrastructure will not be visible inside Cloudstack. It is recommended to create
   brand new POLICIES dedicated to Cloudstack and settings the Protection Periods to match the backup plan retention
   you wish to enable for each of the offerings.
#. For each KVM Cluster you have, a relevant dummy client must be created in the DELL EMC Networker. This is used as a
   placeholder for being able to backup and restore your Virtual Machines from all hosts within the cluster.
#. Cross cluster restores are indirectly supported by restoring to the original cluster and then migrating the Virtual
   Machine to the destination cluster.


Installing DELL EMC Networker Backup and Recovery Plugin
--------------------------------------------------------

The B&R Networker plugin has been designed and implemented taking in mind the particularities of the DELL EMC Networker
backup suite. It has been developed and tested against 19.4.0.6 and the minimum supported version is 9.2.

The installation and configuration of the DELL EMC Networker is out of scope and it is assumed that it has been properly
performed in advance. Kindly make sure that DNS resolution, Timezones and system clocks are set/synced for KVM Hypervisors,
Cloudstack Management Servers and DELL EMC Networker Server.

A brief Outline of the prerequisite steps is provided.

#. Install / Configure DELL EMC Networker Server (if you don't already have one running)
#. Set timezone and enable ntp/chrony
#. Set proper DNS Servers or alternatively add all KVM Hypervisors to /etc/hosts
#. Install DELL EMC Networker client and extended client packages to all Hypervisors
#. Add all KVM Hypervisors as Clients in the EMC Networker (Traditional Backup)
#. Create a USER in EMC DELL Networker with privileges to create/delete backups


Creating POLICIES on the Networker Side
----------------------------------------

#. In the DELL EMC Networker Management Console create the desired POLICIES including the -CSBKP- tag in the
   comment section.

   |BnR-Networker-Policy.jpg|

#. After finishing with the POLICIES you will end up with something like this

   |BnR-Networker-Policies.jpg|

#. Create a dedicated Media Pool (recommended but not required).

    |BnR-Networker-MediaPool-General.jpg|

#. Set the configuration values according to your environment, equipment, needs and constraints.

   |BnR-Networker-MediaPool-Configuration.jpg|

#. In Selection Criteria tab you can select the device(s) associated with that Media Pool. A use of a deduplication
   capable storage device (such as DataDomain) is recommended.

Connecting CloudStack to DELL EMC Networker
----------------------------------------------

Before enabling DELL EMC Networker make sure that the user account that Cloudstack uses to connect to your KVM Hypervisors
can execute via SUDO and with no required passwords the following two scripts:

#. /usr/share/cloudstack-common/scripts/vm/hypervisor/kvm/nsrkvmbackup.sh
#. /usr/share/cloudstack-common/scripts/vm/hypervisor/kvm/nsrkvmrestore.sh

Updating the global settings listed below will allow you to start the importing of the backup offerings to Cloudstack.

Plug-in specific settings:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

(all settings can be global or per-zone)

.. cssclass:: table-striped table-bordered table-hover

==================================== ========================
Configuration                         Description
==================================== ========================
backup.plugin.networker.url              DELL EMC Networker server URL. Default: https://localhost:9090/nwrestapi/v3
backup.plugin.networker.username         DELL EMC Networker server username. Default: administrator
backup.plugin.networker.password         DELL EMC Networker server password. Default: password
backup.plugin.networker.pool             DELL EMC Networker Media Pool. Default: Default
backup.plugin.networker.validate.ssl     Whether to validate API server (SSL/TLS) connection  Default: false
backup.plugin.networker.request.timeout  DELL EMC Networker API request timeout in seconds. Default: 300
backup.plugin.networker.client.verbosity DELL EMC Networker Client verbosity: Default: false
==================================== ========================

Client Logs and Verbosity
-------------------------

The default location for the logs is under /nsr/logs/cloudstack for each KVM Hypervisor. You should be familiar with that
location from your usual Networker debugging. By setting the verbosity to true you will have comprehensive step by step
list of all the actions and failures. For production use and when not debugging it is recommended to not use verbose logging.


.. |BnR-Networker-Policy.jpg| image:: /_static/images/BnR-Networker-Policy.jpg
   :alt: Create Networker Policy.
   :width: 300 px
.. |BnR-Networker-Policies.jpg| image:: /_static/images/BnR-Networker-Policies.jpg
   :alt: Networker Policies.
   :width: 300 px
.. |BnR-Networker-MediaPool-General.jpg| image:: /_static/images/BnR-Networker-MediaPool-General.jpg
   :alt: Media Pool General Properties.
   :width: 300 px
.. |BnR-Networker-MediaPool-Configuration.jpg| image:: /_static/images/BnR-Networker-MediaPool-Configuration.jpg
   :alt: Media Pool Configuration Properties.
   :width: 600 px