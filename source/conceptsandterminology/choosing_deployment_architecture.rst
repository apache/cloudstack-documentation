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



The architecture used in a deployment will vary depending on the size
and purpose of the deployment. This section contains examples of
deployment architecture, including a small-scale deployment useful for
test and trial deployments and a fully-redundant large-scale setup for
production deployments.


Small-Scale Deployment
----------------------

|Small-Scale Deployment|

This diagram illustrates the Network architecture of a small-scale
CloudStack deployment.

-  A firewall provides a connection to the Internet. The firewall is
   configured in NAT mode. The firewall forwards HTTP requests and API
   calls from the Internet to the Management Server. The Management
   Server resides on the Management Network.

-  A layer-2 switch connects all physical servers and storage.

-  A single NFS server functions as both the primary and secondary
   storage.

-  The Management Server is connected to the Management Network.


Large-Scale Redundant Setup
---------------------------

|Large-Scale Redundant Setup|

This diagram illustrates the Network architecture of a large-scale
CloudStack deployment.

-  A layer-3 switching layer is at the core of the data center. A router
   redundancy protocol like VRRP should be deployed. Typically high-end
   core switches also include firewall modules. Separate firewall
   appliances may also be used if the layer-3 switch does not have
   integrated firewall capabilities. The firewalls are configured in NAT
   mode. The firewalls provide the following functions:

   -  Forwards HTTP requests and API calls from the Internet to the
      Management Server. The Management Server resides on the Management
      Network.

   -  When the cloud spans multiple zones, the firewalls should enable
      site-to-site VPN such that servers in different zones can directly
      reach each other.

-  A layer-2 access switch layer is established for each pod. Multiple
   switches can be stacked to increase port count. In either case,
   redundant pairs of layer-2 switches should be deployed.

-  The Management Server cluster (including front-end load balancers,
   Management Server nodes, and the MySQL database) is connected to the
   Management Network through a pair of load balancers.

-  Secondary storage servers are connected to the Management Network.

-  Each pod contains storage and computing servers. Each storage and
   computing server should have redundant NICs connected to separate
   layer-2 access switches.


Separate Storage Network
------------------------

In the large-scale redundant setup described in the previous section,
storage traffic can overload the Management Network. A separate Storage
Network is optional for deployments. Storage protocols such as iSCSI are
sensitive to network delays. A separate Storage Network ensures Guest
Network traffic contention does not impact storage performance.


Multi-Node Management Server
----------------------------

The CloudStack Management Server is deployed on one or more front-end
servers connected to a single MySQL database. Optionally a pair of
hardware load balancers distributes requests from the web. A backup
management server set may be deployed using MySQL replication at a
remote site to add DR capabilities.

|Multi-Node Management Server|

The administrator must decide the following.

-  Whether or not load balancers will be used.

-  How many Management Servers will be deployed.

-  Whether MySQL replication will be deployed to enable disaster
   recovery.


Multi-Site Deployment
---------------------

The CloudStack platform scales well into multiple sites through the use
of zones. The following diagram shows an example of a multi-site
deployment.

|Example Of A Multi-Site Deployment|

Data Center 1 houses the primary Management Server as well as zone 1.
The MySQL database is replicated in real time to the secondary
Management Server installation in Data Center 2.

|Separate Storage Network|

This diagram illustrates a setup with a separate Storage Network. Each
server has four NICs, two connected to pod-level network switches and
two connected to Storage Network switches.

There are two ways to configure the Storage Network:

-  Bonded NIC and redundant switches can be deployed for NFS. In NFS
   deployments, redundant switches and bonded NICs still result in one
   Network (one CIDR block+ default gateway address).

-  iSCSI can take advantage of two separate Storage Networks (two CIDR
   blocks each with its own default gateway). Multipath iSCSI client can
   failover and load balance between separate Storage Networks.

|NIC Bonding And Multipath I/O|

This diagram illustrates the differences between NIC bonding and
Multipath I/O (MPIO). NIC bonding configuration involves only one
network. MPIO involves two separate networks.


Choosing a Hypervisor
---------------------

CloudStack supports many popular hypervisors. Your cloud can consist
entirely of hosts running a single hypervisor, or you can use multiple
hypervisors. Each cluster of hosts must run the same hypervisor.

You might already have an installed base of nodes running a particular
hypervisor, in which case, your choice of hypervisor has already been
made. If you are starting from scratch, you need to decide what
hypervisor software best suits your needs. A discussion of the relative
advantages of each hypervisor is outside the scope of our documentation.
However, it will help you to know which features of each hypervisor are
supported by CloudStack. The following table provides this information.

.. cssclass:: table-striped table-bordered table-hover

+-----------------------------------------+-----------+----------+--------+-----+--------+-------+
| Feature                                 | XenServer | vSphere  | KVM -  | LXC | HyperV | Bare  |
|                                         |           |          | RHEL   |     |        | Metal |
+=========================================+===========+==========+========+=====+========+=======+
| Network Throttling                      | Yes       | Yes      | Yes    | No  | ?      | N/A   |
+-----------------------------------------+-----------+----------+--------+-----+--------+-------+
| Security groups in zones that use       | Yes       | No       | Yes    | Yes | ?      | No    |
| basic networking                        |           |          |        |     |        |       |
+-----------------------------------------+-----------+----------+--------+-----+--------+-------+
| iSCSI                                   | Yes       | Yes      | Yes    | Yes | Yes    | N/A   |
+-----------------------------------------+-----------+----------+--------+-----+--------+-------+
| FibreChannel                            | Yes       | Yes      | Yes    | Yes | Yes    | N/A   |
+-----------------------------------------+-----------+----------+--------+-----+--------+-------+
| Local Disk                              | Yes       | Yes      | Yes    | Yes | Yes    | Yes   |
+-----------------------------------------+-----------+----------+--------+-----+--------+-------+
| HA                                      | Yes       | Yes      | Yes    | ?   | Yes    | N/A   |
|                                         |           | (Native) |        |     |        |       |
+-----------------------------------------+-----------+----------+--------+-----+--------+-------+
| Snapshots of local disk                 | Yes       | Yes      | Yes    | ?   | ?      | N/A   |
+-----------------------------------------+-----------+----------+--------+-----+--------+-------+
| Local disk as data disk                 | Yes       | No       | Yes    | Yes | Yes    | N/A   |
+-----------------------------------------+-----------+----------+--------+-----+--------+-------+
| Work load balancing                     | No        | DRS      | No     | No  | ?      | N/A   |
+-----------------------------------------+-----------+----------+--------+-----+--------+-------+
| Manual live migration of Instances from | Yes       | Yes      | Yes    | ?   | Yes    | N/A   |
| host to host                            |           |          |        |     |        |       |
+-----------------------------------------+-----------+----------+--------+-----+--------+-------+
| Conserve management traffic IP          | Yes       | No       | Yes    | Yes | ?      | N/A   |
| address by using link local             |           |          |        |     |        |       |
| network to communicate with             |           |          |        |     |        |       |
| virtual router                          |           |          |        |     |        |       |
+-----------------------------------------+-----------+----------+--------+-----+--------+-------+


Hypervisor Support for Primary Storage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following table shows storage options and parameters for different
hypervisors.

.. cssclass:: table-striped table-bordered table-hover

+----------------------------------+-------------+---------------+----------------+----------------+--------+
| Primary Storage Type             | XenServer   | vSphere       | KVM - RHEL     | LXC            | HyperV |
+==================================+=============+===============+================+================+========+
| Format for Disks, Templates,     | VHD         | VMDK          | QCOW2          |                | VHD    |
| and Snapshots                    |             |               |                |                |        |
+----------------------------------+-------------+---------------+----------------+----------------+--------+
| iSCSI support                    | CLVM        | VMFS          | Yes via Shared | Yes via Shared | No     |
|                                  |             |               | Mountpoint     | Mountpoint     |        |
+----------------------------------+-------------+---------------+----------------+----------------+--------+
| Fiber Channel support            | Yes, Via    | VMFS          | Yes via Shared | Yes via Shared | No     |
|                                  | existing SR |               | Mountpoint     | Mountpoint     |        |
+----------------------------------+-------------+---------------+----------------+----------------+--------+
| NFS support                      | Yes         | Yes           | Yes            | Yes            | No     |
+----------------------------------+-------------+---------------+----------------+----------------+--------+
| Local storage support            | Yes         | Yes           | Yes            | Yes            | Yes    |
+----------------------------------+-------------+---------------+----------------+----------------+--------+
| Storage over-provisioning        | NFS         | NFS and iSCSI | NFS            |                | No     |
+----------------------------------+-------------+---------------+----------------+----------------+--------+
| SMB/CIFS                         | No          | No            | No             | No             | Yes    |
+----------------------------------+-------------+---------------+----------------+----------------+--------+

XenServer uses a clustered LVM system to store Instance images on iSCSI and
Fiber Channel volumes and does not support over-provisioning in the
hypervisor. The storage server itself, however, can support
thin-provisioning. As a result the CloudStack can still support storage
over-provisioning by running on thin-provisioned storage volumes.

KVM supports "Shared Mountpoint" storage. A shared mountpoint is a file
system path local to each server in a given cluster. The path must be
the same across all Hosts in the cluster, for example /mnt/primary1.
This shared mountpoint is assumed to be a clustered filesystem such as
OCFS2. In this case the CloudStack does not attempt to mount or unmount
the storage as is done with NFS. The CloudStack requires that the
administrator insure that the storage is available

With NFS storage, CloudStack manages the overprovisioning. In this case
the global configuration parameter storage.overprovisioning.factor
controls the degree of overprovisioning. This is independent of
hypervisor type.

Local storage is an option for primary storage for vSphere, XenServer,
and KVM. When the local disk option is enabled, a local disk storage
pool is automatically created on each host. To use local storage for the
System Virtual Machines (such as the Virtual Router), set
system.vm.use.local.storage to true in global configuration.

CloudStack supports multiple primary storage pools in a Cluster. For
example, you could provision 2 NFS servers in primary storage. Or you
could provision 1 iSCSI LUN initially and then add a second iSCSI LUN
when the first approaches capacity.


Best Practices
--------------

Deploying a cloud is challenging. There are many different technology
choices to make, and CloudStack is flexible enough in its configuration
that there are many possible ways to combine and configure the chosen
technology. This section contains suggestions and requirements about
cloud deployments.

These should be treated as suggestions and not absolutes. However, we do
encourage anyone planning to build a cloud outside of these guidelines
to seek guidance and advice on the project mailing lists.


Process Best Practices
~~~~~~~~~~~~~~~~~~~~~~

-  A staging system that models the production environment is strongly
   advised. It is critical if customizations have been applied to
   CloudStack.

-  Allow adequate time for installation, a beta, and learning the
   system. Installs with basic networking can be done in hours. Installs
   with advanced networking usually take several days for the first
   attempt, with complicated installations taking longer. For a full
   production system, allow at least 4-8 weeks for a beta to work
   through all of the integration issues. You can get help from fellow
   users on the cloudstack-users mailing list.


Setup Best Practices
~~~~~~~~~~~~~~~~~~~~

-  Each host should be configured to accept connections only from
   well-known entities such as the CloudStack Management Server or your
   network monitoring software.

-  Use multiple clusters per pod if you need to achieve a certain switch
   density.

-  Primary storage mountpoints or LUNs should not exceed 6 TB in size.
   It is better to have multiple smaller primary storage elements per
   cluster than one large one.

-  When exporting shares on primary storage, avoid data loss by
   restricting the range of IP addresses that can access the storage.
   See "Linux NFS on Local Disks and DAS" or "Linux NFS on iSCSI".

-  NIC bonding is straightforward to implement and provides increased
   reliability.

-  10G networks are generally recommended for storage access when larger
   servers that can support relatively more Instances are used.

-  Host capacity should generally be modeled in terms of RAM for the
   guests. Storage and CPU may be overprovisioned. RAM may not. RAM is
   usually the limiting factor in capacity designs.

-  (XenServer) Configure the XenServer dom0 settings to allocate more
   memory to dom0. This can enable XenServer to handle larger numbers of
   Instances. We recommend 2940 MB of RAM for XenServer dom0. For
   instructions on how to do this, see
   `http://support.citrix.com/article/CTX126531 
   <http://support.citrix.com/article/CTX126531>`_.
   The article refers to XenServer 5.6, but the same information applies
   to XenServer 6.0.


Maintenance Best Practices
~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Monitor host disk space. Many host failures occur because the host's
   root disk fills up from logs that were not rotated adequately.

-  Monitor the total number of Instances in each cluster, and disable
   allocation to the cluster if the total is approaching the maximum
   that the hypervisor can handle. Be sure to leave a safety margin to
   allow for the possibility of one or more hosts failing, which would
   increase the Instance load on the other hosts as the Instances are redeployed.
   Consult the documentation for your chosen hypervisor to find the
   maximum permitted number of Instances per host, then use CloudStack global
   configuration settings to set this as the default limit. Monitor the
   Instance activity in each cluster and keep the total number of Instances below a
   safe level that allows for the occasional host failure. For example,
   if there are N hosts in the cluster, and you want to allow for one
   host in the cluster to be down at any given time, the total number of
   Instances you can permit in the cluster is at most (N-1) \*
   (per-host-limit). Once a cluster reaches this number of Instances, use the
   CloudStack UI to disable allocation to the cluster.

.. warning::
   The lack of up-do-date hotfixes can lead to data corruption and lost Instances.

Be sure all the hotfixes provided by the hypervisor vendor are applied. Track 
the release of hypervisor patches through your hypervisor vendor’s support 
channel, and apply patches as soon as possible after they are released. 
CloudStack will not track or notify you of required hypervisor patches. It is 
essential that your hosts are completely up to date with the provided 
hypervisor patches. The hypervisor vendor is likely to refuse to support any 
system that is not up to date with patches.


.. |Small-Scale Deployment| image:: /_static/images/small-scale-deployment.png
.. |Large-Scale Redundant Setup| image:: /_static/images/large-scale-redundant-setup.png
.. |Multi-Node Management Server| image:: /_static/images/multi-node-management-server.png
.. |Example Of A Multi-Site Deployment| image:: /_static/images/multi-site-deployment.png
.. |Separate Storage Network| image:: /_static/images/separate-storage-network.png
.. |NIC Bonding And Multipath I/O| image:: /_static/images/nic-bonding-and-multipath-io.png
