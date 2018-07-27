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


Host Citrix XenServer Installation
----------------------------------

If you want to use the Citrix XenServer hypervisor to run guest virtual
machines, install XenServer 6.0 or XenServer 6.0.2 on the host(s) in
your cloud. For an initial installation, follow the steps below. If you
have previously installed XenServer and want to upgrade to another
version, see :ref:`upgrading-xenserver-version`.


System Requirements for XenServer Hosts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  The host must be certified as compatible with one of the following.
   See the Citrix Hardware Compatibility Guide:
   `http://hcl.xensource.com <http://hcl.xensource.com>`_

    -  XenServer 5.6 SP2
    -  XenServer 6.0
    -  XenServer 6.0.2
    -  XenServer 6.1.0
    -  XenServer 6.2.0
    -  XenServer 6.5.0

-  You must re-install Citrix XenServer if you are going to re-use a
   host from a previous install.

-  Must support HVM (Intel-VT or AMD-V enabled)

-  Be sure all the hotfixes provided by the hypervisor vendor are
   applied. Track the release of hypervisor patches through your
   hypervisor vendor’s support channel, and apply patches as soon as
   possible after they are released. CloudStack will not track or notify
   you of required hypervisor patches. It is essential that your hosts
   are completely up to date with the provided hypervisor patches. The
   hypervisor vendor is likely to refuse to support any system that is
   not up to date with patches.

-  All hosts within a cluster must be homogeneous. The CPUs must be of
   the same type, count, and feature flags.

-  Must support HVM (Intel-VT or AMD-V enabled in BIOS)

-  64-bit x86 CPU (more cores results in better performance)

-  Hardware virtualization support required

-  4 GB of memory

-  36 GB of local disk

-  At least 1 NIC

-  Statically allocated IP Address

-  When you deploy CloudStack, the hypervisor host must not have any VMs
   already running

.. warning:: 
   The lack of up-to-date hotfixes can lead to data corruption and lost VMs.


XenServer Installation Steps
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. From `https://www.citrix.com/English/ss/downloads/ 
   <https://www.citrix.com/English/ss/downloads/>`_,
   download the appropriate version of XenServer for your CloudStack
   version (see `"System Requirements for XenServer Hosts" 
   <#system-requirements-for-xenserver-hosts>`_). Install it using
   the Citrix XenServer Installation Guide.

   Older Versions of XenServer:

   Note that you can download the most recent release of XenServer
   without having a Citrix account. If you wish to download older
   versions, you will need to create an account and look through the
   download archives.


Configure XenServer dom0 Memory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Configure the XenServer dom0 settings to allocate more memory to dom0.
This can enable XenServer to handle larger numbers of virtual machines.
We recommend 2940 MB of RAM for XenServer dom0. For instructions on how
to do this, see `http://support.citrix.com/article/CTX126531 
<http://support.citrix.com/article/CTX126531>`_. The article refers to 
XenServer 5.6, but the same information applies to XenServer 6.0.


Username and Password
~~~~~~~~~~~~~~~~~~~~~

All XenServers in a cluster must have the same username and password as
configured in CloudStack.


Time Synchronization
~~~~~~~~~~~~~~~~~~~~

The host must be set to use NTP. All hosts in a pod must have the same
time.

#. Install NTP.

   .. parsed-literal::

      # yum install ntp

#. Edit the NTP configuration file to point to your NTP server.

   .. parsed-literal::

      # vi /etc/ntp.conf

   Add one or more server lines in this file with the names of the NTP
   servers you want to use. For example:

   .. parsed-literal::

      server 0.xenserver.pool.ntp.org
      server 1.xenserver.pool.ntp.org
      server 2.xenserver.pool.ntp.org
      server 3.xenserver.pool.ntp.org

#. Restart the NTP client.

   .. parsed-literal::

      # service ntpd restart

#. Make sure NTP will start again upon reboot.

   .. parsed-literal::

      # chkconfig ntpd on


Install CloudStack XenServer Support Package (CSP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

(Optional)

To enable security groups, elastic load balancing, and elastic IP on
XenServer, download and install the CloudStack XenServer Support Package
(CSP). After installing XenServer, perform the following additional
steps on each XenServer host.

**For XenServer 6.1:**

CSP functionality is already present in XenServer 6.1

#. Run the below command
   
   .. parsed-literal::

      xe-switch-network-backend bridge

#. update sysctl.conf with the following

   .. parsed-literal::
   
      net.bridge.bridge-nf-call-iptables = 1
      net.bridge.bridge-nf-call-ip6tables = 0
      net.bridge.bridge-nf-call-arptables = 1
      
      $ sysctl -p /etc/sysctl.conf


**For XenServer 6.0.2, 6.0, 5.6 SP2:**

#. Download the CSP software onto the XenServer host from one of the
   following links:

   For XenServer 6.0.2:

   `http://download.cloud.com/releases/3.0.1/XS-6.0.2/xenserver-cloud-supp.tgz 
   <http://download.cloud.com/releases/3.0.1/XS-6.0.2/xenserver-cloud-supp.tgz>`_

   For XenServer 5.6 SP2:

   `http://download.cloud.com/releases/2.2.0/xenserver-cloud-supp.tgz 
   <http://download.cloud.com/releases/2.2.0/xenserver-cloud-supp.tgz>`_

   For XenServer 6.0:

   `http://download.cloud.com/releases/3.0/xenserver-cloud-supp.tgz 
   <http://download.cloud.com/releases/3.0/xenserver-cloud-supp.tgz>`_

 
#. Extract the file:

   .. parsed-literal::

      # tar xf xenserver-cloud-supp.tgz

#. Run the following script:

   .. parsed-literal::

      # xe-install-supplemental-pack xenserver-cloud-supp.iso

#. If the XenServer host is part of a zone that uses basic networking,
   disable Open vSwitch (OVS):

   .. parsed-literal::

      # xe-switch-network-backend  bridge

   Restart the host machine when prompted.

The XenServer host is now ready to be added to CloudStack.


Primary Storage Setup for XenServer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack natively supports NFS, iSCSI and local storage. If you are
using one of these storage types, there is no need to create the
XenServer Storage Repository ("SR").

If, however, you would like to use storage connected via some other
technology, such as FiberChannel, you must set up the SR yourself. To do
so, perform the following steps. If you have your hosts in a XenServer
pool, perform the steps on the master node. If you are working with a
single XenServer which is not part of a cluster, perform the steps on
that XenServer.

#. Connect FiberChannel cable to all hosts in the cluster and to the
   FiberChannel storage host.

#. Rescan the SCSI bus. Either use the following command or use
   XenCenter to perform an HBA rescan.

   .. parsed-literal::

      # scsi-rescan

#. Repeat step 2 on every host.

#. Check to be sure you see the new SCSI disk.

   .. parsed-literal::

      # ls /dev/disk/by-id/scsi-360a98000503365344e6f6177615a516b -l

   The output should look like this, although the specific file name
   will be different (scsi-<scsiID>):

   .. parsed-literal::

      lrwxrwxrwx 1 root root 9 Mar 16 13:47
      /dev/disk/by-id/scsi-360a98000503365344e6f6177615a516b -> ../../sdc

#. Repeat step 4 on every host.

#. On the storage server, run this command to get a unique ID for the
   new SR.

   .. parsed-literal::

      # uuidgen

   The output should look like this, although the specific ID will be
   different:

   .. parsed-literal::

      e6849e96-86c3-4f2c-8fcc-350cc711be3d

#. Create the FiberChannel SR. In name-label, use the unique ID you just
   generated.

   .. parsed-literal::

      # xe sr-create type=lvmohba shared=true
      device-config:SCSIid=360a98000503365344e6f6177615a516b
      name-label="e6849e96-86c3-4f2c-8fcc-350cc711be3d"

   This command returns a unique ID for the SR, like the following
   example (your ID will be different):

   .. parsed-literal::

      7a143820-e893-6c6a-236e-472da6ee66bf

#. To create a human-readable description for the SR, use the following
   command. In uuid, use the SR ID returned by the previous command. In
   name-description, set whatever friendly text you prefer.

   .. parsed-literal::

      # xe sr-param-set uuid=7a143820-e893-6c6a-236e-472da6ee66bf name-description="Fiber Channel storage repository"

   Make note of the values you will need when you add this storage to
   CloudStack later (see `"Add Primary Storage" 
   <configuration.html#add-primary-storage>`_). In the Add Primary Storage
   dialog, in Protocol, you will choose PreSetup. In SR Name-Label, you
   will enter the name-label you set earlier (in this example,
   e6849e96-86c3-4f2c-8fcc-350cc711be3d).

#. (Optional) If you want to enable multipath I/O on a FiberChannel SAN,
   refer to the documentation provided by the SAN vendor.


iSCSI Multipath Setup for XenServer (Optional)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When setting up the storage repository on a Citrix XenServer, you can
enable multipath I/O, which uses redundant physical components to
provide greater reliability in the connection between the server and the
SAN. To enable multipathing, use a SAN solution that is supported for
Citrix servers and follow the procedures in Citrix documentation. The
following links provide a starting point:

-  `http://support.citrix.com/article/CTX118791 
   <http://support.citrix.com/article/CTX118791>`_

-  `http://support.citrix.com/article/CTX125403 
   <http://support.citrix.com/article/CTX125403>`_

You can also ask your SAN vendor for advice about setting up your Citrix
repository for multipathing.

Make note of the values you will need when you add this storage to the
CloudStack later (see `"Add Primary Storage" 
<configuration.html#add-primary-storage>`_). In the Add Primary Storage 
dialog, in Protocol, you will choose PreSetup. In SR Name-Label, you will 
enter the same name used to create the SR.

If you encounter difficulty, address the support team for the SAN
provided by your vendor. If they are not able to solve your issue, see
Contacting Support.


Physical Networking Setup for XenServer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once XenServer has been installed, you may need to do some additional
network configuration. At this point in the installation, you should
have a plan for what NICs the host will have and what traffic each NIC
will carry. The NICs should be cabled as necessary to implement your
plan.

If you plan on using NIC bonding, the NICs on all hosts in the cluster
must be cabled exactly the same. For example, if eth0 is in the private
bond on one host in a cluster, then eth0 must be in the private bond on
all hosts in the cluster.

The IP address assigned for the management network interface must be
static. It can be set on the host itself or obtained via static DHCP.

CloudStack configures network traffic of various types to use different
NICs or bonds on the XenServer host. You can control this process and
provide input to the Management Server through the use of XenServer
network name labels. The name labels are placed on physical interfaces
or bonds and configured in CloudStack. In some simple cases the name
labels are not required.

When configuring networks in a XenServer environment, network traffic
labels must be properly configured to ensure that the virtual interfaces
are created by CloudStack are bound to the correct physical device. The
name-label of the XenServer network must match the XenServer traffic
label specified while creating the CloudStack network. This is set by
running the following command:

.. parsed-literal::

   xe network-param-set uuid=<network id> name-label=<CloudStack traffic label>


Configuring Public Network with a Dedicated NIC for XenServer (Optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

CloudStack supports the use of a second NIC (or bonded pair of NICs,
described in :ref:`nic-bonding-for-xenserver`) for the public network. If
bonding is not used, the public network can be on any NIC and can be on
different NICs on the hosts in a cluster. For example, the public
network can be on eth0 on node A and eth1 on node B. However, the
XenServer name-label for the public network must be identical across all
hosts. The following examples set the network label to "cloud-public".
After the management server is installed and running you must configure
it with the name of the chosen network label (e.g. "cloud-public"); this
is discussed in `"Management Server Installation" 
<installation.html#management-server-installation>`_.

If you are using two NICs bonded together to create a public network,
see :ref:`nic-bonding-for-xenserver`.

If you are using a single dedicated NIC to provide public network
access, follow this procedure on each new host that is added to
CloudStack before adding the host.

#. Run xe network-list and find the public network. This is usually
   attached to the NIC that is public. Once you find the network make
   note of its UUID. Call this <UUID-Public>.

#. Run the following command.

   .. parsed-literal::

      # xe network-param-set name-label=cloud-public uuid=<UUID-Public>


Configuring Multiple Guest Networks for XenServer (Optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

CloudStack supports the use of multiple guest networks with the
XenServer hypervisor. Each network is assigned a name-label in
XenServer. For example, you might have two networks with the labels
"cloud-guest" and "cloud-guest2". After the management server is
installed and running, you must add the networks and use these labels so
that CloudStack is aware of the networks.

Follow this procedure on each new host before adding the host to
CloudStack:

#. Run xe network-list and find one of the guest networks. Once you find
   the network make note of its UUID. Call this <UUID-Guest>.

#. Run the following command, substituting your own name-label and uuid
   values.

   .. parsed-literal::

      # xe network-param-set name-label=<cloud-guestN> uuid=<UUID-Guest>

#. Repeat these steps for each additional guest network, using a
   different name-label and uuid each time.


Separate Storage Network for XenServer (Optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can optionally set up a separate storage network. This should be
done first on the host, before implementing the bonding steps below.
This can be done using one or two available NICs. With two NICs bonding
may be done as above. It is the administrator's responsibility to set up
a separate storage network.

Give the storage network a different name-label than what will be given
for other networks.

For the separate storage network to work correctly, it must be the only
interface that can ping the primary storage device's IP address. For
example, if eth0 is the management network NIC, ping -I eth0 <primary
storage device IP> must fail. In all deployments, secondary storage
devices must be pingable from the management network NIC or bond. If a
secondary storage device has been placed on the storage network, it must
also be pingable via the storage network NIC or bond on the hosts as
well.

You can set up two separate storage networks as well. For example, if
you intend to implement iSCSI multipath, dedicate two non-bonded NICs to
multipath. Each of the two networks needs a unique name-label.

If no bonding is done, the administrator must set up and name-label the
separate storage network on all hosts (masters and slaves).

Here is an example to set up eth5 to access a storage network on
172.16.0.0/24.

.. parsed-literal::

   # xe pif-list host-name-label='hostname' device=eth5
   uuid(RO): ab0d3dd4-5744-8fae-9693-a022c7a3471d
   device ( RO): eth5
   #xe pif-reconfigure-ip DNS=172.16.3.3 gateway=172.16.0.1 IP=172.16.0.55 mode=static netmask=255.255.255.0 uuid=ab0d3dd4-5744-8fae-9693-a022c7a3471d


.. _nic-bonding-for-xenserver:

NIC Bonding for XenServer (Optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

XenServer supports Source Level Balancing (SLB) NIC bonding. Two NICs
can be bonded together to carry public, private, and guest traffic, or
some combination of these. Separate storage networks are also possible.
Here are some example supported configurations:

-  2 NICs on private, 2 NICs on public, 2 NICs on storage

-  2 NICs on private, 1 NIC on public, storage uses management network

-  2 NICs on private, 2 NICs on public, storage uses management network

-  1 NIC for private, public, and storage

All NIC bonding is optional.

XenServer expects all nodes in a cluster will have the same network
cabling and same bonds implemented. In an installation the master will
be the first host that was added to the cluster and the slave hosts will
be all subsequent hosts added to the cluster. The bonds present on the
master set the expectation for hosts added to the cluster later. The
procedure to set up bonds on the master and slaves are different, and
are described below. There are several important implications of this:

-  You must set bonds on the first host added to a cluster. Then you
   must use xe commands as below to establish the same bonds in the
   second and subsequent hosts added to a cluster.

-  Slave hosts in a cluster must be cabled exactly the same as the
   master. For example, if eth0 is in the private bond on the master, it
   must be in the management network for added slave hosts.


Management Network Bonding
''''''''''''''''''''''''''

The administrator must bond the management network NICs prior to adding
the host to CloudStack.


Creating a Private Bond on the First Host in the Cluster
''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Use the following steps to create a bond in XenServer. These steps
should be run on only the first host in a cluster. This example creates
the cloud-private network with two physical NICs (eth0 and eth1) bonded
into it.

#. Find the physical NICs that you want to bond together.

   .. parsed-literal::

      # xe pif-list host-name-label='hostname' device=eth0
      # xe pif-list host-name-label='hostname' device=eth1

   These command shows the eth0 and eth1 NICs and their UUIDs.
   Substitute the ethX devices of your choice. Call the UUID's returned
   by the above command slave1-UUID and slave2-UUID.

#. Create a new network for the bond. For example, a new network with
   name "cloud-private".

   **This label is important. CloudStack looks for a network by a name
   you configure. You must use the same name-label for all hosts in the
   cloud for the management network.**

   .. parsed-literal::

      # xe network-create name-label=cloud-private
      # xe bond-create network-uuid=[uuid of cloud-private created above]
      pif-uuids=[slave1-uuid],[slave2-uuid]

Now you have a bonded pair that can be recognized by CloudStack as the
management network.


Public Network Bonding
''''''''''''''''''''''

Bonding can be implemented on a separate, public network. The
administrator is responsible for creating a bond for the public network
if that network will be bonded and will be separate from the management
network.


Creating a Public Bond on the First Host in the Cluster
'''''''''''''''''''''''''''''''''''''''''''''''''''''''

These steps should be run on only the first host in a cluster. This
example creates the cloud-public network with two physical NICs (eth2
and eth3) bonded into it.

#. Find the physical NICs that you want to bond together.

   .. parsed-literal::

      # xe pif-list host-name-label='hostname' device=eth2
      # xe pif-list host-name-label='hostname' device=eth3

   These command shows the eth2 and eth3 NICs and their UUIDs.
   Substitute the ethX devices of your choice. Call the UUID's returned
   by the above command slave1-UUID and slave2-UUID.

#. Create a new network for the bond. For example, a new network with
   name "cloud-public".

   **This label is important. CloudStack looks for a network by a name
   you configure. You must use the same name-label for all hosts in the
   cloud for the public network.**

   .. parsed-literal::

      # xe network-create name-label=cloud-public
      # xe bond-create network-uuid=[uuid of cloud-public created above]
      pif-uuids=[slave1-uuid],[slave2-uuid]

Now you have a bonded pair that can be recognized by CloudStack as the
public network.


Adding More Hosts to the Cluster
''''''''''''''''''''''''''''''''

With the bonds (if any) established on the master, you should add
additional, slave hosts. Run the following command for all additional
hosts to be added to the cluster. This will cause the host to join the
master in a single XenServer pool.

.. parsed-literal::

   # xe pool-join master-address=[master IP] master-username=root
   master-password=[your password]


Complete the Bonding Setup Across the Cluster
'''''''''''''''''''''''''''''''''''''''''''''

With all hosts added to the pool, run the cloud-setup-bond script. This
script will complete the configuration and set up of the bonds across
all hosts in the cluster.

#. Copy the script from the Management Server in
   /usr/share/cloudstack-common/scripts/vm/hypervisor/xenserver/cloud-setup-bonding.sh
   to the master host and ensure it is executable.

#. Run the script:

   .. parsed-literal::

      # ./cloud-setup-bonding.sh

Now the bonds are set up and configured properly across the cluster.


.. _upgrading-xenserver-version:

Upgrading XenServer Versions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section tells how to upgrade XenServer software on CloudStack
hosts. The actual upgrade is described in XenServer documentation, but
there are some additional steps you must perform before and after the
upgrade.

.. note:: 
   Be sure the hardware is certified compatible with the new version of
   XenServer.

To upgrade XenServer:

#. Upgrade the database. On the Management Server node:

   #. Back up the database:

      .. parsed-literal::

          # mysqldump --user=root --databases cloud > cloud.backup.sql
          # mysqldump --user=root --databases cloud_usage > cloud_usage.backup.sql

   #. You might need to change the OS type settings for VMs running on
      the upgraded hosts.

      -  If you upgraded from XenServer 5.6 GA to XenServer 5.6 SP2,
         change any VMs that have the OS type CentOS 5.5 (32-bit),
         Oracle Enterprise Linux 5.5 (32-bit), or Red Hat Enterprise
         Linux 5.5 (32-bit) to Other Linux (32-bit). Change any VMs that
         have the 64-bit versions of these same OS types to Other Linux
         (64-bit).

      -  If you upgraded from XenServer 5.6 SP2 to XenServer 6.0.2,
         change any VMs that have the OS type CentOS 5.6 (32-bit),
         CentOS 5.7 (32-bit), Oracle Enterprise Linux 5.6 (32-bit),
         Oracle Enterprise Linux 5.7 (32-bit), Red Hat Enterprise Linux
         5.6 (32-bit) , or Red Hat Enterprise Linux 5.7 (32-bit) to
         Other Linux (32-bit). Change any VMs that have the 64-bit
         versions of these same OS types to Other Linux (64-bit).

      -  If you upgraded from XenServer 5.6 to XenServer 6.0.2, do all
         of the above.

   #. Restart the Management Server and Usage Server. You only need to
      do this once for all clusters.

      .. parsed-literal::

         # service cloudstack-management start
         # service cloudstack-usage start

#. Disconnect the XenServer cluster from CloudStack.

   #. Log in to the CloudStack UI as root.

   #. Navigate to the XenServer cluster, and click Actions – Unmanage.

   #. Watch the cluster status until it shows Unmanaged.

#. Log in to one of the hosts in the cluster, and run this command to
   clean up the VLAN:

   .. parsed-literal::

      # . /opt/xensource/bin/cloud-clean-vlan.sh

#. Still logged in to the host, run the upgrade preparation script:

   .. parsed-literal::

      # /opt/xensource/bin/cloud-prepare-upgrade.sh

   Troubleshooting: If you see the error "can't eject CD," log in to the
   VM and umount the CD, then run the script again.

#. Upgrade the XenServer software on all hosts in the cluster. Upgrade
   the master first.

   #. Live migrate all VMs on this host to other hosts. See the
      instructions for live migration in the Administrator's Guide.

      Troubleshooting: You might see the following error when you
      migrate a VM:

      .. parsed-literal::

         [root@xenserver-qa-2-49-4 ~]# xe vm-migrate live=true host=xenserver-qa-2-49-5 vm=i-2-8-VM
         You attempted an operation on a VM which requires PV drivers to be installed but the drivers were not detected.
         vm: b6cf79c8-02ee-050b-922f-49583d9f1a14 (i-2-8-VM)

      To solve this issue, run the following:

      .. parsed-literal::

         # /opt/xensource/bin/make_migratable.sh  b6cf79c8-02ee-050b-922f-49583d9f1a14

   #. Reboot the host.

   #. Upgrade to the newer version of XenServer. Use the steps in
      XenServer documentation.

   #. After the upgrade is complete, copy the following files from the
      management server to this host, in the directory locations shown
      below:

      .. cssclass:: table-striped table-bordered table-hover
      
      =================================================================================   =======================================
      Copy this Management Server file                                                    To this location on the XenServer host
      =================================================================================   =======================================
      /usr/share/cloudstack-common/scripts/vm/hypervisor/xenserver/xenserver60/NFSSR.py   /opt/xensource/sm/NFSSR.py
      /usr/share/cloudstack-common/scripts/vm/hypervisor/xenserver/setupxenserver.sh      /opt/xensource/bin/setupxenserver.sh
      /usr/share/cloudstack-common/scripts/vm/hypervisor/xenserver/make\_migratable.sh    /opt/xensource/bin/make\_migratable.sh
      /usr/share/cloudstack-common/scripts/vm/hypervisor/xenserver/cloud-clean-vlan.sh    /opt/xensource/bin/cloud-clean-vlan.sh
      =================================================================================   =======================================

   #. Run the following script:

      .. parsed-literal::

         # /opt/xensource/bin/setupxenserver.sh

      Troubleshooting: If you see the following error message, you can
      safely ignore it.

      .. parsed-literal::

         mv: cannot stat `/etc/cron.daily/logrotate`: No such file or directory

   #. Plug in the storage repositories (physical block devices) to the
      XenServer host:

      .. parsed-literal::

         # for pbd in `xe pbd-list currently-attached=false| grep ^uuid | awk '{print $NF}'`; do xe pbd-plug uuid=$pbd ; done

      .. note:: 
         If you add a host to this XenServer pool, you need to migrate all VMs 
         on this host to other hosts, and eject this host from XenServer pool.

#. Repeat these steps to upgrade every host in the cluster to the same
   version of XenServer.

#. Run the following command on one host in the XenServer cluster to
   clean up the host tags:

   .. parsed-literal::

      # for host in $(xe host-list | grep ^uuid | awk '{print $NF}') ; do xe host-param-clear uuid=$host param-name=tags; done;

   .. note:: 
      When copying and pasting a command, be sure the command has pasted as
      a single line before executing. Some document viewers may introduce
      unwanted line breaks in copied text.

#. Reconnect the XenServer cluster to CloudStack.

   #. Log in to the CloudStack UI as root.

   #. Navigate to the XenServer cluster, and click Actions – Manage.

   #. Watch the status to see that all the hosts come up.

#. After all hosts are up, run the following on one host in the cluster:

   .. parsed-literal::

      # /opt/xensource/bin/cloud-clean-vlan.sh
