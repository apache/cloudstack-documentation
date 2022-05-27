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

A template is a reusable configuration for virtual machines. When users
launch VMs, they can choose from a list of templates in CloudStack.

Specifically, a template is a virtual disk image that includes one of a
variety of operating systems, optional additional software such as
office applications, and settings such as access control to determine
who can use the template. Each template is associated with a particular
type of hypervisor, which is specified when the template is added to
CloudStack.

CloudStack ships with a default template. In order to present more
choices to users, CloudStack administrators and users can create
templates and add them to CloudStack.


Creating Templates: Overview
----------------------------

CloudStack ships with a default template for the CentOS operating
system. There are a variety of ways to add more templates.
Administrators and end users can add templates. The typical sequence of
events is:

#. Launch a VM instance that has the operating system you want. Make any
   other desired configuration changes to the VM.

#. Stop the VM.

#. Convert the volume into a template.

There are other ways to add templates to CloudStack. For example, you
can take a snapshot of the VM's volume and create a template from the
snapshot, or import a VHD from another system into CloudStack.

The various techniques for creating templates are described in the next
few sections.


Requirements for Templates
--------------------------

-  For XenServer, install PV drivers / Xen tools on each template that
   you create. This will enable live migration and clean guest shutdown.

-  For vSphere, install VMware Tools on each template that you create.
   This will enable console view to work properly.


Best Practices for Templates
----------------------------

If you plan to use large templates (100 GB or larger), be sure you have
a 10-gigabit network to support the large templates. A slower network
can lead to timeouts and other errors when large templates are used.


The Default Template
--------------------

CloudStack includes a CentOS template. This template is downloaded by
the Secondary Storage VM after the primary and secondary storage are
configured. You can use this template in your production deployment or
you can delete it and use custom templates.

The root password for the default template is "password".

A default template is provided for each of XenServer, KVM, and vSphere.
The templates that are downloaded depend on the hypervisor type that is
available in your cloud. Each template is approximately 2.5 GB physical
size.

The default template includes the standard iptables rules, which will
block most access to the template excluding ssh.

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

When a user creates a template, it can be designated private or public.

Private templates are only available to the user who created them. By
default, an uploaded template is private.

When a user marks a template as “public,” the template becomes available
to all users in all accounts in the user's domain, as well as users in
any other domains that have access to the Zone where the template is
stored. This depends on whether the Zone, in turn, was defined as
private or public. A private Zone is assigned to a single domain, and a
public Zone is accessible to any domain. If a public template is created
in a private Zone, it is available only to users in the domain assigned
to that Zone. If a public template is created in a public Zone, it is
available to all users in all domains.


Creating a Template from an Existing Virtual Machine
----------------------------------------------------

Once you have at least one VM set up in the way you want, you can use it
as the prototype for other VMs.

#. Create and start a virtual machine using any of the techniques given
   in `“Creating VMs” <virtual_machines.html#creating-vms>`_.

#. Make any desired configuration changes on the running VM, then click
   Stop.

#. Wait for the VM to stop. When the status shows Stopped, go to the
   next step.

#. Go into "View Volumes" and select the Volume having the type "ROOT".

#. Click Create Template and provide the following:

   -  **Name and Display Text**. These will be shown in the UI, so
      choose something descriptive.

   -  **OS Type**. (Except for VMware). This helps CloudStack and the hypervisor perform
      certain operations and make assumptions that improve the
      performance of the guest. Select one of the following.

      -  If the operating system of the stopped VM is listed, choose it.

      -  If the OS type of the stopped VM is not listed, choose Other.

      -  If you want to boot from this template in PV mode, choose Other
         PV (32-bit) or Other PV (64-bit). This choice is available only
         for XenServere:

         .. note::
            Generally you should not choose an older version of the OS
            than the version in the image. For example, choosing CentOS
            5.4 to support a CentOS 6.2 image will in general not work.
            In those cases you should choose Other.


   -  **Public**. Choose Yes to make this template accessible to all
      users of this CloudStack installation. The template will appear in
      the Community Templates list. See `“Private and
      Public Templates” <#private-and-public-templates>`_.

   -  **Password Enabled**. Choose Yes if your template has the
      CloudStack password change script installed. See
      :ref:`adding-password-management-to-templates`.

#. Click Add.

The new template will be visible in the Templates section when the
template creation process has been completed. The template is then
available when creating a new VM.

.. note::
   Since version 4.15, CloudStack obtains information from the VMware templates
   automatically at registration time. If a template contains different deployment
   options (or configurations) as in the case of virtual appliances, then CloudStack
   display the information required by the template, allowing users or administrators
   to configure their instances.

Creating a Template from a Snapshot
-----------------------------------

If you do not want to stop the VM in order to use the Create Template
menu item (as described in `“Creating a Template from an Existing
Virtual Machine” <#creating-a-template-from-an-existing-virtual-machine>`_),
you can create a template directly from any snapshot through the
CloudStack UI.


Uploading Templates from a remote HTTP server
---------------------------------------------



vSphere Templates and ISOs
^^^^^^^^^^^^^^^^^^^^^^^^^^
.. warning::
      If you are uploading a template that was created using vSphere Client,
      be sure the OVA file does not contain an ISO. If it does, the deployment
      of VMs from the template will fail

Templates are uploaded based on a URL. HTTP is the supported access
protocol. Templates are frequently large files. You can optionally gzip
them to decrease upload times.

To upload a template:

#. In the left navigation bar, click Templates.

#. Click Register Template.

#. Provide the following:

   -  **Name and Description**. These will be shown in the UI, so choose
      something descriptive.

   -  **URL**. The Management Server will download the file from the
      specified URL, such as ``http://my.web.server/filename.vhd.gz``.

   -  **Zone**. Choose the zone where you want the template to be
      available, or All Zones to make it available throughout
      CloudStack.

   - **Read VM settings from OVA**. (VMware only) If selected, the registered template will allow users to deploy VMs as clones of the template, including all their properties, configurations, end-user license agreements, disks, os type, etc. This option allows users to register virtual appliances. See `Support for Virtual Appliances <virtual_machines.html#about-virtual-appliances>`_.

      .. note:: 
         When this option is selected the following fields are hidden: Root disk controller, Keyboard type and OS Type. 

   -  **OS Type**: This helps CloudStack and the hypervisor perform
      certain operations and make assumptions that improve the
      performance of the guest. Select one of the following:

      -  If the operating system of the stopped VM is listed, choose it.

      -  If the OS type of the stopped VM is not listed, choose Other.

         .. note::
            You should not choose an older version of the OS than the
            version in the image. For example, choosing CentOS 5.4 to
            support a CentOS 6.2 image will in general not work. In
            those cases you should choose Other.

         .. note::
            Since version 4.15.1, VMware templates do not allow users or administrators
            selecting an OS Type when registering a template if the option 'Read VM settings from OVA' is selected. In this case, the OS Type is
            obtained from the template after it is registered.

   -  **Userdata**: The registered Userdata are listed. Select the
      desired one.

   -  **Userdata link policy**: Select the userdata override policy as required. 
      For more information on userdata and override link policy, please check `Userdata section <virtual_machines.html#user-data-and-meta-data>`_.


   -  **Hypervisor**: The supported hypervisors are listed. Select the
      desired one.

   -  **Format**. The format of the template upload file, such as VHD or
      OVA.

   -  **Extractable**. Choose Yes if the template is available for
      extraction. If this option is selected, end users can download a
      full image of a template.

   -  **Public**. Choose Yes to make this template accessible to all
      users of this CloudStack installation. The template will appear in
      the Community Templates list. See `“Private and
      Public Templates” <#private-and-public-templates>`_.

   -  **Featured**. Choose Yes if you would like this template to be
      more prominent for users to select. The template will appear in
      the Featured Templates list. Only an administrator can make a
      template Featured.

Note that uploading multi-disk templates is also supported.

.. note:: 
   VMware only: If the template is registered with the option 'Read VM settings
   from OVA' then the VM deployment wizard will display all the available OVF
   properties, different deployment options or configurations, multiple NICs or
   end-user license agreements.

   See `Support for Virtual Appliances <virtual_machines.html#about-virtual-appliances>`_.



.. include:: templates/_bypass-secondary-storage-kvm.rst



Uploading Templates and ISOs from a local computer
-------------------------------------------

It's also possible to upload an already prepared template or an ISO from your local computer.
The steps are similar as when Uploading a template/ISO from a remote HTTP server, except that you need to choose a local template/ISO file from your PC.
For this feature to work, your SSVMs must be supporting HTTPS (for more info please visit `“Using a SSL Certificate for the Console Proxy”
<systemvm.html#using-a-ssl-certificate-for-the-console-proxy>`_).

Example GUI dialog of uploading Template/ISO from local (browser) is given below:

|template-upload-from-local.png|

|upload-iso-from-local.png|

Note that uploading multi-disk templates is also supported.

Sharing templates and ISOs with other accounts/projects
----------------------------------------------

When adding a template/ISO, the owner can choose to make template/ISO public or to keep it private. Once the template/ISO is created, the owner can choose to share this template/ISO so that other accounts/projects can also use the template/ISO. 

Currently, the owners can share their template/ISO with:
  - other accounts inside their own domain (i.e. can't share the template/ISO with other accounts in the subdomain of their domain or any other domains)
  - projects where they belongs to (i.e. projects where they are the owners/creators or other projects where they have been joined)

Template/ISO permissions can be changed via updateTemplatePermissions/updateIsoPermissions API call or via GUI. It is supported to add, remove or reset (remove all) template/ISO permissions.

When adding or removing permissions to/from a template/ISO, it is required to specify account/project name which is being added/removed from the template/ISO permissions.

Global setting "allow.user.view.all.domain.accounts" has a default value of "false". This makes sure that when the regular users (of a "User" role) wants to share a template/ISO via GUI,  they will not be shown the list of all accounts in their domain and they will need to know the name of the destination account with which they are sharing the template/ISO. This makes sense in public clouds where each account of a single domain is a different tenant/customer and privacy is imperative. In this case, the user will be presented with an input field to enter the account name, as on the images below:

.. warning::
      The images displayed below refer to template permissions, but the same applies for ISO permissions.

|template-permissions-update-manually-1.png|

Sharing the template with account "user2"

|template-permissions-update-manually-2.png|

Revoking permissions from account "user2"

But in environments where privacy within a domain is not an issue, setting "allow.user.view.all.domain.accounts" setting to "true" will make sure that the user, who is sharing the template, will be presented a more user-friendly multi-select list, listing all the accounts in their domain. This is shown in the images below;

|template-permissions-update-1.png|

Sharing the template with just account "user8"

|template-permissions-update-2.png|

Sharing template with 2 specific projects

|template-permissions-update-3.png|

Revoking permissions from account "user8"

|template-permissions-update-4.png|

Revoking permissions from both projects previously added


Finally, template permissions can be reset:

|template-permissions-update-5.png|

Resetting (removing all) permissions

.. warning::
      Project-owned templates are not supported to be shared outside of
      the Project, and if attempted to do so, a proper error message is shown.

Exporting Templates
-------------------

End users and Administrators may export templates from the CloudStack.
Navigate to the template in the UI and choose the Download function from
the Actions menu.

.. include:: templates/_create_linux.rst

.. include:: templates/_create_windows.rst

.. include:: templates/_import_ami.rst

.. include:: templates/_convert_hyperv.rst

.. include:: templates/_password.rst


Deleting Templates
------------------

Templates may be deleted. In general, when a template spans multiple
Zones, only the copy that is selected for deletion will be deleted; the
same template in other Zones will not be deleted. The provided CentOS
template is an exception to this. If the provided CentOS template is
deleted, it will be deleted from all Zones.

When templates are deleted, the VMs instantiated from them will continue
to run. However, new VMs cannot be created based on the deleted
template.

Working with ISOs
===================

CloudStack supports ISOs and their attachment to guest VMs. An ISO is a
read-only file that has an ISO/CD-ROM style file system. Users can
upload their own ISOs and mount them on their guest VMs.

ISOs are uploaded based on a URL. HTTP is the supported protocol. Once
the ISO is available via HTTP specify an upload URL such as
http://my.web.server/filename.iso.

ISOs may be public or private, like templates.ISOs are not
hypervisor-specific. That is, a guest on vSphere can mount the exact
same image that a guest on KVM can mount.

ISO images may be stored in the system and made available with a privacy
level similar to templates. ISO images are classified as either bootable
or not bootable. A bootable ISO image is one that contains an OS image.
CloudStack allows a user to boot a guest VM off of an ISO image. Users
can also attach ISO images to guest VMs. For example, this enables
installing PV drivers into Windows. ISO images are not
hypervisor-specific.


Adding an ISO
---------------

To make additional operating system or other software available for use
with guest VMs, you can add an ISO. The ISO is typically thought of as
an operating system image, but you can also add ISOs for other types of
software, such as desktop applications that you want to be installed as
part of a template.

#. Log in to the CloudStack UI as an administrator or end user.

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

      -  (KVM only) If you choose an OS that is PV-enabled, the VMs
         created from this ISO will have a SCSI (virtio) root disk. If
         the OS is not PV-enabled, the VMs will have an IDE root disk.
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
      users.

   -  **Featured**: Choose Yes if you would like this ISO to be more
      prominent for users to select. The ISO will appear in the Featured
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


Attaching an ISO to a VM
-------------------------

#. In the left navigation, click Instances.

#. Choose the virtual machine you want to work with.

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
   :alt: USharing template with account "user2"
.. |template-permissions-update-manually-2.png| image:: /_static/images/template-permissions-update-manually-2.png
   :alt: Revoking permissions from account "user2"
.. |template-permissions-update-1.png| image:: /_static/images/template-permissions-update-1.png
   :alt: Sharing template with just account "user8"
.. |template-permissions-update-2.png| image:: /_static/images/template-permissions-update-2.png
   :alt: Sharing template with 2 specific projects
.. |template-permissions-update-3.png| image:: /_static/images/template-permissions-update-3.png
   :alt: Revoking permissins from account "user8"
.. |template-permissions-update-4.png| image:: /_static/images/template-permissions-update-4.png
   :alt: Revoking permsissons from both projects previously added
.. |template-permissions-update-5.png| image:: /_static/images/template-permissions-update-5.png
   :alt: Reseting (removing all) permissions
