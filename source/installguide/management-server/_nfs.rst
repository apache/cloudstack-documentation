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

.. _prepare-nfs-shares:

Prepare NFS Shares
------------------

CloudStack needs a place to keep primary and secondary storage (see
Cloud Infrastructure Overview). Both of these can be NFS shares. This
section tells how to set up the NFS shares before adding the storage to
CloudStack.

.. note::
   NFS is not the only option for primary or secondary storage. For example,
   you may use Ceph RBD, PowerFlex, GlusterFS, iSCSI, Fiberchannel and others. The choice of storage
   system will depend on the choice of hypervisor and whether you are dealing
   with primary or secondary storage.

The requirements for primary and secondary storage are described in:

-  :ref:`about-primary-storage`

-  :ref:`about-secondary-storage`

A production installation typically uses a separate NFS server.
See :ref:`using-a-separage-nfs-server`.

You can also use the Management Server node as the NFS server. This is
more typical of a trial installation, but is technically possible in a
larger deployment. See :ref:`using-the-management-server-as-the-nfs-server`.


.. _using-a-separage-nfs-server:

Using a Separate NFS Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section tells how to set up NFS shares for secondary and
(optionally) primary storage on an NFS server running on a separate node
from the Management Server.

The exact commands for the following steps may vary depending on your
operating system version.
The following steps asume you already have an NFS Server installed on your storage
system. Please refer to the guide of your OS on how to install a NFS Server.

.. warning::
   (KVM only) Ensure that no volume is already mounted at your NFS mount point.

#. On the storage server, create an NFS share for secondary storage and,
   if you are using NFS for primary storage as well, create a second NFS
   share. For example:

   .. parsed-literal::

      mkdir -p /export/primary
      mkdir -p /export/secondary

#. To configure the new directories as NFS exports, edit /etc/exports.
   Export the NFS share(s) with
   rw,async,no\_root\_squash,no\_subtree\_check. For example:

   .. parsed-literal::

      vi /etc/exports

   Insert the following line.

   .. parsed-literal::

      /export  \*(rw,async,no_root_squash,no_subtree_check)

#. Export the /export directory.

   .. parsed-literal::

      exportfs -a

#. On the management server, create a mount point for secondary storage.
   For example:

   .. parsed-literal::

      mkdir -p /mnt/secondary

#. Mount the secondary storage on your Management Server. Replace the
   example NFS server name and NFS share paths below with your own.

   .. parsed-literal::

      mount -t nfs nfsservername:/export/secondary /mnt/secondary


.. _using-the-management-server-as-the-nfs-server:

Using the Management Server as the NFS Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section tells how to set up NFS shares for primary and secondary
storage on the same node with the Management Server. This is more
typical of a trial installation, but is technically possible in a larger
deployment. It is assumed that you will have less than 16TB of storage
on the host.

The exact commands for the following steps may vary depending on your
operating system version.

#. On RHEL/CentOS/SUSE systems, you'll need to install the nfs-utils package:

   .. parsed-literal::

      yum install nfs-utils

   .. parsed-literal::

      zypper install nfs-utils

   or for Ubuntu

   .. parsed-literal::

      apt install nfs-kernel-server

#. On the Management Server host, create two directories that you will
   use for primary and secondary storage. For example:

   .. parsed-literal::

      mkdir -p /export/primary
      mkdir -p /export/secondary

#. To configure the new directories as NFS exports, edit /etc/exports.
   Export the NFS share(s) with
   rw,async,no\_root\_squash,no\_subtree\_check. For example:

   .. parsed-literal::

      vi /etc/exports

   Insert the following line.

   .. parsed-literal::

      /export  \*(rw,async,no_root_squash,no_subtree_check)

#. Export the /export directory.

   .. parsed-literal::

      exportfs -a

#. Edit the /etc/sysconfig/nfs file.

   .. parsed-literal::

      vi /etc/sysconfig/nfs

   Uncomment the following lines:

   .. parsed-literal::

      LOCKD_TCPPORT=32803
      LOCKD_UDPPORT=32769
      MOUNTD_PORT=892
      RQUOTAD_PORT=875
      STATD_PORT=662
      STATD_OUTGOING_PORT=2020

#. Edit the /etc/sysconfig/iptables file.

   .. parsed-literal::

      vi /etc/sysconfig/iptables

   Add the following lines at the beginning of the INPUT chain, where
   <NETWORK> is the Network that you'll be using:

   .. parsed-literal::

      -A INPUT -s <NETWORK> -m state --state NEW -p udp --dport 111 -j ACCEPT
      -A INPUT -s <NETWORK> -m state --state NEW -p tcp --dport 111 -j ACCEPT
      -A INPUT -s <NETWORK> -m state --state NEW -p tcp --dport 2049 -j ACCEPT
      -A INPUT -s <NETWORK> -m state --state NEW -p tcp --dport 32803 -j ACCEPT
      -A INPUT -s <NETWORK> -m state --state NEW -p udp --dport 32769 -j ACCEPT
      -A INPUT -s <NETWORK> -m state --state NEW -p tcp --dport 892 -j ACCEPT
      -A INPUT -s <NETWORK> -m state --state NEW -p udp --dport 892 -j ACCEPT
      -A INPUT -s <NETWORK> -m state --state NEW -p tcp --dport 875 -j ACCEPT
      -A INPUT -s <NETWORK> -m state --state NEW -p udp --dport 875 -j ACCEPT
      -A INPUT -s <NETWORK> -m state --state NEW -p tcp --dport 662 -j ACCEPT
      -A INPUT -s <NETWORK> -m state --state NEW -p udp --dport 662 -j ACCEPT

#. Run the following commands:

   .. parsed-literal::

      service iptables restart
      service iptables save

#. If NFS v4 communication is used between client and server, add your
   domain to /etc/idmapd.conf on both the hypervisor host and Management
   Server.

   .. parsed-literal::

      vi /etc/idmapd.conf

   Remove the character # from the beginning of the Domain line in
   idmapd.conf and replace the value in the file with your own domain.
   In the example below, the domain is company.com.

   .. parsed-literal::

      Domain = company.com

#. Reboot the Management Server host.

   Two NFS shares called /export/primary and /export/secondary are now
   set up.

#. It is recommended that you test to be sure the previous steps have
   been successful.

   #. Log in to the hypervisor host.

   #. Be sure NFS and rpcbind are running. The commands might be
      different depending on your OS. For example:

      .. parsed-literal::

         service rpcbind start
         service nfs start
         chkconfig nfs on
         chkconfig rpcbind on
         reboot

   #. Log back in to the hypervisor host and try to mount the /export
      directories. For example, substitute your own management server
      name:

      .. parsed-literal::

         mkdir /primary
         mount -t nfs <management-server-name>:/export/primary
         umount /primary
         mkdir /secondary
         mount -t nfs <management-server-name>:/export/secondary
         umount /secondary
