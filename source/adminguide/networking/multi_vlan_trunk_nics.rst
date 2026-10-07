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


Multi-VLAN Trunk NICs
---------------------

A multi-VLAN trunk NIC lets a single Instance NIC carry traffic for several
guest networks at once, instead of just the one network it is deployed on.
The NIC keeps its usual primary network, delivered untagged exactly as
today, and can additionally be **associated** with one or more other
networks, each delivered to the NIC as its own tagged VLAN. The guest OS
sees ordinary 802.1Q trunked traffic on the NIC and is responsible for
creating a VLAN sub-interface for each associated network it wants to use.

This is supported on KVM only.

Use Cases
~~~~~~~~~

-  **VNF appliances.** A virtual router, firewall, or similar appliance
   often needs to see several Layer 2 segments on one interface, the same
   way it would on a physical trunk port.

-  **Migrating VMware trunk ports to KVM.** A VM that used a VMware trunk
   port to reach multiple VLANs on one vNIC can keep that same topology
   after moving to KVM.

Requirements
~~~~~~~~~~~~

-  The zone-level setting ``multi.network.nic.enabled`` must be enabled.
   It is disabled by default, so this feature is inert until an operator
   opts a zone in.

-  A KVM host can only deliver a trunk NIC if its guest bridge has VLAN
   filtering enabled (``vlan_filtering=1``). CloudStack detects this
   automatically and records it as the ``vlan.filtering.enabled`` host
   detail; hosts without it are never offered as a placement or migration
   destination for a VM with a trunk NIC.

-  Whether libvirt on a given host can express a trunk directly in its
   domain XML (``vlan.trunk.xml.supported``) only changes how the trunk is
   delivered on the wire (native libvirt ``<vlan>`` tags versus a manual
   ``bridge vlan`` fallback); it does not change what the feature can do.

A host's readiness is visible in the UI without needing to inspect its
host details directly: the Hosts list marks a VLAN-filtering-enabled host
with a **VLAN filtering** badge next to its name, and a zone's Resources
tab includes a **Multi-VLAN trunk NIC ready hosts** capacity bar showing
how many of its hosts are ready out of the total.

.. figure:: /_static/images/trunk-nic-host-vlan-filtering-badge.png
   :align: center
   :alt: Hosts list showing the VLAN filtering badge on ready hosts

.. figure:: /_static/images/trunk-nic-zone-readiness-capacity.png
   :align: center
   :alt: Zone Resources tab showing the Multi-VLAN trunk NIC ready hosts capacity bar

Enabling VLAN Filtering on a Host
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``vlan_filtering`` is a property of the host's guest bridge itself, not
something CloudStack sets remotely, so there are two ways to get a host
with it enabled:

-  **Add new hosts with it already set.** The simplest path is to build
   the guest bridge with ``vlan_filtering=1`` from the start when adding
   new capacity, before the host joins the cluster and before any
   Instance is placed on it. There is no workload to evacuate, so none of
   the steps below apply; just make sure the physical uplink prerequisites
   further down are in place before the host goes into service.

-  **Convert an existing host in place.** A host that is already in
   production and carrying Instances needs a brief, careful maintenance
   window instead:

#. Put the host into maintenance mode and confirm every Instance has
   actually moved off it. Do not proceed on the strength of a maintenance
   request alone; verify zero running VMs remain on the host.

   .. code:: bash

      cmk prepareHostForMaintenance id=<host id>

#. On the host itself, enable VLAN filtering on its guest bridge (the
   exact command depends on how the bridge is managed, for example):

   .. code:: bash

      ip link set dev cloudbr1 type bridge vlan_filtering 1

   Make this change persistent in whatever network configuration mechanism
   manages that bridge on the host (netplan, ``ifcfg``, systemd-networkd,
   and so on), so it survives a reboot.

#. Before bringing the host back, also open the VLANs that need to cross
   its physical uplink, see Physical Uplink VLAN Prerequisites below. This
   is just as necessary as the bridge change itself; skipping it does not
   prevent the host from coming back into service, but it will silently
   drop traffic once it does.

#. Restart the CloudStack agent on the host (or simply bring it out of
   maintenance), so CloudStack re-detects ``vlan.filtering.enabled`` as
   true.

#. Take the host out of maintenance.

A cluster can safely contain a mix of converted and not-yet-converted
hosts throughout this process; convert hosts one at a time and confirm
each is correctly detected before moving on to the next.

Physical Uplink VLAN Prerequisites
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack does not manage which VLANs a host's physical uplink is
allowed to carry; that is the operator's responsibility, on the physical
switch port and/or the uplink interface's own configuration. This matters
more once a bridge has VLAN filtering enabled, since the bridge then
enforces VLAN membership on every port, including the uplink itself, not
only the guest taps.

-  Open the zone's entire dynamic guest VLAN range on the uplink, in
   full, up front, before converting any host in that zone. This range is
   already known and bounded by the zone's own configuration, and
   ``specifyvlan=true`` (letting a network request a VLAN outside that
   range) is already restricted to root administrators, so this is a
   one-time, predictable step.

-  Whenever ``specifyvlan=true`` is used to put a network on a VLAN
   outside the zone's normal dynamic range, also open that specific VLAN
   on the uplink at the same time; it falls outside the range already
   opened above.

-  If Storage or Public/Management traffic is also tagged and shares the
   same physical bridge and uplink as guest traffic, rather than having
   its own separate physical NIC, open those VLANs on the uplink as well.
   Once filtering is enabled, the bridge does not distinguish traffic
   type, only VLAN membership; a tagged VLAN that is not explicitly
   allowed gets dropped the same way an unlisted guest VLAN would, even
   if it carries storage or management traffic that has nothing to do
   with this feature.

-  If any network already reaches this bridge untagged (for example, an
   existing Shared/L2 network), make sure the uplink keeps a matching
   native/untagged VLAN assignment. Once the bridge enforces VLAN
   membership, untagged traffic with nowhere to classify to is dropped
   just as a missing tagged VLAN would be.

Key Concepts
~~~~~~~~~~~~

-  A NIC has exactly one **primary** network, delivered native/untagged,
   same as any ordinary NIC.

-  A NIC can additionally have any number of **associated** networks,
   each delivered as its own tagged VLAN. Associating at least one network
   is what makes a NIC a trunk NIC.

-  Associated networks must have non-overlapping subnets from each other
   and from the NIC's primary network, since the guest could not
   otherwise route between them unambiguously.

-  Every network associated with a NIC must be the same type as its
   primary network (for example, all Isolated or all Shared), on the same
   physical network, in the same zone, and VLAN-isolated. An Isolated
   primary network additionally restricts associations to tiers of the
   same VPC, or to other non-VPC networks if the primary is not in a VPC
   itself.

-  Managing associations is an administrator-only operation. A tenant
   cannot create or remove an association on their own NIC.

Guidelines and Limitations
~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Security Groups are not supported on a trunk NIC. Security Group
   rulesets are generated from a NIC's primary address only, which would
   leave an associated network's traffic unfiltered.

-  A VNF appliance's management NIC cannot be trunked. This is rejected
   both at deploy time and on a later ``associateNetworkToNic`` call
   against a Running appliance.

-  A NIC's primary network can only be changed to one of its own
   already-associated networks, and only while the Instance is stopped.
   There is no in-place repointing of a primary network to something it
   was not already associated with.

-  Migrating a VM with a trunk NIC is restricted to destination hosts
   with ``vlan.filtering.enabled``, see Migration Behavior below for the
   full picture across host capability combinations.

Associating and Disassociating Networks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Log in to the CloudStack UI as an administrator.

#. In the left navigation bar, click Instances, then click the name of
   the Instance you want to work with.

#. Click the NICs tab.

#. Use Associate Network / Disassociate Network on the NIC you want to
   change, and choose the network to associate or remove.

.. figure:: /_static/images/trunk-nic-associate-network-nics-tab.png
   :align: center
   :alt: NICs tab showing a NIC's Associate Network action and its existing associated network

.. figure:: /_static/images/trunk-nic-disassociate-network.png
   :align: center
   :alt: Disassociate Network action on an associated network

This can also be done directly via the API:

.. code:: bash

   cmk associateNetworkToNic nicid=<nic id> networkids=<network id>[,<network id>...]

   cmk disassociateNetworkFromNic nicid=<nic id> networkid=<network id>

Both can be called against a Running Instance; the NIC's live VLAN
membership, DHCP, and metadata (see below) are all updated immediately.
``associateNetworkToNic`` optionally accepts ``ipaddresses[N].networkid``/
``ipaddresses[N].ipaddress`` to request a specific address on an
associated network, instead of auto-allocating one.

Changing a Trunk NIC's Primary Network
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

While the Instance is stopped, a trunk NIC's primary network can be
swapped for one of its own associated networks:

.. code:: bash

   cmk changeNicPrimaryNetwork nicid=<nic id> networkid=<already-associated network id>

The operator is responsible for confirming the guest will reacquire an
address on the new primary network (for example via DHCP) after the next
start; CloudStack cannot verify this from the host side.

Deploying an Instance with a Trunk NIC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A trunk NIC can also be requested directly at deploy time, instead of
associating networks afterwards, using the ``nicnetworkslist`` parameter
on ``deployVirtualMachine`` or ``deployVnfAppliance``:

.. code:: bash

   cmk deploy virtualmachine ... \
       "nicnetworkslist[0].networkids=<primary network id>,<associated network id>[,...]"

One entry is given per NIC, in ascending index order; the first network
id in an entry is that NIC's primary network, and any further ids become
associated networks. ``nicnetworkslist`` cannot be combined with
``networkids`` or ``iptonetworklist`` in the same call, and a VNF
appliance's management NIC cannot be requested as a trunk.

In the UI, the same thing is done from the VNF NIC mappings step of the
deploy wizard: click the **+** next to a data-plane NIC's network to open
the Associate Network dialog and pick one or more additional networks for
that NIC.

.. figure:: /_static/images/trunk-nic-vnf-nic-mappings.png
   :align: center
   :alt: VNF NIC mappings step showing Add Associated Networks on a data-plane NIC

.. figure:: /_static/images/trunk-nic-associate-network-modal.png
   :align: center
   :alt: Associate Network dialog at deploy time, selecting additional networks for a NIC

Guest-Side Configuration
~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack does not configure anything inside the guest for an associated
network. The primary network needs nothing extra, since it already
arrives untagged and the guest learns it via DHCP as usual. For each
associated network, the guest must create its own VLAN sub-interface for
the tag that network was given, for example:

.. code:: bash

   ip link add link eth0 name eth0.1161 type vlan id 1161
   dhclient eth0.1161

The VLAN tag for each associated network is visible in the NIC's own API
response (``associatednetworks[].broadcasturi``, as ``vlan://<tag>``), or
can be discovered automatically from inside the guest, see below.

Discovering Associated Networks from Inside the Guest
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hardcoding a VLAN tag into a template only works until that template is
redeployed against a different set of associated networks. To let a boot
script discover its own trunk NIC's associated networks dynamically
instead, CloudStack can expose them through the same metadata service
already used for :doc:`../virtual_machines/user-data`.

This is off by default and controlled per account by the
``account.allow.expose.nic.vlan.mapping`` setting:

.. code:: bash

   cmk updateConfiguration name=account.allow.expose.nic.vlan.mapping value=true accountid=<account id>

Once enabled for an account, every trunk NIC on that account's Instances
gets its own ``nic-vlan-mapping`` metadata entry, fetchable the same way
as any other metadata field:

.. code:: bash

   curl http://data-server./latest/nic-vlan-mapping

The content is a JSON array with one entry per associated network, each
giving that network's id, name, and VLAN tag:

.. code:: json

   [
     {"networkid": "2348f240-7587-4ed2-8b87-18c227f36605", "networkname": "appNetwork", "vlan": 1161}
   ]

A few things worth knowing about this file:

-  It only ever lists **associated** networks, never the primary network.
   The primary arrives untagged on the plain NIC and is already fully
   described by the existing ``local-ipv4`` metadata field, so repeating
   it here would be redundant.

-  It is scoped per NIC, not per Instance. An Instance with more than one
   trunk NIC gets a separate ``nic-vlan-mapping`` file for each one,
   served from that NIC's own primary network's router, each listing only
   that NIC's own associations.

-  It is kept up to date automatically: associating or disassociating a
   network on a Running Instance refreshes the file immediately, the same
   way it refreshes the NIC's live VLAN membership.

Enabling this does not expose anything the guest does not already have
access to by virtue of holding the trunk NIC in the first place; it only
saves the guest from having to learn its own VLAN tags out of band.

Targeting an Associated Network with Static NAT, Port Forwarding, or Load Balancing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Static NAT, Port Forwarding, and Load Balancing rules can all target an
address a NIC holds on one of its associated networks, exactly as they
would its primary address. In the UI, the Add Instance picker for each of
these rule types groups a NIC's addresses under Primary, Secondary IPs,
and Associated Networks, so an associated network's address is clearly
distinguished from an ordinary secondary IP before you pick it.

.. figure:: /_static/images/trunk-nic-rule-ip-picker-grouping.png
   :align: center
   :alt: Enable Static NAT picker grouping a NIC's addresses under Primary, Secondary IPs, and Associated Networks

Via the API, pass the associated network's own id alongside its address:

.. code:: bash

   cmk enableStaticNat ipaddressid=<public ip id> virtualmachineid=<instance id> \
       vmguestip=<associated network's address> networkid=<associated network id>

   cmk createPortForwardingRule ipaddressid=<public ip id> virtualmachineid=<instance id> \
       vmguestip=<associated network's address> networkid=<associated network id> \
       protocol=tcp privateport=22 publicport=2222

Migration Behavior
~~~~~~~~~~~~~~~~~~

A host's relevant capabilities for migration purposes are its two
detected details, ``vlan.filtering.enabled`` and
``vlan.trunk.xml.supported``. Only three combinations matter in practice,
since the second detail has no effect when the first is off:

.. list-table:: Host capability profiles
   :header-rows: 1

   * - Profile
     - ``vlan.filtering.enabled``
     - ``vlan.trunk.xml.supported``
     - Delivery model
   * - Legacy
     - off
     - (irrelevant)
     - Per-VLAN dynamic bridge, one bridge per VLAN. Cannot host a trunk
       NIC at all, see Requirements above.
   * - Shared, manual
     - on
     - off
     - One shared bridge; VLAN membership (including a trunk's tags)
       applied with ``bridge vlan add``.
   * - Shared, native
     - on
     - on
     - One shared bridge; VLAN membership, including a trunk's tags,
       expressed directly in the libvirt domain XML.

These profile names are used by name throughout this guide and in the UI
(for example the host and zone readiness indicators in Requirements
above), so it is worth being precise about what each word means:

-  **Legacy** is a host that has not been converted for this feature at
   all. It keeps CloudStack's original delivery model, a separate dynamic
   bridge per VLAN, and corresponds to ``vlan.filtering.enabled`` being
   off.

-  **Shared** is a host that has been converted (``vlan_filtering=1`` on
   its guest bridge), so every VLAN-tagged guest NIC, trunk or not,
   delivers over that one shared bridge instead of a per-VLAN bridge. It
   refers to this one-shared-bridge delivery model, not to a Shared guest
   network type.

-  **Manual** and **native** only distinguish *how* VLAN membership gets
   applied on that one shared bridge, never what traffic can flow across
   it. **Manual** means CloudStack applies membership itself with
   ``bridge vlan add`` commands, used when the host's libvirt cannot
   express a trunk in its own domain XML. **Native** means libvirt is
   given a ``<vlan>`` block in the domain XML and applies membership
   itself. The two are functionally equivalent to the guest; which one a
   host uses is exactly what ``vlan.trunk.xml.supported`` records, which
   CloudStack derives from the host's libvirt version: libvirt 11.0.0 and
   later support expressing a trunk directly in domain XML, so a host on
   an older libvirt is always detected as manual, regardless of its
   ``vlan_filtering`` setting.

CloudStack rewrites a migrating VM's interface definition to match the
destination host's own profile, so a VM can move between any two hosts
that are both in a Shared profile regardless of which one, with the
exception that a trunk NIC can never reach, or be migrated to, a Legacy
host:

.. list-table:: Migration support, by source and destination profile
   :header-rows: 1
   :stub-columns: 1

   * - Source \\ Destination
     - Legacy
     - Shared, manual
     - Shared, native
   * - **Legacy**
     - Ordinary NIC: supported, unchanged.

       Trunk NIC: not reachable; a trunk NIC is never placed on a Legacy
       host in the first place.
     - Ordinary NIC: supported; bridge renamed to the shared bridge, VLAN
       applied as native/untagged membership.

       Trunk NIC: not reachable, same reason as above.
     - Ordinary NIC: supported; bridge renamed.

       Trunk NIC: not reachable, same reason as above.
   * - **Shared, manual**
     - Ordinary NIC: supported; bridge renamed back to the Legacy model.

       Trunk NIC: blocked; rejected outright since the destination lacks
       ``vlan.filtering.enabled``.
     - Ordinary and Trunk NIC: supported; VLAN membership reapplied with
       ``bridge vlan add`` on the destination.
     - Ordinary and Trunk NIC: supported; membership is upgraded to
       native libvirt ``<vlan>`` XML on the destination.
   * - **Shared, native**
     - Ordinary NIC: supported; bridge renamed, any ``<vlan>`` XML
       stripped.

       Trunk NIC: blocked, same reason as above.
     - Ordinary and Trunk NIC: supported; native ``<vlan>`` XML is
       stripped and replaced with manually-applied ``bridge vlan add``
       membership on the destination.
     - Ordinary and Trunk NIC: supported; native ``<vlan>`` XML is
       preserved.

In short: crossing between a Shared profile and the Legacy profile always
works for an ordinary NIC, and always works between two Shared profiles
for either kind of NIC regardless of which one is manual versus native;
the only hard restriction is that a trunk NIC can never land on a host
that lacks ``vlan.filtering.enabled``, in either direction.

The Migrate Instance wizard surfaces this restriction directly: a
destination host that cannot take the Instance's trunk NIC is marked
unsuitable, with a tooltip explaining why.

.. figure:: /_static/images/trunk-nic-migration-suitability-warning.png
   :align: center
   :alt: Migrate Instance wizard showing a host marked unsuitable because it lacks VLAN filtering
