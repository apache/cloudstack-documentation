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

Additional Management Servers
-----------------------------

For your second and subsequent Management Servers, you will install the
Management Server software, connect it to the database, and set up the
OS for the Management Server.

#. Perform the steps in `“Prepare the Operating System” 
   <#prepare-the-operating-system>`_ and `“Building RPMs from Source” 
   <building_from_source.html#building-rpms-from-source>`__ or 
   `“Building DEB packages” 
   <building_from_source.html#building-deb-packages>`__ as appropriate.

#. This step is required only for installations where XenServer is
   installed on the hypervisor hosts.

   Download vhd-util from
   `vhd-util <http://download.cloudstack.org/tools/vhd-util>`_

   Copy vhd-util to
   ``/usr/share/cloudstack-common/scripts/vm/hypervisor/xenserver``.

#. Ensure that necessary services are started and set to start on boot.

   .. parsed-literal::

      service rpcbind start
      service nfs start
      chkconfig nfs on
      chkconfig rpcbind on

#. Configure the database client. Note the absence of the --deploy-as
   argument in this case. (For more details about the arguments to this
   command, see :ref:`install-database-on-separate-node`.)

   .. parsed-literal::

      cloudstack-setup-databases cloud:dbpassword@dbhost \
      -e encryption_type \
      -m management_server_key \
      -k database_key \
      -i management_server_ip

#. Configure the OS and start the Management Server:

   .. parsed-literal::

      cloudstack-setup-management

   The Management Server on this node should now be running.
   If the servlet container is Tomcat7 the argument --tomcat7 must be used.
   
   .. warning::
      On RHEL and CentOS systems, firewalld (installed by default) will override all 
      iptables rules set by the cloudstack-setup-management script, 
      so ensure that the firewalld is disabled or ensure the correct firewalld rules
      are in place to allow traffic to ports 8080, 8250 and 9090 to the management server.

#. Repeat these steps on each additional Management Server.

#. Be sure to configure a load balancer for the Management Servers. See :ref:`management-server-load-balancing`
