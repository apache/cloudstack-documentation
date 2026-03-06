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

MySQL upgrade
=============

Explicit JDBC driver declaration
--------------------------------

While upgrading, on some environments the following may be required to be
added in CloudStack's db.properties file:

   # Add these to your db.properties file

   db.cloud.driver=jdbc:mysql

   db.usage.driver=jdbc:mysql

MySQL support updated to 8.4
----------------------------

As of Apache CloudStack 4.20.3, support for MySQL 8.4 has been added.

Existing deployments upgraded to version 4.20.3 can still continue using MySQL 8.0
without any changes.

If you are running MySQL 8.0 and would like to upgrade to MySQL 8.4,
you may follow the standard MySQL upgrade process to migrate safely to version 8.4,
and then update the authentication method for the root and CloudStack (cloud) users with
caching_sha2_password plugin using the below steps as the mysql_native_password plugin
is deprecated as of MySQL 8.0.34, and disabled by default in MySQL 8.4. For more details,
refer to MySQL documentation here: https://dev.mysql.com/doc/refman/8.4/en/caching-sha2-pluggable-authentication.html

#. Stop MySQL server if already running

   .. code-block:: bash

      sudo systemctl stop mysqld

#. Start MySQL server in safe mode without auth

   .. code-block:: bash

      sudo mysqld --skip-grant-tables --skip-networking &

#. Login to MySQL without password

   .. code-block:: bash

      mysql -u root

#. Reset passwords for root and CloudStack (cloud) users.

   .. code-block:: mysql

      ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'ROOT_PASSWORD';
      ALTER USER 'root'@'%' IDENTIFIED WITH caching_sha2_password BY 'ROOT_PASSWORD';
      ALTER USER 'cloud'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'CLOUD_PASSWORD';
      ALTER USER 'cloud'@'%' IDENTIFIED WITH caching_sha2_password BY 'CLOUD_PASSWORD';
      FLUSH PRIVILEGES;

   Note: Please ensure that the password used for the cloud database user matches the value
   configured in /etc/cloudstack/management/db.properties. If the password in db.properties
   is encrypted, you can retrieve it using the below command.

   .. code-block:: bash

      java -classpath /usr/share/cloudstack-common/lib/cloudstack-utils.jar \
      com.cloud.utils.crypt.EncryptionCLI -d \
      -i "$(grep -oP 'db.cloud.password=ENC\(\K[^\)]+(?=\))' /etc/cloudstack/management/db.properties)" \
      -p "$(cat /etc/cloudstack/management/key)"

#. Remove deprecated authentication plugin 'mysql_native_password' from the MySQL configuration. Either comment or remove the below line from /etc/my.cnf

   .. parsed-literal::

      default_authentication_plugin=mysql_native_password

#. Restart MySQL server

   .. code-block:: bash

      killall mysqld
      systemctl start mysqld

MySQL 8.0+ sql mode change
--------------------------

MySQL mode (sql_mode) has changed in CloudStack db.properties to
"STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,
ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION".

This gets automatically applies to the MySQL session used by CloudStack management server.

If the admin uses MySQL directly and wants to query tables it is advised to change the sql_mode in the corresponding session or globally.

Eg. mysql> set global sql_mode="STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,
                             "> ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION";
    Query OK, 0 rows affected (0.00 sec)

    mysql> set sql_mode="STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,
                     "> ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION";
    Query OK, 0 rows affected (0.00 sec)

MySQL upgrade problems
----------------------

With certain MySQL versions (see below), issues have been seen with "cloud.nics" table's 
column type (which was not updated properly during CloudStack upgrades, due to MySQL limitations),
which eventually may lead to exception seen in the management server logs, causing Users to
not be able to start any VM.

The following SQL statement needs to be manually executed in order to fix such issue:

   .. parsed-literal::
ALTER TABLE nics MODIFY COLUMN update_time timestamp DEFAULT CURRENT_TIMESTAMP;

The issue is known to affect the following MySQL server versions:

 -  5.7.34 or later
 -  8+
