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

.. sub-section included in upgrade notes.

Once you've upgraded the packages on your management servers, you'll
need to restart the system VMs in order for those VMs to be rebuilt 
from the new systemVM template version.

.. note::

   Restarting system VMs can be done in different ways. You can use script
   "cloudstack-sysvmadm" which is provided with CloudStack, or do a manual restart of system VMs
   or do it by using third-party tools such as Ansible.
   Below we are giving instructions for using the "cloudstack-sysvmadm" script.


Ensure that the admin port is set to
8096 by using the "integration.api.port" global parameter. This port
is used by the cloudstack-sysvmadm script at the end of the upgrade
procedure. For information about how to set this parameter, see :ref:`configuration parameters <configuration-parameters>`
Changing this parameter will require a management server restart.

If you run the cloudstack-sysvmadm script from outside the management
server, make sure port 8096 is open in your local host firewall.

.. warning::

   Never allow access to port 8096 from the public internet! The
   management server accepts API calls without authentication on this
   port, which can pose a serious security risk.

There is a script that will do this for you, all you need to do is
run the script and supply the IP address for your MySQL instance and
your MySQL credentials:

.. parsed-literal::

   # nohup cloudstack-sysvmadm -d IPaddress -u cloud -p password -a > sysvm.log 2>&1 &

You can monitor the log for progress. The process of restarting the
system VMs can take an hour or more.

.. parsed-literal::

   # tail -f sysvm.log

The output to ``sysvm.log`` will look something like this:

.. parsed-literal::

   Stopping and starting 1 secondary storage vm(s)...
   Done stopping and starting secondary storage vm(s)
   Stopping and starting 1 console proxy vm(s)...
   Done stopping and starting console proxy vm(s).
   Stopping and starting 4 running routing vm(s)...
   Done restarting router(s).

After the upgrade process is complete, you can disable unauthenticated
API access again by setting "integration.api.port" to 0.
Don't forget to restart the management server afterwards.

.. sub-section included in upgrade notes.
