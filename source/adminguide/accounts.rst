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


Roles, Accounts, Users, and Domains
-----------------------------------

Roles
~~~~~

A role represents a set of allowed functions. All CloudStack Accounts have a
role attached to them that enforce access rules on them to be allowed or
disallowed to make an API request. Typically there are four default roles:
root admin, resource admin, domain admin and User.
Newer roles have been added which include Read-Only Admin, Read-Only User,
Support Admin and Support User which are in turn based on the aforementioned roles.


Accounts
~~~~~~~~

An Account typically represents a customer of the service provider or a
department in a large organization. Multiple Users can exist in an
Account.


Domains
~~~~~~~

Accounts are grouped by domains. Domains usually contain multiple
Accounts that have some logical relationship to each other and a set of
delegated administrators with some authority over the domain and its
subdomains. For example, a service provider with several resellers could
create a domain for each reseller.

Beside the Root Administrator type of Account (available in the root domain only), two different types
of Accounts can be created for each domain:  Domain Administrator and User.


Users
~~~~~

Users are like aliases in the Account. Users in the same Account are not
isolated from each other, but they are isolated from Users in other
Accounts. Most installations need not surface the notion of Users; they
just have one User per Account. The same User cannot belong to multiple
Accounts.

Username is unique in a domain across Accounts in that domain. The same
username can exist in other domains, including sub-domains. Domain name
can repeat only if the full pathname from root is unique. For example,
you can create root/d1, as well as root/foo/d1, and root/sales/d1.

Administrators are Accounts with special privileges in the system. There
may be multiple administrators in the system. Administrators can create
or delete other administrators, and change the password for any User in
the system.


Domain Administrators
~~~~~~~~~~~~~~~~~~~~~

Domain administrators can perform administrative operations for Users
who belong to that domain. Domain administrators do not have visibility
into physical servers or other domains.


Root Administrator
~~~~~~~~~~~~~~~~~~

Root administrators have complete access to the system, including
managing Templates, service offerings, customer care administrators, and
domains

Read Only Administrator
~~~~~~~~~~~~~~~~~~~~~~~

A restricted admin role in which an Account is only allowed to perform any list, get
or find operations but not perform any other operation which can change the
infrastructure, configuration or User resources.

Read Only User
~~~~~~~~~~~~~~

A restricted User role in which an Account is only allowed to perform list, get or find
operations. It can be used by Users who may only be interested in monitoring and usage
of resources.

Support Admin
~~~~~~~~~~~~~

A restricted admin role in which an admin Account is limited to perform auxiliary support
and maintenance tasks which do not directly affect the infrastructure, such as creating offerings,
and put resources in maintenance, but cannot change the infrastructure such as physical networks.

Support User
~~~~~~~~~~~~

A restricted User role in which an Account cannot create or destroy resources, but can view resources
and perform auxiliary and support operations such as start or stop Instances, attach or detach volumes, ISOs etc.


Resource Ownership
~~~~~~~~~~~~~~~~~~

Resources belong to the Account, not individual Users in that Account.
For example, billing, resource limits, and so on are maintained by the
Account, not the Users. A User can operate on any resource in the
Account provided the User has privileges for that operation. The
privileges are determined by the role. A root administrator can change
the ownership of any Instance from one Account to any other
Account by using the assignVirtualMachine API. A domain or sub-domain
administrator can do the same for Instances within the domain from one Account
to any other Account in the domain or any of its sub-domains.

.. _using-dynamics-roles:

Using Dynamic Roles
-------------------

In addition to the default roles, the dynamic role-based API checker feature
allows CloudStack root admins to create new roles with customized permissions.
The allow/deny rules can be configured dynamically during runtime without
restarting the management server(s).

.. Note:: in versions before 4.16.1, any User given the custom roles
          that include permission to create and/or update Accounts
          will have the ability to assign new custom roles to
          themselves or other Users, irrespective of the privileges
          given in those roles. This could allow such a User to
          escalate their own privileges to include any API they might
          not have had before. Therefore, the dynamic roles should be
          carefully designed and the `createAccount` and
          `updateAccount` privileges should only be given to Users who
          you are content to have this level of privilege.

          Since 4.16.1 a User will be prevented to create an Account
          with a role that has any permissions that they do not have
          themselves. This check will also be performed, since that
          version, on updating an Account-role.

For backward compatibility, all roles resolve to one of the four role types:
admin, resource admin, domain admin and User. A new role can be created using
the roles tab in the UI and specifying a name, either a role type or ID of existing
role, and optionally a description. When a new role is created using ID of existing
role, all the rules of the existing role are copied to the new role and these rules
can be modified as desired.

Role specific rules can be either configured through the rules tab on role specific
details page or imported from a CSV file while creating a new role with role type.
A rule is either an API name or a wildcard string that are one of allow or deny
permission and optionally a description. These rules can be exported to a
CSV file, name defaulted to “<RoleName>_<RoleType>.csv”.

CSV file format:

.. parsed-literal::

   rule,permission,description
   <Rule1>,<Permission1>,<Description1>
   <Rule2>,<Permission2>,<Description2>
   <Rule3>,<Permission3>,<Description3>
   …
   so on

When a User makes an API request, the backend checks the requested API against
configured rules (in the order the rules were configured) for the caller
User-Account's role. It will iterate through the rules and would allow the
API request if the API matches an allow rule, else if it matches a deny rule
it would deny the request. Next, if the request API fails to match any of
the configured rules it would allow if the requested API's default authorized
annotations allow that User role type and finally deny the User API request
if it fails to be explicitly allowed/denied by the role permission rules or the
default API authorize annotations. Note: to avoid root admin being locked
out of the system, all root admin Accounts are allowed all APIs.

The dynamic-roles feature is enabled by default only for all new CloudStack
installations since version `4.9.x <https://cwiki.apache.org/confluence/display/CLOUDSTACK/Dynamic+Role+Based+API+Access+Checker+for+CloudStack>`_.

After an upgrade, existing deployments can be migrated to use this feature by
running a migration tool by the CloudStack admin. The migration tool is located
at ``/usr/share/cloudstack-common/scripts/util/migrate-dynamicroles.py``.

**NOTE: If you have not changed your commands.properties file at any time, then
it is recommended to use the -D (default) option as otherwise new API commands may
not be added to the dynamic roles database.**

During migration, this tool enables an internal flag in the database,
copies existing static role-based rules from provided commands.properties file
(typically at ``/etc/cloudstack/management/commands.properties``) to the database
and renames the commands.properties file (typically to
/etc/cloudstack/management/commands.properties.deprecated). The migration
process does not require restarting the management server(s).

Usage: ``migrate-dynamicroles.py`` [options] [-h for help]

Options:

-b DB
    The name of the database, default: cloud
-u USER
    User name a MySQL user with privileges on cloud database, default: cloud
-p PASSWORD
    Password of a MySQL user with privileges on cloud database
-H HOST
    Host or IP of the MySQL server
-P PORT
    Host or IP of the MySQL server, default: 3306
-f FILE
    The commands.properties file, default: /etc/cloudstack/management/commands.properties
-d
    Dry run and debug operations this tool will perform
-D
    Use the default configuration for Dynamic Roles (does not import commands.properties)


Example:


.. parsed-literal::

   sudo python /usr/share/cloudstack-common/scripts/util/migrate-dynamicroles.py -u cloud -p cloud -H localhost -P 3306 -f /etc/cloudstack/management/commands.properties

   sudo python /usr/share/cloudstack-common/scripts/util/migrate-dynamicroles.py -u cloud -p cloud -H localhost -P 3306 -D

If you've multiple management servers, remove or rename the commands.properties
file on all management servers typically in /etc/cloudstack/management path,
after running the migration tool for the first management server


Dedicating Resources to Accounts and Domains
--------------------------------------------

The root administrator can dedicate resources to a specific domain or
Account that needs private infrastructure for additional security or
performance guarantees. A zone, pod, cluster, or host can be reserved by
the root administrator for a specific domain or Account. Only Users in
that domain or its subdomain may use the infrastructure. For example,
only Users in a given domain can create guests in a zone dedicated to
that domain.

There are several types of dedication available:

-  Explicit dedication. A zone, pod, cluster, or host is dedicated to an
   Account or domain by the root administrator during initial deployment
   and configuration.

-  Strict implicit dedication. A host will not be shared across multiple
   Accounts. For example, strict implicit dedication is useful for
   deployment of certain types of applications, such as desktops, where
   no host can be shared between different Accounts without violating
   the desktop software's terms of license.

-  Preferred implicit dedication. The Instance will be deployed in dedicated
   infrastructure if possible. Otherwise, the Instance can be deployed in
   shared infrastructure.


How to Dedicate a Zone, Cluster, Pod, or Host to an Account or Domain
----------------------------------------------------------------------

For explicit dedication: When deploying a new zone, pod, cluster, or
host, the root administrator can click the Dedicated checkbox, then
choose a domain or Account to own the resource.

To explicitly dedicate an existing zone, pod, cluster, or host: log in
as the root admin, find the resource in the UI, and click the Dedicate
button. |button to dedicate a zone, pod,cluster, or host|

For implicit dedication: The administrator creates a compute service
offering and in the Deployment Planner field, chooses
ImplicitDedicationPlanner. Then in Planner Mode, the administrator
specifies either Strict or Preferred, depending on whether it is
permissible to allow some use of shared resources when dedicated
resources are not available. Whenever a User creates an Instance based on this
service offering, it is allocated on one of the dedicated hosts.


How to Use Dedicated Hosts
~~~~~~~~~~~~~~~~~~~~~~~~~~~

To use an explicitly dedicated host, use the explicit-dedicated type of
affinity group (see `“Affinity Groups” <virtual_machines.html#affinity-groups>`_).
For example, when creating a new Instance, an
end User can choose to place it on dedicated infrastructure. This
operation will succeed only if some infrastructure has already been
assigned as dedicated to the User's Account or domain.


Behavior of Dedicated Hosts, Clusters, Pods, and Zones
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The administrator can live migrate Instances away from dedicated hosts if
desired, whether the destination is a host reserved for a different
Account/domain or a host that is shared (not dedicated to any particular
Account or domain). CloudStack will generate an alert, but the operation
is allowed.

Dedicated hosts can be used in conjunction with host tags. If both a
host tag and dedication are requested, the Instance will be placed only on a
host that meets both requirements. If there is no dedicated resource
available to that User that also has the host tag requested by the User,
then the Instance will not deploy.

If you delete an Account or domain, any hosts, clusters, pods, and zones
that were dedicated to it are freed up. They will now be available to be
shared by any Account or domain, or the administrator may choose to
re-dedicate them to a different Account or domain.

System VMs and virtual routers affect the behavior of host dedication.
System VMs and virtual routers are owned by the CloudStack system
Account, and they can be deployed on any host. They do not adhere to
explicit dedication. The presence of system VMs and virtual routers on a
host makes it unsuitable for strict implicit dedication. The host can
not be used for strict implicit dedication, because the host already has
VMs of a specific Account (the default system Account). However, a host
with system VMs or virtual routers can be used for preferred implicit
dedication.


Using an LDAP Server for User Authentication
--------------------------------------------

You can use an external LDAP server such as Microsoft Active Directory
or ApacheDS to authenticate CloudStack end-users. CloudStack will search
the external LDAP directory tree starting at a specified base directory
and gets User info such as first name, last name, email and username.

Starting with CloudStack 4.11, an LDAP connection per domain can be
defined. In this domain autosync per Account can be configured,
keeping the Users in the domain up to date with their group membership
in LDAP.

.. Note:: A caveat with this is that ApacheDS does not yet support the
          virtual 'memberOf' attribute needed to check if a User moved
          to another Account. Microsoft AD and OpenLDAP as well as
          OpenDJ do support this. It is a planned feature for ApacheDS
          that can be tracked in
          https://issues.apache.org/jira/browse/DIRSERVER-1844.

There are now three ways to link LDAP Users to CloudStack Users. These
three ways where developed as extensions on top of each other.

To authenticate, in all three cases username and password entered by
the User are used.

#. **manual import**. A User is explicitly mapped to a domain/Account
   and created as a User in that Account.

       #. CloudStack does a search for a User with the given username.

       #. If it exists, it checks if the User is enabled.

       #. If the User is enabled, CloudStack searches for it in LDAP
          by the configured ``ldap.username.attribute``.

       #. If the LDAP User is found, CloudStack does a bind request
          with the returned principal for that LDAP User and the
          entered password.

       #. The authentication result from LAP is honoured.

#. **autoimport**. A domain is configured to import any User if it
   does not yet exist in that domain. For these Users, an Account in the
   same name as the User is automatically created  and the User is created
   in that Account.

       #. If the domain is configured to be used with LDAP,

       #. CloudStack searches for it in LDAP by the configured
          ``ldap.username.attribute``.

       #. If an LDAP User is found, CloudStack does a bind
          request with the returned principal for that LDAP User and
          the entered password.

       #. If LDAP authentication checks out, CloudStack checks if the
          authenticated User exists in the domain it is trying to log
          on to.

          #. If the User exists in CloudStack, it is ensured to be enabled.

          #. If it doesn't exist it is created in a new Account with
             the username as names for both Account and User.

       #. In case authentication fails the User will be disabled in
          cloudstack after the configured
          ``incorrect.login.attempts.allowed`` number of attempts.

#. **autosync**. A domain is configured to use a LDAP server and in this
   domain a number of Accounts are 'mapped' against LDAP groups. Any
   User that is in one of these configured Accounts will be checked against the
   current state of LDAP and if they exist they will be asserted to be
   in the right Account according to their LDAP group. If they do not
   exist in LDAP they will be disabled in CloudStack.

       #. If the domain is configured to be used by LDAP,

       #. CloudStack searches for it in LDAP by the configured
          ``ldap.username.attribute``.

       #. If an LDAP User is found, it is checked for
          memberships of mapped Account, i.e. Accounts for which LDAP
          groups are configured.

          #. If the LDAP User has 0, 2 or more memberships the Account
             is disabled and authentication fails.

       #. CloudStack then does a bind request with the returned
          principal for that LDAP User and the entered password.

       #. If no CloudStack User exists it is created in the
          appropriate Account.

       #. If a CloudStack User exists but is not in the appropriate
          Account its credentials will be moved.

To set up LDAP authentication in CloudStack, call the CloudStack API
command ``addLdapConfiguration`` and provide Hostname or IP address
and listening port of the LDAP server. Optionally a domain id can be
given for the domain for which this LDAP connection is valid. You could
configure multiple servers as well, for the same domain. These are expected to be
replicas. If one fails, the next one is used.

.. code:: bash

	  cloudmonkey add ldapconfiguration hostname=localhost\
	                                    port=389\
					    domainid=12345678-90ab-cdef-fedc-ba0987654321

This is all that is required to enable the manual importing of LDAP Users, the
LisLdapUsers API can be used to query for Users to import.

For the auto import method, a CloudStack Domain needs to be linked to
LDAP. For instance

.. code:: bash

          cloudmonkey link domaintoldap domainid=12345678-90ab-cdef-fedc-ba0987654321\
                                        accounttype=2\
                                        ldapdomain="ou=people,dc=cloudstack,dc=apache,dc=org"\
	                                type=OU

When you want to use auto sync, no domain is linked to ldap but one or
more Accounts. Within a CloudStack domain one needs to link Accounts
to LDAP groups. The linkage of the domain is implicit and nit needed
to be applied through the API call described above.

.. code:: bash

   #!/bin/bash
   [ -z "$LDAP1PASSWORD" -o -z "$LDAP2PASSWORD" ] && exit 1
   ROOTDOMAIN=`cloudmonkey -d json list domains name=ROOT filter=id | jq .domain[0].id`

   # mapping domain and Account(s) from ldap server 1
   MAPPEDDOMAIN1=`cloudmonkey -d json create domain name=mappedDomain1 parentdomainid=$ROOTDOMAIN | jq .domain.id`
   cloudmonkey -d json add ldapconfiguration hostname=10.1.2.5 port=389 domainid=$MAPPEDDOMAIN1
   cloudmonkey -d json update configuration domainid=$MAPPEDDOMAIN1 name="ldap.basedn" value="dc=cloudstack,dc=apache,dc=org"
   cloudmonkey -d json update configuration domainid=$MAPPEDDOMAIN1 name='ldap.bind.principal' value='cn=admin,dc=cloudstack,dc=apache,dc=org'
   cloudmonkey -d json update configuration domainid=$MAPPEDDOMAIN1 name='ldap.bind.password' value=$LDAP1PASSWORD
   cloudmonkey -d json update configuration domainid=$MAPPEDDOMAIN1 name='ldap.search.group.principle' value='cn=AcsAccessGroup,dc=cloudstack,dc=apache,dc=org'
   cloudmonkey -d json update configuration domainid=$MAPPEDDOMAIN1 name='ldap.user.memberof.attribute' value='memberOf'

   cloudmonkey -d json ldap createaccount account='seniors' accounttype=2 domainid=$MAPPEDDOMAIN1 username=guru
   cloudmonkey -d json link accounttoldap account='seniors' accounttype=2 domainid=$MAPPEDDOMAIN1 ldapdomain='cn=AcsSeniorAdmins,ou=AcsGroups,dc=cloudstack,dc=apache,dc=org' type=GROUP
   cloudmonkey -d json ldap createaccount account='juniors' accounttype=0 domainid=$MAPPEDDOMAIN1 username=bystander
   cloudmonkey -d json link accounttoldap account='juniors' accounttype=0 domainid=$MAPPEDDOMAIN1 ldapdomain='cn=AcsJuniorAdmins,ou=AcsGroups,dc=cloudstack,dc=apache,dc=org' type=GROUP



In addition to those shown in the example script above, the following
configuration items can be configured (the default values are for
openldap)

-  ``ldap.basedn``:	Sets the basedn for LDAP. Ex: **OU=APAC,DC=company,DC=com**

-  ``ldap.bind.principal``, ``ldap.bind.password``: DN and password for a User
   who can list all the Users in the above basedn. Ex:
   **CN=Administrator, OU=APAC, DC=company, DC=com**

-  ``ldap.user.object``: object type of Users within LDAP. Defaults value is
   **user** for AD and **interorgperson** for openldap.

-  ``ldap.email.attribute``: email attribute within ldap for a User. Default
   value for AD and openldap is **mail**.

-  ``ldap.firstname.attribute``: firstname attribute within ldap for a User.
   Default value for AD and openldap is **givenname**.

-  ``ldap.lastname.attribute``: lastname attribute within ldap for a User.
   Default value for AD and openldap is **sn**.

-  ``ldap.username.attribute``: username attribute for a User within LDAP.
   Default value is **SAMAccountName** for AD and **uid** for openldap.


Restricting LDAP Users to a group:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  ``ldap.search.group.principle``: this is optional and if set only Users from
   this group are listed.


LDAP SSL:
~~~~~~~~~

If the LDAP server requires SSL, you need to enable the below configurations.
Before enabling SSL for LDAP, you need to get the certificate which the LDAP server is using and add it to a trusted keystore.
You will need to know the path to the keystore and the password.

-  ``ldap.truststore`` : truststore path
-  ``ldap.truststore.password`` : truststore password


LDAP groups:
~~~~~~~~~~~~

-  ``ldap.group.object``: object type of groups within LDAP. Default value is
   group for AD and **groupOfUniqueNames** for openldap.

-  ``ldap.group.user.uniquemember``: attribute for uniquemembers within a group.
   Default value is **member** for AD and **uniquemember** for openldap.

Once configured, on Add Account page, you will see an "Add LDAP Account" button
which opens a dialog and the selected Users can be imported.

.. figure:: /_static/images/CloudStack-ldap-screen1.png
   :align:   center


You could also use api commands:
``listLdapUsers``, to list Users in LDAP that could or would be imported in CloudStack
``ldapCreateAccount``, to manually create a User in a specific Account
``importLdapUsers``, to batch import Users from LDAP

Once LDAP is enabled, the Users will not be allowed to changed password
directly in CloudStack.

.. |button to dedicate a zone, pod,cluster, or host| image:: /_static/images/dedicate-resource-button.png

Using a SAML 2.0 Identity Provider for User Authentication
----------------------------------------------------------

You can use a SAML 2.0 Identity Provider with CloudStack for User
authentication. This will require enabling the SAML 2.0 service provider plugin
in CloudStack. To do that first, enable the SAML plugin by setting
``saml2.enabled`` to ``true`` and restart management server.

Starting 4.5.2, the SAML plugin uses an authorization workflow where Users should
be authorized by an admin using ``authorizeSamlSso`` API before those Users can
use Single Sign On against a specific IDP. This can be done by ticking the enable
SAML Single Sign On checkbox and selecting a IDP when adding or importing Users.
For existing Users, admin can go to the User's page and click on configure
SAML SSO option to enable/disable SSO for a User and select a Identity Provider.
A User can be authorized to authenticate against only one IDP.

The CloudStack service provider metadata is accessible using the
``getSPMetadata`` API command, or from the URL
http://acs-server:8080/client/api?command=getSPMetadata where acs-server is the
domain name or IP address of the management server. The IDP administrator can
get the SP metadata from CloudStack and add it to their IDP server.

To start a SAML 2.0 Single Sign-On authentication, on the login page Users need to
select the Identity Provider or Institution/Department they can authenticate with
and click on Login button. This action call the ``samlsso`` API command which
will redirect the User to the Identity Provider's login page. Upon successful
authentication, the IdP will redirect the User to CloudStack. In case a User has
multiple User Accounts with the same username (across domains) for the same
authorized IDP, that User would need to specify domainpath after selecting their
IDP server from the dropdown list. By default, Users don't need to specify any
domain path. After a User is successfully authenticated by an IDP server, the SAML
authentication plugin finds User Accounts whose username match the username
attribute value returned by the SAML authentication response; it fails
only when it finds that there are multiple User Accounts with the same User name
for the specific IDP otherwise the unique useraccount is allowed to proceed and
the User is logged into their Account.

Limitations:

- The plugin uses a User attribute returned by the IDP server in the SAML response
  to find and map the authorized User in CloudStack. The default attribute is `uid`.

- The SAML authentication plugin supports HTTP-Redirect and HTTP-Post bindings.

- Tested with Shibboleth 2.4, SSOCircle, Microsoft ADFS, OneLogin, Feide OpenIDP,
  PingIdentity.

The following global configuration should be configured:

- ``saml2.enabled``: Indicates whether SAML SSO plugin is enabled or not true. Default is **false**

- ``saml2.sp.id``: SAML2 Service Provider Identifier string

- ``saml2.idp.metadata.url``: SAML2 Identity Provider Metadata XML Url or Filename. If a URL is not provided, it will look for a file in the config directory /etc/cloudstack/management

- ``saml2.default.idpid``: The default IdP entity ID to use only in case of multiple IdPs

- ``saml2.sigalg``: The algorithm to use to when signing a SAML request. Default is SHA1, allowed algorithms: SHA1, SHA256, SHA384, SHA512.

- ``saml2.redirect.url``: The CloudStack UI url the SSO should redirected to when successful. Default is **http://localhost:8080/client**

- ``saml2.sp.org.name``: SAML2 Service Provider Organization Name

- ``saml2.sp.org.url``: SAML2 Service Provider Organization URL

- ``saml2.sp.contact.email``: SAML2 Service Provider Contact Email Address

- ``saml2.sp.contact.person``: SAML2 Service Provider Contact Person Name

- ``saml2.sp.slo.url``: SAML2 CloudStack Service Provider Single Log Out URL

- ``saml2.sp.sso.url``: SAML2 CloudStack Service Provider Single Sign On URL

- ``saml2.user.attribute``: Attribute name to be looked for in SAML response that will contain the username. Default is **uid**

- ``saml2.timeout``: SAML2 IDP Metadata refresh interval in seconds, minimum value is set to 300. Default is 1800

Using OAuth2 Authentication For Users
------------------------------------------

OAuth2, the industry-standard authorization or authentication framework, simplifies the process of
granting access to resources. CloudStack supports OAuth2 authentication wherein users can login into
CloudStack without using username and password. CloudStack currently supports Google and Github providers.
Other OAuth2 providers can be easily integrated with CloudStack using its plugin framework.

For admins, the following are the settings available at global level to configure OAuth2.

.. cssclass:: table-striped table-bordered table-hover

================================================   ================   ===================================================================
Global setting                                     Default values     Description
================================================   ================   ===================================================================
oauth2.enabled                                     false              Indicates whether OAuth plugin is enabled or not
oauth2.plugins                                     google,github      List of OAuth plugins
oauth2.plugins.exclude                                                List of OAuth plugins which are excluded
================================================   ================   ===================================================================

The login page when the OAuth2 is enabled and corresponding providers are configured.

.. image:: /_static/images/oauth-login.png
   :width: 400px
   :align: center
   :alt: Login page with OAuth logins

"OAuth configuration" sub-section is added under "Configuration" where admins can register the corresponding
OAuth providers.

.. image:: /_static/images/oauth-sub-section.png
   :width: 120px
   :align: center
   :alt: OAuth configuration section

.. image:: /_static/images/oauth-configuration-details.png
   :width: 400px
   :align: center
   :alt: OAuth configuration details

To register the OAuth provider client ID, redirect URI, secret key have to provided.
OAuth 2.0 has to be first configured in the corresponding provider to obtain the client ID, redirect URI, secret Key.

For Google, please follow the instructions mentioned here `"Setting up OAuth 2.0 in Google" <https://support.google.com/cloud/answer/6158849?hl=en>`_.
For Github, please follow the instructions mentioned here `"Setting up OAuth 2.0 in Github" <https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/creating-an-oauth-app>`_.

In any OAuth 2.0 configuration admin has to use the redirect URI "http://<management server IP>:<port>/#/verifyOauth"

.. Note:: [Google OAuth 2.0 redirect URI] :
          Google OAuth 2.0 configuration wont accept '#' in the URI, please use "http://<management server Domain>:<port>/?verifyOauth"
          Google does not accept direct IP address in the redirect URI, it must be a domain. As a workaround one can add the management
          server IP to host table in the local system and assign a domain, something like "management.cloud". In that redirect URI looks like
          "http://management.cloud:8080/?verifyOauth"

.. image:: /_static/images/oauth-provider-registration.png
   :width: 400px
   :align: center
   :alt: OAuth provider registration

Following are the details needs to be provided to register the OAuth provider, this is to call the API "registerOauthProvider"

   -  **Provider**: Name of the provider from the list of OAuth providers supported in CloudStack

   -  **Description**: A short description for the provider

   -  **Provider Client ID**: Client ID pre-registered in the specific OAuth provider

   -  **Redirect URI**: Redirect URI pre-registered in the specific OAuth provider

   -  **Secret Key**: Secret Key pre-registered in the specific OAuth provider

Cloudmonkey API call looks like

   -  register oauthprovider provider=google description="Google Provider"
      clientid="http://345798102268-3kp6qd6c16v6b9av2tmvqagj40na30l4.apps.googleusercontent.com"
      redirecturi="http://local.cloud:8080/?verifyOauth" secretkey="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"

Email address is the key to identify the user in CloudStack. In case if user belongs to any specific domain, domain name
has to be provided in the login form and then click on OAuth login.

.. image:: /_static/images/user-domain-login.png
   :width: 400px
   :align: center
   :alt: Login page for user under specific domain

Using Two Factor Authentication For Users
------------------------------------------

CloudStack supports two factor authentication wherein Users need to provide a 2FA code after the
regular login using username and password. CloudStack currently supports Google Authenticator or
other TOTP authenticators and static PIN as the 2FA providers. Other 2FA providers can be easily
integrated with CloudStack using its plugin model.

.. Note:: 2FA is applicable to authentication mechanisms in CloudStack using username/password,
          LDAP, SAML. While using apikey/secretkey 2FA checks will be bypassed.

For admins, the following are the settings available at global and domain level to configure 2FA.

.. cssclass:: table-striped table-bordered table-hover

================================================   ================   ===================================================================
Global setting                                     Default values     Description
================================================   ================   ===================================================================
enable.user.2fa                                    false              Determines whether 2FA is enabled or not
mandate.user.2fa                                   false              Determines whether to make the 2FA mandatory or not for the Users
user.2fa.default.provider                          totp               The default User 2FA provider plugin. Eg. totp, staticpin
================================================   ================   ===================================================================

If 2FA is configured for the User, the 2FA verification page looks like below after the login.

The verification page when the User configures 2FA using Google or other TOTP Authenticators.

.. image:: /_static/images/verify-2fa-totp.png
   :width: 400px
   :align: center
   :alt: Verify 2FA page using TOTP

The verification page when the User configures 2FA using Static PIN.

.. image:: /_static/images/verify-2fa-staticpin.png
   :width: 400px
   :align: center
   :alt: Verify 2FA page using static PIN

Users can configure 2FA in CloudStack using the action button in User form.

.. image:: /_static/images/configure-2fa-action-button.png
   :width: 400px
   :align: center
   :alt: Configure 2FA action button


In the 2FA setup form, the User needs to select one of the providers. CloudStack currently supports
Google Authenticator or other TOTP Authenticators and static PIN as the 2FA providers.

When the Google Authenticator or other TOTP 2FA provider is selected, the User must setup the Account in
the respective application in their device by either scanning the QR code or using the setup key provided
by CloudStack. Once this is set up in the authenticator application, the User must always use the provided
2FA codes to log in.

.. image:: /_static/images/configure-google-2fa-form.png
   :width: 400px
   :align: center
   :alt: Configure Google 2FA form


When the static PIN 2FA provider is selected, the User must use the static PIN as the code to verify 2FA
with CloudStack. The User must input this static PIN as a 2FA code every time they need to login.

.. image:: /_static/images/configure-staticpin-2fa-form.png
   :width: 400px
   :align: center
   :alt: Configure static PIN 2FA form

The admin has the capability to mandate 2FA for Users via the setting ``mandate.user.2fa``.
In this case the User must configure 2FA during their first login into CloudStack.

The User's first login page to configure 2FA looks like the below.

.. image:: /_static/images/configure-2fa-at-login-page.png
   :width: 400px
   :align: center
   :alt: Configure 2FA at login page


For the existing Users, the admin can mandate 2FA using the 'updateUser' API with the parameter 'mandate2FA'.

The admin can also disable 2FA for a User using the action button as shown below.

.. image:: /_static/images/disable-2fa.png
   :width: 400px
   :align: center
   :alt: Disable 2FA action button

.. Note:: [2FA Recovery process] :
          If the User loses the authenticator application or forgets the static PIN, then the User must
          contact admin to disable 2FA.
          If the admin themself loses the authenticator application or forgets the static PIN, then the admin
          will have to either use apikey to disable 2FA using the API setupUserTwoFactorAuthentication with
          enable flag to false or to do the database changes in 'user' table by clearing the columns
          'is_user_2fa_enabled', 'key_for_2fa', 'user_2fa_provider' for the specific entry.