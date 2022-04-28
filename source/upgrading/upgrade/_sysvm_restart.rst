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

System-VMs and Virtual-Routers
------------------------------

From Apache CloudStack version 4.17.0 onward, there is support to live patch 
system VMs, namely, SSVM, CPVM, Routers. Live patching provides support 
for zero-downtime upgrades, wherein, the System VM software is updated to the
latest code version without having to destroy and recreate them / restart them.

With this feature, users will have a choice wherein they can use the existing system VM template with the latest
software by using the live patch feature, or can follow the usual workflow of restarting the
system VM to use the latest system VM template. Live Patching system VMs serves to be especially
useful in cases when the code version has upgraded but the template hasn't. In such a scenario users
will no longer need to restart the system VMs to use the latest code.

When one attempts to live-patch the system VMs, it pretty much mimics the patching process
that happens when booting up the System VMs but with having to shut down the system VMs. 
This will update the software packages, which were previously bundled in the systemvm.iso i.e., 
agent.zip and cloud-scripts.tgz and restart the services that are present in the /var/cache/cloud/enabled_svcs file
in the system VMs.

.. note::

   The following services will be restarted once a system VM is live patched:

            +---------------------+-------------------------------+
            | **System VM**       |         **Services**          |
            +---------------------+-------------------------------+
            | SSVM                | cloud, apache2, portmap       |
            +---------------------+-------------------------------+
            | CPVM                | cloud                         |
            +---------------------+-------------------------------+
            | VRs                 | haproxy, apache2, dnsmasq     |
            +---------------------+-------------------------------+

   With respect to VRs, a network restart without cleanup is initiated to during live patching to ensure all rules
   are re-applied. 

   **NOTE:** In case there is an absolute need to upgrade the system VM template due to availability of
   security patches or update in a package provided by the template, then the old workflow of recreating the system
   VM will need to be followed, which would mean noticible downtime.
   
Following matrix lists the versions of CloudStack that support live patching.

         +---------------------+-------------------------+--------------------------------+------------------------------------------+
         | **ACS Version**     |  **Upgrade Version**    |   **Live Patching Support**    |     **Reason / Comment**                 |
         +---------------------+-------------------------+--------------------------------+------------------------------------------+
         | <=4.13              | 4.17+                   |  No                            | Update in the openJDK version            |
         +---------------------+-------------------------+--------------------------------+------------------------------------------+
         | 4.14                | 4.17+                   |Yes                             | May notice some issue with remove access |
         |                     |                         |                                | VPN due to older version of Strongswan   |
         +---------------------+-------------------------+--------------------------------+------------------------------------------+
         | >=4.15              | 4.17+                   |Yes                             |       N/A                                |
         +---------------------+-------------------------+--------------------------------+------------------------------------------+

In addition to the support for live patching, users still have the facility to follow the legacy workflow
of restarting the system VMs once the packages on the management servers have been upgraded. Here you'll
need to restart the system VMs in order for those VMs to be rebuilt 
from the new system VM template version.

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
