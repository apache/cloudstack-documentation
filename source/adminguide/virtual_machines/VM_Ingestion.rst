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

Importing VMs
-------------

Virtual machines that have been created out of band, directly from hypervisor can be imported in CloudStack(currently only for VMware). Import action can only be performed by administrator and only using API. Following APIs can be used while importing unmanaged virtual machines:

-  listUnmanagedInstances - to list unmanaged virtual machines for a cluster.

-  importUnmanagedInstance - to import an unmanaged virtual machine into CloudStack.

listUnmanagedInstances
~~~~~~~~~~~~~~~~~~~~~~

This API will list all unmanaged VMs for a given cluster. Optionally, the vSphere name for an existing unmanaged VM can be given to retrieve VM details. The API will filter all CloudStack managed VMs, and will also filter templates that show up as VMs on vCenter.

Request parameters:

.. parsed-literal::
   clusterid (CloudStack UUID of cluster)
   name (vSphere instance name)

Response:

.. parsed-literal::
   clusterid
   hostid
   name
   osdisplayname
   memory
   powerstate
   cpuCoresPerSocket
   cpunumber
   cpuspeed
   disk
      - id
      - capacity (in bytes)
      - controller
      - controllerunit
      - imagepath
      - position
   nic
      - id
      - macaddress
      - networkname
      - vlanid
      - pcislot
      - adaptertype (when available)
      - ipaddress (Only returned when VMware tools are running on instance)


importUnmanagedInstance
~~~~~~~~~~~~~~~~~~~~~~~

This API will import an existing unmanaged VM into CloudStack for a given cluster and VM name. The service offering for the VM, disk offerings for volumes and networks for NICs of the VM can also be mapped. Some optional parameters such as: account, projectid, domainid, hostname, details, etc. can also be given. Appropriate networks, service offering and disk offerings need to be present before import and cannot be created on the fly during the API call.

Request parameters:

.. parsed-literal::
   clusterid (CloudStack UUID of cluster)
   name (vSphere instance name)
   displayname
   hostname
   account (An optional account name for the virtual machine. Must be used with domainid parameter)
   domainid (An optional domain ID for the virtual machine. Must be used with account parameter)
   projectid
   templateid
   serviceofferingid
   diskofferingid (UUID of disk offering for root disk)
   nicnetworklist (Map for NIC ID and corresponding Network UUID)
   nicipaddresslist (Map for NIC ID and corresponding IP address)
   datadiskofferinglist (Map for data disk ID and corresponding disk offering UUID)
   details (Map for VM details)
   migrateallowed (VM and its volumes are allowed to migrate to different host/storage pool when offering tags conflict with host/storage pool)

Response:

.. parsed-literal::
   Same response as that of deployVirtualMachine API.


Requirements for importUnmanagedInstance API
''''''''''''''''''''''''''''''''''''''''''''

#. API will use `name` for the `hostname` of the VM when hostname parameter is not explicitly passed. `hostname` cannot be longer than 63 characters. Only ASCII letters a-z, A-Z, digits 0-9, hyphen are allowed. Must start with a letter and end with a letter or a digit.

#. For importing a VM, the Custom Constrained type of compute offerings in CloudStack are the recommended type of offerings, as the amount of memory and number of CPUs assigned to the imported VM will automatically be matched to the existing VM.

#. To use Custom Unconstrained type of compute offering, CPU speed will need to be passed using details parameter when the CPU reservation is not set for the unmanaged VM in vSphere. CPU speed in the latter case can be passed as, details[0].cpuSpeed=SOME_VALUE. Fixed compute offerings can also be used for importing VMs, but when the offering’s configuration (CPU cores, memory and CPU speed) does not match the unmanaged VM’s existing configuration, a VM in running state cannot be imported. In such cases, VM will have to be stopped before the import.

#. For importing a VM with data disks, `datadiskofferinglist` (map of disk ID and corresponding disk offering ID) parameter must be passed. Example: datadiskofferinglist[0].disk=DISK_ID datadiskofferinglist[0].diskOffering=DISK_OFFERING_ID

#. If selected disk offering is greater than the actual disk size, CloudStack will not perform resize of the disk when importing, consistent with existing behaviour when creating a template out of disk. The disk will remain with its original size, but CloudStack will have a record as per the offering.

#. `templateid` parameter can be used to associate a template with the imported VM. When the parameter is not defined, CloudStack will import VM using an in-built, dummy ISO. During the very first import of a VM where `templateid` parameter is not defined, a new entry, named system-default-vm-import-dummy-template.iso will be created in the cloud.vm_template table for the purpose of using associating the imported VM with the dummy template and the field template_id in the vm_instance table will have the value of the ID of the dummy template (CloudStack requires each VM instance to be associated with some template inside the DB. If the VM is imported without a valid `templateid` (including even the dummy template ID), it cannot be “reinstalled” later without explicitly specifying a template (restoreVirtualMachine API without specifying the templateid parameter will not work). Import API will try to recognize and map the operating system type for the unmanaged VM to the one from the list of the guest operating systems available in CloudStack. If the operating system type can not be mapped, the API will return an error, and the templateid parameter (value = ID of a template with the appropriate operating system) will be needed for a successful import. When `templateid` is defined in the import API call, the guest operating system details of the imported VM will be set to the operating system details of the specified template after VM restart. NIC adapters and disk controllers of the VM will remain same as they were before the import, irrespective of the template configurations. When the VM operating system is automatically recognized during the import (i.e. templateid parameter is not specified), and the operating system of the VM (as reported by the hypervisor) can be matched to multiple operating systems in the CloudStack, the first match will be used as the operating system for the imported VM in CloudStack. An example of this is i.e. “CentOS 7 (64-bit)” operating system type, as visible in vSphere, since this one can be matched against “CentOS 7” or “CentOS 7.1” or “CentOS 7.2” in CloudStack (based on the existing guest OS mappings), and here the first one (“CentOS 7”) will be used as the operating system for the imported VM.

#. For assigning IP addresses to NICs, `nicipaddresslist` parameter can be used. While importing, if an IP address is not found for a NIC which is assigned to a non-L2 CloudStack network during API call, API will return an error. To auto-assign an IP in such a case, a value of `auto` can be used. Example, nicipaddresslist[0].nic=NIC_ID nicipaddresslist[0].ip4Address=auto. Auto-assigning IP address is not supported if an unmanaged VM reports more than one IP address associated with its NIC.

#. When migrateallowed parameter is set to true, CloudStack will migrate the VM and its volumes to a suitable host / storage pool when compute / disk offering are incompatible with the current host / storage pool due to host / storage tags. i.e., compute / disk offering; host / storage tags are not present in the host / storage pool. When migrateallowed is false and conflict is observed during the import process, an appropriate error will be returned. Migration is supported for both running and stopped VMs. Live-migration is supported for running imported VM. When a stopped VM is imported, CloudStack will migrate VM to a suitable host when it is restarted. For volumes, live-migration will be done for volumes of a running VM. As per existing CloudStack behaviour, a stopped, imported VM might not appear in vCenter when its root volume is migrated until the VM is restarted.

#. Importing VMs with different types of disk controllers for data disks and multiple NICs of different types is not supported and will result in an error response. Root disk and other (data disks) disks can have different type of controller.

#. After import, once the VM is started from CloudStack, its CPU and RAM configuration, including CPU limits, CPU reservations, memory reservation, etc. may change from the original configuration, since all those properties are now controlled by CloudStack (i.e. by cluster-level settings and Compute Offering settings).

#. After importing a running VM, it is required to stop and start the VM via CloudStack, in other to be able to access the console of a VM.


Discovery of Existing Networks (for VMware)
'''''''''''''''''''''''''''''''''''''''''''

A Python 3 based script (discover_networks.py) can be found under vm/hypervisor/vmware directory in the CloudStack scripts install location. For most operating systems, CloudStack installs scripts at /usr/share/cloudstack-common/. It leverages VMware’s pyvmomi library (https://github.com/vmware/pyvmomi) and allows listing all networks for a vCenter host or cluster which have at least one virtual machine attached to them. The script will iterate through such networks and will report following parameters for them:

.. parsed-literal::
   cluster (vCenter Cluster belongs to)
   host (vCenter Host belongs to)
   portgroup (Portgroup of the network)
   switch (Switch to which network is connected)
   virtualmachines (Virtual machines that are currently connect in network alongwith their NIC device details)
   vlanid (VLAN ID of the nework)

Script can take the following arguments:

.. parsed-literal::
   -h, --help show this help message and exit
   -s HOST, --host HOST vSphere service to connect to
   -o PORT, --port PORT Port to connect on
   -u USER, --user USER User name to use
   -p PASSWORD, --password PASSWORD Password to use
   -c CLUSTER, --cluster CLUSTER Cluster for listing network
   -S, --disable_ssl_verification Disable ssl host certificate verification
   -d, --debug Debug log messages

.. note::
   To run this script host machine should have Python 3 and module `pyvmomi` installled.
   Python binaries: https://www.python.org/downloads/
   Install instructions for pyvmomi: https://github.com/vmware/pyvmomi#installing 
