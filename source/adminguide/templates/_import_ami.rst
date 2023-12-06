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


Importing Amazon Machine Images
-------------------------------

The following procedures describe how to import an Amazon Machine Image
(AMI) into CloudStack when using the XenServer hypervisor.

Assume you have an AMI file and this file is called CentOS\_6.2\_x64.
Assume further that you are working on a CentOS host. If the AMI is a
Fedora image, you need to be working on a Fedora host initially.

You need to have a XenServer host with a file-based storage repository
(either a local ext3 SR or an NFS SR) to convert to a VHD once the image
file has been customized on the Centos/Fedora host.

.. note:: 
   When copying and pasting a command, be sure the command has pasted as 
   a single line before executing. Some document viewers may introduce 
   unwanted line breaks in copied text.

To import an AMI:

#. Set up loopback on image file:

   .. code:: bash

      # mkdir -p /mnt/loop/centos62
      # mount -o loop  CentOS_6.2_x64 /mnt/loop/centos54

#. Install the kernel-xen package into the image. This downloads the PV
   kernel and ramdisk to the image.

   .. code:: bash

      # yum -c /mnt/loop/centos54/etc/yum.conf --installroot=/mnt/loop/centos62/ -y install kernel-xen

#. Create a grub entry in /boot/grub/grub.conf.

   .. code:: bash

      # mkdir -p /mnt/loop/centos62/boot/grub
      # touch /mnt/loop/centos62/boot/grub/grub.conf
      # echo "" > /mnt/loop/centos62/boot/grub/grub.conf

#. Determine the name of the PV kernel that has been installed into the
   image.

   .. code:: bash

      # cd /mnt/loop/centos62
      # ls lib/modules/
      2.6.16.33-xenU  2.6.16-xenU  2.6.18-164.15.1.el5xen  2.6.18-164.6.1.el5.centos.plus  2.6.18-xenU-ec2-v1.0  2.6.21.7-2.fc8xen  2.6.31-302-ec2
      # ls boot/initrd*
      boot/initrd-2.6.18-164.6.1.el5.centos.plus.img boot/initrd-2.6.18-164.15.1.el5xen.img
      # ls boot/vmlinuz*
      boot/vmlinuz-2.6.18-164.15.1.el5xen  boot/vmlinuz-2.6.18-164.6.1.el5.centos.plus  boot/vmlinuz-2.6.18-xenU-ec2-v1.0  boot/vmlinuz-2.6.21-2952.fc8xen

   Xen kernels/ramdisk always end with "xen". For the kernel version you
   choose, there has to be an entry for that version under lib/modules,
   there has to be an initrd and vmlinuz corresponding to that. Above,
   the only kernel that satisfies this condition is
   2.6.18-164.15.1.el5xen.

#. Based on your findings, create an entry in the grub.conf file. Below
   is an example entry.

   .. code:: bash

      default=0
      timeout=5
      hiddenmenu
      title CentOS (2.6.18-164.15.1.el5xen)
         root (hd0,0)
         kernel /boot/vmlinuz-2.6.18-164.15.1.el5xen ro root=/dev/xvda 
         initrd /boot/initrd-2.6.18-164.15.1.el5xen.img

#. Edit etc/fstab, changing “sda1” to “xvda” and changing “sdb” to
   “xvdb”.

   .. code:: bash

      # cat etc/fstab
      /dev/xvda  /         ext3    defaults        1 1
      /dev/xvdb  /mnt      ext3    defaults        0 0
      none       /dev/pts  devpts  gid=5,mode=620  0 0
      none       /proc     proc    defaults        0 0
      none       /sys      sysfs   defaults        0 0

#. Enable login via the console. The default console device in a
   XenServer system is xvc0. Ensure that etc/inittab and etc/securetty
   have the following lines respectively:

   .. code:: bash

      # grep xvc0 etc/inittab 
      co:2345:respawn:/sbin/agetty xvc0 9600 vt100-nav
      # grep xvc0 etc/securetty 
      xvc0

#. Ensure the ramdisk supports PV disk and PV network. Customize this
   for the kernel version you have determined above.

   .. code:: bash

      # chroot /mnt/loop/centos54
      # cd /boot/
      # mv initrd-2.6.18-164.15.1.el5xen.img initrd-2.6.18-164.15.1.el5xen.img.bak
      # mkinitrd -f /boot/initrd-2.6.18-164.15.1.el5xen.img --with=xennet --preload=xenblk --omit-scsi-modules 2.6.18-164.15.1.el5xen

#. Change the password.

   .. code:: bash

      # passwd
      Changing password for user root.
      New UNIX password: 
      Retype new UNIX password: 
      passwd: all authentication tokens updated successfully.

#. Exit out of chroot.

   .. code:: bash

      # exit

#. Check `etc/ssh/sshd_config` for lines allowing ssh login using a
   password.

   .. code:: bash

      # egrep "PermitRootLogin|PasswordAuthentication" /mnt/loop/centos54/etc/ssh/sshd_config  
      PermitRootLogin yes
      PasswordAuthentication yes

#. If you need the Template to be enabled to reset passwords from the
   CloudStack UI or API, install the password change script into the
   image at this point. See :ref:`adding-password-management-to-templates`.

#. Unmount and delete loopback mount.

   .. code:: bash

      # umount /mnt/loop/centos54
      # losetup -d /dev/loop0

#. Copy the image file to your XenServer host's file-based storage
   repository. In the example below, the Xenserver is "xenhost". This
   XenServer has an NFS repository whose uuid is
   a9c5b8c8-536b-a193-a6dc-51af3e5ff799.

   .. code:: bash

      # scp CentOS_6.2_x64 xenhost:/var/run/sr-mount/a9c5b8c8-536b-a193-a6dc-51af3e5ff799/

#. Log in to the Xenserver and create a VDI the same size as the image.

   .. code:: bash

      [root@xenhost ~]# cd /var/run/sr-mount/a9c5b8c8-536b-a193-a6dc-51af3e5ff799
      [root@xenhost a9c5b8c8-536b-a193-a6dc-51af3e5ff799]#  ls -lh CentOS_6.2_x64
      -rw-r--r-- 1 root root 10G Mar 16 16:49 CentOS_6.2_x64
      [root@xenhost a9c5b8c8-536b-a193-a6dc-51af3e5ff799]# xe vdi-create virtual-size=10GiB sr-uuid=a9c5b8c8-536b-a193-a6dc-51af3e5ff799 type=user name-label="Centos 6.2 x86_64"
      cad7317c-258b-4ef7-b207-cdf0283a7923

#. Import the image file into the VDI. This may take 10–20 minutes.

   .. code:: bash

      [root@xenhost a9c5b8c8-536b-a193-a6dc-51af3e5ff799]# xe vdi-import filename=CentOS_6.2_x64 uuid=cad7317c-258b-4ef7-b207-cdf0283a7923

#. Locate a the VHD file. This is the file with the VDI’s UUID as its
   name. Compress it and upload it to your web server.

   .. code:: bash

      [root@xenhost a9c5b8c8-536b-a193-a6dc-51af3e5ff799]# bzip2 -c cad7317c-258b-4ef7-b207-cdf0283a7923.vhd > CentOS_6.2_x64.vhd.bz2
      [root@xenhost a9c5b8c8-536b-a193-a6dc-51af3e5ff799]# scp CentOS_6.2_x64.vhd.bz2 webserver:/var/www/html/templates/
