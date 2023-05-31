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

Overview
--------

This section describes installing the Management Server. There are two
slightly different installation flows, depending on how many Management
Server nodes will be in your cloud:

-  A single Management Server node, with MySQL on the same node.

-  Multiple Management Server nodes, with MySQL on a node separate from
   the Management Servers.

In either case, each machine must meet the system requirements described
in :ref:`minimum-system-requirements`.

.. warning::
   For the sake of security, be sure the public Internet can not access port
   8096 or port 8250 on the Management Server.

The procedure for installing the Management Server is:

#. Prepare the Operating System

#. (XenServer only) Download and install vhd-util.

#. Install the First Management Server

#. Install and Configure the MySQL database

#. Prepare NFS Shares

#. Prepare and Start Additional Management Servers (optional)

#. Prepare the System VM Template


Prepare the Operating System
----------------------------

The OS must be prepared to host the Management Server using the
following steps. These steps must be performed on each Management Server
node.

#. Log in to your OS as root.

#. Check for a fully qualified hostname.

   .. parsed-literal::

      hostname --fqdn

   This should return a fully qualified hostname such as
   "management1.lab.example.org". If it does not, edit /etc/hosts so
   that it does.

#. Make sure that the machine can reach the Internet.

   .. parsed-literal::

      ping cloudstack.apache.org

#. Turn on NTP for time synchronization.

   .. note::
      An NTP daemon is required to synchronize the clocks of the servers in your cloud.

   Install chrony.

   In RHEL or CentOS:

      .. parsed-literal::

         $ yum install chrony

   In Ubuntu:

      .. parsed-literal::

         $ apt install chrony

   In SUSE:

      .. parsed-literal::

         $ zypper install chrony

#. Repeat all of these steps on every host where the Management Server
   will be installed.

.. warning::
   CloudStack |version| requires Java 11 JRE. Installing CloudStack packages will
   automatically install Java 11, but it's good to explicitly confirm that the Java 11
   is the selected/active one (in case you had a previous Java version already installed)
   with ``alternatives --config java`` after CloudStack packages are already installed.
