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
   

Multiple Subnets in Shared Network
----------------------------------

CloudStack provides you with the flexibility to add guest IP ranges from
different subnets in Basic zones and security groups-enabled Advanced
zones. For security groups-enabled Advanced zones, it implies multiple
subnets can be added to the same VLAN. With the addition of this
feature, you will be able to add IP address ranges from the same subnet
or from a different one when IP address are exhausted. This would in
turn allows you to employ higher number of subnets and thus reduce the
address management overhead. You can delete the IP ranges you have
added.


Prerequisites and Guidelines
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  This feature can only be implemented:

   -  on IPv4 addresses

   -  if virtual router is the DHCP provider

   -  on KVM, xenServer, and VMware hypervisors

-  Manually configure the gateway of the new subnet before adding the IP
   range.

-  CloudStack supports only one gateway for a subnet; overlapping
   subnets are not currently supported


Adding Multiple Subnets to a Shared Network
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Infrastructure.

#. On Zones, click View More, then click the zone to which you want to
   work with..

#. Click Physical Network.

#. In the Guest node of the diagram, click Configure.

#. Click Networks.

#. Select the networks you want to work with.

#. Click View IP Ranges.

#. Click Add IP Range.

   The Add IP Range dialog is displayed, as follows:

   |add-ip-range.png|

#. Specify the following:

   All the fields are mandatory.

   -  **Gateway**: The gateway for the tier you create. Ensure that the
      gateway is within the Super CIDR range that you specified while
      creating the VPC, and is not overlapped with the CIDR of any
      existing tier within the VPC.

   -  **Netmask**: The netmask for the tier you create.

      For example, if the VPC CIDR is 10.0.0.0/16 and the network tier
      CIDR is 10.0.1.0/24, the gateway of the tier is 10.0.1.1, and the
      netmask of the tier is 255.255.255.0.

   -  **Start IP/ End IP**: A range of IP addresses that are accessible
      from the Internet and will be allocated to guest VMs. Enter the
      first and last IP addresses that define a range that CloudStack
      can assign to guest VMs .

#. Click OK.


.. |add-ip-range.png| image:: /_static/images/add-ip-range.png
   :alt: adding an IP range to a network.
