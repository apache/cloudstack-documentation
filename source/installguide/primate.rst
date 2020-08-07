.. Licensed to the Apache Software Foundation (ASF) under one
   or more contributor license agreements.  See the NOTICE file
   distributed with this work for additional information
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

Primate Guide
=============

What is Primate?
~~~~~~~~~~~~~~~~

Apache CloudStack Primate is a modern role-based progressive UI based on Vue.js
and Ant Design for Apache CloudStack.

.. image:: https://raw.githubusercontent.com/apache/cloudstack-primate/master/docs/screenshot-dashboard.png
   :width: 800px
   :alt: alternate text
   :align: left

Primate GA was released with CloudStack 4.15, where the legacy UI is deprecated,
and will be removed in an eventual major CloudStack release.

`User participation in the community mailing lists
<http://cloudstack.apache.org/mailing-lists.html>`_ is encouraged. Users may
also log issues on Github https://github.com/apache/cloudstack-primate/issues

Requirements
~~~~~~~~~~~~

Primate uses API auto-discovery to discover APIs allowed for a logged-in user
and creates navigation and views based on that.
- Apache CloudStack 4.15 or later
- API auto-discovery (listApis enabled)
- All modern browsers that are `ES5-compliant <https://github.com/vuejs/vue#browser-compatibility>`_

In theory Primate can work with any older version of CloudStack.
However, several Primate list views require API pagination support, some of which are
available starting Apache CloudStack 4.15 as well as several other additions which
might not be available prior to Apache CloudStack 4.15.

Installation on CentOS
~~~~~~~~~~~~~~~~~~~~~~

Users running management server (4.15 or above) on CentOS can setup the
following Primate repository:

.. parsed-literal::

    rpm --import https://download.cloudstack.org/primate/release.asc
    cat << EOF > /etc/yum.repos.d/cloudstack-primate.repo
    [cloudstack-primate]
    name=cloudstack
    baseurl=https://download.cloudstack.org/primate/centos/
    enabled=1
    gpgcheck=1
    gpgkey=https://download.cloudstack.org/primate/release.asc
    EOF

Next, install Primate:

.. parsed-literal::

    yum install cloudstack-primate

Note: there is no need to restart management server post-installation, and
after installation the UI can be accessed on
management-server-host:8080/client/primate using any modern browser.

Installation on Ubuntu
~~~~~~~~~~~~~~~~~~~~~~

Users running CloudStack management server (4.15 or above) on Ubuntu can setup the following Primate repository:

.. parsed-literal::

    apt-key adv --keyserver keys.gnupg.net --recv-keys BDF0E176584DF93F
    echo deb https://download.cloudstack.org/primate/debian / > /etc/apt/sources.list.d/cloudstack-primate.list

Next, install Primate:

.. parsed-literal::

    apt-get update
    apt-get install cloudstack-primate

Note: there is no need to restart management server post-installation, and
after installation the UI can be accessed on
management-server-host:8080/client/primate using any modern browser.

Using Archive
~~~~~~~~~~~~~

Primate archives are tarballs of single-page app builds. They can be simply
downloaded and extracted to the management server webapp directory or hosted
with a custom webserver.

Users can download the builds from https://download.cloudstack.org/primate/archive/

Using Docker
~~~~~~~~~~~~

Users can use docker builds of Primate from https://hub.docker.com/r/apache/cloudstack-primate

For example:

.. parsed-literal::

    docker pull apache/cloudstack-primate:latest
    docker run -ti --rm -p 8080:80 -v $(pwd)/nginx:/etc/nginx/conf.d:ro apache/cloudstack-primate:latest

Example nginx config:

.. parsed-literal::

    server {
        listen       80;
        server_name  localhost;
        location / {
            root   /usr/share/nginx/html;
            index  index.html;
        }
        location /client/ {
            # http://127.0.0.1:8080 should be replaced your CloudStack management
            # Server's actual URI
            proxy_pass   http://127.0.0.1:8080;
        }
    }

Basic Customization in CloudStack Primate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Users can now customize the CloudStack's user interface by means of a configutaion file - config.json found at
https://github.com/apache/cloudstack-primate/tree/master/public. The public/config.json file (or correspondingly, the dist/config.json file, after build, which is available at /usr/share/cloudstack-management/webapp/primate/) can be used to modify the theme, logos, etc. to align to one's requirement.

To change the logo,login banner,error page icon, etc. the following details can be editted in config.json:

.. parsed-literal::

    "logo": "assets/logo.svg",
    "banner": "assets/banner.svg",
    "error": {
        "404": "assets/404.png",
        "403": "assets/403.png",
        "500": "assets/500.png"
    }

where,

- logo changes the logo top-left side image.
- banner changes the login banner image.
- error.404 change the image of error Page not found.
- error.403 change the image of error Forbidden.
- error.500 change the image of error Internal Server Error.

Customization of themes is also possible, such as, modifying banner width, general color, etc. Thsi can be done by editting the "theme" section of the config.json file:

.. parsed-literal::

    "theme": {
        "@primary-color": "#1890ff",
        "@link-color": "#1890ff",
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

- @primary-color change the major background color of the page (background button, icon hover, etc).
- @success-color change success state color.
- @processing-color change processing state color. Exp: progress status.
- @warning-color change warning state color.
- @error-color change error state color.
- @heading-color change table header color.
- @text-color change in major text color.
- @text-color-secondary change of secondary text color (breadcrumb icon).
- @disabled-color change disable state color (disabled button, switch, etc).
- @border-color-base change in major border color.
- @logo-width change the width of the logo top-left side.
- @logo-height change the height of the logo top-left side.
- @banner-width changes the width of the login banner.
- @banner-height changes the height of the login banner.
- @error-width changes the width of the error image.
- @error-height changes the height of the error image.

Some assorted primary theme colours:

- Blue: #1890FF
- Red: #F5222D
- Yellow: #FAAD14
- Cyan: #13C2C2
- Green: #52C41A
- Purple: #722ED1

Also, to add other properties, we can use the theme.config.js file which based on the Ant Design Vue Less variable. Refer: https://www.antdv.com/docs/vue/customize-theme/#Ant-Design-Vue-Less-variables
These properties can then be modified or set in the config.json file. On refresh Vue's modify variable enables the run-time modification of Less variables. When called with new values, the Less file is recompiled without reloading.

CloudStack Primate also supports adding custom plugins, which can be defined in config.json. These plugins are then implemented as iframes in Primate.

.. parsed-literal ::

    "plugins": [
        {
          "name": "ExamplePlugin",
          "icon": "appstore",
          "path": "example.html"
        }
    ]

Advanced Customization
~~~~~~~~~~~~~~~~~~~~~~

CloudStack Primate has been developed in a way that makes it easy for one to add new features/components with minimal effort as most of the complexity has been abstracted by means of auto-generation of basic forms.

Defining a new Section
~~~~~~~~~~~~~~~~~~~~~~

A new section may be added by creating a javascript file in **src/config/section/** of the root directory. Correspondingly, this newly added configuration file (e.g., newSection.js), defining the section, needs to be imported in the **src/config/router.js** configuration file and rules need to be added to the *asyncRouterMap*, so as to render the matched component for the given path

.. code-block :: javascript

    import newSection from '@/config/section/newSection'

    [ ... snipped ... ]

    generateRouterMap(newSection),

An existing or new section config/js file must export the following parameters:

- name: unique path in URL
- title: the name to be displayed in navigation and breadcrumb
- icon: the icon to be displayed, from AntD's icon set https://vue.ant.design/components/icon/
- children: (optional) array of resources sub-navigation under the parent group
- permission: when children are not defined, the array of API to check against allowed auto-discovered APIs
- columns: when children is not defined, list of column keys
- component: when children is not defined, the custom component for rendering the route view

For example, see src/config/section/compute.js and src/config/section/project.js.

The children should have:

- name: unique path in the URL
- title: the name to be displayed in navigation and breadcrumb
- icon: the icon to be displayed, from AntD's icon set https://vue.ant.design/components/icon/
- permission: the array of API to check against auto-discovered APIs
- columns: list of column keys for list view rendering
- details: list of keys for detail list rendering for a resource
- tabs: array of custom components that will get rendered as tabs in the resource view
- component: the custom component for rendering the route view default list view (table)
- actions: arrays of actions/buttons
- related: a list of associated entitiy types that can be listed via passing the current resource's id as a parameter in their respective list api

Action API
~~~~~~~~~~

If a user wants to add an action button to perform as the name implies a specific action, without having to implement a custom component, one may use the Action API in the correspondins section's javascript file. The sections are defined under src/config/section path of the root directory.
The actions defined for a child shows up as a group of buttons on the default autogen view (that shows tables, actions etc.). Each action item should define:


- api: The CloudStack API for the action
- icon: the icon to be displayed from AntD's icon set https://vue.ant.design/components/icon/
- label: The action button's name
- message: The action button's confirmation message
- docHelp: Allows to provide a link to a document to provide details on the action
- listView: (boolean) whether to show the action button in list view (table)
- dataView: (boolean) whether to show the action button in resource/data view
- groupAction: Whether the button supports groupable actions when multiple items are selected in the table
- args: list of API arguments to render/show on auto-generated action form
- mapping: The relation of an arg to an api (from which it's id is used as a select-option) or a given hardcoded list of select-options
- show: function that takes in a records and returns a boolean to control if the action button needs to be shown or hidden
- popup: (boolean) when true, displays any custom component in a popup modal than in its separate route view
- component: the custom component to render the action (in a separate route view)

For example:

.. code-block:: javascript

        actions: [
            {
              api: 'updateVirtualMachine',
              icon: 'edit',
              label: 'label.action.edit.instance',
              message: 'message.action.edit.instance',
              docHelp: 'adminguide/virtual_machines.html#changing-the-vm-name-os-or-group',
              dataView: true,
              args: ['name', 'displayname', 'ostypeid', 'isdynamicallyscalable', 'haenable', 'group'],
              show: (record) => { return ['Stopped'].includes(record.state) }
            }
        ]

However, if one's requirement is to perform further operations as part of their form, then a custom Vue component must be defined under the src/views/<component> folder of the root directory and the defined component must them be imported in the corresponding section's javascript file. Examples of how to create such views are available in the cloudstack-primate repository

For example:

.. code-block:: javascript

    actions: [
        {
          api: 'deployVirtualMachine',
          icon: 'plus',
          label: 'label.vm.add',
          docHelp: 'adminguide/virtual_machines.html#creating-vms',
          listView: true,
          component: () => import('@/views/compute/DeployVM.vue')
        }
    ]

Resource List View
~~~~~~~~~~~~~~~~~~
After having, defined a section and the actions that can be performed in the particular section; on navigating to the section, we can have a list of resources available, for example,On navigating to **Compute > Instances** section, we see a list of all the VM instances (each instance referred to as a resource).
The columns that should be made available while displaying the list of resources can be defined in the section's configuration file under the columns attribute (as mentioned above). **columns** maybe defined as an array or a function in case we need to selectively (i.e., based on certain conditions) restrict the view of certain columns.
For example:

.. code-block :: javascript

    ...
    // columns defined as an array
    columns: ['name', 'state', 'displaytext', 'account', 'domain'],

    // columns can also be defined as a function, so as to conditionally restrict view of certain columns
    columns: () => {
        var fields = ['name', 'hypervisor', 'ostypename']
        if (['Admin', 'DomainAdmin'].includes(store.getters.userInfo.roletype)) {
          fields.push('account')
        }
        ...
    }

Resource Detail View Customization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
From the List View of the resources, on can navigate to the individual resource's detail view, which in CloudStack Primate we refer to as the *Resource View* by click on the specific resource.
The Resource View has 2 sections:
- InfoCard to the left that has basic/ minimal details of that resource
- and the tabs to the right that can be either defined as custom components or if we just want basic details of the resource to be displayed we may use the *DetailsTab* to render the required details of the resource. You can control what needs to be displayed by spcifying their names in the *details* array.
The names specified in the details array should correspond to the api parameters

For example,

.. code-block :: javascript

    ...
    details: ['name', 'id', 'displaytext', 'projectaccountname', 'account', 'domain'],
    ...

    // To render the above mentioned details in the right section of the Resource View, we must import the DetailsTab
    tabs: [
    {
      name: 'details',
      component: () => import('@/components/view/DetailsTab.vue')
    },
    ...
    ]

Additional tabs can be defined by adding on to the tabs section.

Known Issues and Missing Features
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Support for S3 based secondary storage
- Metrics view cell-colouring
- List and switch accounts for saml authorised accounts/domain for a logged in SAML user
- NFS secondary staging storage list/resource view and add/update actions
- Regions
- Guest network LB support for SSL certificate

Please also refer to open issues on https://github.com/apache/cloudstack-primate/issues