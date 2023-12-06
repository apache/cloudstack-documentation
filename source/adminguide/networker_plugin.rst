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
#. A proper timezone set. Identical to the Hypervisors and Management server
#. Proper DNS resolution of the Clients

KVM Hypervisor(s)

#. A BASH shell at minimum version 4.4.19
#. DELL EMC Networker client must be installed and in running state
#. Hypervisor must be associated with the DELL EMC Networker server as CLIENT
#. DELL EMC Networker can connect and verify certificates to the Hyper-v Client
#. A Hypervisor must be in UP and ENABLED state and resource state respectively in order to be able to get backups
   for the Instances running.
#. A proper timezone set. Identical to the EMC Networker Server and Management server
#. Proper DNS resolution of the EMC Networker server

Instances

#. It is HIGHLY recommended to run qemu-guest-agent on the Machines you are planning to backup.
#. There has been no testing regarding KVM Primary Storage Snapshots and possible problems with EMC DELL Networker plugin
#. In case you are using KVM Primary Storage Snapshots, you have EMC Networker and you want to proceed with the
   installation of this plugin proceed with extreme caution.

General Concepts

#. DELL EMC Networker POLICIES are presented as Backup Provider Offerings to Cloudstack.
   At that level we can set the Protection Period (aka Expiration) to specify when backups
   will expire. Restricted data zones can also be defined in POLICIES to create fine grain permissions.
#. As per EMC Networker Glossary and design those POLICIES are not actually used. They act as a placeholder
   for the backup offerings and the retention policies.
#. DELL EMC Networker has no ability to initiate backup tasks for KVM Instances at the moment.
   The implementation is based on manual save sets initiated by the Cloudstack Networker plugin.
#. The tag -CSBKP- in the comment of the POLICY indicates that this policy is available to Cloudstack
   Other POLICIES used in your infrastructure will not be visible inside Cloudstack. It is recommended to create
   brand new POLICIES dedicated to Cloudstack and settings the Protection Periods to match the backup plan retention
   you wish to enable for each of the offerings.
#. For each KVM Cluster you have, a relevant dummy client must be created in the DELL EMC Networker. This is used as a
   placeholder for being able to backup and restore your Instances from all hosts within the cluster.
#. Cross cluster restores are indirectly supported by restoring to the original cluster and then migrating the Virtual
   Machine to the destination cluster.
#. Any manual KVM backup you initiate (from the hyper-v command line) will be registered in Cloudstack automatically.
   You need to use the client scripts and pass the proper parameters to do so.
#. Any backup you expire/remove from the DELL EMC Networker side will be unregistered in Cloudstack automatically.

Installing DELL EMC Networker Backup and Recovery Plugin
--------------------------------------------------------

The B&R Networker plugin has been designed and implemented taking in mind the particularities of the DELL EMC Networker
backup suite. It has been developed and tested against 19.4.0.6 and the minimum supported version is 9.2.

The installation and configuration of the DELL EMC Networker is out of scope and it is assumed that it has been properly
performed in advance. Kindly make sure that DNS resolution, Timezones and system clocks are set/synced for KVM Hypervisors,
Cloudstack Management Servers and DELL EMC Networker Server. Do not forget to perform your staging actions (if any)
before the savesets expire.

Depending on your topology, network bandwidth, backend storage speeds, number of customer Instances you should carefully plan,
design and implement the Storage volumes, media pools. If you have multiple Instances that your customers want to be processed
at the same time (e.g Friday night, end of business day in your timezone) this can easily overwhelm your resources since
the backups are initiated outside DELL EMC Networker.

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

#. Check your cluster name (e.g from cloud monkey).
   Please note that cluster name case sensitivity matters.

   |BnR-Networker-clustername.jpg|

#. Create relevant DNS entries for all your KVM clusters in your nameservers or add it in the /etc/hosts of your
   DELL EMC NETWORKER server. The IP addresses can be anything you want but must be present.

#. Create a client representing the cluster on the EMC Networker Side

   |BnR-Networker-Cluster-Client-General.jpg|
   |BnR-Networker-Cluster-Client-Globals1.jpg|

#. Include all the users and hypervisor hosts on the Global (2 of 2) page

   |BnR-Networker-Cluster-Client-Globals2.jpg|

#. Your final client configuration should have all KVM hosts and Clusters defined.

   |BnR-Networker-Cluster-Clients-overview.jpg|


Connecting CloudStack to DELL EMC Networker
----------------------------------------------

Before enabling DELL EMC Networker make sure that the user account Cloudstack uses to connect to your KVM Hypervisors
can execute via SUDO and with no required password the following binary from EMC Networker:

#. /usr/sbin/recover

Also make sure that the user account Cloudstack uses to connect to your KVM Hypervisors is member of the libvirt group.

Updating the global settings listed below will allow you to start the importing of the backup offerings to Cloudstack.

Plug-in specific settings:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

(all settings can be global or per-zone)

.. cssclass:: table-striped table-bordered table-hover

========================================  =============================================================================
Configuration                             Description
========================================  =============================================================================
backup.plugin.networker.url               DELL EMC Networker server URL. Default: https://localhost:9090/nwrestapi/v3
backup.plugin.networker.username          DELL EMC Networker server username. Default: administrator
backup.plugin.networker.password          DELL EMC Networker server password. Default: password
backup.plugin.networker.pool              DELL EMC Networker Media Pool. Default: Default
backup.plugin.networker.validate.ssl      Whether to validate API server (SSL/TLS) connection.  Default: false
backup.plugin.networker.request.timeout   DELL EMC Networker API request timeout in seconds. Default: 300
backup.plugin.networker.client.verbosity  DELL EMC Networker Client verbosity: Default: false
========================================  =============================================================================


Client Logs and Verbosity
-------------------------

The default location for the logs is under /nsr/logs/cloudstack for each KVM Hypervisor. You should be familiar with that
location from your usual Networker debugging. By setting the verbosity to true you will have comprehensive step by step
list of all the actions and failures. For production use and when not debugging it is recommended to not use verbose logging.

It is also recommended to add that location to your regular log rotating policy.


.. |BnR-Networker-Policy.jpg| image:: /_static/images/BnR-Networker-Policy.jpg
   :alt: Create Networker Policy.
   :width: 350 px
.. |BnR-Networker-Policies.jpg| image:: /_static/images/BnR-Networker-Policies.jpg
   :alt: Networker Policies.
   :width: 400 px
.. |BnR-Networker-MediaPool-General.jpg| image:: /_static/images/BnR-Networker-MediaPool-General.jpg
   :alt: Media Pool General Properties.
   :width: 350 px
.. |BnR-Networker-MediaPool-Configuration.jpg| image:: /_static/images/BnR-Networker-MediaPool-Configuration.jpg
   :alt: Media Pool Configuration Properties.
   :width: 350 px
.. |BnR-Networker-clustername.jpg| image:: /_static/images/BnR-Networker-clustername.jpg
   :alt: Cluster Client CMK.
   :width: 400 px
.. |BnR-Networker-Cluster-Client-General.jpg| image:: /_static/images/BnR-Networker-Cluster-Client-General.jpg
   :alt: Cluster Client Creation.
   :width: 350 px
.. |BnR-Networker-Cluster-Client-Globals1.jpg| image:: /_static/images/BnR-Networker-Cluster-Client-Globals1.jpg
   :alt: Cluster client Globals (1 of 2).
   :width: 350 px
.. |BnR-Networker-Cluster-Client-Globals2.jpg| image:: /_static/images/BnR-Networker-Cluster-Client-Globals2.jpg
   :alt: Cluster client Globals (2 of 2).
   :width: 350 px
.. |BnR-Networker-Cluster-Clients-overview.jpg| image:: /_static/images/BnR-Networker-Cluster-Clients-overview.jpg
   :alt: Cluster Clients Overview.
   :width: 300 px
