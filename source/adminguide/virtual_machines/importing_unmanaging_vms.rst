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

.. note:: This is currently only available for **vSphere** clusters.

About Unmanaged Instances
-------------------------

As of ACS 4.14, CloudStack has the concept of **unmanaged** Instances.  These are Instances that are on CloudStack
managed hosts, but that are not in CloudStack's database and therefore CloudStack cannot control (manage) then in any way.  Previously,
such Instances could exist, but CloudStack did not 'see' them (their existence *would* be reported in logs as unrecognised Instances).

From ACS 4.14 onwards, CloudStack is able to list these Instances via the listUnmanagedInstances API command and then import (also known as ingest)
those unmanaged Instances via the importUnmanagedInstance API so that they become CloudStack managed Guest Instances.
From ACS 4.16 onwards, importing of the unmanaged Instances can also be carried out within the UI.

From ACS 4.15 onwards, administrators are able to unmanage guest Instances.

In the UI, both unmanaged and managed Instances are listed in *Tools > Import-Export Instances* section:

   |vm-unmanagedmanaged.png|


Importing Unmanaged Instances
-----------------------------

Use Cases and General Usage
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The ability to import Instances allows Cloud operators (both public and private) to onboard new tenants simply and quickly,
with the minimum amount disk IO. But also can be used in disaster recovery scenarios at remote sites (if storage is
replicated) and in the recreation of Instances which have been backed up (part of the code is indeed used in
CloudStack's Backup and Recovery feature).

The most complex part of importing Instances is the mapping of an unmanaged Instance's Networks to CloudStack Networks.  As an operator
could be importing tens or even hundreds of Instances, a UI for this feature has not been created as yet.

If the 'destination' Network VLAN(s) and the requested service offerings match the existing Instance, then the Instance can be
imported whilst it is running. If the VLANs or service offerings do not match, then the Instance to be imported must be stopped.
Once the Instance has been added to CloudStack, starting it through CloudStack will alter the Instances settings in line with
those set in the CloudStack DB.

To import Instances, it is imagined that a Cloud Provider will:

#. List all of the existing Networks which the Instances to be imported are on.
#. Create corresponding Networks in CloudStack
#. Use the listUnmanagedInstances API to create a CSV of Instances to be imported.
#. Where required, add metadata to the CSV such as the Account into which each Instance is to associated, the Network which each Instance is to be
   attached to, the Compute Offering required for each Instance, and the Disk Offering for each disk
#. Create a script that will loop through the CSV, sending the importUnmanagedInstance API command with the corresponding
   parameters for each Instance being read from the CSV

Listing unmanaged Instances
---------------------------

Prerequisites to list unmanaged Instances (vSphere)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order for CloudStack to list the Instances that are not managed by CloudStack on a host/cluster, the host(s) in the vSphere cluster
must have been added to CloudStack.  The standard prerequisites for adding a host to CloudStack apply.

listUnmanagedInstances API
~~~~~~~~~~~~~~~~~~~~~~~~~~

This API will list all unmanaged Instances for a given cluster. Optionally, the vSphere name for an existing unmanaged
Instance can be given to retrieve Instance details. The API will filter all CloudStack managed Instances, and will also filter Templates that show up as Instances on vCenter.

**Request parameters**:

.. parsed-literal::
   - **clusterid** (CloudStack UUID of cluster)
   - **name** (vSphere Instance name)

**Response**:

.. parsed-literal::
   - **clusterid**
   - **hostid**
   - **name**
   - **osdisplayname**
   - **memory**
   - **powerstate**
   - **cpuCoresPerSocket**
   - **cpunumber**
   - **cpuspeed**
   - **disk**
      - **id**
      - **capacity** (in bytes)
      - **controller**
      - **controllerunit**
      - **imagepath**
      - **position**
   - **nic**
      - **id**
      - **macaddress**
      - **networkname**
      - **vlanid**
      - **pcislot**
      - **adaptertype** (when available)
      - **ipaddress** (Only returned when VMware tools are running on Instance)


Importing Unmanaged Instances
-----------------------------

Administrators can import unmanaged Instances either using UI or with the importUnmanagedInstance API.

UI provides the following form for importing the Instance when *Import Instance* action is used in *Import-Export Instances* view:

|ImportInstance.png|

importUnmanagedInstance API
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Request parameters**:

.. parsed-literal::
   - **clusterid** (CloudStack UUID of cluster)
   - **name** (vSphere Instance name)
   - **displayname**
   - **hostname**
   - **account** (An optional account name for the Instance. Must be used with domainid parameter)
   - **domainid** (An optional domain ID for the Instance. Must be used with account parameter)
   - **projectid**
   - **templateid**
   - **serviceofferingid**
   - **nicnetworklist** (Map for NIC ID and corresponding Network UUID)
   - **nicipaddresslist** (Map for NIC ID and corresponding IP address)
   - **datadiskofferinglist** (Map for data disk ID and corresponding disk offering UUID)
   - **details** (Map for Instance details)
   - **migrateallowed** (Instance and its volumes are allowed to migrate to different host/storage pool when offering tags conflict with host/storage pool)
   - **forced** (If true, an Instance is imported despite some of its NIC's MAC addresses being already present)

.. note:: The `forced` parameter is false by default and prevents importing an Instance which has a NIC containing a MAC address that has been previously assigned by CloudStack. If it is set to true, the NICs with MAC addresses which already exist in the CloudStack database have the existing MAC addresses reassigned to its NICs.

**Response**:

.. parsed-literal::
   Same response as that of deployVirtualMachine API.



Prerequisites to Importing Unmanaged Instances (vSphere)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are a few prerequisites to importing unmanaged Instances into CloudStack. Largely these are simply that the networks which you are going to
attach the Instance in CloudStack need to already exist in CloudStack also the storage which an unmanaged Instance is on (before importing) and
also the storage which you wish the Instance to be on after importing must already have been added to CloudStack.

Instances can be imported to isolated, shared or L2 networks. Instances can also be imported and then automatically migrated to storage in accordance with
service offerings using the *migrateallowed* API parameter.

Dummy Template
##############

The assumption that all Guest Instances in CloudStack are created from a Template or ISO is hardcoded into CloudStack.  This *source* Template will
not exist for Instances which have been imported into CloudStack, there for a dummy Template has been created in the CloudStack database.  When a
Template ID is not supplied when importing the Instance, the built-in dummy Template ID will be used. As this Template is only a dummy one, it will
not be possible to 'revert' to the original Template unless you specify a **real** Template ID.

Offerings and Automatic Mapping
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Compute Offerings
#################

**Custom vs Fixed Offerings**
'''''''''''''''''''''''''''''

All Guest Instances in CloudStack must have an associated compute offering.  The import API supports using 'fixed' (ie 2 vCPUs with 2GB RAM
hardcoded into the offering) and 'custom' (user can choose the number of vCPUs and memory) offerings.  When a custom offering is chosen,
then the CloudStack will automatically set the number vCPUs, CPU speed and amount of RAM, to be the same as the Instance before importing it. When
using custom offerings, the Instance to be imported can remain running.  If the compute offering is 'fixed' and it matches the vCPU and RAM
of the existing Instance, the Instance can remain running while being imported, otherwise the Instance must be stopped first and it will be
reconfigured with the new values when it is started.

For maximum compatibility when importing an Instance, the *Custom Constrained* type of compute offerings in CloudStack are the recommended type of
offerings. The amount of memory and number of CPUs assigned to the imported Instance will automatically be matched to the existing Instance, while
the CPU speed will have been set to a sensible value by the admin when creating the offering.


.. note::
   To use Custom Unconstrained type of compute offering, CPU speed will need to be passed using details parameter when the CPU reservation is not set for
   the unmanaged Instance in vSphere. CPU speed in the latter case can be passed as, details[0].cpuSpeed=SOME_VALUE.


Disk Offerings
###############


To import an Instance which has data disks attached, a map of the disk ID and corresponding disk offering ID must be passed via the *datadiskofferinglist* parameter.

For example:

.. parsed-literal::  datadiskofferinglist[0].disk=<DISK_ID> datadiskofferinglist[0].diskOffering=<DISK_OFFERING_ID>

.. note::
   If the selected disk offering is greater in size than the actual disk size, CloudStack will not perform
   resize of the disk when importing. The disk will remain with its original size, but CloudStack will have a
   record as per the offering.

Host and Storage Tags
#####################

When the **migrateallowed** parameter is set to true, if the host or storage tags in the compute/disk offerings are incompatible with the current host and/or
storage pool(s), CloudStack will migrate the Instance and its volumes to a suitable host and storage pool.

When **migrateallowed** is false and there is a conflict, an appropriate error will be returned.

Migration is supported for both running and stopped Instances. Live-migration is supported for running imported Instance. When a stopped Instance is imported, CloudStack
will migrate it to a suitable host when it is restarted.

For volumes, live-migration will be carried out for the volumes of a running Instance. As per existing CloudStack behaviour, a stopped
imported Instance may not appear in vCenter when its root volume is migrated until the Instance is restarted.

Networks
########

When importing an Instance, CloudStack needs to attach the virtual network interfaces (vNICs) to CloudStack networks.
vNICs are associated with a network in one of two ways.

#. Automatically (available for L2 and shared networks)
#. Manual assignment of vNIC to network (ID) as a map if an Instance has more that one NIC

In an enterprise, the vast majority of networks will operate as *Layer 2* networks with IP addressing handled by an IPAM system such as Active Directory
or InfoBlox. This makes CloudStack's L2 networks the natural choice for a like-for-like migration/on-boarding of Instances.

When importing an Instance to a shared or L2 network, CloudStack will automatically look for a CloudStack network that has the same VLAN(s) as the Instance's NIC(s)
is already on. This can be overridden by providing a network_id for the **'nicnetworklist'** parameter

.. note:: this includes PVLANs on L2 networks.


IP Addresses
''''''''''''

To assigning a specific IP address to a NIC, the **'nicipaddresslist'** parameter is used. This parameter should not be used for L2 networks, and is optional for shared networks.
To ask CloudStack to assign an Instance's existing IP when importing, a value of `auto` can be used.

.. parsed-literal:: nicipaddresslist[0].nic=NIC_ID nicipaddresslist[0].ip4Address=auto

Auto-assigning IP addresses requires VMware tools to be on the Guest Instance (for the IP to be reported to vCenter) and is not supported if an unmanaged Instance reports more than one IP
address associated with its NIC (CloudStack cannot tell which is the primary address).  For Instances with more than 1 IP addresses per NIC, pass the first IP address via the import API
and then add secondary addresses via the **'addIpToNic**' API


Registered Operating System
###########################

Import API will try to recognize and map the operating system type for the unmanaged Instance to the one from the list of the guest operating systems available in CloudStack.
If the operating system type can not be mapped, the API will return an error, and the templateid parameter (value = ID of a Template with the appropriate operating system)
will be needed for a successful import. When `templateid` is defined in the import API call, the guest operating system details of the imported Instance will be set to the
operating system details of the specified Template after Instance restart.


Other notes for the importUnmanagedInstance API
################################################

- The API will use **name** for the **hostname** of the Instance when hostname parameter is not explicitly passed.
  The **hostname** cannot be longer than 63 characters.
  Only ASCII letters a-z, A-Z, digits 0-9, hyphen are allowed. Must start with a letter and end with a letter or a digit.

- NIC adapters and disk controllers of the Instance will remain same as they were before the import, irrespective of the Template configurations.

- When the Instance operating system is automatically recognized during the import (i.e. templateid parameter is not specified), and the operating system of the Instance
  (as reported by the hypervisor) can be matched to multiple operating systems in the CloudStack, the first match will be used as the operating system for the
  imported Instance in CloudStack. An example of this is i.e. “CentOS 7 (64-bit)” operating system type, as visible in vSphere, since this one can be matched against
  “CentOS 7” or “CentOS 7.1” or “CentOS 7.2” in CloudStack (based on the existing guest OS mappings),
  and here the first one (“CentOS 7”) will be used as the operating system for the imported Instance.

- Importing Instances with different types of disk controllers for data disks and multiple NICs of different types is not supported and will result in an error response.
  Root disk and other (data disks) disks can have different type of controller.

- After import, once the instance is started from CloudStack its CPU and RAM configuration, including CPU limits, CPU reservations, memory reservation, etc. may change from
  the original configuration, since all those properties are now controlled by CloudStack (i.e. by cluster-level settings and Compute Offering settings).

- After importing a running instance, it will need to be stopped and started (not restarted) via CloudStack to be able to access the console of an instance.


Discovery of Existing Networks (for vSphere)
--------------------------------------------

To import existing instances, the networks that they are attached to need to already exist as CloudStack networks.  As an existing environment can have a great many networks which
need creating, A Python 3 script has been created to enumerate the existing networks.

The script (discover_networks.py) can be found in the vm/hypervisor/vmware directory in the CloudStack scripts install location. For most operating systems,
CloudStack installs scripts in /usr/share/cloudstack-common/. The script leverages VMware’s pyvmomi library (https://github.com/vmware/pyvmomi). The script lists all networks
for a vCenter host or cluster which have at least one Instance attached to them. The script will iterate through these networks and will report the following parameters for them:

- **cluster** (vCenter Cluster belongs to)
- **host** (vCenter Host belongs to)
- **portgroup** (Portgroup of the network)
- **switch** (Switch to which network is connected)
- **virtualmachines** (Instances that are currently connected to the network along with their NIC device details)
- **vlanid** (VLAN ID of the network)

The script can take the following arguments:

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
   To run this script host machine should have Python 3 and module *pyvmomi* installed.

   Python binaries can be found here: https://www.python.org/downloads/

   Install instructions for pyvmomi are here: https://github.com/vmware/pyvmomi#installing

The output of this script can then be used in conjunction with the **'createNetwork'** API to add all of the networks to CloudStack that will be required for a
successful import.


Unmanaging Instances
--------------------

Administrators are able to unmanage guest Instances from CloudStack. Once unmanaged, CloudStack can no longer monitor, control or administer the provisioning and orchestration related operations on an Instance.

To unmanage a guest Instance, an administrator must either use the UI or invoke the unmanageVirtualMachine API passing the ID of the Instance to unmanage. The API has the following preconditions:

- The Instance must not be destroyed
- The Instance state must be 'Running’ or ‘Stopped’
- The Instance must be a VMware Instance

The API execution will perform the following pre-checks, failing if they are not met:

- There are no Volume Snapshots associated with any of the Instance volumes
- There is no ISO attached to the Instance

In the UI, *Unmanage instance* action can be used in Instance view. |UnmanageButton.png|

Alternately, the same operation can also be carried out using *Unmanage Instance* action in *Import-Export Instances* view under the *Tools* section.

|UnmanageInstance.png|

Preserving unmanaged Instance NICs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The zone setting: unmanage.vm.preserve.nics can be used to preserve Instance NICs and its MAC addresses after unmanaging them. If set to true, the Instance NICs (and their MAC addresses) are preserved when unmanaging it. Otherwise, NICs are removed and MAC addresses can be reassigned.


Unmanaging Instance actions
~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Clean up Instance NICs and deallocate network resources used such as IP addresses and DHCP entries on virtual routers.

   - If ‘unmanage.vm.preserve.nics’ = ‘false’ then the NICs are deallocated and removed from CloudStack

   - If ‘unmanage.vm.preserve.nics’ = ‘true’ then the NICs remain allocated and are not removed from the database. The NIC’s MAC addresses remain preserved and therefore cannot be assigned to any new NIC.

- Clean up Instance volumes in the CloudStack database

- Clean up Instance Snapshots in the CloudStack database (if any)
- Revoke host access to any managed volumes attached to the instance (applicable to managed storage only)

- Clean up the Instance from the following:

   - Remove the Instance from security groups (if any)

   - Remove the Instance from instance groups (if any)

   - Remove firewall rules for the Instance (if any)

   - Remove port forwarding rules for the Instance (if any)

   - Remove load balancing rules for the Instance (if any)

   - Disable static NAT (if the Instance is assigned to it)

   - Remove the Instance from affinity groups (if any)

- Remove instance details from the CloudStack database

- Decrement the account resources count for volumes and Instances

- Generate usage events:

   - For volumes destroyed, with type: ‘VOLUME.DELETE’

   - For Instance Snapshots destroyed (if any), with type: ‘VMSNAPSHOT.DELETE’ and 'VMSNAPSHOT.OFF_PRIMARY'

   - For Instance NICs destroyed: with type: ‘NETWORK.OFFERING.REMOVE’

   - For the Instance being unmanaged: stopped and destroyed usage events (similar to the generated usage events when expunging an Instance), with types: ‘VM.STOP’ and ‘VM.DESTROY', unless the instance has been already stopped before being unmanaged and in this case only ‘VM.DESTROY' is generated.

.. |br| raw:: html

   <br>
   <br>

.. |ImportInstance.png| image:: /_static/images/vm-importinstance.png
   :alt: Import Unmanaged Instance.
   :width: 600 px
.. |vm-unmanagedmanaged.png| image:: /_static/images/vm-unmanagedmanaged.png
   :alt: Unmanaged and Managed Instances.
   :width: 600 px
.. |UnmanageButton.png| image:: /_static/images/unmanage-instance-icon.png
   :alt: button to unmanage an instance
.. |UnmanageInstance.png| image:: /_static/images/vm-unmanage-instance.png
   :alt: button to unmanage an instance
   :width: 600 px
