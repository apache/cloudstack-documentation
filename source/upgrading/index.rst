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

.. CloudStack Release Notes documentation main file, created by
   sphinx-quickstart on Fri Feb  7 16:00:59 2014.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

|menu_acs_logo|


Upgrading CloudStack
====================


This document contains the instructions for upgrading CloudStack from prior releases, to the current 
release.  Please read through all sections carefully before starting.

From ACS 4.16 onwards, seeding of system-VM Template is optional, as this will be taken care of by either the upgrade process or
in case of a fresh deployment, registration of the systemVM Template(s) is handled during the addition of the first image store to a zone.
The `cloudstack-management` package will now include the systemVM Templates for KVM, XenServer and VMWare. In case Templates aren't already registered
either prior upgrade or during fresh installation, ACS will handle the Template registration automatically, by mounting the secondary store onto the
management server, copying the respective Templates to the store and then creating the `template.properties` file.

.. note::
   For information on the API changes and issues fixed in this release, please see the Release Notes section of the documentation

Contents:

.. toctree::
   :maxdepth: 1

   upgrade/mysql
   upgrade/valid_source
   upgrade/upgrade-4.19
   upgrade/upgrade-4.18
   upgrade/upgrade-4.17
   upgrade/upgrade-4.16
   upgrade/upgrade-4.15
   upgrade/upgrade-4.14
   upgrade/upgrade-4.13
   upgrade/upgrade-4.12
   upgrade/upgrade-4.11
   upgrade/upgrade-4.10
   upgrade/upgrade-4.9
   upgrade/upgrade-4.8
   upgrade/upgrade-4.7
   upgrade/upgrade-4.6
   upgrade/upgrade-4.5
   upgrade/upgrade-4.4
   upgrade/upgrade-4.3
..   upgrade/upgrade-4.2
..   upgrade/upgrade-4.1
..   upgrade/upgrade-4.0
..   upgrade/upgrade-3.0.x
..   upgrade/upgrade-2.2.14
