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
 

The CloudStack API is a low level API that has been used to implement
the CloudStack web UIs. It is also a good basis for implementing other
popular APIs such as EC2/S3 and emerging DMTF standards.

Many CloudStack API calls are asynchronous. These will return a Job ID
immediately when called. This Job ID can be used to query the status of
the job later. Also, status calls on impacted resources will provide
some indication of their state.

The API has a REST-like query basis and returns results in XML or JSON.

See `the Developer’s Guide <https://cwiki.apache.org/confluence/display/CLOUDSTACK/Development+101>`_
and `the API Reference <http://cloudstack.apache.org/docs/api/>`_.


Provisioning and Authentication API
-----------------------------------

CloudStack expects that a customer will have their own user provisioning
infrastructure. It provides APIs to integrate with these existing
systems where the systems call out to CloudStack to add/remove users..

CloudStack supports pluggable authenticators. By default, CloudStack
assumes it is provisioned with the user’s password, and as a result
authentication is done locally. However, external authentication is
possible as well. For example, see Using an LDAP Server for User
Authentication.


User Data and Meta Data
-----------------------

CloudStack provides API access to attach up to 32KB of user data to a
deployed VM. Deployed VMs also have access to instance metadata via the
virtual router.

User data can be accessed once the IP address of the virtual router is
known. Once the IP address is known, use the following steps to access
the user data:

#. Run the following command to find the virtual router.

   .. code:: bash

      # cat /var/lib/dhclient/dhclient-eth0.leases | grep dhcp-server-identifier | tail -1

#. Access user data by running the following command using the result of
   the above command

   .. code:: bash

      # curl http://10.1.1.1/latest/user-data

Meta Data can be accessed similarly, using a URL of the form
http://10.1.1.1/latest/meta-data/{metadata type}. (For backwards
compatibility, the previous URL http://10.1.1.1/latest/{metadata type}
is also supported.) For metadata type, use one of the following:

-  service-offering. A description of the VMs service offering

-  availability-zone. The Zone name

-  local-ipv4. The guest IP of the VM

-  local-hostname. The hostname of the VM

-  public-ipv4. The first public IP for the router. (E.g. the first IP
   of eth2)

-  public-hostname. This is the same as public-ipv4

-  instance-id. The instance name of the VM


