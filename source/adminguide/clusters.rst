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


Adding Clusters
---------------

Additional clusters can be added at any time to add a new set of hosts. 
For requirements and instructions, see :ref:`adding-a-cluster`.


CloudStack DRS
--------------
DRS is a process that can rebalance instances across hypervisor hosts in a cluster as defined by the algorithm selected. 
There are two algorithms available:

#. **Condensed** spread instances across hosts as densely as possible. 
   This is useful for reducing the number of hosts used.
#. **Balanced** spread instances across hosts as evenly as possible. 
   This is useful for reducing the load on each host. This is the default algorithm.

.. note::
   Deployment planner will not consider DRS while deploying instances.

Configuring DRS
~~~~~~~~~~~~~~~
Following are the configuration parameters for DRS.

.. list-table:: DRS related cluster parameters
   :header-rows: 1

   * - Parameter
     - Default
     - Description
   * - ``drs.plan.expire.interval``
     - `30`
     - The interval in days after which the DRS events will be cleaned up.
   * - ``drs.automatic.enable``
     - `false`
     - Enable/disable automatic DRS on a cluster.
   * - ``drs.automatic.interval``
     - `60`
     - The interval in minutes after which a periodic background thread will schedule DRS for a cluster.
   * - ``drs.max.migrations``
     - `50`
     - Maximum number of instances to be migrated in one DRS execution.
   * - ``drs.algorithm``
     - `condensed`
     - DRS algorithm to be executed on the cluster. Available algorithms - `condensed`, `balanced`.
   * - ``drs.imbalance``
     - `0.4`
     - Percentage (as a value between 0.0 and 1.0) of imbalance allowed in the cluster. 1.0 means no imbalance
       is allowed and 0.0 means imbalance is allowed.
   * - ``drs.metric``
     - `memory`
     - The allocated resource metric to use for measuring imbalance for a cluster. Possible values are memory, cpu.

.. note::
  Scope of ``drs.plan.expire.interval`` is global and for rest is cluster level.

.. note::
   Very high value for ``drs.max.migrations`` can result in management server using up all of it's workers for DRS tasks
   and not being able to execute other tasks.

There are some advanced parameters that can be configured for DRS. These parameters impact the way imbalance is calculated
for a cluster. Do not change these parameters unless you know what you are doing.

.. list-table:: Advanced DRS related cluster parameters
   :header-rows: 1

   * - Parameter
     - Default
     - Description
   * - ``drs.metric.type``
     - `used`
     - The metric type used to measure imbalance in a cluster. This can completely change the imbalance value. 
       Possible values are free, used.
   * - ``drs.metric.use.ratio``
     - `true`
     - Whether to use ratio of selected metric & total. Useful when the cluster has hosts with different capacities.
   * - ``drs.imbalance.condensed.skip.threshold``
     - `0.95`
     - Threshold to ignore the metric for a host while calculating the imbalance to decide whether DRS is required for 
       a cluster. This is to avoid cases when the calculated imbalance gets skewed due to a single host having a very 
       high/low metric value resulting in imbalance being higher than 1. If ``drs.metric.type`` is ``free``, set a lower 
       value and if it is ``used`` set a higher value. The value should be between `0.0` and `1.0`. 
       This is applicable only for Condensed algorithm.

Executing manual DRS on a cluster
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DRS can also be manually executed for a cluster.

Follow these steps to execute DRS for a cluster using the UI:

#. Configure DRS parameters as per the requirement.
   |drs-cluster-settings.png|
#. Open DRS tab for the cluster.
   |drs-cluster-tab.png|
#. Select the iteration percentage to execute for the cluster.
#. Click on `Generate DRS Plan` button. A modal will appear showing migrations 
   for that cluster as per the configured algorithm.
   |drs-plan.png|
#. Validate the migrations, and click on `Execute` button to execute the 
   suggested migrations.


.. note:: 
   Only one DRS process can run for a cluster at a time. If you try to run DRS while another 
   DRS process is running, the second process will fail.


.. |drs-cluster-settings.png| image:: /_static/images/drs-cluster-settings.png
   :alt: DRS settings for a cluster.

.. |drs-cluster-tab.png| image:: /_static/images/drs-cluster-tab.png
   :alt: DRS tab for a cluster.

.. |drs-plan.png| image:: /_static/images/drs-plan.png
   :alt: DRS plan for a cluster.
