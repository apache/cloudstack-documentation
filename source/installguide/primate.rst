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

With Apache CloudStack 4.14, a technical preview of Primate is proposed that
users can evaluate. The technical preview release is not an officially voted
release by the Apache CloudStack project but offers a snapshot build of Primate
for users for testing and evaluation. The official Primate GA is expected with
the next CloudStack release where the legacy UI will be deprecated, and the
legacy UI will be removed in an eventual major CloudStack release.

.. parsed-literal::

    NOTE: Primate tech-preview is not suitable to run in production environments.

`User participation in the community mailing lists
<http://cloudstack.apache.org/mailing-lists.html>`_ is encouraged. Users may
also log issues on Github https://github.com/apache/cloudstack-primate/issues

:ref:`primate-install-guide`

Requirements
~~~~~~~~~~~~

Primate uses API auto-discovery to discover APIs allowed for a logged-in user
and creates navigation and views based on that.

- Apache CloudStack 4.13.1.0 or later
- API auto-discovery (listApis enabled)
- All modern browsers that are `ES5-compliant <https://github.com/vuejs/vue#browser-compatibility>`_

While in theory Primate can work with any older version of CloudStack however
several Primate list views require API pagination support some of which are
available starting Apache CloudStack 4.13.1.0.

Installation on CentOS
~~~~~~~~~~~~~~~~~~~~~~

Users running management server (4.13 or above) on CentOS can setup the
following Primate tech-preview repository:

.. parsed-literal::

    rpm --import https://download.cloudstack.org/primate/release.asc
    cat << EOF > /etc/yum.repos.d/cloudstack-primate-tech-preview.repo
    [cloudstack-primate-tech-preview]
    name=cloudstack
    baseurl=https://download.cloudstack.org/primate/testing/preview/centos/
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

Users running CloudStack management server (4.13 or above) on Ubuntu can setup the following Primate tech-preview repository:

.. parsed-literal::

    apt-key adv --keyserver keys.gnupg.net --recv-keys BDF0E176584DF93F
    echo deb https://download.cloudstack.org/primate/testing/preview/debian / > /etc/apt/sources.list.d/cloudstack-primate-tech-preview.list

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

Users can download the builds from https://download.cloudstack.org/primate/testing/preview/archive/

Using Docker
~~~~~~~~~~~~

Users can use docker builds of the tech preview from https://hub.docker.com/r/apache/cloudstack-primate

For example:

.. parsed-literal::

    docker pull apache/cloudstack-primate:tech-preview
    docker run -ti --rm -p 8080:80 -v $(pwd)/nginx:/etc/nginx/conf.d:ro apache/cloudstack-primate:tech-preview

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

Known Issues and Missing Features
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Support for network service providers
- Support for S3 based secondary storage
- Full support for all Quota plugin views
- Group actions for events, alerts and instances
- Metrics view cell-colouring
- Authorisation management for SAML users
- Filter by feature for searching
- Guest network LB support for SSL certificate
- Not all translations are not fully migrated from legacy UI to Primate.
- Feature and enhancements added in 4.14 except CloudStack Kubernetes Service and Backup and Recovery

Please also refer to open issues on https://github.com/apache/cloudstack-primate/issues
