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

Configure package repository
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

CloudStack is only distributed from source from the official mirrors.
However, members of the CloudStack community may build convenience
binaries so that users can install Apache CloudStack without needing to
build from source.

If you didn't follow the steps to build your own packages from source in
the sections for `“Building RPMs from Source” 
<../building_from_source.html#building-rpms-from-source>`_ or 
`“Building DEB packages” <../building_from_source.html#building-deb-packages>`_ 
you may find pre-built DEB and RPM packages for your convenience linked from 
the `downloads <http://cloudstack.apache.org/downloads.html>`_ page.

.. note::
   These repositories contain both the Management Server and KVM Hypervisor 
   packages.

RPM package repository
~~~~~~~~~~~~~~~~~~~~~~

There is a RPM package repository for CloudStack so you can easily
install on RHEL based platforms.

If you're using an RPM-based system, you'll want to add the Yum
repository so that you can install CloudStack with Yum.

Yum repository information is found under ``/etc/yum.repos.d``. You'll
see several ``.repo`` files in this directory, each one denoting a
specific repository.

To add the CloudStack repository, create
``/etc/yum.repos.d/cloudstack.repo`` and insert the following
information.

.. parsed-literal::

   [cloudstack]
   name=cloudstack
   baseurl=http://download.cloudstack.org/centos/$releasever/|version|/
   enabled=1
   gpgcheck=0


Now you should now be able to install CloudStack using Yum.


DEB package repository
~~~~~~~~~~~~~~~~~~~~~~

You can add a DEB package repository to your apt sources with the
following commands. Please note that only packages for Ubuntu 14.04 LTS
(Trusty) and Ubuntu 16.04 (Xenial) are being built at this time. DISCLAIMER: Ubuntu 12.04 (Precise) is no longer supported.

Use your preferred editor and open (or create)
``/etc/apt/sources.list.d/cloudstack.list``. Add the community provided
repository to the file:

.. parsed-literal::

   deb http://download.cloudstack.org/ubuntu trusty |version|

We now have to add the public key to the trusted keys.

.. parsed-literal::

   sudo wget -O - http://download.cloudstack.org/release.asc|apt-key add -

Now update your local apt cache.

.. parsed-literal::

   sudo apt-get update

Your DEB package repository should now be configured and ready for use.


