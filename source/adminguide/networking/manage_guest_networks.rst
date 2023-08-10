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


Editing, Restarting, and Removing a Guest Network
--------------------------------------------------

.. note:: Ensure that all the Instances are removed before you remove a guest Network.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. In the Select view, select Guest Networks.

   All the guest Networks that you have created for the account are listed in the
   page.

#. Select the guest Network you want to work with.

#. In the Details tab, click the "Delete Network" button

   You can also remove the guest Network by using the remove button in the Quick
   View.

   You can edit the name, description, Network offering, CIDR, Network domain of a
   guest Network. To do that, click the "Edit" button.

   To restart a guest Network, click the "Restart Network" button. Please note
   all services provided by this Network will be interrupted. When you enable "Clean up",
   the virtual routers of guest Network will be destroyed and new virtual routers will
   be provisioned.
