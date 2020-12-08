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

.. _log-in-to-ui:

Log In to the UI
----------------

CloudStack provides a web-based UI that can be used by both
administrators and end users. The appropriate version of the UI is
displayed depending on the credentials used to log in. The UI is
available in all modern popular browsers including Chrome, Firefox, Edge and
Safari. The UI uses API auto-discovery to discover APIs allowed for a logged-in
user and creates navigation and views based on that, and requires the following:

- API discovery (listApis) enabled for all roles that must use the UI
- Modern browsers that are `ES5-compliant <https://github.com/vuejs/vue#browser-compatibility>`_

The URL is: (substitute your own management server IP address)

.. parsed-literal::

   http://<management-server-ip-address>:8080/client

On a fresh Management Server installation, a guided tour splash screen
appears. On later visits, you’ll see a login screen where you specify
the following to proceed to your Dashboard:

Username -> The user ID of your account. The default username is admin.

Password -> The password associated with the user ID. The password for 
the default username is password.

Domain -> If you are a root user, leave this field blank.

If you are a user in the sub-domains, enter the full path to the domain,
excluding the root domain.

For example, suppose multiple levels are created under the root domain,
such as Comp1/hr. The users in the Comp1 domain should enter Comp1 in
the Domain field, whereas the users in the Comp1/sales domain should
enter Comp1/sales.

For more guidance about the choices that appear when you log in to this
UI, see Logging In as the Root Administrator.


End User's UI Overview
~~~~~~~~~~~~~~~~~~~~~~

The CloudStack UI helps users of cloud infrastructure to view and use
their cloud resources, including virtual machines, templates and ISOs,
data volumes and snapshots, guest networks, and IP addresses. If the
user is a member or administrator of one or more CloudStack projects,
the UI can provide a project-oriented view.


Root Administrator's UI Overview
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: https://raw.githubusercontent.com/apache/cloudstack-primate/master/docs/screenshot-dashboard.png
   :width: 800px
   :alt: alternate text
   :align: left

The CloudStack UI helps the CloudStack administrator provision, view,
and manage the cloud infrastructure, domains, user accounts, projects,
and configuration settings. The first time you start the UI after a
fresh Management Server installation, you can choose to follow a guided
tour to provision your cloud infrastructure. On subsequent logins, the
dashboard of the logged-in user appears. The various links in this
screen and the navigation bar on the left provide access to a variety of
administrative functions. The root administrator can also use the UI to
perform all the same tasks that are present in the end-user’s UI.


Logging In as the Root Administrator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After the Management Server software is installed and running, you can
run the CloudStack user interface. This UI is there to help you
provision, view, and manage your cloud infrastructure.

#. Open your favorite Web browser and go to this URL. Substitute the IP
   address of your own Management Server:

   .. parsed-literal::

      http://<management-server-ip-address>:8080/client

   After logging into a fresh Management Server installation, a guided
   tour splash screen appears. On later visits, you’ll be taken directly
   into the Dashboard.

#. If you see the first-time splash screen, choose one of the following.

   -  **Continue with basic setup.** Choose this if you're just trying
      CloudStack, and you want a guided walkthrough of the simplest
      possible configuration so that you can get started right away.
      We'll help you set up a cloud with the following features: a
      single machine that runs CloudStack software and uses NFS to
      provide storage; a single machine running VMs under the XenServer
      or KVM hypervisor; and a shared public network.

      The prompts in this guided tour should give you all the
      information you need, but if you want just a bit more detail, you
      can follow along in the Trial Installation Guide.

   -  **I have used CloudStack before.** Choose this if you have already
      gone through a design phase and planned a more sophisticated
      deployment, or you are ready to start scaling up a trial cloud
      that you set up earlier with the basic setup screens. In the
      Administrator UI, you can start using the more powerful features
      of CloudStack, such as advanced VLAN networking, high
      availability, additional network elements such as load balancers
      and firewalls, and support for multiple hypervisors including
      Citrix XenServer, KVM, and VMware vSphere.

      The root administrator Dashboard appears.

#. You should set a new root administrator password. If you chose basic
   setup, you’ll be prompted to create a new password right away. If you
   chose experienced user, use the steps in :ref:`changing-root-password`.

.. warning::
   You are logging in as the root administrator. This account manages the 
   CloudStack deployment, including physical infrastructure. The root 
   administrator can modify configuration settings to change basic 
   functionality, create or delete user accounts, and take many actions 
   that should be performed only by an authorized person. Please change 
   the default password to a new, unique password.

.. _changing-root-password:

Changing the Root Password
~~~~~~~~~~~~~~~~~~~~~~~~~~

During installation and ongoing cloud administration, you will need to
log in to the UI as the root administrator. The root administrator
account manages the CloudStack deployment, including physical
infrastructure. The root administrator can modify configuration settings
to change basic functionality, create or delete user accounts, and take
many actions that should be performed only by an authorized person. When
first installing CloudStack, be sure to change the default password to a
new, unique value.

#. Open your favorite Web browser and go to this URL. Substitute the IP
   address of your own Management Server:

   .. parsed-literal::

      http://<management-server-ip-address>:8080/client

#. Log in to the UI using the current root user ID and password. The
   default is admin, password.

#. Click Accounts.

#. Click the admin account name.

#. Click View Users.

#. Click the admin user name.

#. Click the Change Password button. |change-password.png|

#. Type the new password, and click OK.

Basic UI Customization
~~~~~~~~~~~~~~~~~~~~~~

Users can now customize the CloudStack's user interface by means of a configuration file at /usr/share/cloudstack-management/webapp/config.json which can be used to modify the theme, logos, etc. to align to one's requirement.

To change the logo, login banner, error page icon, etc. the following details can be edited in config.json:

.. parsed-literal::

    "logo": "assets/logo.svg",
    "banner": "assets/banner.svg",
    "error": {
        "404": "assets/404.png",
        "403": "assets/403.png",
        "500": "assets/500.png"
    }

where,

- logo: changes the logo top-left side image.
- banner: changes the login banner image.
- error.404: changes the image of error Page not found.
- error.403: changes the image of error Forbidden.
- error.500: changes the image of error Internal Server Error.

Customization of themes is also possible, such as, modifying banner width, general color, etc. This can be done by editing the "theme" section of the config.json file:

.. parsed-literal::

    "theme": {
        "@logo-background-color": "#ffffff",
        "@project-nav-text-color": "#001529",
        "@navigation-text-color": "rgba(255, 255, 255, 0.65)",
        "@navigation-background-color": "#ffffff",
        "@navigation-text-color": "rgba(0, 0, 0, 0.65)",
        "@primary-color": "#1890ff",
        "@link-color": "#1890ff",
        "@link-hover-color": "#40a9ff",
        "@loading-color": "#1890ff",
        "@processing-color": "#1890ff",
        "@success-color": "#52c41a",
        "@warning-color": "#faad14",
        "@error-color": "#f5222d",
        "@font-size-base": "14px",
        "@heading-color": "rgba(0, 0, 0, 0.85)",
        "@text-color": "rgba(0, 0, 0, 0.65)",
        "@text-color-secondary": "rgba(0, 0, 0, 0.45)",
        "@disabled-color": "rgba(0, 0, 0, 0.25)",
        "@border-color-base": "#d9d9d9",
        "@border-radius-base": "4px",
        "@box-shadow-base": "0 2px 8px rgba(0, 0, 0, 0.15)",
        "@logo-width": "256px",
        "@logo-height": "64px",
        "@banner-width": "700px",
        "@banner-height": "110px",
        "@error-width": "256px",
        "@error-height": "256px"
    }

where,

- @logo-background-color changes the logo background color.
- @project-nav-background-color changes the navigation menu background color of the project.
- @project-nav-text-color changes the navigation menu background color of the project view.
- @navigation-background-color changes the navigation menu background color.
- @navigation-text-color changes the navigation text color.
- @primary-color: changes the major background color of the page (background button, icon hover, etc).
- @link-color changes the link color.
- @link-hover-color changes the link hover color.
- @loading-color changes the message loading color and page loading bar at the top page.
- @success-color: changes success state color.
- @processing-color: changes processing state color. Exp: progress status.
- @warning-color: changes warning state color.
- @error-color: changes error state color.
- @heading-color: changes table header color.
- @text-color: change in major text color.
- @text-color-secondary: change of secondary text color (breadcrumb icon).
- @disabled-color: disable state color (disabled button, switch, etc).
- @border-color-base: change in major border color.
- @logo-width: change the width of the logo top-left side.
- @logo-height: change the height of the logo top-left side.
- @banner-width: changes the width of the login banner.
- @banner-height: changes the height of the login banner.
- @error-width: changes the width of the error image.
- @error-height: changes the height of the error image.

Some assorted primary theme colours:

- Blue: #1890FF
- Red: #F5222D
- Yellow: #FAAD14
- Cyan: #13C2C2
- Green: #52C41A
- Purple: #722ED1

Advanced Customisation
~~~~~~~~~~~~~~~~~~~~~~

The advanced UI customisation is possible only by changing JavaScript based config
files which define rules for sections, names, icons, actions and components and by
building the UI from the source available on `github.com/apache/cloudstack
<https://github.com/apache/cloudstack>`_ repository. Advanced customisation may
require some experience in JavaScript and VueJS, a development and customisation
guide in the source repository.

Known Limitations
~~~~~~~~~~~~~~~~~

The following features are no longer supported or available:

- Deployment of a basic zone is not supported. However, existing basic zones will continue to be supported as well as all the actions and views of various resources within the existing basic zone.
- Support for S3 based secondary storage.
- NFS secondary staging storage list/resource view and add/update actions.
- SSL certificate for Guest network LB rule.
- Regions.

.. |change-password.png| image:: /_static/images/change-password.png
   :alt: button to change a user's password
