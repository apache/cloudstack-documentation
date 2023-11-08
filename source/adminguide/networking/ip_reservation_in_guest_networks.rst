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


IP Reservation in Isolated Guest Networks
-----------------------------------------

In isolated guest networks, a part of the guest IP address space can be
reserved for non-CloudStack instances or physical servers. To do so, you
configure a range of Reserved IP addresses by specifying the CIDR when a
guest network is in Implemented state. If your customers wish to have
non-CloudStack controlled instances or physical servers on the same network,
they can share a part of the IP address space that is primarily provided
to the guest network.

In an Advanced zone, an IP address range or a CIDR is assigned to a
network when the network is defined. The CloudStack virtual router acts
as the DHCP server and uses CIDR for assigning IP addresses to the guest
instances. If you decide to reserve CIDR for non-CloudStack purposes, you can
specify a part of the IP address range or the CIDR that should only be
allocated by the DHCP service of the virtual router to the Guest Instances
created in CloudStack. The remaining IPs in that network are called
Reserved IP Range. When IP reservation is configured, the administrator
can add additional instances or physical servers that are not part of
CloudStack to the same network and assign them the Reserved IP
addresses. CloudStack Guest Instances cannot acquire IPs from the Reserved IP
Range.


IP Reservation Considerations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Consider the following before you reserve an IP range for non-CloudStack
machines:

-  IP Reservation is supported only in Isolated networks.

-  IP Reservation can be applied only when the network is in Implemented
   state.

-  No IP Reservation is done by default.

-  Guest instance CIDR you specify must be a subset of the network CIDR.

-  Specify a valid Guest instance CIDR. IP Reservation is applied only if no
   active IPs exist outside the Guest instance CIDR.

   You cannot apply IP Reservation if any instance is alloted with an IP
   address that is outside the Guest instance CIDR.

-  To reset an existing IP Reservation, apply IP reservation by
   specifying the value of network CIDR in the CIDR field.

   For example, the following table describes three scenarios of guest
   network creation:

   .. cssclass:: table-striped table-bordered table-hover

   ===== ============= ============== ============================================== ========================================================
   Case  CIDR          Network CIDR   Reserved IP Range for Non-CloudStack instances Description
   ===== ============= ============== ============================================== ========================================================
   1     10.1.1.0/24   None           None                                           No IP Reservation.
   2     10.1.1.0/26   10.1.1.0/24    10.1.1.64 to 10.1.1.254                        IP Reservation configured by the UpdateNetwork API with
                                                                                     guestvmcidr=10.1.1.0/26 or enter 10.1.1.0/26 in the CIDR
                                                                                     field in the UI.
   3     10.1.1.0/24   None           None                                           Removing IP Reservation by the UpdateNetwork API with
                                                                                     guestvmcidr=10.1.1.0/24 or enter 10.1.1.0/24 in the CIDR
                                                                                     field in the UI.
   ===== ============= ============== ============================================== ========================================================


Limitations
~~~~~~~~~~~

-  The IP Reservation is not supported if active IPs that are found
   outside the Guest instance CIDR.

-  Upgrading network offering which causes a change in CIDR (such as
   upgrading an offering with no external devices to one with external
   devices) IP Reservation becomes void if any. Reconfigure IP
   Reservation in the new re-implemeted network.


Best Practices
~~~~~~~~~~~~~~

Apply IP Reservation to the guest network as soon as the network state
changes to Implemented. If you apply reservation soon after the first
Guest Instance is deployed, lesser conflicts occurs while applying
reservation.


Reserving an IP Range
~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. Click the name of the network you want to modify.

#. Click Edit. |ip-edit-icon.png|

#. In CIDR, specify the Guest instance CIDR.

#. Click Apply.

   Wait for the update to complete. The Network CIDR and the Reserved IP
   Range are displayed on the Details page.


.. |ip-edit-icon.png| image:: /_static/images/edit-icon.png
   :alt: button to edit.
