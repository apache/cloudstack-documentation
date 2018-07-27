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
referred to as "Template Master". This guide currently covers legacy
setups which do not take advantage of UserData and cloud-init and
assumes openssh-server is installed during installation.

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

The following steps will prepare a basic Linux installation for
templating.

#. **Installation**

   It is good practice to name your VM something generic during
   installation, this will ensure components such as LVM do not appear
   unique to a machine. It is recommended that the name of "localhost"
   is used for installation.

   .. warning:: 
      For CentOS, it is necessary to take unique identification out of the
      interface configuration file, for this edit
      /etc/sysconfig/network-scripts/ifcfg-eth0 and change the content to
      the following. 

   .. code:: bash

      DEVICE=eth0
      TYPE=Ethernet
      BOOTPROTO=dhcp
      ONBOOT=yes

   The next steps updates the packages on the Template Master.

   -  Ubuntu

      .. code:: bash

         sudo -i
         apt-get update
         apt-get upgrade -y
         apt-get install -y acpid ntp
         reboot

   -  CentOS

      .. code:: bash

         ifup eth0
         yum update -y
         reboot

#. **Password management**

   .. note:: 
      If preferred, custom users (such as ones created during the Ubuntu 
      installation) should be removed. First ensure the root user account 
      is enabled by giving it a password and then login as root to continue.

   .. code:: bash

      sudo passwd root
      logout

   As root, remove any custom user accounts created during the
   installation process.

   .. code:: bash

      deluser myuser --remove-home

   See :ref:`adding-password-management-to-templates` for
   instructions to setup the password management script, this will allow
   CloudStack to change your root password from the web interface.

#. **Hostname Management**

   CentOS configures the hostname by default on boot. Unfortunately
   Ubuntu does not have this functionality, for Ubuntu installations use
   the following steps.

   -  Ubuntu

      The hostname of a Templated VM is set by a custom script in
      `/etc/dhcp/dhclient-exit-hooks.d`, this script first checks if the
      current hostname is localhost, if true, it will get the host-name,
      domain-name and fixed-ip from the DHCP lease file and use those
      values to set the hostname and append the `/etc/hosts` file for
      local hostname resolution. Once this script, or a user has changed
      the hostname from localhost, it will no longer adjust system files
      regardless of its new hostname. The script also recreates
      openssh-server keys, which should have been deleted before
      templating (shown below). Save the following script to
      `/etc/dhcp/dhclient-exit-hooks.d/sethostname`, and adjust the
      permissions.

      .. code:: bash

         #!/bin/sh
         # dhclient change hostname script for Ubuntu
         oldhostname=$(hostname -s)
         if [ $oldhostname = 'localhost' ]
         then
             sleep 10 # Wait for configuration to be written to disk
             hostname=$(cat /var/lib/dhcp/dhclient.eth0.leases  |  awk ' /host-name/ { host = $3 }  END { printf host } ' | sed     's/[";]//g' )
             fqdn="$hostname.$(cat /var/lib/dhcp/dhclient.eth0.leases  |  awk ' /domain-name/ { domain = $3 }  END { printf     domain } ' | sed 's/[";]//g')"
             ip=$(cat /var/lib/dhcp/dhclient.eth0.leases  |  awk ' /fixed-address/ { lease = $2 }  END { printf lease } ' | sed     's/[";]//g')
             echo "cloudstack-hostname: Hostname _localhost_ detected. Changing hostname and adding hosts."
             printf " Hostname: $hostname\n FQDN: $fqdn\n IP: $ip"
             # Update /etc/hosts
             awk -v i="$ip" -v f="$fqdn" -v h="$hostname" "/^127/{x=1} !/^127/ && x { x=0; print i,f,h; } { print $0; }" /etc/hosts > /etc/hosts.dhcp.tmp
             mv /etc/hosts /etc/hosts.dhcp.bak
             mv /etc/hosts.dhcp.tmp /etc/hosts
             # Rename Host
             echo $hostname > /etc/hostname
             hostname -b -F /etc/hostname
             echo $hostname > /proc/sys/kernel/hostname
             # Recreate SSH2
             export DEBIAN_FRONTEND=noninteractive
             dpkg-reconfigure openssh-server
         fi
         ### End of Script ###
         
         chmod 774  /etc/dhcp/dhclient-exit-hooks.d/sethostname

   .. warning:: 
      The following steps should be run when you are ready to template 
      your Template Master. If the Template Master is rebooted during 
      these steps you will have to run all the steps again. At the end 
      of this process the Template Master should be shutdown and the 
      template created in order to create and deploy the final template.

#. **Remove the udev persistent device rules**

   This step removes information unique to your Template Master such as
   network MAC addresses, lease files and CD block devices, the files
   are automatically generated on next boot.

   -  Ubuntu

      .. code:: bash

         rm -f /etc/udev/rules.d/70*
         rm -f /var/lib/dhcp/dhclient.*

   -  CentOS

      .. code:: bash

         rm -f /etc/udev/rules.d/70*
         rm -f /var/lib/dhclient/*

#. **Remove SSH Keys**

   This step is to ensure all your Templated VMs do not have the same
   SSH keys, which would decrease the security of the machines
   dramatically.

   .. code:: bash

      rm -f /etc/ssh/*key*

#. **Cleaning log files**

   It is good practice to remove old logs from the Template Master.

   .. code:: bash

      cat /dev/null > /var/log/audit/audit.log 2>/dev/null
      cat /dev/null > /var/log/wtmp 2>/dev/null
      logrotate -f /etc/logrotate.conf 2>/dev/null
      rm -f /var/log/*-* /var/log/*.gz 2>/dev/null

#. **Setting hostname**

   In order for the Ubuntu DHCP script to function and the CentOS
   dhclient to set the VM hostname they both require the Template
   Master's hostname to be "localhost", run the following commands to
   change the hostname.

   .. code:: bash

      hostname localhost
      echo "localhost" > /etc/hostname

#. **Set user password to expire**

   This step forces the user to change the password of the VM after the
   template has been deployed.

   .. code:: bash

      passwd --expire root

#. **Clearing User History**

   The next step clears the bash commands you have just run.

   .. code:: bash

      history -c
      unset HISTFILE

#. **Shutdown the VM**

   Your now ready to shutdown your Template Master and create a
   template!

   .. code:: bash

      halt -p

#. **Create the template!**

   You are now ready to create the template, for more information see
   `“Creating a Template from an Existing Virtual
   Machine” <#creating-a-template-from-an-existing-virtual-machine>`_.

.. note::
   Templated VMs for both Ubuntu and CentOS may require a reboot after 
   provisioning in order to pickup the hostname.
