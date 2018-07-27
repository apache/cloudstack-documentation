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


Configuring AutoScale without using NetScaler
=============================================

.. warning:: 
   This feature is currently only available on the master branch and will be 
   released in the 4.4 release.


What is AutoScaling?
--------------------

AutoScaling allows you to scale your back-end services or application VMs up 
or down seamlessly and automatically according to the conditions you define. 
With AutoScaling enabled, you can ensure that the number of VMs you are using 
seamlessly scale up when demand increases, and automatically decreases when 
demand subsides. Thus it helps you save compute costs by terminating underused 
VMs automatically and launching new VMs when you need them, without the need 
for manual intervention.


Hypervisor support
------------------

At that time, AutoScaling without NetScaler only supports for Xenserver. We 
are working to support KVM also.


Prerequisites
-------------

Before you configure an AutoScale rule, consider the following:

-  Ensure that the necessary template is prepared before configuring AutoScale. 
   Firstly you must install the PV-driver, which helps Xenserver collect 
   performance parameters (CPU and memory) into VMs. Beside, When a VM is 
   deployed by using a template and when it comes up, the application should be 
   up and running.


Configuration
-------------

Specify the following:

.. image:: /_static/images/autoscale-config.png

-  Template: A template consists of a base OS image and application. A 
   template is used to provision the new instance of an application on a 
   scaleup action. When a VM is deployed from a template, the VM can start 
   taking the traffic from the load balancer without any admin intervention. 
   For example, if the VM is deployed for a Web service, it should have the 
   Web server running, the database connected, and so on.

-  Compute offering: A predefined set of virtual hardware attributes, 
   including CPU speed, number of CPUs, and RAM size, that the user can select 
   when creating a new virtual machine instance. Choose one of the compute 
   offerings to be used while provisioning a VM instance as part of scaleup 
   action.

-  Min Instance: The minimum number of active VM instances that is assigned to 
   a load balancing rule. The active VM instances are the application 
   instances that are up and serving the traffic, and are being load balanced. 
   This parameter ensures that a load balancing rule has at least the 
   configured number of active VM instances are available to serve the traffic.

-  Max Instance: Maximum number of active VM instances that should be assigned 
   to a load balancing rule. This parameter defines the upper limit of active 
   VM instances that can be assigned to a load balancing rule.

   Specifying a large value for the maximum instance parameter might result in 
   provisioning large number of VM instances, which in turn leads to a single 
   load balancing rule exhausting the VM instances limit specified at the 
   account or domain level.

Specify the following scale-up and scale-down policies:

-  Duration: The duration, in seconds, for which the conditions you specify 
   must be true to trigger a scaleup action. The conditions defined should 
   hold true for the entire duration you specify for an AutoScale action to be 
   invoked.

-  Counter: The performance counters expose the state of the monitored 
   instances. We added two new counter to work with that feature:

   -  Linux User CPU [native] - percentage
   -  Linux User RAM [native] - percentage

   Remember to choose one of them. If you choose anything else, the 
   autoscaling will not work.

-  Operator: The following five relational operators are supported in 
   AutoScale feature: Greater than, Less than, Less than or equal to, Greater 
   than or equal to, and Equal to.

-  Threshold: Threshold value to be used for the counter. Once the counter 
   defined above breaches the threshold value, the AutoScale feature initiates 
   a scaleup or scaledown action.

-  Add: Click Add to add the condition.

   Additionally, if you want to configure the advanced settings, click Show 
   advanced settings, and specify the following:

-  Polling interval: Frequency in which the conditions, combination of counter, 
   operator and threshold, are to be evaluated before taking a scale up or 
   down action. The default polling interval is 30 seconds.

-  Quiet Time: This is the cool down period after an AutoScale action is 
   initiated. The time includes the time taken to complete provisioning a VM 
   instance from its template and the time taken by an application to be ready 
   to serve traffic. This quiet time allows the fleet to come up to a stable 
   state before any action can take place. The default is 300 seconds.

-  Destroy VM Grace Period: The duration in seconds, after a scaledown action 
   is initiated, to wait before the VM is destroyed as part of scaledown 
   action. This is to ensure graceful close of any pending sessions or 
   transactions being served by the VM marked for destroy. The default is 120 
   seconds.

-  Apply: Click Apply to create the AutoScale configuration.


Disabling and Enabling an AutoScale Configuration
-------------------------------------------------

If you want to perform any maintenance operation on the AutoScale VM instances, 
disable the AutoScale configuration. When the AutoScale configuration is 
disabled, no scaleup or scaledown action is performed. You can use this 
downtime for the maintenance activities. To disable the AutoScale 
configuration, click the Disable AutoScale button.

The button toggles between enable and disable, depending on whether AutoScale 
is currently enabled or not. After the maintenance operations are done, you 
can enable the AutoScale configuration back. To enable, open the AutoScale 
configuration page again, then click the Enable AutoScale button.


Updating an AutoScale Configuration
-----------------------------------

You can update the various parameters and add or delete the conditions in a 
scaleup or scaledown rule. Before you update an AutoScale configuration, 
ensure that you disable the AutoScale load balancer rule by clicking the 
Disable AutoScale button.

After you modify the required AutoScale parameters, click Apply. To apply the 
new AutoScale policies, open the AutoScale configuration page again, then 
click the Enable AutoScale button.


Runtime Considerations
----------------------

An administrator should not assign a VM to a load balancing rule which is 
configured for AutoScale.

Making API calls outside the context of AutoScale, such as destroyVM, on an 
autoscaled VM leaves the load balancing configuration in an inconsistent state. 
Though VM is destroyed from the load balancer rule, it continues be showed as 
a service assigned to a rule inside the context of AutoScale.

