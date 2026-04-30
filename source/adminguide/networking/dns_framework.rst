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


CloudStack DNS Framework
=======================

Overview
^^^^^^^^
The DNS Framework in Apache CloudStack introduces a pluggable architecture for Domain Name System (DNS) management.
It enables CloudStack to integrate with external DNS providers and manage DNS zones and records as part of cloud orchestration.

This framework is designed with extensibility in mind, allowing additional DNS provider plugins to be added in the future with minimal changes to the core system.

As part of the initial implementation, PowerDNS is the supported DNS provider.

Architecture
^^^^^^^^^^^^
The DNS Framework consists of the following components:

- Core DNS service layer: Defines interfaces and orchestrates DNS operations
- Provider plugins: Implementations for specific DNS providers (e.g., PowerDNS)
- API layer: Exposes DNS functionality to users and administrators
- UI integration: Provides user interface components for DNS management

The framework abstracts provider-specific logic, enabling seamless integration of multiple DNS backends.

Terminology and Hierarchy
^^^^^^^^^^^^^^^^^^^^^^^^^
The DNS Framework introduces several new concepts and entities:

- DNS Provider Type: The underlying software or service facilitating DNS integration (e.g., PowerDNS).
- DNS Server: A configured, operational instance of a DNS Provider Type containing connection details, API endpoints, and access credentials (e.g., NYC-PowerDNS-01).
- DNS Zone: The domain namespace managed by a specific DNS Server (e.g., prod.example.com).
- DNS Record: An individual entry within a DNS zone that maps a domain name to an IP address or other resource.

Capabilities
^^^^^^^^^^^^
The DNS Framework provides two primary capabilities:

- DNS Management: create and manage DNS zones and records.
- Automatic DNS Record Registration: Automatically manages DNS records for Instances based on their lifecycle events.

These capabilities can be used independently or together, depending on deployment requirements and operational preferences.


DNS Server Configuration
^^^^^^^^^^^^^^^^^^^^^^^^

Before using DNS management or automatic DNS record registration, a DNS server must be configured in CloudStack.

A DNS server represents integration between CloudStack and a supported DNS provider (for example, PowerDNS) and includes all necessary connection details and credentials.

UI Overview
-----------

The CloudStack UI has been enhanced to include DNS management capabilities.

DNS Servers and DNS Zones are now available under the **Network** section in the left navigation panel.

.. figure:: /_static/images/dns_server_zone_nav.png
   :width: 300px
   :alt: DNS UI navigation showing DNS Servers and DNS Zones under Network
   :align: center

Adding a DNS Server
-------------------

DNS server configuration is required to manage zones and records in CloudStack.

When adding a DNS server, CloudStack stores the following information:

- Provider type (for example, PowerDNS)
- API endpoint used to communicate with the DNS provider
- Authentication credentials (API key or username/password)
- Name servers used for zone delegation
- Optional metadata such as public accessibility and domain suffix rules

This configuration enables CloudStack to perform DNS operations on behalf of users, including zone creation, record management, and automatic instance DNS registration.

DNS servers can be added either through the CloudStack UI or using the API.

.. image:: /_static/images/add_dns_server.png
   :width: 400px
   :align: center
   :alt: Add DNS Server in CloudStack UI

.. raw:: html

   <br>

Using the API, a DNS server can be added with a command similar to the following:

.. code:: bash

   cmk add dnsserver name="pdns-01" provider="PowerDNS" \
      url="http://<powerdns-ip>:8081" dnsapikey="<api-key>" \
      nameservers="ns1.cloud.internal,ns2.cloud.internal" details[0].pdnsServerId=localhost

**Parameters**

.. list-table::
   :widths: 20 15 65
   :header-rows: 1

   * - Name
     - Required
     - Description
   * - ``name``
     - Yes
     - Unique name for the DNS server
   * - ``provider``
     - Yes
     - DNS provider type (e.g., ``PowerDNS``)
   * - ``url``
     - Yes
     - API URL of the DNS provider
   * - ``dnsapikey``
     - Yes
     - API key or token used for authentication
   * - ``nameservers``
     - Yes
     - Comma separated list of name servers; used to create NS records for the DNS Zone (for example, ns1.example.com, ns2.example.com)
   * - ``dnsusername``
     - No
     - Username or email associated with the DNS provider account
   * - ``details``
     - No
     - Additional provider-specific details in key-value format (e.g., for PowerDNS, ``pdnsServerId`` can be used to specify the server ID in PowerDNS)
   * - ``port``
     - No
     - Port number of the DNS server (if different from default)
   * - ``ispublic``
     - No
     - Specifies whether the DNS server is publicly accessible to other accounts
   * - ``publicdomainsuffix``
     - No
     - Specifies the domain suffix under which the DNS zone is created when the DNS server is not owned by the user (e.g., ``example.com``)

.. note::
   1. Public DNS servers can be used by other accounts, only admin and domain admins can create Public DNS server.
   2. If user creates a DNS zone using non-owned Public DNS server, the zone will be created with a domain suffix defined in the Public DNS server configuration (e.g., if the suffix is ``example.com`` and user creates a zone named ``test.com``, the actual zone created in the DNS provider will be ``test.example.com``).
   3. Nameservers provided during DNS server addition are used for DNS zone creation.


Listing DNS Servers
-------------------

The ``listDnsServers`` API returns DNS servers accessible to the caller.

This includes:

- DNS servers owned by the calling account
- Public DNS servers available in the same domain or any parent domain

.. code:: bash

   cmk list dnsservers


Updating a DNS Server
---------------------

DNS Server configuration can be updated to modify connection details, credentials, name servers, and other metadata. This allows administrators to maintain accurate configurations as DNS provider details change or to update operational parameters without needing to recreate the DNS server.

From UI:

.. image:: /_static/images/update_dns_server.png
   :width: 400px
   :align: center
   :alt: Update DNS Server in CloudStack UI

.. raw:: html

   <br>

Using the API:

.. code:: bash

    cmk update dnsserver id=<dns-server-id> \
         nameservers="ns1.cloud.internal,ns2.cloud.internal,ns3.cloud.internal" \
         name="pdns-new-server"


**Parameters**

.. list-table::
    :widths: 20 15 65
    :header-rows: 1

    * - Name
       - Required
       - Description
    * - ``id``
       - Yes
       - The ID of the DNS server to update
    * - ``nameservers``
       - No
       - Comma separated list of name servers; used to create NS records for the DNS Zone (for example, ns1.example.com, ns2.example.com)
    * - ``name``
       - No
       - Name of the DNS server
    * - ``dnsapikey``
       - No
       - API key or credentials for the external provider
    * - ``ispublic``
       - No
       - Whether this DNS server can be used by accounts other than the owner to create and manage DNS zones
    * - ``port``
       - No
       - Port number of the external DNS server
    * - ``publicdomainsuffix``
       - No
       - Domain suffix that restricts DNS zones created by non-owner accounts to subdomains of this suffix
    * - ``url``
       - No
       - API URL of the provider

.. note:: Updating ``nameservers`` only affects new DNS zones created through this server. Existing DNS zones and their current NS records are not modified.


DNS Zone Management
^^^^^^^^^^^^^^^^^^^

Creating a DNS Zone
-------------------

A DNS zone is always created under an existing DNS server configured in CloudStack, which determines the external DNS provider where the zone will be provisioned and managed.

From UI:

.. image:: /_static/images/create_dns_zone.png
   :width: 400px
   :align: center
   :alt: Create DNS Zone in CloudStack UI

.. raw:: html

   <br>

Using the API:

.. code:: bash

   cmk create dnszone dnsserverid=<dns-server-id> name="example.com" existing=false description="Example DNS zone"


**Parameters**

.. list-table::
   :widths: 20 15 65
   :header-rows: 1

   * - Name
     - Required
     - Description
   * - ``name``
     - Yes
     - The name of the DNS zone (e.g. ``example.com``)
   * - ``dnsserverid``
     - Yes
     - The ID of the DNS server to host this zone
   * - ``description``
     - No
     - The description of the DNS zone
   * - ``existing``
     - No
     - If true, imports an existing DNS zone from the external DNS provider into CloudStack; if false, creates a new DNS zone in both CloudStack and the DNS provider. **Default**: ``false``


Listing DNS Zones
-----------------

The ``listDnsZones`` API returns DNS zones accessible to the caller.

This includes:

- DNS zones owned by the calling account
- Any DNS zones created using DNS servers owned by the caller

.. code:: bash

   cmk list dnszones dnsserverid=<dns-server-id>

Updating a DNS Zone
-------------------

Only description is allowed to be updated.

.. code:: bash

   cmk update dnszone id=<zone-id> description="New description for the DNS zone"


Deleting a DNS Zone
-------------------

Quick action buttons are available in the UI to delete a DNS zone.

From UI:

.. image:: /_static/images/delete_dns_zone.png
   :width: 400px
   :align: center
   :alt: Delete DNS Zone in CloudStack UI

.. raw:: html

   <br>

Using the API:

.. code:: bash

   cmk delete dnszone id=<zone-id> unmanage=false


**Parameters**

.. list-table::
   :widths: 20 15 65
   :header-rows: 1

   * - Name
     - Required
     - Description
   * - ``id``
     - Yes
     - The ID of the DNS zone
   * - ``unmanage``
     - No
     - If false, removes it from both CloudStack and the DNS provider, if true, removes the DNS zone only from CloudStack. **Default**: ``false``


.. note:: Deleting a DNS zone will also delete all DNS records within that zone.


DNS Record Management
^^^^^^^^^^^^^^^^^^^^^

DNS records can be managed using both API and CloudStack UI. In the UI, DNS records are accessible after navigating into a specific DNS zone, where users can perform create, update, and delete operations.

UI Overview
------------

The DNS records can be managed under a selected DNS zone in the CloudStack UI.

.. image:: /_static/images/dns_record_management.png
   :width: 800px
   :align: center
   :alt: DNS record management UI within a DNS zone

.. raw:: html

   <br>

Creating a DNS Record
---------------------

A DNS record represents a mapping between a domain name and its corresponding resource. Records are created within a DNS zone and stored in the configured DNS provider.

**Parameters**

.. list-table::
   :widths: 20 15 65
   :header-rows: 1

   * - Name
     - Required
     - Description
   * - ``dnszoneid``
     - Yes
     - The ID of the DNS zone where the record will be created
   * - ``name``
     - Yes
     - DNS record name (e.g. ``www`` or ``app.example.com``)
   * - ``type``
     - Yes
     - DNS record type (e.g. ``A``, ``AAAA``, ``CNAME``, ``MX``, ``TXT``)
   * - ``contents``
     - Yes
     - Content of the record (IP address for ``A/AAAA``, FQDN for ``CNAME/NS``, quoted string for ``TXT``, etc.)
   * - ``ttl``
     - No
     - Time to live (TTL) value for the record

From UI:

.. image:: /_static/images/create_dns_record.png
   :width: 400px
   :align: center
   :alt: Create DNS Record in CloudStack UI

.. raw:: html

   <br>

From API:

.. code:: bash

   cmk create dnsrecord dnszoneid=<zone-id> name="www" type="A" contents="10.1.1.10" ttl=3600

.. note::
   - The format of ``contents`` depends on the record type.
   - DNS records are immutable, to update a record, it must be deleted and recreated with the new values.

Deleting a DNS Record
---------------------

A DNS record can be deleted from the configured DNS provider using CloudStack. This operation removes the record from the associated DNS zone.

From API:

.. code:: bash

   cmk delete dnsrecord dnszoneid=<zone-id> name="www" type="A"

.. note:: The combination of ``name`` and ``type`` must match an existing record in the zone.


Automatic DNS Record Registration for Instances
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The DNS Framework supports automatic registration and management of DNS records for Instances based on their lifecycle events.

When enabled, CloudStack automatically creates, updates, and removes DNS records corresponding to Instance state changes, ensuring DNS consistency without manual intervention.

Overview
--------

Automatic DNS registration operates at the Instance level and integrates with Instance lifecycle operations.

The feature ensures that DNS records reflect the current state of deployed Instances in real time or near real time, depending on the configured DNS provider behavior.

Behavior
--------

Automatic DNS registration is driven by instance lifecycle events and NIC-level changes within networks that have an associated DNS zone.

**Prerequisites**

Before automatic DNS registration can function, the following conditions must be met:

- A DNS server must be configured in CloudStack
- A DNS zone must be created and associated with the DNS server
- The DNS zone must be associated with a network

If any of the above prerequisites are not met, no automatic DNS operations will be performed.


**Event Mapping**

The following table summarizes DNS record operations:


.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - Event
     - DNS Action
   * - Instance creation
     - Create DNS record using instance hostname and NIC IP
   * - NIC addition (plugged into network with DNS zone)
     - Create DNS record using instance hostname and NIC IP
   * - NIC IP address change
     - Update corresponding DNS record with new IP address
   * - Instance deletion
     - Delete all DNS records associated with the instance
   * - NIC removal (unplugged)
     - Delete DNS record associated with the NIC

Associating a DNS Zone to a Network
-----------------------------------

A DNS zone must be associated with a network before automatic registration can function. Once associated, instance lifecycle events in that network will trigger automatic DNS record creation and management.

This can be done either via the CloudStack UI or API.

From UI:

We can associate a DNS zone to a network using a quick action on the Network by navigating to the **Guest Networks** page.

.. image:: /_static/images/associate_dns_zone_network.png
   :width: 400px
   :align: center
   :alt: Associate DNS Zone to Network in CloudStack UI

.. raw:: html

   <br>

From API:

.. code:: bash

   cmk associate dnszonetonetwork dnszoneid=<dns-zone-id> networkid=<network-id> subdomain=<optional-subdomain>


**Parameters**

.. list-table::
   :widths: 20 15 65
   :header-rows: 1

   * - Name
     - Required
     - Description
   * - ``dnszoneid``
     - Yes
     - The ID of the DNS zone
   * - ``networkid``
     - Yes
     - The ID of the network
   * - ``subdomain``
     - No
     - Optional subdomain to append to the DNS zone (e.g. ``dev`` creates ``vm1.dev.example.com`` for vm1 Instance in the network instead of ``vm1.example.com``)

.. note::
   - Existing Instances in the network are not automatically assigned DNS records.
   - If a DNS zone is associated with multiple networks, instance events from all networks will trigger DNS record management in the same zone, using the subdomain (if provided) to differentiate records between networks.

DNS Naming Convention
---------------------
By default, DNS records are created using the Instance hostname with following format:

.. code:: bash

   <hostname>.<subdomain>.<dns-zone>

``<subdomain>`` is optional based on the association configuration.

For example, if the hostname is ``vm1``, subdomain is ``dev``, and DNS zone is ``example.com``, the resulting DNS record will be ``vm1.dev.example.com``.

In case of DNS record name collision, creation is skipped to avoid inconsistencies.
A warning is logged and an event of type ``DNS.NAME.COLLISION`` is generated for the affected instance.
Users can then choose to manually create a unique DNS record for the instance or update the hostname to resolve the conflict

Instance DNS Information
---------------------
Once a DNS zone is associated with a network, Instances deployed in that network will automatically receive DNS records based on their NIC configuration.

In the Instance details view, the DNS name assigned to each NIC is displayed along with the corresponding IP address. This reflects the DNS record that has been automatically created for the instance.

.. image:: /_static/images/instance_dns_nic.png
   :width: 800px
   :align: center
   :alt: Instance details showing DNS name assigned to NIC

.. raw:: html

   <br>

.. note::
   - This feature requires a properly configured DNS server and an associated DNS zone.
   - Record updates depend on the Instance lifecycle events triggered within CloudStack.
   - Provider synchronization delays may affect DNS propagation time.
   - Manual DNS records created in the same zone may conflict with auto-managed records. In such cases, automatic registration may skip creation and log a collision event.


Disassociating a DNS Zone from a Network
----------------------------------------

A DNS zone can be disassociated from a network, which will stop automatic DNS record management for instances in that network.

Navigate to the **Guest Networks** page, select the network, and use the quick action to disassociate the DNS zone.

Or use the API to disassociate:

.. code:: bash

   cmk disassociate dnszonefromnetwork networkid=<network-id>

.. note::
   - Disassociating a DNS zone from a network does not delete existing DNS records in the DNS provider.
   - After disassociation, no new DNS records will be created or updated for instances in that network.


Limitations
^^^^^^^^^^^

- Automatic DNS registration for Instances is limited to **Shared Networks**
