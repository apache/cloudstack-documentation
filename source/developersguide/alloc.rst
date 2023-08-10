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


Allocators
==========

CloudStack enables administrators to write custom allocators that will
choose the Host to place a new guest and the storage host from which to
allocate guest virtual disk images.

These are following categories of allocators currently supported:

-  HostAllocators - Allows you to create custom rules to determine which
   physical host to allocate the Guest Instances on.

-  StoragePoolAllocators - Allows you to create custom rules to
   determine which storage pool to allocate the Guest Instances
   on.


Implementing a custom HostAllocator
-----------------------------------

HostAllocators are written by extending
com.cloud.agent.manager.allocator.HostAllocator interface.


HostAllocator Interface
~~~~~~~~~~~~~~~~~~~~~~~

The interface defines the following two methods.

::

   /**
     * Checks if the Instance can be upgraded to the specified ServiceOffering
     * @param UserVm vm
     * @param ServiceOffering offering
     * @return boolean true if the VM can be upgraded
   **/

   publicboolean isVirtualMachineUpgradable(final UserVm vm, final ServiceOffering offering);

   /**
     * Determines which physical hosts are suitable to allocate the Guest Instances on
     *
     * @paramVirtualMachineProfile vmProfile
     * @paramDeploymentPlan plan
     * @paramType type
     * @paramExcludeList avoid
     * @paramint returnUpTo
     * @returnList<Host>List of hosts that are suitable for VM allocation
   **/

   publicList<Host> allocateTo( VirtualMachineProfile<?extendsVirtualMachine> vmProfile,  DeploymentPlan plan, Type type, ExcludeList avoid, intreturnUpTo);   

A custom HostAllocator can be written by implementing the ‘allocateTo’
method


Input Parameters for the method ‘HostAllocator :: allocateTo’
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*com.cloud.vm.VirtualMachineProfile vmProfile*

VirtualMachineProfile describes one Instance. This allows the
adapters like Allocators to process the information in the virtual
machine and make determinations on what the Instance profile
should look like before it is actually started on the hypervisor.

HostAllocators can make use of the following information present in the
VirtualMachineProfile:

-  The ServiceOffering that specifies configuration like requested CPU
   speed, RAM etc necessary for the Guest Instance.

-  The VirtualMachineTemplate, the Template to be used to start the Instance.

*com.cloud.deploy.DeploymentPlan plan*

DeploymentPlan should specify:

-  dataCenterId: The data center the Instance should deploy in

-  podId: The pod the Instance should deploy in; null if no preference

-  clusterId: The cluster the Instance should deploy in; null if no preference

-  poolId: The storage pool the Instance should be created in; null if no
   preference

*com.cloud.host.Host.Type type*

Type of the Host needed for this Guest Instance. Currently
com.cloud.host.Host.Type interface defines the following Host types:

-  Storage

-  Routing

-  SecondaryStorage

-  ConsoleProxy

-  ExternalFirewall

-  ExternalLoadBalancer

*com.cloud.deploy.DeploymentPlanner.ExcludeList avoid*

The ExcludeList specifies what datacenters, pods, clusters, hosts,
storagePools should not be considered for allocating this Guest Instance.
HostAllocators should avoid the hosts that are mentioned in
ExcludeList.hostIds.

-  Set Long dcIds;

-  Set Long podIds;

-  Set Long clusterIds;

-  Set Long hostIds;

-  Set Long poolIds;

*int returnUpTo*

This specifies return up to that many available hosts for this Guest Instance.

To get all possible hosts, set this value to -1.


Reference HostAllocator implementation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Refer com.cloud.agent.manager.allocator.impl.FirstFitAllocator that
implements the HostAllocator interface. This allocator checks available
hosts in the specified datacenter, Pod, Cluster and considering the
given ServiceOffering requirements.

If returnUpTo = 1, this allocator would return the first Host that fits
the requirements of the Guest Instance.


Loading a custom HostAllocator
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Write a custom HostAllocator class, implementing the interface
   described above.

#. Package the code into a JAR file and make the JAR available in the
   classpath of the Management Server/tomcat.

#. Modify the components.xml and components-premium.xml files found in
   /client/ tomcatconf as follows.

#. Search for ‘HostAllocator’ in these files.

   ::

      <adapters key="com.cloud.agent.manager.allocator.HostAllocator">
        <adapter name="FirstFit" class="com.cloud.agent.manager.allocator.impl.FirstFitAllocator"/>
      </adapters>                  
                 

#. Replace the FirstFitAllocator with your class name. Optionally, you
   can change the name of the adapter as well.

#. Restart the Management Server.


Implementing a custom StoragePoolAllocator
------------------------------------------

StoragePoolAllocators are written by extending
com.cloud.storage.allocator. StoragePoolAllocator interface.


StoragePoolAllocator Interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A custom StoragePoolAllocator can be written by implementing the
‘allocateTo’ method.

::

   /**
     * Determines which storage pools are suitable for the guest Instance
     * @param DiskProfile dskCh
     * @param VirtualMachineProfile vmProfile
     * @param DeploymentPlan plan
     * @param ExcludeList avoid
     * @param int returnUpTo
     * @return List<StoragePool> List of storage pools that are suitable for the VM
   **/

   public List<StoragePool> allocateToPool(DiskProfile dskCh, VirtualMachineProfile<? extends VirtualMachine> vm, DeploymentPlan plan, ExcludeList avoid, int returnUpTo);         
        

This interface also contains some other methods to support some legacy
code. However your custom allocator can extend the existing
com.cloud.storage.allocator. AbstractStoragePoolAllocator. This class
provides default implementation for all the other interface methods.


Input Parameters for the method ‘StoragePoolAllocator :: allocateTo’
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*com.cloud.vm.DiskProfile dskCh*

DiskCharacteristics describes a disk and what functionality is required
from it. It specifies the storage pool tags if any to be used while
searching for a storage pool.

*com.cloud.vm.VirtualMachineProfile vmProfile*

VirtualMachineProfile describes one Instance. This allows the
adapters like Allocators to process the information in the virtual
machine and make determinations on what the Instance profile
should look like before it is actually started on the hypervisor.

StoragePoolAllocators can make use of the following information present
in the VirtualMachineProfile:

-  The VirtualMachine Instance that specifies properties of the guest
   Instance.

-  The VirtualMachineTemplate, the Template to be used to start the Instance.

*com.cloud.deploy.DeploymentPlan plan*

DeploymentPlan should specify:

-  dataCenterId: The data center the Instance should deploy in

-  podId: The pod the Instance should deploy in; null if no preference

-  clusterId: The cluster the Instance should deploy in; null if no preference

-  poolId: The storage pool the Instance should be created in; null if no
   preference

*com.cloud.deploy.DeploymentPlanner.ExcludeList avoid*

The ExcludeList specifies what datacenters, pods, clusters, hosts,
storagePools should not be considered for allocating this Guest Instance.
StoragePoolAllocators should avoid the pools that are mentioned in
ExcludeList.poolIds

-  Set Long dcIds;

-  Set Long podIds;

-  Set Long clusterIds;

-  Set Long hostIds;

-  Set Long poolIds;

*int returnUpTo*

This specifies return up to that many available pools for this Guest Instance

To get all possible pools, set this value to -1


Reference StoragePoolAllocator implementation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Refer com.cloud.storage.allocator.FirstFitStoragePoolAllocator that
implements the StoragePoolAllocator interface. This allocator checks
available pools in the specified datacenter, Pod, Cluster and
considering the given DiskProfile characteristics.

If returnUpTo = 1, this allocator would return the first Storage Pool
that fits the requirements of the Guest Instance.


Loading a custom StoragePoolAllocator
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Write a custom StoragePoolAllocator class, implementing the interface
   described above.

#. Package the code into a JAR file and make the JAR available in the
   classpath of the Management Server/tomcat.

#. Modify the components.xml and components-premium.xml files found in
   /client/ tomcatconf as follows.

#. Search for ‘StoragePoolAllocator’ in these files.

   ::

      <adapters key="com.cloud.storage.allocator.StoragePoolAllocator">
         <adapter name="Storage" class="com.cloud.storage.allocator.FirstFitStoragePoolAllocator"/>
      </adapters>             
                 
#. Replace the FirstFitStoragePoolAllocator with your class name.
   Optionally, you can change the name of the adapter as well.

#. Restart the Management Server.
