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


Using Multiple Guest Networks
-----------------------------

In zones that use advanced networking, additional networks for guest
traffic may be added at any time after the initial installation. You can
also customize the domain name associated with the network by specifying
a DNS suffix for each network.

A instance's networks are defined at instance creation time. An instance cannot add or
remove networks after it has been created, although the user can go into
the guest and remove the IP address from the NIC on a particular
network.

Each instance has just one default network. The virtual router's DHCP reply
will set the guest's default gateway as that for the default network.
Multiple non-default networks may be added to a guest in addition to the
single, required default network. The administrator can control which
networks are available as the default network.

Additional networks can either be available to all accounts or be
assigned to a specific account. Networks that are available to all
accounts are zone-wide. Any user with access to the zone can create an instance
with access to that network. These zone-wide networks provide little or
no isolation between guests.Networks that are assigned to a specific
account provide strong isolation.


Adding an Additional Guest Network
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. Click Add Network and select the Isolated tab. Provide the following information:

   -  **Name**: The name of the network. This will be user-visible.

   -  **Display Text**: The description of the network. This will be
      user-visible.

   -  **Zone**. The name of the zone this network applies to. Each zone
      is a broadcast domain, and therefore each zone has a different IP
      range for the guest network. The administrator must configure the
      IP range for each zone.

   -  **Network offering**: If the administrator has configured multiple
      network offerings, select the one you want to use for this
      network.

   -  **Gateway**: The gateway that the guests should use.

   -  **Netmask**: The netmask in use on the subnet the guests
      will use.

#. Click Create.


Reconfiguring Networks in instances
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack provides you the ability to move instances between networks and
reconfigure an instance's network. You can remove an instance from a network and add
to a new network. You can also change the default network of a virtual
machine. With this functionality, hybrid or traditional server loads can
be accommodated with ease.

This feature is supported on XenServer, VMware, and KVM hypervisors.


Prerequisites
^^^^^^^^^^^^^

Ensure that vm-tools are running on Guest Instances for adding or removing
networks to work on VMware hypervisor.


Adding a Network
^^^^^^^^^^^^^^^^

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, click Instances.

#. Choose the instance that you want to work with.

#. Click the NICs tab.

#. Click Add network to instance.

   The Add network to instance dialog is displayed.

#. In the drop-down list, select the network that you would like to add
   this instance to.

   A new NIC is added for this network. You can view the following
   details in the NICs page:

   -  ID

   -  Network Name

   -  Type

   -  IP Address

   -  Gateway

   -  Netmask

   -  Is default

   -  CIDR (for IPv6)


Removing a Network
^^^^^^^^^^^^^^^^^^

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, click Instances.

#. Choose the instance that you want to work with.

#. Click the NICs tab.

#. Locate the NIC you want to remove.

#. Click Remove NIC button. |remove-nic.png|

#. Click Yes to confirm.


Selecting the Default Network
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, click Instances.

#. Choose the instance that you want to work with.

#. Click the NICs tab.

#. Locate the NIC you want to work with.

#. Click the Set default NIC button. |set-default-nic.png|.

#. Click Yes to confirm.

Changing the Network Offering on a Guest Network
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A user or administrator can change the network offering that is
associated with an existing guest network.

#. Log in to the CloudStack UI as an administrator or end user.

#. If you are changing from a network offering that uses the CloudStack
   virtual router to one that uses external devices as network service
   providers, you must first stop all the instances on the network.

#. In the left navigation, choose Network.

#. Click the name of the network you want to modify.

#. In the Details tab, click Edit. |edit-icon.png|

#. In Network Offering, choose the new network offering, then click
   Apply.

   A prompt is displayed asking whether you want to keep the existing
   CIDR. This is to let you know that if you change the network
   offering, the CIDR will be affected.

   If you upgrade between virtual router as a provider and an external
   network device as provider, acknowledge the change of CIDR to
   continue, so choose Yes.

#. Wait for the update to complete. Don't try to restart instances until the
   network change is complete.

#. If you stopped any instances, restart them.


.. |remove-nic.png| image:: /_static/images/remove-nic.png
   :alt: button to remove a NIC.
.. |set-default-nic.png| image:: /_static/images/set-default-nic.png
   :alt: button to set a NIC as default one.
.. |edit-icon.png| image:: /_static/images/edit-icon.png
   :alt: button to edit.
