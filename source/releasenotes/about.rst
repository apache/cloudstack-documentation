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


What's New in |release|
=======================

Apache CloudStack |release| is a |version| LTS release with over 15 major new features, and over 200 enhancements and fixes since 4.13.  Highlights include:

•	New modern UI (Project Primate, Technical preview)
•	Backup and Recovery framework
•	Backup and Recovery Provider for Veeam
•	VM ingestion
•	L2 network PVLAN enhancements
•	CloudStack Kubernetes Service
•	UEFI support
•	KVM rolling maintenance
•	Enable Direct Download for systemVM templates
•	VR health checks
•	Download logs and diagnostics data from SSVM/CPVM/VRs
•	Enable additional configuration metadata to virtual machines


The full list of new features can be found in the project release notes at http://docs.cloudstack.apache.org/en/4.14.0.0/releasenotes/changes.html

.. note:: 
   This version of CloudStack allows control over the visibility of the DNS services provided
   by the Virtual Router. One can control whether the service on the routers be available to 
   networks outside the local network. This might be important on Shared Networks which are 
   using Internet routable/public (i.e. non-RFC 1918) IP addresses. The new global setting 
   "expose.dns.externally" has been added with a default value of "true" in order to keep backward compatibility
   with the previous installations. If you wish to disable public access to the DNS services
   running on Virtual Router, set the value to "false" and recreate the related Virtual Routers.

Apache CloudStack powers numerous elastic Cloud computing services, including solutions that have ranked as Gartner Magic Quadrant leaders. Highlighted in the Forrester Q4 2017 Enterprise Open Source Cloud Adoption report, Apache CloudStack "sits beneath hundreds of service provider clouds", including Fortune 5 multinational corporations. A list of known Apache CloudStack users are available at http://cloudstack.apache.org/users.html

New Modern UI / Old UI Deprecation Notice
------------------------------------------

A modern UI for Apache CloudStack - Primate has been proposed, a technical preview of which
can be evaluated with this release. Please see the `Primate install guide <../installguide/primate.html>`_.

The current legacy UI will be deprecated in the next CloudStack major release which will ship
Primate GA and in later CloudStack major release the legacy UI will be removed.
