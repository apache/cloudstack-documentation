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


Deployment Planners
======================


Deployment planners determine *how and where instances* are placed across clusters within a zone.  
A planner builds and orders a *list of candidate clusters* based on a placement strategy such as available capacity, user dispersion, or pod concentration.  
This ordered list is then passed to the *host allocator*, which attempts to deploy the instance following the planner’s priority order.

Administrators can configure the global setting ``vm.deployment.planner`` to define the default deployment planner for the environment.  
This can also be overridden per *Compute Offering*, allowing flexible control over how instances are distributed across the infrastructure.

Available Planners
------------------

FirstFitPlanner
~~~~~~~~~~~~~~~

The ``FirstFitPlanner`` ranks all clusters in a zone by their *available (free) capacity*, placing clusters with the most available resources at the top of the list.  
This approach prioritizes capacity-driven placement, ensuring efficient utilization of resources across the zone.

UserDispersingPlanner
~~~~~~~~~~~~~~~~~~~~~

The ``UserDispersingPlanner`` aims to *spread a user’s instances across multiple clusters*, reducing the impact of any single cluster failure on that user.

#. The planner counts the number of instances in the *Running* or *Starting* state for the user’s account in each cluster.  
#. Clusters are sorted in **ascending order** based on this count, so clusters with fewer instances from the user are preferred.  
#. The global setting ``vm.user.dispersion.weight`` (default: ``1``) controls how strongly dispersion affects ordering:  
   * ``1``: Ranking is based entirely on dispersion.  
   * ``< 1``: Available capacity has more influence in placement decisions.  

Lowering the dispersion weight allows a balance between *even distribution* and *efficient capacity usage*.

UserConcentratedPodPlanner
~~~~~~~~~~~~~~~~~~~~~~~~~~

The ``UserConcentratedPodPlanner`` focuses on *pod-level affinity*, preferring pods where the user already has active instances.

#. The planner identifies all pods in the zone that contain *Running* instances for the user’s account.  
#. Pods are sorted in **descending order** by the number of user instances — pods with more user instances come first.  
#. Clusters from these pods are then added to the top of the list in that order, so deployment is biased toward pods where the user is already active.  
#. Clusters within each pod are *not* further sorted by capacity or instance count.  
#. If no pods contain user instances, the cluster order remains unchanged.

Summary of Planner Behavior
---------------------------

.. list-table::
   :header-rows: 1

   * - Planner
     - Placement Focus
     - Ordering Criteria
     - Typical Use Case
   * - FirstFitPlanner
     - Capacity
     - Descending by available resources
     - Capacity-optimized or general-purpose placement
   * - UserDispersingPlanner
     - Dispersion
     - Ascending by user instance count (optionally weighted with capacity)
     - Distribute user instances evenly across clusters
   * - UserConcentratedPodPlanner
     - Pod Affinity
     - Descending by user instance count per pod
     - Keep user instances within the same pod for locality or data proximity

Pod-Level vs Cluster-Level Allocation
------------------------------------

When ``apply.allocation.algorithm.to.pods = true``:  
The allocation algorithm (for example, *FirstFit*) is applied at *pod granularity* first.  
The planner will evaluate or rank pods according to the allocation heuristics — for *FirstFit*, that means prioritizing pods with more available capacity according to the FirstFit capacity checks.  
After pods are ordered, the planner then considers clusters *inside each pod* — typically evaluating clusters within the selected pod in order (or applying cluster-level heuristics only within that pod).  
In other words, *pod-level ordering happens before cluster selection*.

When ``apply.allocation.algorithm.to.pods = false`` (the default in many deployments):  
The allocation algorithm operates at the *cluster level* across the entire zone.  

|deployment-planner-diagram.png|

.. |deployment-planner-diagram.png| image:: /_static/images/deployment-planner-diagram.png
   :alt: Deployment Planner Diagram
