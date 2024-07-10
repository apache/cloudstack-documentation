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
   

DNS and DHCP
------------

The Virtual Router & ConfigDrive (since Apache CloudStack 4.20) provides
DNS and DHCP services to the guests. It proxies DNS requests to the DNS
server configured on the Availability Zone.

.. note::
   In case of a network with ConfigDrive, adding/removing nic to/from an
   instance or updating the ip address of a nic will not be reflected in the
   instance if the instance is already running. To do so, run
   `cloud-init clean --machine-id -s` to clean the machine id and seed data.
   Then reboot the instance to apply the changes.