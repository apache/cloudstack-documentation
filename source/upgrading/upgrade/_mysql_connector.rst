Install new MySQL connector
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Starting with 4.9.0, cloudstack-management RPM's now depend on the
``mysql-connector-python`` package. Therefore Apache CloudStack 
|release| requires the instalation of the MySQL connector on CentOS.


MySQL connector RPM repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add a new yum repo ``/etc/yum.repos.d/mysql.repo``:

.. parsed-literal::

   [mysql-community]
   name=MySQL Community connectors
   baseurl=http://repo.mysql.com/yum/mysql-connectors-community/el/$releasever/$basearch/
   enabled=1
   gpgcheck=1

Import GPG public key from MySQL:

.. parsed-literal::

   rpm --import http://repo.mysql.com/RPM-GPG-KEY-mysql

Install mysql-connector

.. parsed-literal::

   yum install mysql-connector-python

