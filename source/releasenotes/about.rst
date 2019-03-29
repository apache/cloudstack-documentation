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


What's New in |release|
=======================
Version |release| is a |version| non-LTS release adding multiple features for those who want to access a fresh CloudStack prior to our next LTS.
|release| combines 12 months of work and adds +200 commits, with multiple new features and fixes.

Some of the changes are presented in this quick summary (this is not a complete list):

* Allow users of all types to create L2 networks
* systemd: Fix -Dpid arg passing to systemd usage service
* Add back ability to disable backup of snapshot to
* keystore: don't restart systemvm cloud.service post cert
* Keep iotune section in the VM's XML after live migration
* Copy template to target KVM host if needed when migrating local <> local storage
* systemd: fix services to allow TLS configurations via
* java.security.ciphers
* feature: add libvirt / qemu io bursting
* Add back ability to disable backup of snapshot to secondary
* API: add command to list management servers
* UI: Fix "Migrate instance to another host" popup modal
* UI: Fix issue with verification of ipv4/ipv6 address.
* UI: Fix UI bug: Create Network Offering Popup has no fields
* UI: Update jquery and related libraries
* network: Offerings do not have to have Security Grouping enabled
* Vmware offline migration
* IP address acquired with associate ip address is marked as source nat
* ipv6: allow Secondary IPv6 addresses to be EUI-64
* ipv6: Send userdata to Virtual Router if IPv6 is enabled
* ipv6: Calculate IPv6 address instead of fetching one from a pool
* ipv6: Advanced Networking Security Groups are supported
* ipv6: Allow specification of IPv6 details when creating Basic network
* Enable remote debugging for the management server, usage server, and KVM agent
* Security Group: add secondary ips to the correct ipset based on ip family (4.11)
* Security Group: add secondary ips to the correct ipset
* XenServer: fix Security Groups 'vmops' script
* XenServer: Support online storage migration from non-managed to managed storage
* KVM: Security Group enhancements and refactor old code
* KVM: Properly report available memory to Management Server
* KVM: Add influxdb to statscollector
* KVM: Refactory VXLAN script and add IPv6 support
* KVM: Set amount of queues for Virtio SCSI driver to vCPU of Instance
* KVM: Use 'ip route show default 0.0.0.0/0' to find the default gateway
* KVM: Add KVM Guest OS mapping for Windows Server 2019
* KVM: Enable DPDK support on KVM
* Prevent corner case for infinite PrepareForMaintenance
* Enhance bypass vlan overlap checkAllow KVM VM live migration with ROOT volume on file storage type
* Destroy VM also removes volumes
* Users are able to change/edit the protocol of an ACL rule
* allows to remove local primary storage
* Allow password enabled for iso (#2745)
* Support requesting a specific IPv4 address in Basic Networking during Instance creation
* Adding zone disablement during deletion of the range
* Display mac address in nic detail view
* Cleanup methods, classes, and POMs


What's New in 4.11.2.0
----------------------

The new 4.11.2.0 version is a 4.11 maintainance release containing over 70
fixes and improvements on the 4.11.1.0 release.


What's New in 4.11.1.0
----------------------

The new 4.11.1.0 version is a 4.11 maintainance release containing over 140
fixes and improvements on the 4.11.0.0 release.

These include the speeding up of virtual router deployments and fixes for corner cases
effecting the new config drive and L2 features and some hypervisor specific fixes to improve compatibility
with current hypervisor versions including the XCP-ng fork of XenServer.

What's New in 4.11.0.0
----------------------

Version 4.11.0.0 included more than 400 commits, 220 pull requests that fixes
more than 250 issues since the last release. Version 4.11.0.0 was a large
release that was worked on for 8 months.

A LOT changed in this release, so this is not a complete list, but here is a
quick summary of some of the changes:

* Support for XenServer 7.1, 7.2, 7.3 and 7.4, and support for XCP-ng 7.4.
* Improved support for VMware 6.5.
* Host-HA framework and HA-provider for KVM hosts with and NFS as primary storage, and a new background polling task manager.
* Secure agents communication: new certificate authority framework and a default built-in root CA provider.
* New network type - L2.
* CloudStack metrics exporter for Prometheus.
* Cloudian Hyperstore connector for CloudStack.
* Annotation feature for CloudStack entities such as hosts.
* Separation of volume snapshot creation on primary storage and backing operation on secondary storage.
* Limit admin access from specified CIDRs.
* Expansion of Management IP Range.
* Dedication of public IPs to SSVM and CPVM.
* Support for separate subnet for SSVM and CPVM.
* Bypass secondary storage template copy/transfer for KVM.
* Support for multi-disk OVA template for VMware.
* Storage overprovisioning for local storage.
* LDAP mapping with domain scope, and mapping of LDAP group to an account.
* Move user across accounts.
* Managed storage enhancements.
* Extend config drive support for user data, metadata, and password (Nuage Networks).
* Extra DHCP options support (Nuage Networks).
* Nuage VSP 5.0 support and caching of NuageVsp ID's.
* Nuage domain template selection per VPC and support for network migration.
* Support for watchdog timer to KVM Instances.
* Support for Secondary IPv6 Addresses and Subnets.
* IPv6 Prefix Delegation support in basic networking.
* Ability to specific MAC address while deploying VM or adding a NIC to a VM.
* VMware dvSwitch security policies configuration in network offering
* Allow more than 7 NICs to be added to a VMware VM.
* Network rate usage for guest offering for VRs.
* Usage metrics for VM snapshot on primary storage.
* Enable Netscaler inline mode.
* NCC integration in CloudStack.
* The retirement of the Midonet network plugin.
* Several UI Improvements.
* Embedded Jetty and improved CloudStack management server configuration.
* Improved support for Java 8 for building artifacts/modules, packaging, and in
  the systemvm template.
* A faster console proxy startup and service availability.
* A new Debian 9 based smaller systemvm template that patches systemvm without
  requiring reboot.
* Several optimizations and improvements to the virtual router including better
  support for redundant virtual routers and strongswan provided s2s and remote
  access vpn.

