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


Static NAT
----------

A static NAT rule maps a public IP address to the private IP address of
an instance in order to allow Internet traffic into the instance. The public IP
address always remains the same, which is why it is called static NAT.
This section tells how to enable or disable static NAT for a particular
IP address.


Enabling or Disabling Static NAT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If port forwarding rules are already in effect for an IP address, you
cannot enable static NAT to that IP.

If a Guest Instance is part of more than one network, static NAT rules will
function only if they are defined on the default network.

#. Log in to the CloudStack UI as an administrator or end user.

#. In the left navigation, choose Network.

#. Click the name of the network where you want to work with.

#. Click Public IP Addresses.

#. Click the IP address you want to work with.

#. Click the Static NAT |enabledisablenat.png| button.

   The button toggles between Enable and Disable, depending on whether
   static NAT is currently enabled for the IP address.

#. If you are enabling static NAT, a dialog appears where you can choose
   the destination instance and click Apply.


.. |enabledisablenat.png| image:: /_static/images/enable-disable.png
   :alt: button to enable/disable NAT.
