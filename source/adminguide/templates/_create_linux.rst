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


Creating a Linux Template
-------------------------

Linux templates should be prepared using this documentation in order to
prepare your linux VMs for template deployment. For ease of
documentation, the VM which you are configuring the template on will be
referred to as "Main Template". The final product, as created and usable
for deplyoment in Cloudstack, will be referred as "Final Template".
This guide will cover cloud-init setup.  It is assumed that openssh-server
is installed during installation.

An overview of the procedure is as follow:

#. Upload your Linux ISO.

   For more information, see `“Adding an
   ISO” <virtual_machines.html#adding-an-iso>`_.

#. Create a VM Instance with this ISO.

   For more information, see `“Creating
   VMs” <virtual_machines.html#creating-vms>`_.

#. Prepare the Linux VM

#. Create a template from the VM.

   For more information, see `“Creating a Template from an Existing 
   Virtual Machine” <#creating-a-template-from-an-existing-virtual-machine>`_.


System preparation for Linux
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following steps will provide basic Linux installation for
templating of Centos and Ubuntu.

#. **Install packages and configure cloud-init**

   The next step update the packages on the Main Template and install cloud-init.
   
   ~  CentOS
   
    .. code:: bash

	 yum update -y
	 yum install -y cloud-init 
	 reboot
   
   ~  Ubuntu
   
    .. code:: bash

     sudo -i
     apt-get update
     apt-get upgrade -y
     apt-get install -y acpid ntp cloud-init
     reboot
	  
	Configure cloud-init to run on-boot.
	
   ~  CentOS
   
    .. code:: bash

     echo "datasource: CloudStack" > /etc/cloud/ds-identify.cfg 
   
    ~  Ubuntu
   
    .. code:: bash

     echo "datasource_list: [ ConfigDrive, CloudStack, None ]
     datasource:
       CloudStack: {}
       None: {}" > /etc/cloud/cloud.cfg.d/99_cloudstack.cfg

#. **Networking**

   Set template network interface configuration to DHCP so Cloudstack infrastructure can assign one on boot.
	
   .. warning:: 
      For CentOS, it is mandatory to take unique identification out of the
      interface configuration file /etc/sysconfig/network-scripts/ifcfg-eth0. Any entries starting with <VALUE> should be removed.

   .. code:: bash

      echo "DEVICE=eth0
      TYPE=Ethernet
      BOOTPROTO=dhcp
      ONBOOT=yes" > /etc/sysconfig/network-scripts/ifcfg-eth0

#. **Hostname Management**

   It is good practice to name the template VM something generic during installation, this will ensure components such as LVM do not appear unique to a machine. It is recommended that the name of "localhost" is used for installation.

   .. code:: bash

	   hostname localhost
	   echo "localhost" > /etc/hostname
	
   CentOS configures the hostname by default on boot. Ubuntu does not but cloud-init will do it automatically with no additional cofiguration required.

#. **Password management**

   Cloudstack `set-passwords module <https://cloudinit.readthedocs.io/en/latest/topics/modules.html?highlight=ssh_pwauth#set-passwords>`_ can set a password for each instance created from the Main Template and also allow the user the reset the user password through the GUI. This feature is enabled through communication between the new instance and Cloudstack infrastructure via the cloud-init middleware. 
   
   - **Enable set-passwords module on every boot**
   
     By default the set-passwords module runs only on first boot, change that to run on every boot.
   
     .. code:: bash
   
      sudo sed -i s/"set-passwords"/"[set-passwords, always]"/g /etc/cloud/cloud.cfg
	
     .. note:: 
	 
	  It is a good practice to remove any non root users that come with the OS (such as ones created during the Ubuntu 
	  installation). First ensure the root user account is enabled by giving it a password and then login as root to continue.

     Once logged in as root, any custom user can be removed.

     .. code:: bash

	  deluser myuser --remove-home
	
   - **Specify the managed user**
   
     Cloudstack will create the user, set a password and reset it when requested. To do that set the following configuration in /etc/cloud/cloud.cfg.d/80_user.cfg
		
     .. code:: bash

	  echo "system_info\:
	    default_user\:
	      name: cloud-user	              # this is the username
		  lock_passwd: false	          # If set to True it will disable password login for this particular user
		  sudo: [\"ALL=(ALL) ALL\"] 	  # Define user permissions
	    disable_root: 0	                  # Should OS root user be unavailable (0) or available (1) for remote login
	    ssh_pwauth: 1	                  # 1 - enables password login functionality; 0 - disables" > /etc/cloud/cloud.cfg.d/80_user.cfg

#. **Partition management**
	
   Cloud-init allows detection and resize of one or more existing partitions automatically after reboot. This guide will cover root partition.
   First install the `Growpart module <https://cloudinit.readthedocs.io/en/latest/topics/modules.html#growpart>`_ as it is not shipped with cloud-init.
   
    ~ Centos 
	
     .. code:: bash
	  
      yum -y install cloud-init cloud-utils-growpart
	
    ~ Ubuntu 
	
     .. code:: bash
	  
      apt-get install cloud-initramfs-growroot -y
	  
   - **Detect and extend MBR partitions**
      
     Configure growpart module by runnning the following code.
	 
    ~ CentOS
	 
     .. note::
	 
	  /dev/xvda2 is the default root partition if no changes are done during 
	  CentOS 7 installation. Change the value accordingly if setup is different.
	  
     .. code:: bash
	
      echo "growpart:
      mode: auto
      devices:
        - \"/dev/xvda2\"
      ignore_growroot_disabled: false" > /etc/cloud/cloud.cfg.d/50_growpartion.cfg

    ~ Ubuntu
	 
     .. note::
	 
	  /dev/xvda3 is the default root partition if no changes are done during 
	  Ubuntu 20 installation. Change the value accordingly if setup is different.
	   
     .. code:: bash
	  
      echo "growpart:
      mode: auto
      devices:
       - \"/dev/xvda3\"
      ignore_growroot_disabled: false" > /etc/cloud/cloud.cfg.d/50_growpartion.cfg
	   
   - **Extend Physical volume, Volume group and root lvm**
   
     After parition is extended the upper layers should be resized as well. This can be achived by automating the CLI commands with cloud-init `bootcmd module <https://cloudinit.readthedocs.io/en/latest/topics/modules.html?highlight=bootcmd#bootcmd>`_ .
	
     .. warning::
      Cloud-init `runcmd module <https://cloudinit.readthedocs.io/en/latest/topics/modules.html?highlight=runcmd#runcmd>`_ frequency
      syntax does not work as intended. Even if command is entered as *"[ cloud-init-per, always, command ]"* it will still run on first boot only.
      This is the reason in bootcmd is used in this guide to make sure partition check and resize operations are done on every boot.
	 
     ~ CentOS
	 
      .. note::
	 
	   /dev/centos/root is the default root volume if no changes are done during 
	   Centos 7 installation. Change the value accordingly if setup is different.
	   
      .. code:: bash
	  
       echo "bootcmd:
        - [ cloud-init-per, always, grow_VG, pvresize, /dev/xvda2 ]
        - [ cloud-init-per, always, grow_LV, lvresize, -l, '+100%FREE', /dev/centos/root ]
        - [ cloud-init-per, always, grow_FS, xfs_growfs, /dev/centos/root ]" > /etc/cloud/cloud.cfg.d/51_extend_volume.cfg 
	  
     ~ Ubuntu
	 
      .. note::
	 
	   /dev/ubuntu-vg/ubuntu-lv is the default root volume if no changes are done during 
	   Ubuntu 20 installation. Change the value accordingly if setup is different.
	   
      .. code:: bash
	  
       echo "bootcmd:
        - [ cloud-init-per, always, grow_VG, pvresize, /dev/xvda3 ]
        - [ cloud-init-per, always, grow_LV, lvresize, -l, '+100%FREE', /dev/ubuntu-vg/ubuntu-lv ]
        - [ cloud-init-per, always, grow_FS, xfs_growfs, /dev/ubuntu-vg/ubuntu-lv ]" > /etc/cloud/cloud.cfg.d/51_extend_volume.cfg
	   
#. **Template cleanup**
    
   .. warning:: 
	  Cleanup steps should be run when all Main Template configuration
	  is done and just before the shutdown step. After shut down Final
	  template should be created. If the Main Template is started or 
	  rebooted before Final template creation all cleanup steps will
	  have to be rerun.

   - **Remove the udev persistent device rules**
   
     This step removes information unique to the Main Template such as
     network MAC addresses, lease files and CD block devices, the files
     are automatically generated on next boot.
   
     ~  CentOS

      .. code:: bash

       rm -f /etc/udev/rules.d/70*
       rm -f /var/lib/dhclient/*
	
     ~  Ubuntu

      .. code:: bash

       rm -f /etc/udev/rules.d/70*
       rm -f /var/lib/dhcp/dhclient.*

   - **Remove SSH Keys**

     This step is to ensure all Templated VMs do not have the same
     SSH keys, which would decrease the security of the machines
     dramatically.

     .. code:: bash

      rm -f /etc/ssh/*key*

   - **Cleaning log files**

     It is good practice to remove old logs from the Main Template.

     .. code:: bash

      cat /dev/null > /var/log/audit/audit.log 2>/dev/null
      cat /dev/null > /var/log/wtmp 2>/dev/null
      logrotate -f /etc/logrotate.conf 2>/dev/null
      rm -f /var/log/*-* /var/log/*.gz 2>/dev/null

   - **Set user password to expire**

     This step forces the user to change the password of the VM after the
     template has been deployed.

     .. code:: bash

      passwd --expire root

   - **Clearing User History**

     The next step clears the bash commands you have just run.

    .. code:: bash

      history -c
      unset HISTFILE

#. **Shutdown the VM**

   Shutdown the Main Template.

   .. code:: bash

      halt -p

#. **Create the template!**

   You are now ready to create the Final Template, for more information see
   `“Creating a Template from an Existing Virtual
   Machine” <#creating-a-template-from-an-existing-virtual-machine>`_.
