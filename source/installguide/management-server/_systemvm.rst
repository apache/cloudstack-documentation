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

Prepare the System VM Template
------------------------------

From Apache CloudStack v4.16 onwards, upgrade path handles SystemVM Template registration, if not done prior to initiating upgrade.
One may choose, to also omit the SystemVM Template seeding step during fresh installation of CloudStack, as support has been added to
initiate SystemVM Template registration for all hypervisors present in the zone when the first secondary storage pool is added.
Secondary storage must be seeded with a Template that is used for CloudStack System VMs.

.. note::
   When copying and pasting a command, be sure the command has pasted as a 
   single line before executing. Some document viewers may introduce unwanted 
   line breaks in copied text.

#. On the Management Server, run one or more of the following
   ``cloud-install-sys-tmplt`` commands to retrieve and decompress the
   System VM Template. Run the command for each hypervisor type that you
   expect end Users to run in this Zone.

   If your secondary storage mount point is not named ``/mnt/secondary``,
   substitute your own mount point name.

   If you set the CloudStack database encryption type to "web" when you
   set up the database, you must now add the parameter ``-s
   <management-server-secret-key>``. See :ref:`about-password-key-encryption`.

   This process will require approximately 5 GB of free space on the
   local file system and up to 30 minutes each time it runs.

   *  For Hyper-V

      .. parsed-literal::

         /usr/share/cloudstack-common/scripts/storage/secondary/cloud-install-sys-tmplt \
         -m /mnt/secondary \
         -u |sysvm64-url-hyperv| \
         -h hyperv \
         -s <optional-management-server-secret-key> \
         -F

   *  For XenServer:

      .. parsed-literal::

         /usr/share/cloudstack-common/scripts/storage/secondary/cloud-install-sys-tmplt \
         -m /mnt/secondary \
         -u |sysvm64-url-xen| \
         -h xenserver \
         -s <optional-management-server-secret-key> \
         -F

   *  For vSphere:

      .. parsed-literal::

         /usr/share/cloudstack-common/scripts/storage/secondary/cloud-install-sys-tmplt \
         -m /mnt/secondary \
         -u |sysvm64-url-vmware| \
         -h vmware \
         -s <optional-management-server-secret-key> \
         -F

   *  For KVM:

      .. parsed-literal::

         /usr/share/cloudstack-common/scripts/storage/secondary/cloud-install-sys-tmplt \
         -m /mnt/secondary \
         -u |sysvm64-url-kvm| \
         -h kvm \
         -s <optional-management-server-secret-key> \
         -F

   *  For LXC:

      .. parsed-literal::

         /usr/share/cloudstack-common/scripts/storage/secondary/cloud-install-sys-tmplt \
         -m /mnt/secondary \
         -u |sysvm64-url-kvm| \
         -h lxc \
         -s <optional-management-server-secret-key> \
         -F

   *  For OVM3:

      .. parsed-literal::

         /usr/share/cloudstack-common/scripts/storage/secondary/cloud-install-sys-tmplt \
         -m /mnt/secondary \
         -u |sysvm64-url-ovm| \
         -h ovm3 \
         -s <optional-management-server-secret-key> \
         -F

#. If you are using a separate NFS server, perform this step. If you are
   using the Management Server as the NFS server, you MUST NOT perform
   this step.

   When the script has finished, unmount secondary storage and remove
   the created directory.

   .. parsed-literal::

      umount /mnt/secondary
      rmdir /mnt/secondary

#. Repeat these steps for each secondary storage server.
