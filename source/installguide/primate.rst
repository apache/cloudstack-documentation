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
Users can now customize the CloudStack's user interface by means of a configuration file at /usr/share/cloudstack-management/webapp/primate/config.json which can be used to modify the theme, logos, etc. to align to one's requirement.

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

- @primary-color: changes the major background color of the page (background button, icon hover, etc).
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

Advanced Customization
~~~~~~~~~~~~~~~~~~~~~~

Users comfortable with development in JavaScript and VueJS can add / modify additional sections, actions and components
by building primate from source available on the `cloudstack-primate
<https://github.com/apache/cloudstack-primate>`_
repository and following the guide available `here
<https://github.com/apache/cloudstack-primate/blob/master/docs/development.md>`_

Known Issues and Missing Features
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Support for S3 based secondary storage
- NFS secondary staging storage list/resource view and add/update actions
- Regions
- Guest network LB support for SSL certificate

Please also refer to open issues on https://github.com/apache/cloudstack-primate/issues
