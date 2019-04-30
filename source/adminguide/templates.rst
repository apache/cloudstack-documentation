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

   -  **OS Type**. This helps CloudStack and the hypervisor perform
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


Creating a Template from a Snapshot
-----------------------------------

If you do not want to stop the VM in order to use the Create Template
menu item (as described in `“Creating a Template from an Existing 
Virtual Machine” <#creating-a-template-from-an-existing-virtual-machine>`_), 
you can create a template directly from any snapshot through the 
CloudStack UI.


Uploading Templates
-------------------


vSphere Templates and ISOs
--------------------------

If you are uploading a template that was created using vSphere Client,
be sure the OVA file does not contain an ISO. If it does, the deployment
of VMs from the template will fail.

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

   -  **Hypervisor**: The supported hypervisors are listed. Select the
      desired one.

   -  **Format**. The format of the template upload file, such as VHD or
      OVA.

   -  **Password Enabled**. Choose Yes if your template has the
      CloudStack password change script installed. 
      See :ref:`adding-password-management-to-templates`.

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


.. |sysmanager.png| image:: /_static/images/sysmanager.png
   :alt: System Image Manager
.. |software-license.png| image:: /_static/images/software-license.png
   :alt: Depicts hiding the EULA page.
.. |change-admin-password.png| image:: /_static/images/change-admin-password.png
   :alt: Depicts changing the administrator password
