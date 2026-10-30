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
   opts a zone in. The host and zone readiness indicators described below
   are themselves only shown in the UI while the setting is on.

   Turning the setting off does not remove any existing association.
   ``disassociateNetworkFromNic`` and ``changeNicPrimaryNetwork`` are
   refused while the setting is off, so remove any associations an
   Instance still needs removed before disabling it for the zone.

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

#. Restart the CloudStack agent on the host, so CloudStack re-detects
   ``vlan.filtering.enabled`` as true. Only an actual agent restart (or
   reconnect) triggers this re-detection; cancelling maintenance on its
   own does not restart or reconnect the agent, so it will not pick up
   the change by itself.

#. Confirm ``vlan.filtering.enabled`` is now true for the host (host
   details, or the VLAN filtering badge in the UI) before proceeding.

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

-  Storage or Public/Management traffic that is also tagged and shares
   the same physical uplink NIC as guest traffic needs no action here.
   That traffic rides its own dedicated per-VLAN bridge (a kernel VLAN
   sub-interface on the uplink feeding a separate bridge), not the
   VLAN-filtering-enabled guest bridge, so the guest bridge's VLAN
   membership enforcement never applies to it regardless of this
   feature.

-  On a converted host, VLAN 1 is the uplink's untagged segment, so an
   Instance with a NIC on a VLAN 1 network (trunk or not) is not started,
   migrated or live-plugged on a converted host; it is only placed on
   Legacy hosts, where VLAN 1 keeps its own bridge and leaves tagged.

-  If any network already reaches this bridge untagged (for example, an
   existing Shared/L2 network), make sure the uplink keeps a matching
   native/untagged VLAN assignment. Once the bridge enforces VLAN
   membership, untagged traffic with nowhere to classify to is dropped
   just as a missing tagged VLAN would be.

Bridge STP and Forward Delay
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Some bridge management tools (NetworkManager on EL hosts, for example)
enable Spanning Tree Protocol with a 15 second forward delay by default
on a newly created bridge. If the guest bridge is left this way after
converting a host, every new port on it, not just a trunk NIC, spends
about twice the forward delay (around 30 seconds with the default) in
STP's listening and learning states before it forwards any traffic. This
hits a freshly started Instance, a NIC plugged into a running Instance,
and an Instance migrated onto the host equally; it is not specific to
trunk NICs.

As part of converting a host, also disable STP (or set its forward delay
to 0) on the guest bridge, the same way the per-VLAN dynamic bridges
CloudStack creates for a legacy host already have it off by kernel
default:

.. code:: bash

   ip link set dev cloudbr1 type bridge stp_state 0

Make this persistent in whatever network configuration mechanism manages
the bridge, the same as the ``vlan_filtering`` setting above.

If STP is left enabled on a ``vlan_filtering`` host's guest bridge,
CloudStack detects it and adds a non-blocking caution to that host's
entry in the Migrate Instance wizard (and the ``findHostsForMigration``
API), warning of the forward-delay outage. This caution does not prevent
the migration, and only appears there; it is not raised for a freshly
started Instance or a NIC plug, even though those are affected the same
way.

Host Network Changes on a Converted Host
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

On a converted host, the guest taps of running Instances and virtual
routers are ports of the guest bridge that CloudStack added at runtime. The
host's network tool (NetworkManager, for example) does not know about them
and rebuilds the bridge or its port VLANs without them. CloudStack does not
detect this and raises no alert.

.. warning::

   On a converted host with running Instances:

   -  Do not re-activate the guest bridge or uplink connection (for example
      ``nmcli connection up cloudbr1``). Re-activating the guest bridge
      removes every guest tap from it, and all Instances and routers on the
      host lose network until they are restarted.

   -  Do not restart the network service (for example NetworkManager) and
      then re-activate the uplink connection. This makes VLAN 1 the PVID of
      every guest tap, so Instances of different networks end up in one
      VLAN and their traffic leaves the host untagged.

   Before any such network change, put the host into maintenance mode so
   its Instances are migrated off.

This is recoverable. No Instance data is lost, and only the network
attachment of the affected guests is wrong. If it happens anyway, check for
these symptoms on the host:

-  Guest taps are no longer ports of the guest bridge (``bridge link
   show``). The affected Instances and routers have no network.

-  Guest taps show ``1 PVID Egress Untagged`` (``bridge vlan show``). The
   affected Instances and routers are in the wrong VLAN.

To recover, stop and start each affected Instance and reboot each
affected virtual router. Starting or rebooting re-plugs the guest taps with
the correct VLANs, and it is only needed for the guests on that host. An
agent restart alone does not repair the taps. Fix the host network
configuration first, so the guests are not affected again.

A legacy host is not affected, because its guest taps are on per-VLAN
bridges created by the agent.

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
   physical network, in the same zone, and VLAN-isolated.

-  Associations are not limited by VPC: a NIC can carry tiers of
   different VPCs, or a VPC tier on a non-VPC primary network. As with
   multiple NICs, traffic between these networks inside the guest is not
   subject to the VPC network ACLs.

-  Managing associations is an administrator-only operation. A tenant
   cannot create or remove an association on their own NIC.

Guidelines and Limitations
~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Security Groups are not supported on a trunk NIC. Security Group
   rulesets are generated from a NIC's primary address only, which would
   leave an associated network's traffic unfiltered.

-  A VNF appliance's management NIC cannot be trunked. This is rejected
   both at deploy time and on a later ``associateNetworkToNic`` call,
   whatever the appliance's state.

-  A NIC's primary network can only be changed to one of its own
   already-associated networks, and only while the Instance is stopped.
   There is no in-place repointing of a primary network to something it
   was not already associated with.

-  While an Instance has Instance snapshots, a trunk NIC's networks
   cannot be associated, disassociated or made primary; delete the
   snapshots first. Reverting to a snapshot keeps the NIC's associations.

-  Migrating a VM with a trunk NIC is restricted to destination hosts
   with ``vlan.filtering.enabled``, see Migration Behavior below for the
   full picture across host capability combinations.

-  Multi-VLAN trunk NICs are supported only in zones with a single Guest
   physical network. A host's VLAN filtering readiness is detected per
   host, not per physical network, so it is only guaranteed correct when
   there is exactly one. Using trunk NICs in a zone with more than one
   Guest physical network is unsupported in this release.

-  A router's DHCP script is only refreshed by the standard post-upgrade
   Virtual Router restart or live patch (see the
   :doc:`upgrade instructions </upgrading/index>`). Associating or
   disassociating a network on a trunk NIC whose router existed before
   the upgrade, and has not yet been restarted or live-patched since, can
   drop the DHCP entry for the primary or an associated network.

-  An Instance with a trunk NIC cannot be unmanaged (the call is refused
   with an error such as ``Instance [...] has a trunk nic [...] with
   network associations; unmanaging such instances is not supported.``),
   imported, or backed up and restored; restoring a backup today does not
   recreate the NIC's associations.

-  A network on VLAN 1 cannot be on a trunk NIC, as VLAN 1 is the native
   VLAN of the host uplink. Associating it, or deploying with it in
   ``nicnetworkslist``, is refused with ``Network <uuid> is on VLAN 1,
   the native VLAN of the host uplink, and cannot be on a trunk nic``.

-  Assigning an Instance with a trunk NIC to another account
   (``assignVirtualMachine``) requires ``nicnetworkslist``, usable only
   by a root administrator; otherwise the call is refused, as a plain
   move would drop the NIC's associations.

-  Also not supported in this release: VXLAN-isolated associated
   networks, two untagged networks on the same host, and preserving a
   trunk NIC's tap VLAN membership when the host's own network tooling
   recreates its guest bridge (keeping that membership across such a
   recreation is the operator's responsibility). After an in-place
   libvirt upgrade (for example 9 to 11) on a host with running Instances,
   stop and start any Instance with a trunk NIC on that host rather than
   relying on a live transition.

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

Each association is billed separately: associating a network raises its
own ``NETWORK.OFFERING.ASSIGN`` usage event, and disassociating it (or
removing the NIC) raises the matching ``NETWORK.OFFERING.REMOVE`` event,
the same as the primary network's own offering usage.

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
the tag that network was given, bring it up, and obtain an address on it.
The exact commands depend on the guest OS and image; for example, on
Ubuntu 24.04, which ships ``dhcpcd``/``networkctl`` rather than
``dhclient``:

.. code:: bash

   ip link add link eth0 name eth0.1161 type vlan id 1161
   ip link set eth0.1161 up
   dhcpcd -4 eth0.1161

The base interface name (``eth0`` above) depends on the image and is not
guaranteed; it may instead be ``ens3``, ``enp1s0``, or similar.

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
     {"networkId": "2348f240-7587-4ed2-8b87-18c227f36605", "networkName": "appNetwork", "vlan": "1161"}
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

A NIC's own ``listNics`` response carries the same addresses, under
``ip4address``/``ip6address`` for its primary address and
``ip4addresses``/``ip6addresses`` for its secondary and associated
addresses.

Via the API, pass the associated network's own id alongside its address:

.. code:: bash

   cmk enableStaticNat ipaddressid=<public ip id> virtualmachineid=<instance id> \
       vmguestip=<associated network's address> networkid=<associated network id>

   cmk createPortForwardingRule ipaddressid=<public ip id> virtualmachineid=<instance id> \
       vmguestip=<associated network's address> networkid=<associated network id> \
       protocol=tcp privateport=22 publicport=2222

   cmk createLoadBalancerRule algorithm=roundrobin name=<rule name> \
       privateport=80 publicport=80 publicipid=<public ip id> \
       networkid=<associated network id>
   cmk assignToLoadBalancerRule id=<load balancer rule id> \
       virtualmachineid=<instance id> vmguestip=<associated network's address>

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

One exception: Instances and routers powered on out of band after their
host recovered from Down cannot be live migrated until restarted. The
migration is refused with ``Refusing to migrate nic <MAC>: the broadcast
URI of its primary or an associated network is not set``, and the
Instance keeps running on the source host. Reboot the router or stop and
start the Instance, then migrate.

The Migrate Instance wizard surfaces this restriction directly: a
destination host that cannot take the Instance's trunk NIC is marked
unsuitable, with a tooltip explaining why.

.. figure:: /_static/images/trunk-nic-migration-suitability-warning.png
   :align: center
   :alt: Migrate Instance wizard showing a host marked unsuitable because it lacks VLAN filtering
