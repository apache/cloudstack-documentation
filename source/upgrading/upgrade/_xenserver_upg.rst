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

.. sub-section included in upgrade notes pre 4.4.

XenServer HA
^^^^^^^^^^^^

As of Apache CloudStack 4.4, CloudStack is not responsible to promote a new pool
master on a Citrix XenServer pool. In case of failure of the pool master host,
the responsibility of electing a new pool master as been delegated back to the
HA feature of XenServer. CloudStack remain responsible to honored HA capability
for Compute Offerings of Instances. The XenServer HA feature must be enabled
only for the pool master, not for virtual-machines.


Make sure XenServer has enabled HA on the pool.

To test if poolHA is currently turned on:

.. parsed-literal::

   xe pool-list params=all | grep -E "ha-enabled|ha-config"

Output when poolHA is ON:

.. parsed-literal::

   ha-enabled ( RO): true
   ha-configuration ( RO): timeout: 180

Output when poolHA is OFF:

.. parsed-literal::

   ha-enabled ( RO): false
   ha-configuration ( RO):

To enable poolHA, use something like this:

.. parsed-literal::

   xe pool-enable-ha heartbeat-sr-uuids={SR-UUID} ha-config:timeout=180

Please refer to the `XenServer documentation <http://docs.vmd.citrix.com/XenServer/>`_, as there are multiple ways of configuring it either on NFS, iSCSI or Fibre Channel. Be aware though, that the timeout setting is not documented. The default is 30 seconds so you may want to bump that towards 120-180 seconds.
