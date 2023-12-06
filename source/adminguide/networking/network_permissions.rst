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


Guest Network Permissions
-----------------------------

From Apache CloudStack 4.17.0.0, guest Networks can be shared to other
accounts in the same domain by managing Network permissions.

The following Networks can be shared:

#. L2 Networks not in Project

#. Isolated Networks not in Project

#. Shared Networks with scope is Account

Adding a Network permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select Guest Networks.

#. Select the guest Network you want to work with.

#. Click the Network Permissions tab.

   All the Network permissions that you have created for the Network are
   listed in the page. |network-permissions.png|

#. Click Add Network Permission icon. Provide the following information:

   -  **Account**: The name of the accounts this Network will be shared to.

   -  **Project**. The name of the projects this Network will be shared to.

#. Click OK.

   .. note::
      The accounts/projects are permitted to create Instances on the Network.
      However, they are not permitted to restart and update Network, and
      modify Network rules (e.g. firewall, static nat, load balancer, port
      forwarding).


Removing a Network permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To remove a Network permission, click the Delete Network Permission icon of
the Network permission. |delete-button.png|


Resetting Network permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack provides the ability to reset the Network permissions of a Network.
All Network permissions will be removed. To reset the Network permission, click
the Reset Network Permissions button on the page.


.. |network-permissions.png| image:: /_static/images/network-permissions.png
   :alt: network permissions.
.. |delete-button.png| image:: /_static/images/delete-button.png
   :alt: button to delete.
