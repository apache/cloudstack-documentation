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

Introduction
------------

Who Should Read This
^^^^^^^^^^^^^^^^^^^^

For those who have already gone through a design phase and planned a
more sophisticated deployment, or those who are ready to start scaling
up a trial installation. With the following procedures, you can start
using the more powerful features of CloudStack, such as advanced VLAN
networking, high availability, additional Network elements such as load
balancers and firewalls, and support for multiple hypervisors including
Citrix XenServer, KVM, and VMware vSphere.


Installation Steps
^^^^^^^^^^^^^^^^^^

For anything more than a simple trial installation, you will need
guidance for a variety of configuration choices. It is strongly
recommended that you read the following:

-  Choosing a Deployment Architecture
-  Choosing a Hypervisor: Supported Features
-  Network Setup
-  Storage Setup
-  Best Practices


#. Make sure you have the required hardware ready. 
   See :ref:`minimum-system-requirements`

#. Install the Management Server (choose single-node or multi-node).
   See :ref:`install-mgt`

#. Configure your cloud. See :ref:`Configuring_your_CloudStack_Installation`

   #. Using CloudStack UI. See `*User Interface* :ref:`log-in-to-ui`

   #. Add a zone. Includes the first pod, cluster, and host. See :ref:`adding-a-zone`

   #. Add more pods (optional). See :ref:`adding-a-pod`

   #. Add more clusters (optional). See :ref:`adding-a-cluster`

   #. Add more hosts (optional). See :ref:`adding-a-host`

   #. Add more primary storage (optional). See :ref:`add-primary-storage`

   #. Add more secondary storage (optional). See :ref:`add-secondary-storage`

#. Try using the cloud. See :ref:`initialize-and-test`
