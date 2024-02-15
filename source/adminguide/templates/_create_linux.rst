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

Linux Templates should be prepared using this documentation in order to
prepare your linux Instances for Template deployment. For ease of
documentation, the Instance which you are configuring the Template on will be
referred to as "Main Template". The final product, as created and usable
for deployment in Cloudstack, will be referred as "Final Template".
This guide will cover cloud-init setup and scripted setups where available.  It is assumed that openssh-server
is installed during installation.

An overview of the procedure is as follow:

#. Upload your Linux ISO.

   For more information, see `“Adding an
   ISO” <templates.html#adding-an-iso>`_.

#. Create an Instance with this ISO.

   For more information, see `“Creating
   Instances” <virtual_machines.html#creating-instances>`_.

#. Prepare the Linux Instance

#. Create a Template from the Instance.

   For more information, see `“Creating a Template from an Existing 
   Instance” <#creating-a-template-from-an-existing-instance>`_.


System preparation for Linux
----------------------------

The following steps will provide basic Linux installation for
templating of Centos and Ubuntu.
	 
#. **Update OS**

   The next step update the packages on the Main Template.
   
   ~  CentOS
   
    .. code:: bash

	 yum update -y
	 reboot
   
   ~  Ubuntu
   
    .. code:: bash

     sudo -i
     apt-get update
     apt-get upgrade -y
     apt-get install -y acpid ntp
     reboot
   
#. **Networking**

   Set Template Network interface configuration to DHCP so Cloudstack infrastructure can assign one on boot.
	
   .. warning::
   
     For CentOS, it is mandatory to take unique identification out of the
     interface configuration file /etc/sysconfig/network-scripts/ifcfg-eth0. Any entries starting with <VALUE> should be removed.
	
   ~ Centos
	
    .. code:: bash

     echo "DEVICE=eth0
     TYPE=Ethernet
     BOOTPROTO=dhcp
     ONBOOT=yes" > /etc/sysconfig/network-scripts/ifcfg-eth0

#. **Hostname Management**

   Set a generic name to the Template Instance during installation, this will ensure components such as LVM do not appear unique to a machine. It is recommended that the name of "localhost" is used for installation.

   .. code:: bash

	  hostname localhost
	  echo "localhost" > /etc/hostname

#. **Password management**
   
   .. note:: 
	 
    It is a good practice to remove any non root Users that come with the OS (such as ones created during the Ubuntu
    installation). First ensure the root user Account is enabled by giving it a password and then login as root to continue.

   Once logged in as root, any custom User can be removed.

   .. code:: bash

     deluser myuser --remove-home
	 
   User password management and reset cappabilities in GUI are available with:
   
   *  `Cloud-init integration <templates/_cloud_init.html#linux-with-cloud-init>`_
   *  `Adding Password Management to Your Templates <templates.html#adding-password-management-to-templates>`_ /Legacy for non systemd systems only/
	 
#. **SSH keys management**

   Cloudstack can create key pair and push certificates to Instances. This feature is available with:
   
   *  `Cloud-init integration <templates/_cloud_init.html#linux-with-cloud-init>`_
   *  `Implementing a SSH-Key bash script <http://docs.cloudstack.apache.org/en/latest/adminguide/virtual_machines.html#creating-an-instance-template-that-supports-ssh-keys>`_   
	 
#. **Partition management**
	
   Volumes can autorextend after reboot when partition is extended in the GUI.
   This feature is possible with `Cloud-init integration <templates/_cloud_init.html#linux-with-cloud-init>`_.
   
#. **User-data**
	
   Cloudstack can push user-data during Instance creation.
   This feature is possible with `Cloud-init integration <templates/_cloud_init.html#linux-with-cloud-init>`_.
	
#. **Template cleanup**
    
   .. warning:: 
   
    Cleanup steps should be run when all Main Template configuration
    is done and just before the shutdown step. After shut down Final
    Template should be created. If the Main Template is started or
    rebooted before Final Template creation all cleanup steps have to be rerun.

   - **Remove the udev persistent device rules**
   
     This step removes information unique to the Main Template such as
     Network MAC addresses, lease files and CD block devices, the files
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

     This step is to ensure all Templated Instances do not have the same
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

   - **Set User password to expire**

     This step forces the User to change the password of the Instance after the
     Template has been deployed.

     .. code:: bash

      passwd --expire root

   - **Clearing User History**

     The next step clears the bash commands you have just run.

    .. code:: bash

      history -c
      unset HISTFILE

#. **Shutdown the Instance**

   Shutdown the Main Template.

   .. code:: bash

      halt -p

#. **Create the Template!**

   You are now ready to create the Final Template, for more information see
   `“Creating a Template from an Existing Virtual
   Machine” <#creating-a-template-from-an-existing-instance>`_.
