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

Apache CloudStack 4.16.0.0 is a 4.16 LTS release with over 22 major new
features, and over 244 enhancements and fixes since 4.15. Highlights include:

• System VM Template improvements
• CKS Support for Cluster Autoscaling
• Dell EMC VxFlex integration
• Linstor Volume Plugin integration
• Support for OpenSuse
• Support for Rocky Linux
• Granular control of dynamic scaling of VM's CPU/RAM
• Comments in the UI
• Resource Icons
• Bulk actions through the UI
• UI for VM Ingestion
• L2 Networks Persistent modern
• Script cloudstack-setup-databases improvement
• Add mac learning mode in network offering
• API-call to declare host as Degraded
• New API endpoint to update pod management network IP range
• Add New API endpoint: UpdateVlanIpRange

The full list of new features can be found in the project release notes at
http://docs.cloudstack.apache.org/en/4.16.0.0/releasenotes/changes.html

What's New in 4.15.2.0
=======================

Apache CloudStack 4.15.2.0 is a 4.15 LTS release with over 75 fixes and
improvements since 4.15.1.0. Highlights include:

• Several VMware fixes and improvements
• Several UI and VR fixes and improvements

What's New in 4.15.1.0
=======================

Apache CloudStack 4.15.1.0 is a 4.15 LTS release with over 350 enhancements and
fixes since 4.15.0.0. Highlights include:

• Support for XCP-ng 8.2
• Support for VMware 7.0
• Several VMware improvements such as vSphere datastore cluster synchronisation, deploy-as-is OVA template support and VM migration
• Several VR fixes and improvements, support for IKEv2 VPN option
• Several UI fixes and improvements, support for UI customisation and updated localisation

What's New in 4.15.0.0
======================

Apache CloudStack 4.15.0.0 is a 4.15 LTS release with over 15 major new
features, and over 250 enhancements and fixes since 4.14. Highlights include:

• New modern UI (GA release)
• Support for CentOS8 and Ubuntu 20.04 for management server and KVM hosts (note: CentOS 8 will EOL in Dec 2021)
• Support for XCP-ng 8.1
• Support for MySQL 8
• NoVNC console integration
• Unmanaging guest VMs
• VMware advanced storage capabilities (vSAN, vVols, VMFS6, datastore clusters)
• VMware full OVF properties support
• Secondary Storage usage improvements
• PVLAN support for L2 networks
• Role-based users in Projects
• Dynamic roles improvements
• Boot into BIOS on VMware
• Redfish OOBM Support
• Human readable sizes in logs

The full list of new features can be found in the project release notes at
http://docs.cloudstack.apache.org/en/4.15.0.0/releasenotes/changes.html

.. important::
   This version of CloudStack allows control over the visibility of the DNS services provided
   by the Virtual Router in Shared networks. By default CloudStack allows DNS queries via the
   Guest interface from any IP address. This allows for the DNS resolution of guest VMs on the
   Shared network by services outside of the shared network. While this can be useful, it can
   also be an issue on Shared Networks which are using Internet routable/public (i.e. non-RFC1918)
   IP addresses, as the DNS service is then queriable from the public internet at large. A new
   global setting "expose.dns.externally" has been added (with a default value of "true" in
   order to keep backward compatibility) which controls whether the source of DNS queries
   should be limited to only hosts on the Shared Network guest subnet or not. If you wish
   to disable 'outside' access to the DNS services running on Virtual Routers; set the value
   to "false" and recreate the related Virtual Routers.

Apache CloudStack powers numerous elastic Cloud computing services, including solutions that have
ranked as Gartner Magic Quadrant leaders. Highlighted in the Forrester Q4 2017 Enterprise Open Source
Cloud Adoption report, Apache CloudStack "sits beneath hundreds of service provider clouds", including
Fortune 5 multinational corporations. A list of known Apache CloudStack users are available
at http://cloudstack.apache.org/users.html

Libvirt Python Dependency on KVM and CentOS
===========================================

For CentOS users using the security groups feature on KVM it is needed to install the epel-release and python36-libvirt packages.

Workaround for adding newer KVM hosts
=====================================

Newer GNU/Linux distributions with latest OpenSSH package disables some older
SSH algorithms and ciphers and newer algorithms are not supported by trilead-ssh
library used by CloudStack to SSH into KVM hosts during the host-add operation.
Until the dependency library can support that users can use the following
workaround in their KVM host's /etc/ssh/sshd_config and restart ssh server
before adding the KVM host in CloudStack:

   PubkeyAcceptedKeyTypes=+ssh-dss

   HostKeyAlgorithms=+ssh-dss

   KexAlgorithms=+diffie-hellman-group1-sha1

New UI GA and Legacy UI Deprecation and Removal Notice
=======================================================

Cloudstack 4.15 ships with the GA release of a new and modern User Interface as
the default UI which deprecates the current legacy UI. With version 4.15, the
existing legacy UI (deprecated) along with the new UI are the supported UI for
production environments.

The default URL <host>:8080/client will serve the new UI and
<host>:8080/client/legacy will serve the deprecated legacy UI.

In the next release (4.16), the Apache Cloudstack community will remove the legacy
UI. Users are encouraged to implement a migration path towards deprecating the
legacy UI in their production environments.
