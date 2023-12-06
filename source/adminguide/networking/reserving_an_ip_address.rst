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


Reserving a Public IP Address
-----------------------

When a public IP address is Free, you can reserve the public IP address.
The public IP address can be reserved to the caller or other accounts.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. Click Public IP Addresses. By default, it displays the Public IP Addresses
   in Allocate state.

#. Filter the Public IP Addresses by state 'Free'

#. Click the Public IP address you want to reserve.

#. Click the Reserve IP button.

   The Reserve Public IP dialog is displayed.

#. In the drop-down list, select the Account Type (Account or Project), Domain,
   and Account or Project that you would like to reserve this Public IP to.

#. Click Submit button.

    Reserved Public IP Addresses can be acquired and used in isolated Networks
    or VPCs of the accounts which the Public IP Addresses are reserved to.

    Reserved Public IP Addresses will be considered as an used Public IP of 
    the account and domain.

Releasing a Reserved Public IP Address
-----------------------

When a public IP address is Reserved, you can release the public IP address so
that the public IP address is ready for use by other accounts.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. Click Public IP Addresses. By default, it displays the Public IP Addresses
   in Allocate state.

#. Filter the Public IP Addresses by state 'Reserved'

#. Click the Public IP address you want to release.

#. Click the Release IP button.

#. Click OK button.

