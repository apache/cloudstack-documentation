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


Overview of Projects
--------------------

Projects are used to organize people and resources. CloudStack Users
within a single domain can group themselves into project teams so they
can collaborate and share virtual resources such as Instances, Snapshots,
Templates, data disks, and IP addresses. CloudStack tracks resource
usage per project as well as per User, so the usage can be billed to
either a User Account or a project. For example, a private cloud within
a software company might have all members of the QA department assigned
to one project, so the company can track the resources used in testing
while the project members can more easily isolate their efforts from
other Users of the same cloud

You can configure CloudStack to allow any User to create a new project,
or you can restrict that ability to just CloudStack administrators. Once
you have created a project, you become that project’s administrator, and
you can add others within your domain to the project. CloudStack can be
set up to either add people directly to a project, or to send an
invitation which the recipient must accept. Project members can view
and manage all virtual resources created by anyone in the project
(for example, share Instances). A User can be a member of any number of projects
and can switch views in the CloudStack UI to show only project-related information,
such as project Instances, fellow project members, project-related alerts, and so on.

From CloudStack 4.15 onwards, it is possible for a project to have
multiple project administrators and to add/invite specific Users of
an Account to a project in addition to adding Accounts. By means of
Project Roles associated with a User or an Account of the project,
it is possible to restrict access of Users in a project, i.e., in
addition to Account-level roles, one can further restrict access to
operations (or APIs) by associating a project-level role to the
User or Account. However, if an Account has already been added, one will not
be able to associate a role to a specific User of that Account.

**NOTE:** Project Roles work over Account level Roles. If a User/Account is
added to a project without a project role, it would imply that the
User / Account added will have access to all APIs that are made available
by the Account level role. If there are no specific deny rules in the
project role, it would again fallback onto the Account-level role to decide
whether the User has permissions to perform a specific action. It is also to be
noted that Project roles are restrictive in nature, i.e., to say that, one may
not allow a User to perform an operation that is NOT allowed at the Account level.
Even if a rule is added at the project level, allowing such an action, it will not
have any effect as the action will be prohibited by the Account Role.


The project administrator can promote or demote a User in the project.
The project administrator can also add more members, remove members
from the project, set new resource limits (as long as they are
below the global defaults set by the CloudStack administrator), and
delete the project. When the administrator removes a member from the
project, resources created by that User, such as Instances, remain
with the project. This brings us to the subject of resource ownership
and which resources can be used by a project.

Resources created within a project are owned by the project, not by any
particular CloudStack Account, and they can be used only within the
project. A User who belongs to one or more projects can still create
resources outside of those projects, and those resources belong to the
User’s Account; they will not be counted against the project’s usage or
resource limits. You can create project-level networks to isolate
traffic within the project and provide network services such as port
forwarding, load balancing, VPN, and static NAT. A project can also make
use of certain types of resources from outside the project, if those
resources are shared. For example, a shared network or public Template
is available to any project in the domain. A project can get access to a
private Template if the Template’s owner will grant permission. A
project can use any service offering or disk offering available in its
domain; however, you can not create private service and disk offerings
at the project level.


Configuring Projects
--------------------

Before CloudStack Users start using projects, the CloudStack
administrator must set up various systems to support them, including
membership invitations, limits on project resources, and controls on who
can create projects.


Setting Up Invitations
~~~~~~~~~~~~~~~~~~~~~~

CloudStack can be set up either so that project administrators can add
people directly to a project, or so that it is necessary to send an
invitation which the recipient must accept. The invitation can be sent
by email or through the User’s CloudStack Account. If you want
administrators to use invitations to add members to projects, turn on
and set up the invitations feature in CloudStack.

#. Log in as administrator to the CloudStack UI.

#. In the left navigation, click Global Settings.

#. In the search box, type project and click the search button.
   |Searches projects|

#. In the search results, you can see a few other parameters you need to
   set to control how invitations behave. The table below shows global
   configuration parameters related to project invitations. Click the
   edit button to set each parameter.

   .. cssclass:: table-striped table-bordered table-hover

   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Configuration Parameters   | Description                                                                                                                                           |
   +============================+=======================================================================================================================================================+
   | project.invite.required    | Set to true to turn on the invitations feature.                                                                                                       |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | project.email.sender       | The email address to show in the From field of invitation emails.                                                                                     |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | project.invite.timeout     | Amount of time to allow for a new member to respond to the invitation.                                                                                |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | project.smtp.host          | Name of the host that acts as an email server to handle invitations.                                                                                  |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | project.smtp.password      | (Optional) Password required by the SMTP server. You must also set project.smtp.username and set project.smtp.useAuth to true.                        |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | project.smtp.port          | SMTP server’s listening port.                                                                                                                         |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | project.smtp.useAuth       | Set to true if the SMTP server requires a username and password.                                                                                      |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | project.smtp.username      | (Optional) User name required by the SMTP server for authentication. You must also set project.smtp.password and set project.smtp.useAuth to true..   |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Restart the Management Server:

   .. code:: bash

      service cloudstack-management restart

Setting Resource Limits for Projects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The CloudStack administrator can set global default limits to control
the amount of resources that can be owned by each project in the cloud.
This serves to prevent uncontrolled usage of resources such as
Snapshots, IP addresses, and Instances. Domain administrators can override
these resource limits for individual projects with their domains,
as long as the new limits are below the global defaults set by the CloudStack
root administrator. The root administrator can also set lower resource limits
for any project in the cloud.

Setting Per-Project Resource Limits
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The CloudStack root administrator or the domain administrator of the
domain where the project resides can set new resource limits for an
individual project. The project owner can set resource limits only if
the owner is also a domain or root administrator.

The new limits must be below the global default limits set by the
CloudStack administrator (as described in `“Setting
Resource Limits for Projects” <#setting-resource-limits-for-projects>`_).
If the project already owns more of a given type of resource than the
new maximum, the resources are not affected; however, the project can
not add any new resources of that type until the total drops below the
new limit.

#. Log in as administrator to the CloudStack UI.

#. In the left navigation, click Projects.

#. Click the name of the project you want to work with.

#. Click the Resources tab. This tab lists the current maximum amount
   that the project is allowed to own for each type of resource.

#. Type new values for one or more resources.

#. Click Apply.


Setting the Global Project Resource Limits
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Log in as administrator to the CloudStack UI.

#. In the left navigation, click Global Settings.

#. In the search box, type max.projects and click the search button.

#. In the search results, you will see the parameters you can use to set
   per-project maximum resource amounts that apply to all projects in
   the cloud. No project can have more resources, but an individual
   project can have lower limits. Click the edit button to set each
   parameter. |Edits parameters|

   .. cssclass:: table-striped table-bordered table-hover

   +--------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | max.project.public.ips   | Maximum number of public IP addresses that can be owned by any project in the cloud. See About Public IP Addresses.          |
   +--------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | max.project.snapshots    | Maximum number of Snapshots that can be owned by any project in the cloud. See Working with Snapshots.                       |
   +--------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | max.project.templates    | Maximum number of Templates that can be owned by any project in the cloud. See Working with Templates.                       |
   +--------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | max.project.uservms      | Maximum number of guest Instances that can be owned by any project in the cloud. See Working With Instances.                 |
   +--------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | max.project.volumes      | Maximum number of data volumes that can be owned by any project in the cloud. See Working with Volumes.                      |
   +--------------------------+------------------------------------------------------------------------------------------------------------------------------+


#. Restart the Management Server.

   .. code:: bash

      # service cloudstack-management restart

Setting Project Creator Permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can configure CloudStack to allow any User to create a new project,
or you can restrict that ability to just CloudStack administrators.

#. Log in as administrator to the CloudStack UI.

#. In the left navigation, click Global Settings.

#. In the search box, type allow.user.create.projects.

#. Click the edit button to set the parameter. |Edits parameters|

   ``allow.user.create.projects``

   Set to true to allow end Users to create projects. Set to false if
   you want only the CloudStack root administrator and domain
   administrators to create projects.

#. Restart the Management Server.

   .. code:: bash

      # service cloudstack-management restart


Creating a New Project
----------------------

CloudStack administrators and domain administrators can create projects.
If the global configuration parameter allow.user.create.projects is set
to true, end Users can also create projects.

#. Log in as administrator to the CloudStack UI.

#. In the left navigation, click Projects.

#. Click New Project.

#. Give the project a name and description for display to Users, then
   click Create Project.

#. A screen appears where you can immediately add more members to the
   project. This is optional. Click Next when you are ready to move on.

#. Click Save.


Adding Members to a Project
---------------------------

New members can be added to a project by the project’s administrator,
the domain administrator of the domain where the project resides or any
parent domain, or the CloudStack root administrator. There are two ways
to add members in CloudStack, but only one way is enabled at a time:

-  If invitations have been enabled, you can send invitations to new
   members.

-  If invitations are not enabled, you can add members directly through
   the UI.


Working with Project Roles
--------------------------
CloudStack allows adding project members with a desired project role. A
project role will be assigned to the member in addition to their base
account role. Project Roles are retrictive in nature and can be used to
further restrict certain API access to the members within the project.
It is important to note that a project role cannot be used to elevate an
existing user's permissions. Project roles can be created or managed
using `Project roles` tab in the project details UI.


Sending Project Membership Invitations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use these steps to add a new member to a project if the invitations
feature is enabled in the cloud as described in `“Setting
Up Invitations” <#setting-up-invitations>`_. If the invitations feature is
not turned on, use the procedure in Adding Project Members From the UI.

#. Log in to the CloudStack UI.

#. In the left navigation, click Projects.

#. Click the name of the project you want to work with.

#. Click on the `Add Account to Project` button. This will have 2 tabs, one to add Account to the project and the other to add a User to the project. Here, we can specify the:

      - Account or User and/or email id of the User to be invited,
      - (Optional) the Role i.e, Admin or Regular that the User is to be added as, defaults to Regular role,
      - (Optional) the Project role specifying the list of APIs the User is allowed/ denied access to

   You can invite only people who have an Account in this cloud within the same domain as the project. However, you can send the invitation to any email address.

#. To view and manage the invitations you have sent, return to this tab.
   When an invitation is accepted, the new member will appear in the
   project’s Accounts tab.


Adding Project Members From the UI
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The steps below tell how to add a new member to a project if the
invitations feature is not enabled in the cloud. If the invitations
feature is enabled cloud,as described in `“Setting Up
Invitations” <#setting-up-invitations>`_, use the procedure in
`“Sending Project Membership
Invitations” <#sending-project-membership-invitations>`_.

#. Log in to the CloudStack UI.

#. In the left navigation, click Projects.

#. Click the name of the project you want to work with.

#. Click on the `Add Account to Project` button. This will have 2 tabs, one to add Account to the project and the other to add a User to the project. Here, we can specify the:

      - Account or User and/or email id of the User to be invited,
      - (Optional) the Role i.e, Admin or Regular that the User is to be added as, defaults to Regular role,
      - (Optional) the Project role specifying the list of APIs the User is allowed/ denied access to

#. You can add only people who have an Account in this cloud and within the same domain as the project.


Accepting a Membership Invitation
---------------------------------

If you have received an invitation to join a CloudStack project, and you
want to accept the invitation, follow these steps:

#. Log in to the CloudStack’s UI.

#. In the left navigation, click Projects.

#. Click on the Project Invitations button

#. If you see the invitation listed onscreen, click the Accept button.

   Invitations listed on screen were sent to you using your CloudStack
   Account name.

#. If you received an email invitation, click the Enter Token button,
   and provide the project ID and unique ID code (token) from the email.


Suspending or Deleting a Project
--------------------------------

When a project is suspended, it retains the resources it owns, but they
can no longer be used. No new resources or members can be added to a
suspended project.

When a project is deleted, its resources are destroyed, and member
Accounts are removed from the project. The project’s status is shown as
Disabled pending final deletion.

A project can be suspended or deleted by the project administrator, the
domain administrator of the domain the project belongs to or of its
parent domain, or the CloudStack root administrator.

#. Log in to the CloudStack UI.

#. In the left navigation, click Projects.

#. Click the name of the project.

#. Click one of the buttons:

   To delete, use |Removes a project|

   To suspend, use |Suspends a project|


Using the Project View
----------------------

If you are a member of a project, you can use CloudStack’s project view
to see project members, resources consumed, and more. The project view
shows only information related to one project. It is a useful way to
filter out other information so you can concentrate on a project status
and resources.

#. Log in to the CloudStack UI.

#. Click Project View.

#. The project dashboard appears, showing the project’s Instances, volumes,
   Users, events, network settings, and more. From the dashboard, you
   can:

   -  Click the Accounts tab to view and manage project members. If you
      are the project administrator, you can add new members, remove
      members, or change the role of a member from User to admin or vice versa.

   -  (If invitations are enabled) Click the Invitations button to view and
      manage invitations that have been sent to new project members but
      not yet accepted. Pending invitations will remain in this list
      until the new member accepts, the invitation timeout is reached,
      or you cancel the invitation.


.. |Edits Parameters| image:: /_static/images/edit-icon.png
.. |Searches projects| image:: /_static/images/search-button.png
.. |Removes a project| image:: /_static/images/delete-button.png
.. |Suspends a project| image:: /_static/images/suspend-icon.png
