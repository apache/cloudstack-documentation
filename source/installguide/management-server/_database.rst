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

Install the database server
---------------------------

The CloudStack management server uses a MySQL database server to store
its data. When you are installing the management server on a single
node, you can install the MySQL server locally. For an installation that
has multiple management server nodes, we assume the MySQL database also
runs on a separate node.

CloudStack has been tested with MySQL 5.1 and 5.5. These versions are
included in RHEL/CentOS and Ubuntu.


Install the Database on the Management Server Node
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section describes how to install MySQL on the same machine with the
Management Server. This technique is intended for a simple deployment
that has a single Management Server node. If you have a multi-node
Management Server deployment, you will typically use a separate node for
MySQL. See :ref:`install-database-on-separate-node`.

#. Install MySQL from the package repository of your distribution:

   .. parsed-literal::

      yum install mysql-server

   .. parsed-literal::

      sudo apt-get install mysql-server

#. Open the MySQL configuration file. The configuration file is
   ``/etc/my.cnf`` or ``/etc/mysql/my.cnf``, depending on your OS.

   Insert the following lines in the ``[mysqld]`` section.

   You can put these lines below the datadir line. The max\_connections
   parameter should be set to 350 multiplied by the number of Management
   Servers you are deploying. This example assumes one Management
   Server.

   .. parsed-literal::

      innodb_rollback_on_timeout=1
      innodb_lock_wait_timeout=600
      max_connections=350
      log-bin=mysql-bin
      binlog-format = 'ROW'

   .. note:: 
      You can also create a file ``/etc/mysql/conf.d/cloudstack.cnf`` 
      and add these directives there. Don't forget to add ``[mysqld]`` on the 
      first line of the file.



#. Start or restart MySQL to put the new configuration into effect.

   On RHEL/CentOS, MySQL doesn't automatically start after installation.
   Start it manually.

   .. parsed-literal::

      service mysqld start

   On Ubuntu, restart MySQL.

   .. parsed-literal::

      sudo service mysql restart

#. (CentOS and RHEL only; not required on Ubuntu)

   .. warning::
      On RHEL and CentOS, MySQL does not set a root password by default. It is 
      very strongly recommended that you set a root password as a security 
      precaution.

   Run the following command to secure your installation. You can answer "Y" 
   to all questions.

   .. parsed-literal::

      mysql_secure_installation

#. CloudStack can be blocked by security mechanisms, such as SELinux.
   Disable SELinux to ensure + that the Agent has all the required
   permissions.

   Configure SELinux (RHEL and CentOS):

   #. Check whether SELinux is installed on your machine. If not, you
      can skip this section.

      In RHEL or CentOS, SELinux is installed and enabled by default.
      You can verify this with:

      .. parsed-literal::

         rpm -qa | grep selinux

   #. Set the SELINUX variable in ``/etc/selinux/config`` to
      "permissive". This ensures that the permissive setting will be
      maintained after a system reboot.

      In RHEL or CentOS:

      .. parsed-literal::

         vi /etc/selinux/config

      Change the following line

      .. parsed-literal::

         SELINUX=enforcing

      to this:

      .. parsed-literal::

         SELINUX=permissive

   #. Set SELinux to permissive starting immediately, without requiring
      a system reboot.

      .. parsed-literal::

         setenforce permissive

#. Set up the database. The following command creates the "cloud" user
   on the database.

   .. parsed-literal::

      cloudstack-setup-databases cloud:<dbpassword>@localhost \
      --deploy-as=root:<password> \
      -e <encryption_type> \
      -m <management_server_key> \
      -k <database_key> \
      -i <management_server_ip>

   -  In dbpassword, specify the password to be assigned to the "cloud"
      user. You can choose to provide no password although that is not
      recommended.

   -  In deploy-as, specify the username and password of the user
      deploying the database. In the following command, it is assumed
      the root user is deploying the database and creating the "cloud"
      user.

   -  (Optional) For encryption\_type, use file or web to indicate the
      technique used to pass in the database encryption password.
      Default: file. See :ref:`about-password-key-encryption`.

   -  (Optional) For management\_server\_key, substitute the default key
      that is used to encrypt confidential parameters in the CloudStack
      properties file. Default: password. It is highly recommended that
      you replace this with a more secure value. See 
      :ref:`about-password-key-encryption`.

   -  (Optional) For database\_key, substitute the default key that is
      used to encrypt confidential parameters in the CloudStack
      database. Default: password. It is highly recommended that you
      replace this with a more secure value. See 
      :ref:`about-password-key-encryption`.

   -  (Optional) For management\_server\_ip, you may explicitly specify
      cluster management server node IP. If not specified, the local IP
      address will be used.


   When this script is finished, you should see a message like
   “Successfully initialized the database.”

   .. note::
      If the script is unable to connect to the MySQL database, check the 
      "localhost" loopback address in ``/etc/hosts``. It should be pointing to 
      the IPv4 loopback address "127.0.0.1" and not the IPv6 loopback address 
      ``::1``. Alternatively, reconfigure MySQL to bind to the IPv6 loopback 
      interface.

#. If you are running the KVM hypervisor on the same machine with the
   Management Server, edit /etc/sudoers and add the following line:

   .. parsed-literal::

      Defaults:cloud !requiretty

#. Now that the database is set up, you can finish configuring the OS
   for the Management Server. This command will set up iptables,
   sudoers, and start the Management Server.

   .. parsed-literal::

      cloudstack-setup-management

   You should get the output message “CloudStack Management Server setup is
   done.”
   If the servlet container is Tomcat7 the argument --tomcat7 must be used.


.. _install-database-on-separate-node:

Install the Database on a Separate Node
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section describes how to install MySQL on a standalone machine,
separate from the Management Server. This technique is intended for a
deployment that includes several Management Server nodes. If you have a
single-node Management Server deployment, you will typically use the
same node for MySQL. See `“Install the Database on the Management Server Node” 
<#install-the-database-on-the-management-server-node>`_.

.. note:: 
   The management server doesn't require a specific distribution for the MySQL 
   node. You can use a distribution or Operating System of your choice. Using 
   the same distribution as the management server is recommended, but not 
   required. See `“Management Server, Database, and Storage System Requirements” 
   <#management-server-database-and-storage-system-requirements>`_.

#. Install MySQL from the package repository from your distribution:

   .. parsed-literal::

      yum install mysql-server

   .. parsed-literal::

      sudo apt-get install mysql-server

#. Edit the MySQL configuration (/etc/my.cnf or /etc/mysql/my.cnf,
   depending on your OS) and insert the following lines in the [mysqld]
   section. You can put these lines below the datadir line. The
   max\_connections parameter should be set to 350 multiplied by the
   number of Management Servers you are deploying. This example assumes
   two Management Servers.

   .. note::
      On Ubuntu, you can also create /etc/mysql/conf.d/cloudstack.cnf file and 
      add these directives there. Don't forget to add [mysqld] on the first 
      line of the file.

   .. parsed-literal::

      innodb_rollback_on_timeout=1
      innodb_lock_wait_timeout=600
      max_connections=700
      log-bin=mysql-bin
      binlog-format = 'ROW'
      bind-address = 0.0.0.0

#. Start or restart MySQL to put the new configuration into effect.

   On RHEL/CentOS, MySQL doesn't automatically start after installation.
   Start it manually.

   .. parsed-literal::

      service mysqld start

   On Ubuntu, restart MySQL.

   .. parsed-literal::

      sudo service mysql restart

#. (CentOS and RHEL only; not required on Ubuntu)

   .. warning::
      On RHEL and CentOS, MySQL does not set a root password by default. It is 
      very strongly recommended that you set a root password as a security 
      precaution. Run the following command to secure your installation. You 
      can answer "Y" to all questions except "Disallow root login remotely?". 
      Remote root login is required to set up the databases.

   .. parsed-literal::

      mysql_secure_installation

#. If a firewall is present on the system, open TCP port 3306 so
   external MySQL connections can be established.

   On Ubuntu, UFW is the default firewall. Open the port with this
   command:

   .. parsed-literal::

      ufw allow mysql

   On RHEL/CentOS:

   #. Edit the /etc/sysconfig/iptables file and add the following line
      at the beginning of the INPUT chain.

      .. parsed-literal::

         -A INPUT -p tcp --dport 3306 -j ACCEPT

   #. Now reload the iptables rules.

      .. parsed-literal::

         service iptables restart

#. Return to the root shell on your first Management Server.

#. Set up the database. The following command creates the cloud user on
   the database.

   -  In dbpassword, specify the password to be assigned to the cloud
      user. You can choose to provide no password.

   -  In deploy-as, specify the username and password of the user
      deploying the database. In the following command, it is assumed
      the root user is deploying the database and creating the cloud
      user.

   -  (Optional) For encryption\_type, use file or web to indicate the
      technique used to pass in the database encryption password.
      Default: file. See :ref:`about-password-key-encryption`.

   -  (Optional) For management\_server\_key, substitute the default key
      that is used to encrypt confidential parameters in the CloudStack
      properties file. Default: password. It is highly recommended that
      you replace this with a more secure value. See About Password and
      Key Encryption.

   -  (Optional) For database\_key, substitute the default key that is
      used to encrypt confidential parameters in the CloudStack
      database. Default: password. It is highly recommended that you
      replace this with a more secure value. See 
      :ref:`about-password-key-encryption`.

   -  (Optional) For management\_server\_ip, you may explicitly specify
      cluster management server node IP. If not specified, the local IP
      address will be used.

   .. parsed-literal::

      cloudstack-setup-databases cloud:<dbpassword>@<ip address mysql server> \
      --deploy-as=root:<password> \
      -e <encryption_type> \
      -m <management_server_key> \
      -k <database_key> \
      -i <management_server_ip>

   When this script is finished, you should see a message like 
   “Successfully initialized the database.”

#. Now that the database is set up, you can finish configuring the OS
   for the Management Server. This command will set up iptables,
   sudoers, and start the Management Server.

   .. parsed-literal::

      cloudstack-setup-management

   You should get the output message “CloudStack Management Server setup is
   done.”

