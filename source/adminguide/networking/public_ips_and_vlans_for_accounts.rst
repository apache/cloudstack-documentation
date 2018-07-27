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


Reserving Public IP Addresses and VLANs for Accounts
----------------------------------------------------

CloudStack provides you the ability to reserve a set of public IP
addresses and VLANs exclusively for an account. During zone creation,
you can continue defining a set of VLANs and multiple public IP ranges.
This feature extends the functionality to enable you to dedicate a fixed
set of VLANs and guest IP addresses for a tenant.

Note that if an account has consumed all the VLANs and IPs dedicated to
it, the account can acquire two more resources from the system.
CloudStack provides the root admin with two configuration parameter to
modify this default behavior: use.system.public.ips and
use.system.guest.vlans. These global parameters enable the root admin to
disallow an account from acquiring public IPs and guest VLANs from the
system, if the account has dedicated resources and these dedicated
resources have all been consumed. Both these configurations are
configurable at the account level.

This feature provides you the following capabilities:

-  Reserve a VLAN range and public IP address range from an Advanced
   zone and assign it to an account

-  Disassociate a VLAN and public IP address range from an account

-  View the number of public IP addresses allocated to an account

-  Check whether the required range is available and is conforms to
   account limits.

   The maximum IPs per account limit cannot be superseded.


Dedicating IP Address Ranges to an Account
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as administrator.

#. In the left navigation bar, click Infrastructure.

#. In Zones, click View All.

#. Choose the zone you want to work with.

#. Click the Physical Network tab.

#. In the Public node of the diagram, click Configure.

#. Click the IP Ranges tab.

   You can either assign an existing IP range to an account, or create a
   new IP range and assign to an account.

#. To assign an existing IP range to an account, perform the following:

   #. Locate the IP range you want to work with.

   #. Click Add Account |addAccount-icon.png| button.

      The Add Account dialog is displayed.

   #. Specify the following:

      -  **Account**: The account to which you want to assign the IP
         address range.

      -  **Domain**: The domain associated with the account.

      To create a new IP range and assign an account, perform the
      following:

      #. Specify the following:

         -  **Gateway**

         -  **Netmask**

         -  **VLAN**

         -  **Start IP**

         -  **End IP**

         -  **Account**: Perform the following:

            #. Click Account.

               The Add Account page is displayed.

            #. Specify the following:

               -  **Account**: The account to which you want to
                  assign an IP address range.

               -  **Domain**: The domain associated with the
                  account.

            #. Click OK.

      #. Click Add.


Dedicating VLAN Ranges to an Account
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. After the CloudStack Management Server is installed, log in to the
   CloudStack UI as administrator.

#. In the left navigation bar, click Infrastructure.

#. In Zones, click View All.

#. Choose the zone you want to work with.

#. Click the Physical Network tab.

#. In the Guest node of the diagram, click Configure.

#. Select the Dedicated VLAN Ranges tab.

#. Click Dedicate VLAN Range.

   The Dedicate VLAN Range dialog is displayed.

#. Specify the following:

   -  **VLAN Range**: The VLAN range that you want to assign to an
      account.

   -  **Account**: The account to which you want to assign the
      selected VLAN range.

   -  **Domain**: The domain associated with the account.


.. |addAccount-icon.png| image:: /_static/images/addAccount-icon.png
   :alt: button to assign an IP range to an account.
