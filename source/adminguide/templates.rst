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

Working With Templates
=======================

A Template is a reusable configuration for Instances. When Users
launch Instances, they can choose from a list of Templates in CloudStack.

Specifically, a Template is a virtual disk image that includes one of a
variety of operating systems, optional additional software such as
office applications, and settings such as access control to determine
who can use the Template. Each Template is associated with a particular
type of hypervisor, which is specified when the Template is added to
CloudStack.

CloudStack ships with a default Template. In order to present more
choices to Users, CloudStack administrators and Users can create
Templates and add them to CloudStack.


Creating Templates: Overview
----------------------------

CloudStack ships with a default Template for the CentOS operating
system. There are a variety of ways to add more Templates.
Administrators and end Users can add Templates. The typical sequence of
events is:

#. Launch an Instance that has the operating system you want. Make any
   other desired configuration changes to the Instance.

#. Stop the Instance.

#. Convert the volume into a Template.

There are other ways to add Templates to CloudStack. For example, you
can take a Snapshot of the Instance's volume and create a Template from the
Snapshot, or import a VHD from another system into CloudStack.

The various techniques for creating Templates are described in the next
few sections.


Requirements for Templates
--------------------------

-  For XenServer, install PV drivers / Xen tools on each Template that
   you create. This will enable live migration and clean guest shutdown.

-  For vSphere, install VMware Tools on each Template that you create.
   This will enable console view to work properly.


Best Practices for Templates
----------------------------

If you plan to use large Templates (100 GB or larger), be sure you have
a 10-gigabit Network to support the large Templates. A slower Network
can lead to timeouts and other errors when large Templates are used.


The Default Template
--------------------

CloudStack includes a CentOS Template. This Template is downloaded by
the Secondary Storage VM after the primary and secondary storage are
configured. You can use this Template in your production deployment or
you can delete it and use custom Templates.

The root password for the default Template is "password".

A default Template is provided for each of XenServer, KVM, and vSphere.
The Templates that are downloaded depend on the hypervisor type that is
available in your cloud. Each Template is approximately 2.5 GB physical
size.

The default Template includes the standard iptables rules, which will
block most access to the Template excluding ssh.

.. code:: bash

   # iptables --list
   Chain INPUT (policy ACCEPT)
   target     prot opt source               destination
   RH-Firewall-1-INPUT  all  --  anywhere             anywhere

   Chain FORWARD (policy ACCEPT)
   target     prot opt source               destination
   RH-Firewall-1-INPUT  all  --  anywhere             anywhere

   Chain OUTPUT (policy ACCEPT)
   target     prot opt source               destination

   Chain RH-Firewall-1-INPUT (2 references)
   target     prot opt source               destination
   ACCEPT     all  --  anywhere             anywhere
   ACCEPT     icmp --  anywhere        anywhere       icmp any
   ACCEPT     esp  --  anywhere        anywhere
   ACCEPT     ah   --  anywhere        anywhere
   ACCEPT     udp  --  anywhere        224.0.0.251    udp dpt:mdns
   ACCEPT     udp  --  anywhere        anywhere       udp dpt:ipp
   ACCEPT     tcp  --  anywhere        anywhere       tcp dpt:ipp
   ACCEPT     all  --  anywhere        anywhere       state RELATED,ESTABLISHED
   ACCEPT     tcp  --  anywhere        anywhere       state NEW tcp dpt:ssh
   REJECT     all  --  anywhere        anywhere       reject-with icmp-host-


Private and Public Templates
----------------------------

When a User creates a Template, it can be designated private or public.

Private Templates are only available to the User who created them. By
default, an uploaded Template is private.

When a User marks a Template as “public,” the Template becomes available
to all Users in all Accounts in the User's domain, as well as Users in
any other domains that have access to the Zone where the Template is
stored. This depends on whether the Zone, in turn, was defined as
private or public. A private Zone is assigned to a single domain, and a
public Zone is accessible to any domain. If a public Template is created
in a private Zone, it is available only to Users in the domain assigned
to that Zone. If a public Template is created in a public Zone, it is
available to all Users in all domains.


Creating a Template from an Existing Instance
---------------------------------------------

Once you have at least one Instance set up in the way you want, you can use it
as the prototype for other Instances.

#. Create and start an Instance using any of the techniques given
   in `“Creating Instances” <virtual_machines.html#creating-instances>`_.

#. Make any desired configuration changes on the running Instance, then click
   Stop.

#. Wait for the Instance to stop. When the status shows Stopped, go to the
   next step.

#. Go into "View Volumes" and select the Volume having the type "ROOT".

#. Click Create Template and provide the following:

   -  **Name and Display Text**. These will be shown in the UI, so
      choose something descriptive.

   -  **OS Type**. (Except for VMware). This helps CloudStack and the hypervisor perform
      certain operations and make assumptions that improve the
      performance of the guest. Select one of the following.

      -  If the operating system of the stopped Instance is listed, choose it.

      -  If the OS type of the stopped Instance is not listed, choose Other.

      -  If you want to boot from this Template in PV mode, choose Other
         PV (32-bit) or Other PV (64-bit). This choice is available only
         for XenServer:

         .. note::
            Generally you should not choose an older version of the OS
            than the version in the image. For example, choosing CentOS
            5.4 to support a CentOS 6.2 image will in general not work.
            In those cases you should choose Other.


   -  **Public**. Choose Yes to make this Template accessible to all
      Users of this CloudStack installation. The Template will appear in
      the Community Templates list. See `“Private and
      Public Templates” <#private-and-public-templates>`_.

   -  **Password Enabled**. Choose Yes if your Template has the
      CloudStack password change script installed. See
      :ref:`adding-password-management-to-templates`.

#. Click Add.

The new Template will be visible in the Templates section when the
Template creation process has been completed. The Template is then
available when creating a new Instance.

.. note::
   Since version 4.15, CloudStack obtains information from the VMware Templates
   automatically at registration time. If a Template contains different deployment
   options (or configurations) as in the case of virtual appliances, then CloudStack
   display the information required by the Template, allowing Users or administrators
   to configure their Instances.

Creating a Template from a Snapshot
-----------------------------------

If you do not want to stop the Instance in order to use the Create Template
menu item (as described in `“Creating a Template from an Existing
Instance” <#creating-a-template-from-an-existing-virtual-machine>`_),
you can create a Template directly from any Snapshot through the
CloudStack UI.


Uploading Templates from a remote HTTP server
---------------------------------------------



vSphere Templates and ISOs
^^^^^^^^^^^^^^^^^^^^^^^^^^
.. warning::
      If you are uploading a Template that was created using vSphere Client,
      be sure the OVA file does not contain an ISO. If it does, the deployment
      of Instances from the Template will fail

Templates are uploaded based on a URL. HTTP is the supported access
protocol. Templates are frequently large files. You can optionally gzip
them to decrease upload times.

To upload a Template:

#. In the left navigation bar, click Templates.

#. Click Register Template.

#. Provide the following:

   -  **Name and Description**. These will be shown in the UI, so choose
      something descriptive.

   -  **URL**. The Management Server will download the file from the
      specified URL, such as ``http://my.web.server/filename.vhd.gz``.

   -  **Zone**. Choose the zone where you want the Template to be
      available, or All Zones to make it available throughout
      CloudStack.

   - **Read Instance settings from OVA**. (VMware only) If selected, the registered Template will allow Users to deploy Instances as clones of the Template, including all their properties, configurations, end-user license agreements, disks, os type, etc. This option allows Users to register virtual appliances. See `Support for Virtual Appliances <virtual_machines.html#about-virtual-appliances>`_.

      .. note:: 
         When this option is selected the following fields are hidden: Root disk controller, Keyboard type and OS Type. 

   -  **OS Type**: This helps CloudStack and the hypervisor perform
      certain operations and make assumptions that improve the
      performance of the guest. Select one of the following:

      -  If the operating system of the stopped Instance is listed, choose it.

      -  If the OS type of the stopped Instance is not listed, choose Other.

         .. note::
            You should not choose an older version of the OS than the
            version in the image. For example, choosing CentOS 5.4 to
            support a CentOS 6.2 image will in general not work. In
            those cases you should choose Other.

         .. note::
            Since version 4.15.1, VMware Templates do not allow Users or administrators
            selecting an OS Type when registering a Template if the option 'Read Instance settings from OVA' is selected. In this case, the OS Type is
            obtained from the Template after it is registered.

   -  **Userdata**: The registered Userdata are listed. Select the
      desired one.

   -  **Userdata link policy**: Select the userdata override policy as required. 
      For more information on userdata and override link policy, please check `Userdata section <virtual_machines.html#user-data-and-meta-data>`_.


   -  **Hypervisor**: The supported hypervisors are listed. Select the
      desired one.

   -  **Format**. The format of the Template upload file, such as VHD or
      OVA.

   -  **Extractable**. Choose Yes if the Template is available for
      extraction. If this option is selected, end Users can download a
      full image of a Template.

   -  **Public**. Choose Yes to make this Template accessible to all
      Users of this CloudStack installation. The Template will appear in
      the Community Templates list. See `“Private and
      Public Templates” <#private-and-public-templates>`_.

   -  **Featured**. Choose Yes if you would like this Template to be
      more prominent for Users to select. The Template will appear in
      the Featured Templates list. Only an administrator can make a
      Template Featured.

Note that uploading multi-disk Templates is also supported.

.. note:: 
   VMware only: If the Template is registered with the option 'Read Instance settings
   from OVA' then the Instance deployment wizard will display all the available OVF
   properties, different deployment options or configurations, multiple NICs or
   end-user license agreements.

   See `Support for Virtual Appliances <virtual_machines.html#about-virtual-appliances>`_.



.. include:: templates/_bypass-secondary-storage-kvm.rst



Uploading Templates and ISOs from a local computer
-------------------------------------------

It's also possible to upload an already prepared Template or an ISO from your local computer.
The steps are similar as when Uploading a Template/ISO from a remote HTTP server, except that you need to choose a local Template/ISO file from your PC.
For this feature to work, your SSVMs must be supporting HTTPS (for more info please visit `“Using a SSL Certificate for the Console Proxy”
<systemvm.html#using-a-ssl-certificate-for-the-console-proxy>`_).

Example GUI dialog of uploading Template/ISO from local (browser) is given below:

|template-upload-from-local.png|

|upload-iso-from-local.png|

Note that uploading multi-disk Templates is also supported.

Sharing Templates and ISOs with other Accounts/projects
-------------------------------------------------------

When adding a Template/ISO, the owner can choose to make Template/ISO public or to keep it private. Once the Template/ISO is created, the owner can choose to share this Template/ISO so that other Accounts/Projects can also use the Template/ISO.

Currently, the owners can share their Template/ISO with:
  - other Accounts inside their own domain (i.e. can't share the Template/ISO with other Accounts in the subdomain of their domain or any other domains)
  - projects where they belongs to (i.e. projects where they are the owners/creators or other projects where they have been joined)

Template/ISO permissions can be changed via updateTemplatePermissions/updateIsoPermissions API call or via GUI. It is supported to add, remove or reset (remove all) Template/ISO permissions.

When adding or removing permissions to/from a Template/ISO, it is required to specify Account/Project name which is being added/removed from the Template/ISO permissions.

Global setting "allow.user.view.all.domain.accounts" has a default value of "false". This makes sure that when the regular Users (of a "User" role) wants to share a Template/ISO via GUI, they will not be shown the list of all Accounts in their domain and they will need to know the name of the destination Account with which they are sharing the Template/ISO. This makes sense in public clouds where each Account of a single domain is a different tenant/customer and privacy is imperative. In this case, the User will be presented with an input field to enter the Account name, as on the images below:

.. warning::
      The images displayed below refer to Template permissions, but the same applies for ISO permissions.

|template-permissions-update-manually-1.png|

Sharing the Template with Account "user2"

|template-permissions-update-manually-2.png|

Revoking permissions from Account "user2"

But in environments where privacy within a domain is not an issue, setting "allow.user.view.all.domain.accounts" setting to "true" will make sure that the User, who is sharing the Template, will be presented a more User-friendly multi-select list, listing all the Accounts in their domain. This is shown in the images below;

|template-permissions-update-1.png|

Sharing the Template with just Account "user8"

|template-permissions-update-2.png|

Sharing Template with 2 specific projects

|template-permissions-update-3.png|

Revoking permissions from Account "user8"

|template-permissions-update-4.png|

Revoking permissions from both projects previously added


Finally, Template permissions can be reset:

|template-permissions-update-5.png|

Resetting (removing all) permissions

.. warning::
      Project-owned Templates are not supported to be shared outside of
      the Project, and if attempted to do so, a proper error message is shown.

Exporting Templates
-------------------

End Users and Administrators may export Templates from the CloudStack.
Navigate to the Template in the UI and choose the Download function from
the Actions menu.

.. include:: templates/_create_linux.rst

.. include:: templates/_create_windows.rst

.. include:: templates/_import_ami.rst

.. include:: templates/_convert_hyperv.rst

.. include:: templates/_password.rst


Deleting Templates
------------------

Templates may be deleted. However when the Templates are used the default 
behaviour is to refuse deletion. In general, when a Template spans multiple
Zones, only the copy that is selected for deletion will be deleted; the
same Template in other Zones will not be deleted. The provided CentOS
Template is an exception to this. If the provided CentOS Template is
deleted, it will be deleted from all Zones.

When Templates are deleted, the Instances instantiated from them will continue
to run. However, new Instances cannot be created based on the deleted
Template.

As said, Cloudstack refuses to delete a template when VMs based on the
template exist. If this is the case, the parameter "forced" can be set 
to "true" to delete the template anyways. These VMs can no longer be
reinstalled from that template, but will be unaffected otherwise.

Working with ISOs
===================

CloudStack supports ISOs and their attachment to Guest Instances. An ISO is a
read-only file that has an ISO/CD-ROM style file system. Users can
upload their own ISOs and mount them on their Guest Instances.

ISOs are uploaded based on a URL. HTTP is the supported protocol. Once
the ISO is available via HTTP specify an upload URL such as
http://my.web.server/filename.iso.

ISOs may be public or private, like Templates.ISOs are not
hypervisor-specific. That is, a guest on vSphere can mount the exact
same image that a guest on KVM can mount.

ISO images may be stored in the system and made available with a privacy
level similar to Templates. ISO images are classified as either bootable
or not bootable. A bootable ISO image is one that contains an OS image.
CloudStack allows a User to boot a Guest Instance off of an ISO image. Users
can also attach ISO images to Guest Instances. For example, this enables
installing PV drivers into Windows. ISO images are not
hypervisor-specific.


Adding an ISO
-------------

To make additional operating system or other software available for use
with Guest Instances, you can add an ISO. The ISO is typically thought of as
an operating system image, but you can also add ISOs for other types of
software, such as desktop applications that you want to be installed as
part of a Template.

#. Log in to the CloudStack UI as an administrator or end User.

#. In the left navigation bar, click Templates.

#. In Select View, choose ISOs.

#. Click Add ISO.

#. In the Add ISO screen, provide the following:

   -  **Name**: Short name for the ISO image. For example, CentOS 6.2
      64-bit.

   -  **Description**: Display test for the ISO image. For example,
      CentOS 6.2 64-bit.

   -  **URL**: The URL that hosts the ISO image. The Management Server
      must be able to access this location via HTTP. If needed you can
      place the ISO image directly on the Management Server

   -  **Zone**: Choose the zone where you want the ISO to be available,
      or All Zones to make it available throughout CloudStack.

   -  **Bootable**: Whether or not a guest could boot off this ISO
      image. For example, a CentOS ISO is bootable, a Microsoft Office
      ISO is not bootable.

   -  **OS Type**: This helps CloudStack and the hypervisor perform
      certain operations and make assumptions that improve the
      performance of the guest. Select one of the following.

      -  If the operating system of your desired ISO image is listed,
         choose it.

      -  If the OS Type of the ISO is not listed or if the ISO is not
         bootable, choose Other.

      -  (XenServer only) If you want to boot from this ISO in PV mode,
         choose Other PV (32-bit) or Other PV (64-bit)

      -  (KVM only) If you choose an OS that is PV-enabled, the Instances
         created from this ISO will have a SCSI (virtio) root disk. If
         the OS is not PV-enabled, the Instances will have an IDE root disk.
         The PV-enabled types are:

         -  Fedora 13

         -  Fedora 12

         -  Fedora 11

         -  Fedora 10

         -  Fedora 9

         -  Other PV

         -  Debian GNU/Linux

         -  CentOS 5.3

         -  CentOS 5.4

         -  CentOS 5.5

         -  Red Hat Enterprise Linux 5.3

         -  Red Hat Enterprise Linux 5.4

         -  Red Hat Enterprise Linux 5.5

         -  Red Hat Enterprise Linux 6


      .. note::
         It is not recommended to choose an older version of the OS than
         the version in the image. For example, choosing CentOS 5.4 to
         support a CentOS 6.2 image will usually not work. In these
         cases, choose Other.

   -  **Extractable**: Choose Yes if the ISO should be available for
      extraction.

   -  **Public**: Choose Yes if this ISO should be available to other
      Users.

   -  **Featured**: Choose Yes if you would like this ISO to be more
      prominent for Users to select. The ISO will appear in the Featured
      ISOs list. Only an administrator can make an ISO Featured.

#. Click OK.

   The Management Server will download the ISO. Depending on the size of
   the ISO, this may take a long time. The ISO status column will
   display Ready once it has been successfully downloaded into secondary
   storage. Clicking Refresh updates the download percentage.

#. **Important**: Wait for the ISO to finish downloading. If you move on
   to the next task and try to use the ISO right away, it will appear to
   fail. The entire ISO must be available before CloudStack can work
   with it.


Attaching an ISO to a Instance
------------------------------

#. In the left navigation, click Instances.

#. Choose the Instance you want to work with.

#. Click the Attach ISO button. |iso.png|

#. In the Attach ISO dialog box, select the desired ISO.

#. Click OK.



.. |sysmanager.png| image:: /_static/images/sysmanager.png
   :alt: System Image Manager
.. |software-license.png| image:: /_static/images/software-license.png
   :alt: Depicts hiding the EULA page.
.. |change-admin-password.png| image:: /_static/images/change-admin-password.png
   :alt: Depicts changing the administrator password
.. |kvm-direct-download.png| image:: /_static/images/kvm-direct-download.png
.. |upload-iso-from-local.png| image:: /_static/images/upload-iso-from-local.png
   :alt: Upload ISO from local
.. |template-upload-from-local.png| image:: /_static/images/template-upload-from-local.png
   :alt: Upload Template from local
.. |template-permissions-update-manually-1.png| image:: /_static/images/template-permissions-update-manually-1.png
   :alt: USharing template with Account "user2"
.. |template-permissions-update-manually-2.png| image:: /_static/images/template-permissions-update-manually-2.png
   :alt: Revoking permissions from Account "user2"
.. |template-permissions-update-1.png| image:: /_static/images/template-permissions-update-1.png
   :alt: Sharing template with just Account "user8"
.. |template-permissions-update-2.png| image:: /_static/images/template-permissions-update-2.png
   :alt: Sharing template with 2 specific projects
.. |template-permissions-update-3.png| image:: /_static/images/template-permissions-update-3.png
   :alt: Revoking permissins from Account "user8"
.. |template-permissions-update-4.png| image:: /_static/images/template-permissions-update-4.png
   :alt: Revoking permsissons from both projects previously added
.. |template-permissions-update-5.png| image:: /_static/images/template-permissions-update-5.png
   :alt: Reseting (removing all) permissions
