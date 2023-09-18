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
<../building_from_source.html#building-rpms-from-source>`__ or
`“Building DEB packages” <../building_from_source.html#building-deb-packages>`__
you may find pre-built DEB and RPM packages for your convenience linked from
the `downloads <http://cloudstack.apache.org/downloads.html>`_ page.

.. note::
   These repositories contain both the Management Server and KVM Hypervisor
   packages.

RPM package repository
~~~~~~~~~~~~~~~~~~~~~~

There is a RPM package repository for CloudStack so you can easily
install on RHEL and SUSE based platforms.

If you're using an RPM-based system, you'll want to add the Yum
repository so that you can install CloudStack with Yum.

In RHEL or CentOS:

Yum repository information is found under ``/etc/yum.repos.d``. You'll
see several ``.repo`` files in this directory, each one denoting a
specific repository.

To add the CloudStack repository, create
``/etc/yum.repos.d/cloudstack.repo`` and insert the following
information.

In the case of RHEL being used, you can replace 'centos' by 'rhel' in the value of baseurl

.. parsed-literal::

   [cloudstack]
   name=cloudstack
   baseurl=http://download.cloudstack.org/centos/$releasever/|version|/
   enabled=1
   gpgcheck=0

Now you should now be able to install CloudStack using Yum.

In SUSE:

Zypper repository information is found under ``/etc/zypp/repos.d/``. You'll
see several ``.repo`` files in this directory, each one denoting a
specific repository.

To add the CloudStack repository, create
``/etc/zypp/repos.d/cloudstack.repo`` and insert the following
information.

.. parsed-literal::

   [cloudstack]
   name=cloudstack
   baseurl=http://download.cloudstack.org/suse/|version|/
   enabled=1
   gpgcheck=0


Now you should now be able to install CloudStack using zypper.


DEB package repository
~~~~~~~~~~~~~~~~~~~~~~

You can add a DEB package repository to your apt sources with the
following commands. Replace the code name with your Ubuntu LTS version :
Ubuntu 16.04 (Xenial), Ubuntu 18.04 (Bionic) and Ubuntu 20.04 (Focal) .
Ubuntu 14.04 (Trusty) is no longer supported.

Use your preferred editor and open (or create)
``/etc/apt/sources.list.d/cloudstack.list``. Add the community provided
repository to the file (replace "trusty" with "xenial" or "bionic" if it is the case):

.. parsed-literal::

   deb https://download.cloudstack.org/ubuntu focal |version|

We now have to add the public key to the trusted keys.

.. parsed-literal::

   wget -O - https://download.cloudstack.org/release.asc |sudo tee /etc/apt/trusted.gpg.d/cloudstack.asc

Now update your local apt cache.

.. parsed-literal::

   sudo apt update

Your DEB package repository should now be configured and ready for use.


