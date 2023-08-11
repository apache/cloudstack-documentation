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


TroubleShooting
===============

Working with Server Logs
------------------------

The CloudStack Management Server logs all web site, middle tier, and
database activities for diagnostics purposes in
`/var/log/cloudstack/management/`. The CloudStack logs a variety of error
messages. We recommend this command to find the problematic output in
the Management Server log:.

.. note::
   When copying and pasting a command, be sure the command has pasted as a
   single line before executing. Some document viewers may introduce
   unwanted line breaks in copied text.

.. code:: bash

   grep -i -E 'exception|unable|fail|invalid|leak|warn|error' /var/log/cloudstack/management/management-server.log

The CloudStack processes requests with a Job ID. If you find an error in
the logs and you are interested in debugging the issue you can grep for
this job ID in the management server log. For example, suppose that you
find the following ERROR message:

.. code:: bash

   2010-10-04 13:49:32,595 ERROR [cloud.vm.UserVmManagerImpl] (Job-Executor-11:job-1076) Unable to find any host for [User|i-8-42-VM-untagged]

Note that the job ID is 1076. You can track back the events relating to
job 1076 with the following grep:

.. code:: bash

   grep "job-1076)" management-server.log

The CloudStack Agent Server logs its activities in `/var/log/cloudstack/agent/`.


Data Loss on Exported Primary Storage
-------------------------------------

Symptom
~~~~~~~

Loss of existing data on primary storage which has been exposed as a
Linux NFS server export on an iSCSI volume.


Cause
~~~~~

It is possible that a client from outside the intended pool has mounted
the storage. When this occurs, the LVM is wiped and all data in the
volume is lost


Solution
~~~~~~~~

When setting up LUN exports, restrict the range of IP addresses that are
allowed access by specifying a subnet mask. For example:

.. code:: bash

   echo “/export 192.168.1.0/24(rw,async,no_root_squash,no_subtree_check)” > /etc/exports

Adjust the above command to suit your deployment needs.


More Information
~~~~~~~~~~~~~~~~

See the export procedure in the "Secondary Storage" section of the
CloudStack Installation Guide


Recovering a Lost Virtual Router
--------------------------------

Symptom
~~~~~~~

A virtual router is running, but the host is disconnected. A virtual
router no longer functions as expected.


Cause
~~~~~

The Virtual router is lost or down.


Solution
~~~~~~~~

If you are sure that a virtual router is down forever, or no longer
functions as expected, destroy it. You must create one afresh while
keeping the backup router up and running (it is assumed this is in a
redundant router setup):

-  Force stop the router. Use the stopRouter API with forced=true
   parameter to do so.

-  Before you continue with destroying this router, ensure that the
   backup router is running. Otherwise the network connection will be
   lost.

-  Destroy the router by using the destroyRouter API.

Recreate the missing router by using the restartNetwork API with
cleanup=false parameter. For more information about redundant router
setup, see Creating a New Network Offering.

For more information about the API syntax, see the API Reference at
`https://cloudstack.apache.org/api.html <https://cloudstack.apache.org/api.html>`_.


Maintenance mode not working on vCenter
---------------------------------------

Symptom
~~~~~~~

Host was placed in maintenance mode, but still appears live in vCenter.


Cause
~~~~~~

The CloudStack administrator UI was used to place the host in scheduled
maintenance mode. This mode is separate from vCenter's maintenance mode.


Solution
~~~~~~~~

Use vCenter to place the host in maintenance mode.


Unable to deploy Instances from uploaded vSphere Template
---------------------------------------------------------

Symptom
~~~~~~~~

When attempting to create an Instance, it does not deploy.


Cause
~~~~~

If the Template was created by uploading an OVA file that was created
using vSphere Client, it is possible the OVA contained an ISO image. If
it does, the deployment of Instances from the Template will fail.


Solution
~~~~~~~~

Remove the ISO and re-upload the Template.


Unable to power on Instance on VMware
-------------------------------------

Symptom
~~~~~~~

Instance does not power on. You might see errors like:

-  Unable to open Swap File

-  Unable to access a file since it is locked

-  Unable to access Instance configuration


Cause
~~~~~

A known issue on VMware machines. ESX hosts lock certain critical
Instance files and file systems to prevent concurrent changes.
Sometimes the files are not unlocked when the Instance is powered
off. When an Instance attempts to power on, it can not access
these critical files, and the Instance is unable to power on.


Solution
~~~~~~~~

See the following:

`VMware Knowledge Base Article
<http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=10051/>`_


Load balancer rules fail after changing network offering
--------------------------------------------------------

Symptom
~~~~~~~

After changing the network offering on a network, load balancer rules
stop working.


Cause
~~~~~

Load balancing rules were created while using a network service offering
that includes an external load balancer device such as NetScaler, and
later the network service offering changed to one that uses the
CloudStack virtual router.


Solution
~~~~~~~~

Create a firewall rule on the virtual router for each of your existing
load balancing rules so that they continue to function.


Troubleshooting Internet Traffic
--------------------------------

Below are a few troubleshooting steps to check whats going wrong with your
network...


Trouble Shooting Steps
~~~~~~~~~~~~~~~~~~~~~~

#. The switches have to be configured correctly to pass VLAN traffic. You can
   verify if VLAN traffic is working by bringing up a tagged interface on the
   hosts and pinging between them as below...

   On *host1 (kvm1)*

   ::

      kvm1 ~$ vconfig add eth0 64
      kvm1 ~$ ifconfig eth0.64 1.2.3.4 netmask 255.255.255.0 up
      kvm1 ~$ ping 1.2.3.5

   On *host2 (kvm2)*

   ::

      kvm2 ~$ vconfig add eth0 64
      kvm2 ~$ ifconfig eth0.64 1.2.3.5 netmask 255.255.255.0 up
      kvm2 ~$ ping 1.2.3.4

   If the pings dont work, run *tcpdump(8)* all over the place to check
   who is gobbling up the packets. Ultimately, if the switches are not
   configured correctly, CloudStack networking wont work so fix the
   physical networking issues before you proceed to the next steps

#. Ensure `Traffic Labels <http://cloudstack.apache.org/docs/en-US/Apache_CloudStack/4.2.0/html/Installation_Guide/about-physical-networks.html>`_ are set for the Zone.

   Traffic labels need to be set for all hypervisors including
   XenServer, KVM and VMware types. You can configure traffic labels when
   you creating a new zone from the *Add Zone Wizard*.

   .. image:: /_static/images/networking-zone-traffic-labels.png

   On an existing zone, you can modify the traffic labels by going to
   *Infrastructure, Zones, Physical Network, Traffic Types* tab.

   .. image:: /_static/images/networking-infra-traffic-labels.png

   List labels using *CloudMonkey*

   ::

      acs-manager ~$ cloudmonkey list traffictypes physicalnetworkid=41cb7ff6-8eb2-4630-b577-1da25e0e1145
      count = 4
      traffictype:
      id = cd0915fe-a660-4a82-9df7-34aebf90003e
      kvmnetworklabel = cloudbr0
      physicalnetworkid = 41cb7ff6-8eb2-4630-b577-1da25e0e1145
      traffictype = Guest
      xennetworklabel = MGMT
      ========================================================
      id = f5524b8f-6605-41e4-a982-81a356b2a196
      kvmnetworklabel = cloudbr0
      physicalnetworkid = 41cb7ff6-8eb2-4630-b577-1da25e0e1145
      traffictype = Management
      xennetworklabel = MGMT
      ========================================================
      id = 266bad0e-7b68-4242-b3ad-f59739346cfd
      kvmnetworklabel = cloudbr0
      physicalnetworkid = 41cb7ff6-8eb2-4630-b577-1da25e0e1145
      traffictype = Public
      xennetworklabel = MGMT
      ========================================================
      id = a2baad4f-7ce7-45a8-9caf-a0b9240adf04
      kvmnetworklabel = cloudbr0
      physicalnetworkid = 41cb7ff6-8eb2-4630-b577-1da25e0e1145
      traffictype = Storage
      xennetworklabel = MGMT
      =========================================================

#. KVM traffic labels require to be named as *"cloudbr0"*, *"cloudbr2"*,
   *"cloudbrN"* etc and the corresponding bridge must exist on the KVM
   hosts. If you create labels/bridges with any other names, CloudStack
   (atleast earlier versions did) seems to ignore them. CloudStack does not
   create the physical bridges on the KVM hosts, you need to create them
   **before** before adding the host to Cloudstack.

   ::

      kvm1 ~$ ifconfig cloudbr0
      cloudbr0  Link encap:Ethernet  HWaddr 00:0C:29:EF:7D:78
         inet addr:192.168.44.22  Bcast:192.168.44.255  Mask:255.255.255.0
         inet6 addr: fe80::20c:29ff:feef:7d78/64 Scope:Link
         UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:92435 errors:0 dropped:0 overruns:0 frame:0
         TX packets:50596 errors:0 dropped:0 overruns:0 carrier:0
         collisions:0 txqueuelen:0
         RX bytes:94985932 (90.5 MiB)  TX bytes:61635793 (58.7 MiB)

#. The Virtual Router, SSVM, CPVM *public* interface would be bridged to
   a physical interface on the host. In the example below, *cloudbr0* is
   the public interface and CloudStack has correctly created the virtual
   interfaces bridge. This virtual interface to physical interface mapping
   is done automatically by CloudStack using the traffic label settings for
   the Zone. If you have provided correct settings and still dont have a
   working Internet, check the switching layer before you debug any
   further. You can verify traffic using tcpdump on the virtual, physical
   and bridge interfaces.

   ::

      kvm-host1 ~$ brctl show
      bridge name  bridge id           STP enabled interfaces
      breth0-64    8000.000c29ef7d78   no          eth0.64
                                                   vnet2
      cloud0       8000.fe00a9fe0219   no          vnet0
      cloudbr0     8000.000c29ef7d78   no          eth0
                                                   vnet1
                                                   vnet3
      virbr0       8000.5254008e321a   yes         virbr0-nic

   ::

      xenserver1 ~$ brctl show
      bridge name  bridge id           STP enabled interfaces
      xapi0    0000.e2b76d0a1149       no          vif1.0
      xenbr0   0000.000c299b54dc       no          eth0
                                                  xapi1
                                                  vif1.1
                                                  vif1.2

#. Pre-create labels on the XenServer Hosts. Similar to KVM bridge
   setup, traffic labels must also be pre-created on the XenServer hosts
   before adding them to CloudStack.

   ::

      xenserver1 ~$ xe network-list
      uuid ( RO)                : aaa-bbb-ccc-ddd
                name-label ( RW): MGMT
          name-description ( RW):
                    bridge ( RO): xenbr0


#. The Internet would be accessible from both the SSVM and CPVM
   Instances by default. Their public IPs will also be directly pingable
   from the Internet. Please note that these test would work only if your
   switches and traffic labels are configured correctly for your
   environment. If your SSVM/CPVM cant reach the Internet, its very
   unlikely that the Virtual Router (VR) can also the reach the Internet
   suggesting that its either a switching issue or incorrectly assigned
   traffic labels. Fix the SSVM/CPVM issues before you debug VR issues.

   ::

      root@s-1-VM:~# ping -c 3 google.com
      PING google.com (74.125.236.164): 56 data bytes
      64 bytes from 74.125.236.164: icmp_seq=0 ttl=55 time=26.932 ms
      64 bytes from 74.125.236.164: icmp_seq=1 ttl=55 time=29.156 ms
      64 bytes from 74.125.236.164: icmp_seq=2 ttl=55 time=25.000 ms
      --- google.com ping statistics ---
      3 packets transmitted, 3 packets received, 0% packet loss
      round-trip min/avg/max/stddev = 25.000/27.029/29.156/1.698 ms

   ::

      root@v-2-VM:~# ping -c 3 google.com
      PING google.com (74.125.236.164): 56 data bytes
      64 bytes from 74.125.236.164: icmp_seq=0 ttl=55 time=32.125 ms
      64 bytes from 74.125.236.164: icmp_seq=1 ttl=55 time=26.324 ms
      64 bytes from 74.125.236.164: icmp_seq=2 ttl=55 time=37.001 ms
      --- google.com ping statistics ---
      3 packets transmitted, 3 packets received, 0% packet loss
      round-trip min/avg/max/stddev = 26.324/31.817/37.001/4.364 ms


#. The Virtual Router (VR) should also be able to reach the Internet
   without having any Egress rules. The Egress rules only control forwarded
   traffic and not traffic that originates on the VR itself.

   ::

      root@r-4-VM:~# ping -c 3 google.com
      PING google.com (74.125.236.164): 56 data bytes
      64 bytes from 74.125.236.164: icmp_seq=0 ttl=55 time=28.098 ms
      64 bytes from 74.125.236.164: icmp_seq=1 ttl=55 time=34.785 ms
      64 bytes from 74.125.236.164: icmp_seq=2 ttl=55 time=69.179 ms
      --- google.com ping statistics ---
      3 packets transmitted, 3 packets received, 0% packet loss
      round-trip min/avg/max/stddev = 28.098/44.021/69.179/17.998 ms

#. However, the Virtual Router's (VR) Source NAT Public IP address
   **WONT** be reachable until appropriate Ingress rules are
   in place. You can add *Ingress* rules under *Network, Guest Network, IP
   Address, Firewall* setting page.

   .. image:: /_static/images/networking-ingress-rule.png

#. The Instances by default won't be able to access the Internet. Add
   Egress rules to permit traffic.

   .. image:: /_static/images/networking-egress-rule.png

#. Some users have reported that flushing IPTables rules (or changing
   routes) on the SSVM, CPVM or the Virtual Router makes the Internet work.
   This is not expected behaviour and suggests that your networking
   settings are incorrect. No IPtables/route changes are required on the
   SSVM, CPVM or the VR. Go back and double check all your settings.


In a vast majority of the cases, the problem has turned out to be at the
switching layer where the L3 switches were configured incorrectly.

This section was contibuted by Shanker Balan and was originally published on
`Shapeblue's blog <http://shankerbalan.net/blog/internet-not-working-on-cloudstack-vms/>`_

