.. Licensed to the Apache Software Foundation (ASF) under one or more
   contributor license agreements.  See the NOTICE file distributed with this work
   for additional information# regarding copyright ownership. The ASF licenses this
   file to you under the Apache License, Version 2.0 (the "License"); you may not
   use this file except in compliance with the License.  You may obtain a copy of
   the License at http://www.apache.org/licenses/LICENSE-2.0 Unless required by
   applicable law or agreed to in writing, software distributed under the License
   is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
   KIND, either express or implied.  See the License for the specific language
   governing permissions and limitations under the License.


Quota Plugin 
=============

Quota service, while allowing for scalability, will make sure that the cloud is
not exploited by attacks, careless use and program errors. To address this
problem, employ the quota-enforcement service that allows resource
usage within certain bounds as defined by policies and available quotas for
various entities. Quota service extends the functionality of usage server to
provide a measurement for the resources used by the Accounts and domains using a
common unit referred to as cloud currency in this document. It can be configured
to ensure that your usage won’t exceed the budget allocated to Accounts/domain
in cloud currency. It will let users know how much of the cloud resources they are
using. It will help the cloud admins, if they want, to ensure that a user does
not go beyond their allocated quota. Per usage cycle if an Account is found to be
exceeding its quota then it is locked. Locking an Account means that it will not
be able to initiate a new resource allocation request, whether it is more
storage or an additional IP. To unlock an Account you need to add more credit to it.
In case you want the locking to be disabled on global or on Account scope those
provisions are also provided. Needless to say quota service as well as any action
on the Account is configurable.

Enabling the Quota Service 
----------------------------

Before installing and configuring the quota service you need to make sure that
the Usage Server has been installed. This requires extra steps beyond just
installing the CloudStack software. See Installing the Usage Server (Optional)
in the Advanced Installation Guide.

#. enable.usage.server: Set to true to enable usage server.

The quota plugin is disabled by default. To enable it goto Global Settings and
set the following global configuration to true:

#.  quota.enable.service

By default Quota service does not lock the Accounts that have exceeded the quota
usage. To enable quota service to lock Accounts set the following global
configuration to true:

#. quota.enable.enforcement

The other configurations that are there for quota service are as:

#. quota.currency.symbol : The symbol that is used before any currency 
   figure in various quota forms and reports. 
#. quota.usage.smtp.host: Quota SMTP host for sending quota alerts. 
#. quota.usage.smtp.port: Quota SMTP port. 
#. quota.usage.smtp.user: Quota SMTP user. 
#. quota.usage.smtp.password: Quota SMTP password. 
#. quota.usage.smtp.sender: Quota SMTP alert sender email address. 
#. quota.usage.smtp.useAuth: If true, use secure SMTP authentication when sending emails. 
#. quota.usage.smtp.connection.timeout: Quota SMTP server connection timeout duration.

There are several configuration variables that are inherited from usage server, 
these are listed below:

#. usage.aggregation.timezone

All these are described in details in Usage Server documentation.

Restart the Management Server and  the Usage Server to enable the set configuration 
values.

.. code:: bash

   service cloudstack-management restart 
   service cloudstack-usage restart

Once the quota service is running it will calculate the quota balance for each Account.
The quota usage is calculated as per the quota tariff provided by the site administrator.


Quota Tariff
-------------

The following table shows all quota types for which you can specify tariff.

.. cssclass:: table-striped table-bordered table-hover

+------------------+-----------------------------------+--------------------------+
| Type ID          | Type Name                         | Tariff Description       |
|                  |                                   |                          |
+==================+===================================+==========================+
| 1                | RUNNING\_VM                       | One month of running     |
|                  |                                   | Compute-Month            |
+------------------+-----------------------------------+--------------------------+
| 2                | ALLOCATED\_VM                     | One month of allocated   |
|                  |                                   | Instance                 |
+------------------+-----------------------------------+--------------------------+
| 3                | IP\_ADDRESS                       | Quota for a month of     |
|                  |                                   | allocated IP             |
+------------------+-----------------------------------+--------------------------+
| 4                | NETWORK\_BYTES\_SENT              | Quota for 1GB bytes sent |
+------------------+-----------------------------------+--------------------------+
| 5                | NETWORK\_BYTES\_RECEIVED          | Quota for 1GB bytes sent |
+------------------+-----------------------------------+--------------------------+
| 6                | VOLUME                            | Quota for 1 GB of        |
|                  |                                   | Volume use for a month   |
+------------------+-----------------------------------+--------------------------+
| 7                | TEMPLATE                          | Quota for 1 GB of        |
|                  |                                   | Template use for a month |
+------------------+-----------------------------------+--------------------------+
| 8                | ISO                               | Quota for 1 GB of        |
|                  |                                   | ISO use for a month      |
+------------------+-----------------------------------+--------------------------+
| 9                | SNAPSHOT                          | Quota for 1 GB of        |
|                  |                                   | SNAPSHOT use for a month |
+------------------+-----------------------------------+--------------------------+
| 11               | LOAD\_BALANCER\_POLICY            | Quota for load balancer  |
|                  |                                   | policy month             |
+------------------+-----------------------------------+--------------------------+
| 12               | PORT\_FORWARDING\_RULE            | Quota for port forwarding|
|                  |                                   | policy month             |
+------------------+-----------------------------------+--------------------------+
| 13               | NETWORK\_OFFERING                 | Quota for Network        |
|                  |                                   | Offering for a month     |
+------------------+-----------------------------------+--------------------------+
| 14               | VPN\_USERS                        | Quota for VPN usage      |
|                  |                                   | for a month              |
+------------------+-----------------------------------+--------------------------+
| 15               | CPU\_CLOCK\_RATE                  | The tariff for using     |
|                  |                                   | 1 CPU i100 MHz clock     |
+------------------+-----------------------------------+--------------------------+
| 16               | CPU\_NUMBER                       | The quota tariff for     |
|                  |                                   | using 1 virtual CPU.     |
+------------------+-----------------------------------+--------------------------+
| 17               | MEMORY                            | The quota tariff for     |
|                  |                                   | using 1MB RAM size.      |
+------------------+-----------------------------------+--------------------------+

The quota tariff can be listed using listQuotaTariff API.

quotaTariff: Lists all quota tariff plans

The tariff for each of the above can be set by using the updateQuotaTariff API.

Quota Credits
-------------

The quota credit (quotaCredit) API lets you add or remove quota currency credits to
an Account. With this API you can also control the quota enforcement policy at
Account level. This will enable you to have some Accounts where the quota policy is
not enforced. The overall quota enforcement is controlled by the quota.enable.enforcement
global setting.

In addition to above the quota API lets you can fine tune the alert generation by specifying
the quota threshold for each Account. If not explicitly stated, the threshold is taken as 80%
of the last deposit.

Quota Balance
--------------

Quota balance API states the start balance and end balance(optional) from a start date
to end date (optional).
 
Quota Statement
----------------
 
Quota statement for a period consist of the quota usage under various quota types for 
the given period from a start date to an end date.

Quota Monthly Statement
------------------------

Quota service emails the monthly quota statement for the last month at the beginning of
each month. For this service to work properly you need to ensure that the usage server
is running.
 
Quota Alert Management
-----------------------

Quota module also provides APIs to customize various email Templates that are used to
alert Account owners about quota going down below threshold and quota getting over.


All the above functionality is also available via quota UI plugin.
