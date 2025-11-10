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


VM and Volume Allocators
======================

Each Instance must be deployed in suitable deployment destination. Deployment destination is set of recommended resources that you can choose for deploying an instance.
A deployment planner provides the suitable deployment destination that is required for a instance. 

Allocators are used to figure out suitable host and storage pools for deploying the Instance:

#. VM Allocator
#. Volume Allocator


VM Allocator
------------

VM allocator returns suitable hosts in the cluster where you can deploy the given instance. Various parameters e.g. CPU and
RAM capacity, current state of the host are considered to decide the host.

VM allocator supports following algorithms to select a host in the cluster:

.. cssclass:: table-striped table-bordered table-hover

============================= ========================
Algorithm                      Description
============================= ========================
random		                   Selects a host in the cluster randomly.
firstfit		               Selects the first available host in the cluster.
userdispersing	               Selects the host running least instances for the account, aims to spread out the instances belonging to a single user account.
userconcentratedpod_random     Selects the host randomly aiming to keep all instances belonging to single user account in same pod.
userconcentratedpod_firstfit   Selects the first suitable host from a pod running most instances for the user.
firstfitleastconsumed          Selects the first host after sorting eligible hosts by least allocated resources (such as CPU or RAM).
============================= ========================

Use global configuration parameter: 
**vm.allocation.algorithm** to specify the algorithm that the Allocator must use. By default it is configured to use "random" algorithm.


Volume Allocator
--------------

Volume allocator returns suitable storage pools available in the cluster where volumes of the given instance can be created. 
To decide the storage pools, it considers factors such as disk offering, storage capacity, availability scope etc.

Volume allocator supports following algorithms to select a host in the cluster:

.. cssclass:: table-striped table-bordered table-hover

============================= ========================
Algorithm                      Description
============================= ========================
random		                   Selects a storage pool in the cluster randomly.
firstfit		                   Selects the first available storage pool in the cluster.
userdispersing	                Selects the storage pool running least instances for the account, aims to spread out the instances belonging to a single user account.
userconcentratedpod_random     Selects the storage pool randomly aiming to keep all instances belonging to single user account in same pod.
userconcentratedpod_firstfit   Selects the first suitable pool from a pod running most instances for the user.
firstfitleastconsumed          Selects the first storage pool after sorting eligible pools by least allocated resources.
============================= ========================

.. note::
   Since 4.21.0, dedicated named configuration is provided for admin to configure volume allocation algorithm.
   
      **volume.allocation.algorithm**: random (default)

   Before 4.21.0, **vm.allocation.algorithm** was used for both VM as well as Volume allocation.


Cluster, Pod and Host Ordering
==============================

Overview
--------

`The host.capacityType.to.order.clusters` is a global advanced configuration parameter in Apache CloudStack that controls how pods, clusters, 
and hosts are prioritized during Instance deployment, based on available CPU, RAM, or a weighted combination of both in Host.
This configuration is specifically leveraged when the VM allocation algorithm is set to `firstfitleastconsumed`.

Configuration
-------------

Key: `host.capacityType.to.order.clusters`

.. cssclass:: table-striped table-bordered table-hover

========= ========================
Value      Behavior
========= ========================
CPU		  Prioritizes resources with the most available CPU.
RAM		  Prioritizes resources with the most available memory.
COMBINED	  Uses a weighted formula to balance CPU and RAM in prioritization.
========= ========================

**Additional Configuration for COMBINED**

- Key: `host.capacityType.to.order.clusters.cputomemoryweight`
- Type: Float(0.0 to 1.0)
- Default: 0.5
- Purpose: Determines the weight of CPU vs RAM in the combined capacity calculation.

Capacity calculation formula:

.. code:: bash

   capacity = (host.capacityType.to.order.clusters.cputomemoryweight * CPU) + ((1 - host.capacityType.to.order.clusters.cputomemoryweight) * RAM)


This allows flexible tuning of prioritization depending on workload sensitivity.

Example Configuration
---------------------

.. code:: bash

   host.capacityType.to.order.clusters: COMBINED
   host.capacityType.to.order.clusters.cputomemoryweight: 0.7

Above config prioritizes CPU at 70% weight and RAM at 30% when ranking pods, clusters, and hosts.

.. note::
   - `host.capacityType.to.order.clusters` is only respected for cluster/host ordering when:
   .. code:: bash

      vm.deployment.planner: FirstFitPlanner, UserDispersingPlanner ( when vm.user.dispersion.weight is < 1) 
      vm.allocation.algorithm: firstfitleastconsumed
   - When using COMBINED, make sure to tune cpu.to.memory.capacity.weight to reflect your environment’s resource constraints and workload profiles.
