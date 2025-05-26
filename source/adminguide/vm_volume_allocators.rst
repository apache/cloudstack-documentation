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


Volme Allocator
--------------

Volume allocator returns suitable storage pools available in the cluster where volumes of the given instance can be created. 
To decide the storage pools, it considers factors such as disk offering, storage capactiy, availability scope etc.

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