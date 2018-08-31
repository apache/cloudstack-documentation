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


Adding Hosts
------------

Additional hosts can be added at any time to provide more capacity for
guest VMs. For requirements and instructions, see :ref:`adding-a-host`.


Scheduled Maintenance and Maintenance Mode for Hosts
----------------------------------------------------

You can place a host into maintenance mode. When maintenance mode is
activated, the host becomes unavailable to receive new guest VMs, and
the guest VMs already running on the host are seamlessly migrated to
another host not in maintenance mode. This migration uses live migration
technology and does not interrupt the execution of the guest.


vCenter and Maintenance Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To enter maintenance mode on a vCenter host, both vCenter and CloudStack
must be used in concert. CloudStack and vCenter have separate
maintenance modes that work closely together.

#. Place the host into CloudStack's "scheduled maintenance" mode. This
   does not invoke the vCenter maintenance mode, but only causes VMs to
   be migrated off the host

   When the CloudStack maintenance mode is requested, the host first
   moves into the Prepare for Maintenance state. In this state it cannot
   be the target of new guest VM starts. Then all VMs will be migrated
   off the server. Live migration will be used to move VMs off the host.
   This allows the guests to be migrated to other hosts with no
   disruption to the guests. After this migration is completed, the host
   will enter the Ready for Maintenance mode.

#. Wait for the "Ready for Maintenance" indicator to appear in the UI.

#. Now use vCenter to perform whatever actions are necessary to maintain
   the host. During this time, the host cannot be the target of new VM
   allocations.

#. When the maintenance tasks are complete, take the host out of
   maintenance mode as follows:

   #. First use vCenter to exit the vCenter maintenance mode.

      This makes the host ready for CloudStack to reactivate it.

   #. Then use CloudStack's administrator UI to cancel the CloudStack
      maintenance mode

      When the host comes back online, the VMs that were migrated off of
      it may be migrated back to it manually and new VMs can be added.


XenServer and Maintenance Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For XenServer, you can take a server offline temporarily by using the
Maintenance Mode feature in XenCenter. When you place a server into
Maintenance Mode, all running VMs are automatically migrated from it to
another host in the same pool. If the server is the pool master, a new
master will also be selected for the pool. While a server is Maintenance
Mode, you cannot create or start any VMs on it.

**To place a server in Maintenance Mode:**

#. In the Resources pane, select the server, then do one of the
   following:

   -  Right-click, then click Enter Maintenance Mode on the shortcut
      menu.

   -  On the Server menu, click Enter Maintenance Mode.

#. Click Enter Maintenance Mode.

The server's status in the Resources pane shows when all running VMs
have been successfully migrated off the server.

**To take a server out of Maintenance Mode:**

#. In the Resources pane, select the server, then do one of the
   following:

   -  Right-click, then click Exit Maintenance Mode on the shortcut
      menu.

   -  On the Server menu, click Exit Maintenance Mode.

#. Click Exit Maintenance Mode.


Disabling and Enabling Zones, Pods, and Clusters
------------------------------------------------

You can enable or disable a zone, pod, or cluster without permanently
removing it from the cloud. This is useful for maintenance or when there
are problems that make a portion of the cloud infrastructure unreliable.
No new allocations will be made to a disabled zone, pod, or cluster
until its state is returned to Enabled. When a zone, pod, or cluster is
first added to the cloud, it is Disabled by default.

To disable and enable a zone, pod, or cluster:

#. Log in to the CloudStack UI as administrator

#. In the left navigation bar, click Infrastructure.

#. In Zones, click View More.

#. If you are disabling or enabling a zone, find the name of the zone in
   the list, and click the Enable/Disable button. |enable-disable.png|

#. If you are disabling or enabling a pod or cluster, click the name of
   the zone that contains the pod or cluster.

#. Click the Compute tab.

#. In the Pods or Clusters node of the diagram, click View All.

#. Click the pod or cluster name in the list.

#. Click the Enable/Disable button. |enable-disable.png|


Removing Hosts
--------------

Hosts can be removed from the cloud as needed. The procedure to remove a
host depends on the hypervisor type.


Removing XenServer and KVM Hosts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A node cannot be removed from a cluster until it has been placed in
maintenance mode. This will ensure that all of the VMs on it have been
migrated to other Hosts. To remove a Host from the cloud:

#. Place the node in maintenance mode.

   See `“Scheduled Maintenance and Maintenance Mode for
   Hosts” <#scheduled-maintenance-and-maintenance-mode-for-hosts>`_.

#. For KVM, stop the cloud-agent service.

#. Use the UI option to remove the node.

   Then you may power down the Host, re-use its IP address, re-install
   it, etc


Removing vSphere Hosts
~~~~~~~~~~~~~~~~~~~~~~

To remove this type of host, first place it in maintenance mode, as
described in `“Scheduled Maintenance and Maintenance Mode
for Hosts” <#scheduled-maintenance-and-maintenance-mode-for-hosts>`_. Then use
CloudStack to remove the host. CloudStack will not direct commands to a
host that has been removed using CloudStack. However, the host may still
exist in the vCenter cluster.


Re-Installing Hosts
-------------------

You can re-install a host after placing it in maintenance mode and then
removing it. If a host is down and cannot be placed in maintenance mode,
it should still be removed before the re-install.


Maintaining Hypervisors on Hosts
--------------------------------

When running hypervisor software on hosts, be sure all the hotfixes
provided by the hypervisor vendor are applied. Track the release of
hypervisor patches through your hypervisor vendor’s support channel, and
apply patches as soon as possible after they are released. CloudStack
will not track or notify you of required hypervisor patches. It is
essential that your hosts are completely up to date with the provided
hypervisor patches. The hypervisor vendor is likely to refuse to support
any system that is not up to date with patches.

.. note:: 
   The lack of up-do-date hotfixes can lead to data corruption and lost VMs.

(XenServer) For more information, see 
`Highly Recommended Hotfixes for XenServer in the CloudStack Knowledge Base 
<http://docs.cloudstack.org/Knowledge_Base/Possible_VM_corruption_if_XenServer_Hotfix_is_not_Applied/Highly_Recommended_Hotfixes_for_XenServer_5.6_SP2>`_.


Changing Host Password
----------------------

The password for a XenServer Node, KVM Node, or vSphere Node may be
changed in the database. Note that all Nodes in a Cluster must have the
same password.

To change a Node's password:

#. Identify all hosts in the cluster.

#. Change the password on all hosts in the cluster. Now the password for
   the host and the password known to CloudStack will not match.
   Operations on the cluster will fail until the two passwords match.

#. if the password in the database is encrypted, it is (likely) necessary to
   encrypt the new password using the database key before adding it to the database.

   .. code:: bash

      java -classpath /usr/share/cloudstack-common/lib/jasypt-1.9.0.jar \
      org.jasypt.intf.cli.JasyptPBEStringEncryptionCLI \
      encrypt.sh input="newrootpassword" \
      password="databasekey" \
      verbose=false

#. Get the list of host IDs for the host in the cluster where you are
   changing the password. You will need to access the database to
   determine these host IDs. For each hostname "h" (or vSphere cluster)
   that you are changing the password for, execute:

   .. code:: bash

      mysql> SELECT id FROM cloud.host WHERE name like '%h%';

#. This should return a single ID. Record the set of such IDs for these
   hosts. Now retrieve the host_details row id for the host

   .. code:: bash

      mysql> SELECT * FROM cloud.host_details WHERE name='password' AND host_id={previous step ID}; 

#. Update the passwords for the host in the database. In this example,
   we change the passwords for hosts with host IDs 5 and 12 and host_details IDs 8 and 22 to
   "password".

   .. code:: bash

      mysql> UPDATE cloud.host_details SET value='password' WHERE id=8 OR id=22;


Over-Provisioning and Service Offering Limits
---------------------------------------------

(Supported for XenServer, KVM, and VMware)

CPU and memory (RAM) over-provisioning factors can be set for each
cluster to change the number of VMs that can run on each host in the
cluster. This helps optimize the use of resources. By increasing the
over-provisioning ratio, more resource capacity will be used. If the
ratio is set to 1, no over-provisioning is done.

The administrator can also set global default over-provisioning ratios
in the cpu.overprovisioning.factor and mem.overprovisioning.factor
global configuration variables. The default value of these variables is
1: over-provisioning is turned off by default.

Over-provisioning ratios are dynamically substituted in CloudStack's
capacity calculations. For example:

Capacity = 2 GB
Over-provisioning factor = 2
Capacity after over-provisioning = 4 GB

With this configuration, suppose you deploy 3 VMs of 1 GB each:

Used = 3 GB
Free = 1 GB

The administrator can specify a memory over-provisioning ratio, and can
specify both CPU and memory over-provisioning ratios on a per-cluster
basis.

In any given cloud, the optimum number of VMs for each host is affected
by such things as the hypervisor, storage, and hardware configuration.
These may be different for each cluster in the same cloud. A single
global over-provisioning setting can not provide the best utilization
for all the different clusters in the cloud. It has to be set for the
lowest common denominator. The per-cluster setting provides a finer
granularity for better utilization of resources, no matter where the
CloudStack placement algorithm decides to place a VM.

The overprovisioning settings can be used along with dedicated resources
(assigning a specific cluster to an account) to effectively offer
different levels of service to different accounts. For example, an
account paying for a more expensive level of service could be assigned
to a dedicated cluster with an over-provisioning ratio of 1, and a
lower-paying account to a cluster with a ratio of 2.

When a new host is added to a cluster, CloudStack will assume the host
has the capability to perform the CPU and RAM over-provisioning which is
configured for that cluster. It is up to the administrator to be sure
the host is actually suitable for the level of over-provisioning which
has been set.


Limitations on Over-Provisioning in XenServer and KVM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  In XenServer, due to a constraint of this hypervisor, you can not use
   an over-provisioning factor greater than 4.

-  The KVM hypervisor can not manage memory allocation to VMs
   dynamically. CloudStack sets the minimum and maximum amount of memory
   that a VM can use. The hypervisor adjusts the memory within the set
   limits based on the memory contention.


Requirements for Over-Provisioning
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Several prerequisites are required in order for over-provisioning to
function properly. The feature is dependent on the OS type, hypervisor
capabilities, and certain scripts. It is the administrator's
responsibility to ensure that these requirements are met.


Balloon Driver
^^^^^^^^^^^^^^

All VMs should have a balloon driver installed in them. The hypervisor
communicates with the balloon driver to free up and make the memory
available to a VM.


XenServer
'''''''''

The balloon driver can be found as a part of xen pv or PVHVM drivers.
The xen pvhvm drivers are included in upstream linux kernels 2.6.36+.


VMware
''''''

The balloon driver can be found as a part of the VMware tools. All the
VMs that are deployed in a over-provisioned cluster should have the
VMware tools installed.


KVM
'''

All VMs are required to support the virtio drivers. These drivers are
installed in all Linux kernel versions 2.6.25 and greater. The
administrator must set CONFIG\_VIRTIO\_BALLOON=y in the virtio
configuration.


Hypervisor capabilities
^^^^^^^^^^^^^^^^^^^^^^^

The hypervisor must be capable of using the memory ballooning.


XenServer
'''''''''

The DMC (Dynamic Memory Control) capability of the hypervisor should be
enabled. Only XenServer Advanced and above versions have this feature.


VMware, KVM
'''''''''''

Memory ballooning is supported by default.


Setting Over-Provisioning Ratios
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are two ways the root admin can set CPU and RAM over-provisioning
ratios. First, the global configuration settings
cpu.overprovisioning.factor and mem.overprovisioning.factor will be
applied when a new cluster is created. Later, the ratios can be modified
for an existing cluster.

Only VMs deployed after the change are affected by the new setting. If
you want VMs deployed before the change to adopt the new
over-provisioning ratio, you must stop and restart the VMs. When this is
done, CloudStack recalculates or scales the used and reserved capacities
based on the new over-provisioning ratios, to ensure that CloudStack is
correctly tracking the amount of free capacity.

.. note:: 
   It is safer not to deploy additional new VMs while the capacity 
   recalculation is underway, in case the new values for available 
   capacity are not high enough to accommodate the new VMs. Just wait 
   for the new used/available values to become available, to be sure 
   there is room for all the new VMs you want.

To change the over-provisioning ratios for an existing cluster:

#. Log in as administrator to the CloudStack UI.

#. In the left navigation bar, click Infrastructure.

#. Under Clusters, click View All.

#. Select the cluster you want to work with, and click the Edit button.

#. Fill in your desired over-provisioning multipliers in the fields CPU
   overcommit ratio and RAM overcommit ratio. The value which is
   intially shown in these fields is the default value inherited from
   the global configuration settings.

   .. note:: 
      In XenServer, due to a constraint of this hypervisor, you can not 
      use an over-provisioning factor greater than 4.


Service Offering Limits and Over-Provisioning
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Service offering limits (e.g. 1 GHz, 1 core) are strictly enforced for
core count. For example, a guest with a service offering of one core
will have only one core available to it regardless of other activity on
the Host.

Service offering limits for gigahertz are enforced only in the presence
of contention for CPU resources. For example, suppose that a guest was
created with a service offering of 1 GHz on a Host that has 2 GHz cores,
and that guest is the only guest running on the Host. The guest will
have the full 2 GHz available to it. When multiple guests are attempting
to use the CPU a weighting factor is used to schedule CPU resources. The
weight is based on the clock speed in the service offering. Guests
receive a CPU allocation that is proportionate to the GHz in the service
offering. For example, a guest created from a 2 GHz service offering
will receive twice the CPU allocation as a guest created from a 1 GHz
service offering. CloudStack does not perform memory over-provisioning.


VLAN Provisioning
-----------------

CloudStack automatically creates and destroys interfaces bridged to
VLANs on the hosts. In general the administrator does not need to manage
this process.

CloudStack manages VLANs differently based on hypervisor type. For
XenServer or KVM, the VLANs are created on only the hosts where they
will be used and then they are destroyed when all guests that require
them have been terminated or moved to another host.

For vSphere the VLANs are provisioned on all hosts in the cluster even
if there is no guest running on a particular Host that requires the
VLAN. This allows the administrator to perform live migration and other
functions in vCenter without having to create the VLAN on the
destination Host. Additionally, the VLANs are not removed from the Hosts
when they are no longer needed.

You can use the same VLANs on different physical networks provided that
each physical network has its own underlying layer-2 infrastructure,
such as switches. For example, you can specify VLAN range 500 to 1000
while deploying physical networks A and B in an Advanced zone setup.
This capability allows you to set up an additional layer-2 physical
infrastructure on a different physical NIC and use the same set of VLANs
if you run out of VLANs. Another advantage is that you can use the same
set of IPs for different customers, each one with their own routers and
the guest networks on different physical NICs.


VLAN Allocation Example
~~~~~~~~~~~~~~~~~~~~~~~

VLANs are required for public and guest traffic. The following is an
example of a VLAN allocation scheme:

.. cssclass:: table-striped table-bordered table-hover

=================   =============================   ====================================================================================================
VLAN IDs            Traffic type                    Scope
=================   =============================   ====================================================================================================
less than 500       Management traffic.             Reserved for administrative purposes.  CloudStack software can access this, hypervisors, system VMs.
500-599             VLAN carrying public traffic.   CloudStack accounts.
600-799             VLANs carrying guest traffic.   CloudStack accounts. Account-specific VLAN is chosen from this pool.
800-899             VLANs carrying guest traffic.   CloudStack accounts. Account-specific VLAN chosen by CloudStack admin to assign to that account.
900-999             VLAN carrying guest traffic     CloudStack accounts. Can be scoped by project, domain, or all accounts.
greater than 1000   Reserved for future use
=================   =============================   ====================================================================================================


Adding Non Contiguous VLAN Ranges
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack provides you with the flexibility to add non contiguous VLAN
ranges to your network. The administrator can either update an existing
VLAN range or add multiple non contiguous VLAN ranges while creating a
zone. You can also use the UpdatephysicalNetwork API to extend the VLAN
range.

#. Log in to the CloudStack UI as an administrator or end user.

#. Ensure that the VLAN range does not already exist.

#. In the left navigation, choose Infrastructure.

#. On Zones, click View More, then click the zone to which you want to
   work with.

#. Click Physical Network.

#. In the Guest node of the diagram, click Configure.

#. Click Edit |edit-icon.png|.

   The VLAN Ranges field now is editable.

#. Specify the start and end of the VLAN range in comma-separated list.

   Specify all the VLANs you want to use, VLANs not specified will be
   removed if you are adding new ranges to the existing list.

#. Click Apply.


Assigning VLANs to Isolated Networks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack provides you the ability to control VLAN assignment to
Isolated networks. As a Root admin, you can assign a VLAN ID when a
network is created, just the way it's done for Shared networks.

The former behaviour also is supported — VLAN is randomly allocated to a
network from the VNET range of the physical network when the network
turns to Implemented state. The VLAN is released back to the VNET pool
when the network shuts down as a part of the Network Garbage Collection.
The VLAN can be re-used either by the same network when it is
implemented again, or by any other network. On each subsequent
implementation of a network, a new VLAN can be assigned.

Only the Root admin can assign VLANs because the regular users or domain
admin are not aware of the physical network topology. They cannot even
view what VLAN is assigned to a network.

To enable you to assign VLANs to Isolated networks,

#. Create a network offering by specifying the following:

   -  **Guest Type**: Select Isolated.

   -  **Specify VLAN**: Select the option.

   For more information, see the CloudStack Installation Guide.

#. Using this network offering, create a network.

   You can create a VPC tier or an Isolated network.

#. Specify the VLAN when you create the network.

   When VLAN is specified, a CIDR and gateway are assigned to this
   network and the state is changed to Setup. In this state, the network
   will not be garbage collected.

.. note:: 
   You cannot change a VLAN once it's assigned to the network. The VLAN 
   remains with the network for its entire life cycle.


.. |enable-disable.png| image:: /_static/images/enable-disable.png
   :alt: button to enable or disable zone, pod, or cluster.
.. |edit-icon.png| image:: /_static/images/edit-icon.png
   :alt: button to edit the VLAN range.


Out-of-band Management
----------------------

CloudStack provides Root admins the ability to configure and use supported
out-of-band management interface (e.g. IPMI, iLO, DRAC, etc.) on a physical
host to manage host power operations such as on, off, reset etc. By default,
IPMI 2.0 baseboard controller are supported out of the box with ``IPMITOOL``
out-of-band management driver in CloudStack that uses ``ipmitool`` for performing
IPMI 2.0 management operations.

Following are some global settings that control various aspects of this feature.

.. cssclass:: table-striped table-bordered table-hover

=======================================   =============================   ====================================================================================================
Global setting                            Default values                  Description
=======================================   =============================   ====================================================================================================
outofbandmanagement.action.timeout        60                              The out of band management action timeout in seconds, configurable per cluster
outofbandmanagement.ipmitool.interface    lanplus                         The out of band management IpmiTool driver interface to use. Valid values are: lan, lanplus etc
outofbandmanagement.ipmitool.path         /usr/bin/ipmitool               The out of band management ipmitool path used by the IpmiTool driver
outofbandmanagement.ipmitool.retries      1                               The out of band management IpmiTool driver retries option -R
outofbandmanagement.sync.poolsize         50                              The out of band management background sync thread pool size 50
=======================================   =============================   ====================================================================================================

A change in ``outofbandmanagement.sync.poolsize`` settings requires restarting of
management server(s) as the thread pool and a background (power state) sync
thread are configured during load time when CloudStack management server starts.
Rest of the global settings can be changed without requiring restarting of
management server(s).

The ``outofbandmanagement.sync.poolsize`` is the maximum number of ipmitool
background power state scanners that can run at a time. Based on the maximum
number of hosts you've, you can increase/decrease the value depending on how much
stress your management server host can endure. It will take atmost number of
total out-of-band-management enabled hosts in a round *
``outofbandmanagement.action.timeout`` / ``outofbandmanagement.sync.poolsize`` seconds
to complete a background power-state sync scan in a single round.

In order to use this feature, the Root admin needs to first configure
out-of-band management for a host using either the UI or the
``configureOutOfBandManagement`` API. Next, the Root admin needs to enable it.
The feature can be enabled or disabled across a zone or a cluster or a host,

Once out-of-band management is configured and enabled for a host (and provided
not disabled at zone or cluster level), Root admins would be able to issue
power management actions such as on, off, reset, cycle, soft and status.

If a host is in maintenance mode, Root admins are still allowed to perform
power management actions but in the UI a warning is displayed.

.. _host-security:

Security
--------

Starting 4.11, CloudStack has an inbuilt certicate authority (CA) framework and
a default 'root' CA provider which acts as a self-signed CA. The CA framework
participates in certificate issuance, renewal, revocation, and propagation of
certificates during setup of a host. This framework is primary used to
secure communications between CloudStack management server(s), the
KVM/LXC/SSVM/CPVM agent(s) and peer management server(s).

Following are some global settings that control various aspects of this feature.

.. cssclass:: table-striped table-bordered table-hover

=======================================   ====================================================================
Global setting                            Description
=======================================   ====================================================================
ca.framework.provider.plugin              The configured CA provider plugin
ca.framework.cert.keysize                 The key size used for certificate generation
ca.framework.cert.signature.algorithm     The certificate signature algorithm
ca.framework.cert.validity.period         Certificate validity in days
ca.framework.cert.automatic.renewal       Whether to auto-renew expiring certificate on hosts
ca.framework.background.task.delay        The delay between each CA background task round in seconds
ca.framework.cert.expiry.alert.period     The number of days to check and alert expiring certificates
ca.plugin.root.private.key                (hidden/encrypted in database) Auto-generated CA private key
ca.plugin.root.public.key                 (hidden/encrypted in database) CA public key
ca.plugin.root.ca.certificate             (hidden/encrypted in database) CA certificate
ca.plugin.root.issuer.dn                  The CA issue distinguished name used by the root CA provider
ca.plugin.root.auth.strictness            Setting to enforce two-way SSL authentication and trust validation
ca.plugin.root.allow.expired.cert         Setting to allow clients with expired certificates
=======================================   ====================================================================

A change in ``ca.framework.background.task.delay`` settings requires restarting of
management server(s) as the thread pool and a background tasks are configured
only when CloudStack management server(s) start.

After upgrade to CloudStack 4.11+, the CA framework will by default use the
``root`` CA provider. This CA provider will auto-generate its private/public keys
and CA certificate on first boot post-upgrade. For freshly installed
environments, the ``ca.plugin.root.auth.strictness`` setting will be ``true`` to
enforce two-way SSL authentication and trust validation between client and
server components, however, it will be ``false`` on upgraded environments to
be backward compatible with legacy behaviour of trusting all clients and
servers, and one-way SSL authentication. Upgraded/existing environments can
use the ``provisionCertificate`` API to renew/setup certificates for already
connected agents/hosts, and once all the agents/hosts are secured they may
enforce authentication and validation strictness by setting
``ca.plugin.root.auth.strictness`` to ``true`` and restarting the management
server(s).

Server Address Usage
--------------------

Historically, when multiple management servers are used a tcp-LB is used on
port 8250 (default) of the management servers and the VIP/LB-IP is used as the
``host`` setting to be used by various CloudStack agents such as the KVM, CPVM,
SSVM agents, who connect to the ``host`` on port 8250. However, starting
CloudStack 4.11+ the ``host`` setting can accept comma separated list of
management server IPs to which new CloudStack hosts/agents will get a shuffled
list of the same to which they can cycle reconnections in a round-robin way.

Securing Process
----------------

Agents while making connections/reconnections to management server will only
validate server certificate and be able to present client certificate (issued to
them) when ``cloud.jks`` is accessible to them. On older hosts that are setup
prior to this feature the keystore won't be available, however, they can still
connect to management server(s) if ``ca.plugin.root.auth.strictness`` is set to
``false``. Management server(s) will check and setup their own ``cloud.jks``
keystore on startup, this keystore will be used for connecting to peer
management server(s).

When a new host is being setup, such as adding a KVM host or starting a systemvm
host, the CA framework kicks in and uses ssh to execute ``keystore-setup`` to
generate a new keystore file ``cloud.jks.new``, save a random passphrase of the
keystore in the agent's properties file and a CSR ``cloud.csr`` file. The CSR is
then used to issue certificate for that agent/host and ssh is used to execute
``keystore-cert-import`` to import the issued certificate along with the CA
certificate(s), the keystore is that renamed as ``cloud.jks`` replacing an
previous keystore in-use. During this process, keys and certificates files are
also stored in ``cloud.key``, ``cloud.crt``, ``cloud.ca.crt`` in the
agent's configuration directory.

When hosts are added out-of-band, for example a KVM host that is setup first
outside of CloudStack and added to a cluster, the keystore file will not be
available however the keystore and security could be setup by using keystore
utility scripts manually. The ``keystore-setup`` can be ran first to generate a
keystore and a CSR, then CloudStack CA can be used to issue certificate by
providing the CSR to the ``issueCertificate`` API, and finally issued certificate
and CA certificate(s) can be imported to the keystore using ``keystore-cert-import``
script.

Following lists the usage of these scripts, when using these script use full
paths, use the final keystore filename as ``cloud.jks``, and the certificate/key
content need to be encoded and provided such that newlines are replace with ``^``
and space are replaced with ``~``:

.. code:: bash

  keystore-setup <properties file> <keystore file> <passphrase> <validity> <csr file>

  keystore-cert-import <properties file> <keystore file> <mode: ssh|agent> <cert file> <cert content> <ca-cert file> <ca-cert content> <private-key file> <private key content:optional>

Starting 4.11.1, a KVM host is considered secured when it has its keystore and
certificates setup for both the agent and libvirtd process. A secured host will
only allow and initiate TLS enabled live VM migration. This requires libvirtd
to listen on default port 16514, and the port to be allowed in the firewall
rules. Certificate renewal (using the ``provisionCertificate`` API) will restart
both the libvirtd process and agent after deploying new certificates.


KVM Libvirt Hook Script Include
--------------------------------

Feature Overview
~~~~~~~~~~~~~~~~~

-  This feature applies to KVM hosts.
-  KVM utilised under CloudStack uses the standard Libvirt hook script behaviour as outlined in the Libvirt documentation page `hooks`_.
-  During the install of the KVM CloudStack agent, the Libvirt hook script "/etc/libvirt/hooks/qemu", referred to as the qemu script hereafter is installed. 
-  This is a python script that carries out network management tasks every time a VM is started, stopped or migrated, as per the Libvirt hooks specification.
-  Custom network configuration tasks can be done at the same time as the qemu script is called.
-  Since the tasks in question are user-specific, they cannot be included in the CloudStack-provided qemu script.

-  The Libvirt documentation page `qemu`_ describes the parameters that can be passed to the qemu script, based on what actions KVM and Libvirt are carrying out on each VM: 'prepare', 'start', 'started', 'stopped', 'release', 'migrate', 'restore', 'reconnect' and 'attach'.

The KVM Libvirt Hook script allows for
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. The inclusion and execution of custom scripts to perform additional networking configuration tasks.
#. The included custom scripts can be bash scripts and/or python scripts.
#. Each custom script's start-up and return commands are captured and logged.
#. There are no limits to the number of custom scripts that can be included or called.

Usage
~~~~~~

-  The cloudstack-agent package will install the qemu script in the /etc/libvirt/hooks directory of Libvirt.
-  The Libvirt documentation page `arguments`_ describes the arguments that can be passed to the qemu script. 
-  The input arguments are: 

    #. Name of the object involved in the operation, or '-' if there is none. For example, the name of a guest being started.
    #. Name of the operation being performed. For example, 'start' if a guest is being started.
    #. Sub-operation indication, or '-' if there is none.
    #. An extra argument string, or '-' if there is none.

-  The operation argument is based on what actions KVM and Libvirt are carrying out on each VM: 'prepare', 'start', 'started', 'stopped', 'release', 'migrate', 'restore', 'reconnect', 'attach'.

-  If an invalid operation argument is received, the qemu script will log the fact, not execute any custom scripts and exit.

-  All input arguments that are passed to the qemu script will also be passed to each custom script. 

-  For each of the above actions, the qemu script will find and run scripts by the name "<action>_<custom script name>" in a custom include path /etc/libvirt/hooks/custom/. Custom scripts that do not follow this naming convention will be ignored and not be executed.

-  In addition to the Libvirt standard actions, the qemu script will also find and run custom scripts with an "all" prefixed to the script name. For example: "all_<custom script name>". These custom scripts will run every time the qemu script is called with a valid Libvirt action.
-  In the case of multiple custom scripts, they will be executed in sorted (alphabetical) order. The alphabetical ordering will use the file name part after the prefix and underscore have been removed from the file name. For example, if there are two custom script files in the directory: all_cde.sh, migrate_abc.py; they will be sorted and executed in this order: migrate_abc.py, all_cde.sh.
-  Custom scripts can either be bash scripts and/or python scripts.
-  Custom scripts must be executable by the underlying host operating system. Non-executable scripts will be logged and ignored.
-  Each custom script's start-up and return commands will be captured and logged.
-  During execution of a custom script, the standard out (stdout) and standard error (stderr) outputs of the custom script will be logged (appended) to /var/log/libvirt/qemu-hook.log. If the custom script needs to log anything, it can also use this file for logging purposes.
-  There is a timeout setting in the qemu script that counts down at the start of every execution of a custom script. If the custom script is still executing after the timeout time has elapsed, the custom script will be gracefully terminated.

Timeout Configuration
~~~~~~~~~~~~~~~~~~~~~~

-  The timeout setting called "timeoutSeconds", at the top of the qemu script, has a default timeout setting of 10 minutes, expressed as 10 * 60 seconds, and can be manually modified if a different timeout is required.
-  To configure a different timeout, do the following:

    #. Navigate to the /etc/libvirt/hooks/ folder.
    #. Open the qemu script in an editor.
    #. Find the "timeoutSeconds" timeout setting.
    #. Change the 10 * 60 value to a preferred timeout value. For example 20 * 60, for a 20-minute timeout.

Custom Script Naming for a Specific VM Action
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-  For a custom script that needs to be executed at the end of a specific VM action, do the following: 

    #. Navigate to the custom script that needs to be executed for a specific action.
    #. Rename the file by prefixing to the filename the specific action name followed by an underscore. For example, if a custom script is named abc.sh, then prefix 'migrate' and an underscore to the name to become migrate_abc.sh.


Custom Script Naming for All VM Actions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  For a custom script that needs to be executed at the end of all VM actions, do the following:

    #. Navigate to the custom script that needs to be executed for all actions.
    #. Rename the file by prefixing 'all' to the filename, followed by an underscore.  For example, if a custom script is named def.py, then prefix 'all' and an underscore to the name to become all_def.py.

Custom Script Execution Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ 
-  Grant each custom script execute permissions so that the underlying host operating system can execute them:

    #. Navigate to the custom script that needs to be executable.
    #. Grant the custom script execute permissions.

-  Place the custom scripts in the custom include folder /etc/libvirt/hooks/custom/ so that the qemu script will be able to find and execute them:

    #. Make sure that the /etc/libvirt/hooks/custom/ folder is created and that it has the correct access permissions.
    #. Navigate to the custom scripts that need to be copied.
    #. Copy the scripts to the /etc/libvirt/hooks/custom/ folder.


-  In shell custom scripts include #!/bin/bash in the first line of the file so that the script will be executed with bash.
-  In Python custom scripts include #!/usr/bin/python in the first line of the file so that the script will be executed with python.

.. _`hooks`: https://libvirt.org/hooks.html
.. _`qemu`: https://libvirt.org/hooks.html#qemu
.. _`arguments`: https://libvirt.org/hooks.html#arguments
