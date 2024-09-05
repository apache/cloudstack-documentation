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


.. _resource-tags:

Using Tags to Organize Resources in the Cloud
---------------------------------------------

A tag is a key-value pair that stores metadata about a resource in the
cloud. Tags are useful for categorizing resources. For example, you can
tag a User Instance with a value that indicates the User's city of residence.
In this case, the key would be "city" and the value might be "Toronto"
or "Tokyo." You can then request CloudStack to find all resources that
have a given tag; for example, Instances for Users in a given city.

You can tag a User Instance, Volume, Snapshot, Guest Network,
Template, ISO, firewall rule, port forwarding rule, public IP address,
security group, load balancer rule, project, VPC, Network ACL, or static
route. You can not tag a remote access VPN.

You can work with tags through the UI or through the API commands
createTags, deleteTags, and listTags. You can define multiple tags for
each resource. There is no limit on the number of tags you can define.
Each tag can be up to 255 characters long. Users can define tags on the
resources they own, and administrators can define tags on any resources
in the cloud.

An optional input parameter, "tags," exists on many of the list\* API
commands. The following example shows how to use this new parameter to
find all the volumes having tag region=canada OR tag city=Toronto:

.. code:: bash

   command=listVolumes
      &listAll=true
      &tags[0].key=region
      &tags[0].value=canada
      &tags[1].key=city
      &tags[1].value=Toronto

The following API commands have the "tags" input parameter:

-  listVirtualMachines

-  listVolumes

-  listSnapshots

-  listNetworks

-  listTemplates

-  listIsos

-  listFirewallRules

-  listPortForwardingRules

-  listPublicIpAddresses

-  listSecurityGroups

-  listLoadBalancerRules

-  listProjects

-  listVPCs

-  listNetworkACLs

-  listStaticRoutes

Using Comments on the Resources in the Cloud
--------------------------------------------

CloudStack allows Users and administrators to create comments against cloud objects with a UUID. The listing page of any cloud object includes a blue icon next to the object name indicating that the object contains comments.

To create a new comment on an object:

1. Click on the object to display the detail view

2. Navigate to the Comments tab

3. Add a comment on the text area and click the Submit button

.. note::
   Administrators only: Select the 'Only visible to Administrators' checkbox to create private comments across administrators

To display al the comments created by the logged in User (or administrator):

1. In the left navigation bar, click Tools

2. Click Comments (the default filter is 'Created by me')

To display all the comments on the objects that the logged in User (or administrator) has access:

1. In the left navigation bar, click Tools

2. Click Comments

3. Select the 'All Comments' filter

Reporting CPU Sockets
---------------------

Cloudstack manages different types of hosts that contains one or more
physical CPU sockets. CPU socket is considered as a unit of measure used
for licensing and billing cloud infrastructure. Cloudstack provides both UI
and API support to collect the CPU socket statistics for billing
purpose. The Infrastructure tab has a new tab for CPU sockets. You can
view the statistics for CPU sockets managed by Cloudstack, which in turn
reflects the size of the cloud. The CPU Socket page will give you the
number of hosts and sockets used for each host type.

1. Log in to the Cloudstack UI.

2. In the left navigation bar, click Infrastructure.

3. On CPU Sockets, click View all.

   The CPU Socket page is displayed. The page shows the number of hosts
   and CPU sockets based on hypervisor types.


Changing the Database Configuration
-----------------------------------

The CloudStack Management Server stores database configuration
information (e.g., hostname, port, credentials) in the file
``/etc/cloudstack/management/db.properties``. To effect a change, edit
this file on each Management Server, then restart the Management Server.

Changing the Database Password
------------------------------

You may need to change the password for the MySQL account used by
CloudStack. If so, you'll need to change the password in MySQL, and then
add the encrypted password to
``/etc/cloudstack/management/db.properties``.

#. Before changing the password, you'll need to stop CloudStack's
   management server and the usage engine if you've deployed that
   component.

   .. code:: bash

       # service cloudstack-management stop
       # service cloudstack-usage stop

#. Next, you'll update the password for the CloudStack user on the MySQL
   server.

   .. code:: bash

       # mysql -u root -p

   At the MySQL shell, you'll change the password and flush privileges:

   .. code:: bash

       update mysql.user set password=PASSWORD("newpassword123") where User='cloud';
       flush privileges;
       quit;

#. The next step is to encrypt the password and copy the encrypted
   password to CloudStack's database configuration
   (``/etc/cloudstack/management/db.properties``).

   .. code:: bash

           # java -classpath /usr/share/cloudstack-common/lib/cloudstack-utils.jar com.cloud.utils.crypt.EncryptionCLI -p `cat /etc/cloudstack/management/key` -i newpassword123


File encryption type
--------------------

   Note that this is for the file encryption type. If you're using the
   web encryption type then you'll use
   password="management\_server\_secret\_key"

#. Now, you'll update ``/etc/cloudstack/management/db.properties`` with
   the new ciphertext. Open ``/etc/cloudstack/management/db.properties``
   in a text editor, and update these parameters:

   .. code:: bash

       db.cloud.password=ENC(encrypted_password_from_above)
       db.usage.password=ENC(encrypted_password_from_above)

#. After copying the new password over, you can now start CloudStack
   (and the usage engine, if necessary).

   .. code:: bash

               # service cloudstack-management start
               # service cloud-usage start


Administrator Alerts
--------------------

The system provides alerts and events to help with the management of the
cloud. Alerts are notices to an administrator, generally delivered by
e-mail, notifying the administrator that an error has occurred in the
cloud. Alert behavior is configurable.

Events track all of the User and administrator actions in the cloud. For
example, every Guest Instance start creates an associated event. Events are
stored in the Management Server’s database.

Emails will be sent to administrators under the following circumstances:

-  The Management Server cluster runs low on CPU, memory, or storage
   resources

-  The Management Server loses heartbeat from a Host for more than 3
   minutes

-  The Host cluster runs low on CPU, memory, or storage resources


Sending Alerts to External SNMP and Syslog Managers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In addition to showing administrator alerts on the Dashboard in the
CloudStack UI and sending them in email, CloudStack can also send the
same alerts to external SNMP or Syslog management software. This is
useful if you prefer to use an SNMP or Syslog manager to monitor your
cloud.

The alerts which can be sent are:

The following is the list of alert type numbers. The current alerts can
be found by calling listAlerts.

::

   MEMORY = 0 // Available Memory below configured threshold

::

   CPU = 1 // Unallocated CPU below configured threshold

::

   STORAGE =2 // Available Storage below configured threshold

::

   STORAGE_ALLOCATED = 3 // Remaining unallocated Storage is below configured threshold

::

   PUBLIC_IP = 4 // Number of unallocated virtual Network public IPs is below configured threshold

::

   PRIVATE_IP = 5 // Number of unallocated private IPs is below configured threshold

::

   SECONDARY_STORAGE = 6 //  Available Secondary Storage in availability zone is below configured threshold

::

   HOST = 7 // Host related alerts like host disconnected

::

   USERVM = 8 // User Instance stopped unexpectedly

::

   DOMAIN_ROUTER = 9 // Domain Router VM stopped unexpectedly

::

   CONSOLE_PROXY = 10 // Console Proxy VM stopped unexpectedly

::

   ROUTING = 11 // Lost connection to default route (to the gateway)

::

   STORAGE_MISC = 12 // Storage issue in system VMs

::

   USAGE_SERVER = 13 // No usage server process running

::

   MANAGMENT_NODE = 14 // Management Network CIDR is not configured originally

::

   DOMAIN_ROUTER_MIGRATE = 15 // Domain Router VM Migration was unsuccessful

::

   CONSOLE_PROXY_MIGRATE = 16 // Console Proxy VM Migration was unsuccessful

::

   USERVM_MIGRATE = 17 // User Instance Migration was unsuccessful

::

   VLAN = 18 // Number of unallocated VLANs is below configured threshold in availability zone

::

   SSVM = 19 // SSVM stopped unexpectedly

::

   USAGE_SERVER_RESULT = 20 // Usage job failed

::

   STORAGE_DELETE = 21 // Failed to delete storage pool

::

   UPDATE_RESOURCE_COUNT = 22 // Failed to update the resource count

::

   USAGE_SANITY_RESULT = 23 // Usage Sanity Check failed

::

   DIRECT_ATTACHED_PUBLIC_IP = 24 // Number of unallocated shared Network IPs is low in availability zone

::

   LOCAL_STORAGE = 25 // Remaining unallocated Local Storage is below configured threshold

::

   RESOURCE_LIMIT_EXCEEDED = 26 //Generated when the resource limit exceeds the limit. Currently used for recurring Snapshots only


You can also display the most up to date list by calling the API command ``listAlerts``.


SNMP Alert Details
^^^^^^^^^^^^^^^^^^

The supported protocol is SNMP version 2.

Each SNMP trap contains the following information: message, podId,
dataCenterId, clusterId, and generationTime.


Syslog Alert Details
^^^^^^^^^^^^^^^^^^^^

CloudStack generates a syslog message for every alert. Each syslog
message incudes the fields alertType, message, podId, dataCenterId, and
clusterId, in the following format. If any field does not have a valid
value, it will not be included.

.. code:: bash

   Date severity_level Management_Server_IP_Address/Name  alertType:: value dataCenterId:: value  podId:: value  clusterId:: value  message:: value

For example:

.. code:: bash

   Mar  4 10:13:47    WARN    localhost    alertType:: managementNode message:: Management server node 127.0.0.1 is up

Configuring SNMP and Syslog Managers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To configure one or more SNMP managers or Syslog managers to receive
alerts from CloudStack:

#. For an SNMP manager, install the CloudStack MIB file on your SNMP
   manager system. This maps the SNMP OIDs to trap types that can be
   more easily read by users. The file must be publicly available. For
   more information on how to install this file, consult the
   documentation provided with the SNMP manager.

#. Edit the file /etc/cloudstack/management/log4j-cloud.xml.

   .. code:: bash

      # vi /etc/cloudstack/management/log4j-cloud.xml

#. Add an entry using the syntax shown below. Follow the appropriate
   example depending on whether you are adding an SNMP manager or a
   Syslog manager. To specify multiple external managers, separate the
   IP addresses and other configuration values with commas (,).

   .. note::
      The recommended maximum number of SNMP or Syslog managers is 20
      for each.

   The following example shows how to configure two SNMP managers at IP
   addresses 10.1.1.1 and 10.1.1.2. Substitute your own IP addresses,
   ports, and communities. Do not change the other values (name,
   threshold, class, and layout values).

   .. code:: bash

      <appender name="SNMP" class="org.apache.cloudstack.alert.snmp.SnmpTrapAppender">
        <param name="Threshold" value="WARN"/>  <!-- Do not edit. The alert feature assumes WARN. -->
        <param name="SnmpManagerIpAddresses" value="10.1.1.1,10.1.1.2"/>
        <param name="SnmpManagerPorts" value="162,162"/>
        <param name="SnmpManagerCommunities" value="public,public"/>
        <layout class="org.apache.cloudstack.alert.snmp.SnmpEnhancedPatternLayout"> <!-- Do not edit -->
          <param name="PairDelimeter" value="//"/>
          <param name="KeyValueDelimeter" value="::"/>
        </layout>
      </appender>

   The following example shows how to configure two Syslog managers at
   IP addresses 10.1.1.1 and 10.1.1.2. Substitute your own IP addresses.
   You can set Facility to any syslog-defined value, such as LOCAL0 -
   LOCAL7. Do not change the other values.

   .. code:: bash

      <appender name="ALERTSYSLOG">
        <param name="Threshold" value="WARN"/>
        <param name="SyslogHosts" value="10.1.1.1,10.1.1.2"/>
        <param name="Facility" value="LOCAL6"/>
        <layout>
          <param name="ConversionPattern" value=""/>
        </layout>
      </appender>

#. If your cloud has multiple Management Server nodes, repeat these
   steps to edit log4j-cloud.xml on every Instance.

#. If you have made these changes while the Management Server is
   running, wait a few minutes for the change to take effect.

**Troubleshooting:** If no alerts appear at the configured SNMP or
Syslog manager after a reasonable amount of time, it is likely that
there is an error in the syntax of the <appender> entry in
log4j-cloud.xml. Check to be sure that the format and settings are
correct.


Deleting an SNMP or Syslog Manager
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To remove an external SNMP manager or Syslog manager so that it no
longer receives alerts from CloudStack, remove the corresponding entry
from the file ``/etc/cloudstack/management/log4j-cloud.xml``.


Customizing the Network Domain Name
-----------------------------------

The root administrator can optionally assign a custom DNS suffix at the
level of a Network, Account, domain, zone, or entire CloudStack
installation, and a domain administrator can do so within their own
domain. To specify a custom domain name and put it into effect, follow
these steps.

#. Set the DNS suffix at the desired scope

   -  At the Network level, the DNS suffix can be assigned through the
      UI when creating a new Network, as described in
      `“Adding an Additional Guest Network”
      <networking2#adding-an-additional-guest-network>`_ or with the
      updateNetwork command in the CloudStack API.

   -  At the Account, domain, or zone level, the DNS suffix can be
      assigned with the appropriate CloudStack API commands:
      createAccount, editAccount, createDomain, editDomain, createZone,
      or editZone.

   -  At the global level, use the configuration parameter
      guest.domain.suffix. You can also use the CloudStack API command
      updateConfiguration. After modifying this global configuration,
      restart the Management Server to put the new setting into effect.

#. To make the new DNS suffix take effect for an existing Network, call
   the CloudStack API command updateNetwork. This step is not necessary
   when the DNS suffix was specified while creating a new Network.

The source of the Network domain that is used depends on the following
rules.

-  For all Networks, if a Network domain is specified as part of a
   Network's own configuration, that value is used.

-  For an Account-specific Network, the Network domain specified for the
   Account is used. If none is specified, the system looks for a value
   in the domain, zone, and global configuration, in that order.

-  For a domain-specific Network, the Network domain specified for the
   domain is used. If none is specified, the system looks for a value in
   the zone and global configuration, in that order.

-  For a zone-specific Network, the Network domain specified for the
   zone is used. If none is specified, the system looks for a value in
   the global configuration.


Stopping and Restarting the Management Server
---------------------------------------------------

The root administrator will need to stop and restart the Management
Server from time to time.

For example, after changing a global configuration parameter, a restart
is required. If you have multiple Management Server nodes, restart all
of them to put the new parameter value into effect consistently
throughout the cloud..

To stop the Management Server, issue the following command at the
operating system prompt on the Management Server node:

.. code:: bash

   # service cloudstack-management stop

To start the Management Server:

.. code:: bash

   # service cloudstack-management start

