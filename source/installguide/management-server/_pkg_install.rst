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

Install the Management Server on the First Host
-----------------------------------------------

The first step in installation, whether you are installing the
Management Server on one host or many, is to install the software on a
single node.

.. note::
   If you are planning to install the Management Server on multiple nodes for
   high availability, do not proceed to the additional nodes yet. That step
   will come later.

The CloudStack Management server can be installed using either RPM or
DEB packages. These packages will depend on everything you need to run
the Management server.

.. include:: _pkg_repo.rst


Install on CentOS/RHEL
^^^^^^^^^^^^^^^^^^^^^^

.. parsed-literal::

   yum install cloudstack-management

Install on SUSE
^^^^^^^^^^^^^^^

.. parsed-literal::

   zypper install cloudstack-management

Install on Ubuntu
^^^^^^^^^^^^^^^^^

.. parsed-literal::

   sudo apt install cloudstack-management

