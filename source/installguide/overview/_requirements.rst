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

.. _minimum-system-requirements:

Minimum System Requirements
---------------------------


Management Server, Database, and Storage System Requirements
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The machines that will run the Management Server and MySQL database must
meet the following requirements. The same machines can also be used to
provide primary and secondary storage, such as via localdisk or NFS. The
Management Server may be placed on an Instance.

-  Operating system:

   -  Preferred: CentOS/RHEL 7.2+ or Ubuntu 16.04(.2) or higher

-  64-bit x86 CPU (more cores results in better performance)

-  4 GB of memory

-  250 GB of local disk (more results in better capability; 500 GB
   recommended)

-  At least 1 NIC

-  Statically allocated IP address

-  Fully qualified domain name as returned by the hostname command


Host/Hypervisor System Requirements
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The host is where the cloud services run in the form of guest virtual
machines. Each host is one machine that meets the following
requirements:

-  Must support HVM (Intel-VT or AMD-V enabled).

-  64-bit x86 CPU (more cores results in better performance)

-  Hardware virtualization support required

-  4 GB of memory

-  36 GB of local disk

-  At least 1 NIC

-  Latest hotfixes applied to hypervisor software

-  When you deploy CloudStack, the hypervisor host must not have any VMs
   already running

-  All hosts within a cluster must be homogeneous. The CPUs must be of
   the same type, count, and feature flags.

Hosts have additional requirements depending on the hypervisor. See the
requirements listed at the top of the Installation section for your
chosen hypervisor:

.. warning::
   Be sure you fulfill the additional hypervisor requirements and installation 
   steps provided in this Guide. Hypervisor hosts must be properly prepared to 
   work with CloudStack. For example, the requirements for XenServer are 
   listed under Citrix XenServer Installation.
