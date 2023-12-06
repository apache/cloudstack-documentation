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


Using Remote Access VPN
=======================

.. sidebar:: Clients
   :subtitle: Per Operating System instructions

   .. contents::
      :local: 
      :depth: 1

Remote Access VPN connection to VPC or Guest Network to access Instances and applications. This section considers you have enabled Remote acccess VPN, refer to: :ref:`remote-access-vpn`.

When connected to a VPC via VPN, the client have access to all Network Tiers.

Following information is required to confiture VPN client:

   - ``Public IP``: source NAT with VPN enabled.
   - ``IPsec pre-shared key``: Provide at the VPN activation.
   - ``Username`` VPN account username. 
   - ``Password`` VPN account password.


Mac OSX
-------

Mac OSX provide native IPsec VPN client.

#. Into System Preferences -> Network 

#. Click "+" button and add a VPN:

   - Interface: VPN
   - VPN Type: L2TP over IPSec
   - Service Name: (ex: test-vpc1)

   .. image:: /_static/images/vpn/osxvpn_netconf.png
      :align: center 
      :width: 400 px

#. Configure L2TP over IPsec

   .. image:: /_static/images/vpn/osxvpn_form1.png
      :align: center
      :width: 400 px

   .. image:: /_static/images/vpn/osxvpn_form2.png
      :align: center
      :width: 400 px 

#. Inside Authentication Settings...

   .. image:: /_static/images/vpn/osxvpn_form3.png
      :align: center
      :width: 400 px 

#. Connect into VPN

   #. Click Apply to apply Network configuration changes.
   #. Click Connect to initiate VPN connection.

      .. image:: /_static/images/vpn/osxvpn_connected.png
         :align: center
         :width: 400 px


Microsoft Windows 8
-------------------

Following instruction have been perform using Windows 8.1 using Native VPN client.

#. Create network VPN connection

   .. image:: /_static/images/vpn/win1.png
      :align: center 
      :width: 400 px

   .. image:: /_static/images/vpn/win2.png
      :align: center 
      :width: 400 px

   .. image:: /_static/images/vpn/win3.png
      :align: center 
      :width: 400 px

   .. image:: /_static/images/vpn/win4.png
      :align: center 
      :width: 400 px

   .. image:: /_static/images/vpn/win5.png
      :align: center 
      :width: 400 px

   .. image:: /_static/images/vpn/win6.png
      :align: center 
      :width: 400 px


#. Configure VPN settings

   .. image:: /_static/images/vpn/win7.png
      :align: center 
      :width: 400 px

   .. image:: /_static/images/vpn/win8.png
      :align: center 
      :width: 400 px

   .. image:: /_static/images/vpn/win9.png
      :align: center 
      :width: 400 px

   .. image:: /_static/images/vpn/win10.png
      :align: center 
      :width: 400 px

   .. image:: /_static/images/vpn/win11.png
      :align: center 
      :width: 400 px

#. Initiate VPN connection

   .. image:: /_static/images/vpn/win12.png
      :align: center 
      :width: 400 px

   .. image:: /_static/images/vpn/win13.png
      :align: center 
      :width: 400 px

   .. image:: /_static/images/vpn/win14.png
      :align: center 
      :width: 400 px
