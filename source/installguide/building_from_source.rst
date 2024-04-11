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


Introduction
------------

The official CloudStack release is always in source code form. You will
likely be able to find "convenience binaries", where the source is the
canonical release. In this section, we will cover acquiring and building
the source release so that you can deploy using Maven or
build packages for distribution (e.g. ``.deb``, ``.rpm``).

.. note::

   Building and deploying directly from source is typically not
   the most efficient way to deploy CloudStack. Also, please be aware that
   development branches may contain unstable code. If you run into any issues
   during the build process, please check the CloudStack `Issues
   <https://github.com/apache/cloudstack/issues>`_ page on GitHub. You may find
   that the issue you are experiencing has already been reported.

The instructions here are likely version-specific (i.e. Building 4.7.x
is different from building 4.2.x).

If you are working with an unreleased version of CloudStack, please read the
``INSTALL.md`` file in the top-level directory of the release.


Downloading the Release
-----------------------

You can download the latest CloudStack release from the `Apache
CloudStack project download page
<http://cloudstack.apache.org/downloads.html>`_.

Prior releases are available via `archive.apache.org
<https://archive.apache.org>`_ as well. Please see the
Downloads page for more information on archived releases.

You will notice several links under the *Latest CloudStack Releases* section.
A link to a file ending in ``tar.bz2``, as well as a PGP/GPG signature, MD5,
and SHA512 file.

-  The ``tar.bz2`` file contains the bzip2-compressed tarball with the
   source code.

-  The ``.asc`` file is a detached cryptographic signature that can be
   used to verify release authenticity.

-  The ``.md5`` file is a MD5 hash that can be used to verify release
   authenticity.

-  The ``.sha`` file is a SHA512 hash that can be used to verify release
   authenticity.


Verifying the Downloaded Release
--------------------------------

There are a number of mechanisms to check the authenticity and validity
of a downloaded release.


Getting the KEYS
~~~~~~~~~~~~~~~~

To enable you to verify the GPG signature, you will need to download the
`KEYS <http://www.apache.org/dist/cloudstack/KEYS>`_ file.

You next need to import those keys, which you can do by running:

.. parsed-literal::

   $ wget http://www.apache.org/dist/cloudstack/KEYS
   $ gpg --import KEYS


GPG
~~~

The CloudStack project provides a detached GPG signature of the release.
To check the signature, run the following command:

.. parsed-literal::

   $ gpg --verify apache-cloudstack-|release|-src.tar.bz2.asc

If the signature is valid you will see a line of output that contains
'Good signature'.


MD5
~~~

In addition to the cryptographic signature, CloudStack has an MD5
checksum that you can use to verify the download matches the release.
You can verify this hash by executing the following command:

.. parsed-literal::

   $ gpg --print-md MD5 apache-cloudstack-|release|-src.tar.bz2 | diff - apache-cloudstack-|release|-src.tar.bz2.md5

If this successfully completes you should see no output. If there is any
output from them, then there is a difference between the hash you
generated locally and the hash that has been pulled from the server.


SHA512
~~~~~~

In addition to the MD5 hash, the CloudStack project provides a SHA512
cryptographic hash to aid in assurance of the validity of the downloaded
release. You can verify this hash by executing the following command:

.. parsed-literal::

   $ gpg --print-md SHA512 apache-cloudstack-|release|-src.tar.bz2 | diff - apache-cloudstack-|release|-src.tar.bz2.sha

If this command successfully completes you should see no output. If
there is any output from them, then there is a difference between the
hash you generated locally and the hash that has been pulled from the
server.


Prerequisites for building Apache CloudStack
--------------------------------------------

There are a number of prerequisites needed to build CloudStack. This
document assumes compilation on a Linux system that uses RPMs or DEBs
for package management.

You will need, at a minimum, the following to compile CloudStack:

#. Maven (version 3)

#. Java (Java 11/OpenJDK 1.11)

#. NodeJS (LTS/12)

#. Apache Web Services Common Utilities (ws-commons-util)

#. MySQL

#. MySQLdb (provides Python database API)

#. genisoimage

#. rpmbuild or dpkg-dev


Extracting source
-----------------

Extracting the CloudStack release is relatively simple and can be done
with a single command as follows:

.. parsed-literal::

   $ tar -jxvf apache-cloudstack-|release|-src.tar.bz2

You can now move into the directory:

.. parsed-literal::

   $ cd ./apache-cloudstack-|release|-src

Install new MySQL connector
---------------------------

Install Python MySQL connector using the official MySQL packages repository.


MySQL connector APT repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

   Procedure below should work for Ubuntu 14.04 and 16.04.
   For Ubuntu 18.04, please read later below.

Install the following package provided by MySQL to enable official repositories:

.. note::

   If the download fails check the current version number. The version available may
   have been updated.

.. parsed-literal::

   wget http://dev.mysql.com/get/mysql-apt-config_0.7.3-1_all.deb
   sudo dpkg -i mysql-apt-config_0.7.3-1_all.deb

Make sure to activate the repository for MySQL connectors.

.. parsed-literal::

   sudo apt-get update
   sudo apt-get install mysql-connector-python

.. note::

   Below is given a bit different procedure if you are compiling on Ubuntu 18.04

Due to default python version changes (and some others) in Ubuntu 18.04 version, we will need to install python 2.7, python-mysql.connector from Universe repo (instead from official MySQL repo) and later make sure we are using Java 8, since Java 10 comes as default

.. parsed-literal::

   apt-add-repository universe
   apt-get install python-mysql.connector python-setuptools dh-systemd
   (installs python 2.7 with needed dependencies)

MySQL connector RPM repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add a new yum repo ``/etc/yum.repos.d/mysql.repo``:

.. parsed-literal::

   [mysql-community]
   name=MySQL Community connectors
   baseurl=http://repo.mysql.com/yum/mysql-connectors-community/el/$releasever/$basearch/
   gpgkey=http://repo.mysql.com/RPM-GPG-KEY-mysql
   enabled=1
   gpgcheck=1

Install mysql-connector

.. parsed-literal::

   yum install mysql-connector-python

.. _building_deb_packages:

Building DEB packages
---------------------

In addition to the bootstrap dependencies, you'll also need to install
several other dependencies. Note that we recommend using Maven 3.

.. parsed-literal::

   $ sudo apt-get update
   $ sudo apt-get install python-software-properties
   $ sudo apt-get update
   $ sudo apt-get install debhelper openjdk-11-jdk libws-commons-util-java genisoimage libcommons-codec-java libcommons-httpclient-java liblog4j1.2-java maven
   $ curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
   $ sudo apt-get install -y nodejs

.. note::

   If on Ubuntu 18.04, in above command, please replace "python-software-properties" with "software-properties-common"
   If on Ubuntu 18.04, above command will install both Java 10 and Java 8, so make sure to switch to Java8 with "update-alternatives --config java" - otherwise you will get errors during dependency check and code compiling.

While we have defined, and you have presumably already installed the
bootstrap prerequisites, there are a number of build time prerequisites
that need to be resolved. CloudStack uses maven for dependency
resolution. You can resolve the buildtime depdencies for CloudStack by
running:

.. parsed-literal::

   $ mvn -P deps

Now that we have resolved the dependencies we can move on to building
CloudStack and packaging them into DEBs by running the script in ``packaging`` folder:


.. parsed-literal::

   $ cd packaging/
   $ ./build-deb.sh

This script will build the following debian packages. You should have
all of the following:

.. parsed-literal::

   cloudstack-common-|release|.amd64.deb
   cloudstack-management-|release|.amd64.deb
   cloudstack-agent-|release|.amd64.deb
   cloudstack-usage-|release|.amd64.deb
   cloudstack-cli-|release|.amd64.deb


Setting up an APT repo
~~~~~~~~~~~~~~~~~~~~~~

After you've created the packages, you'll want to copy them to a system
where you can serve the packages over HTTP. You'll create a directory
for the packages and then use ``dpkg-scanpackages`` to create
``Packages.gz``, which holds information about the archive structure.
Finally, you'll add the repository to your system(s) so you can install
the packages using APT.

The first step is to make sure that you have the **dpkg-dev** package
installed. This should have been installed when you pulled in the
**debhelper** application previously, but if you're generating
``Packages.gz`` on a different system, be sure that it's installed there
as well.

.. parsed-literal::

   $ sudo apt-get install dpkg-dev apt-utils

The next step is to copy the DEBs to the directory where they can be
served over HTTP. We'll use ``/var/www/cloudstack/repo`` in the
examples, but change the directory to whatever works for you.

.. parsed-literal::

   $ sudo mkdir -p /var/www/cloudstack/repo/binary
   $ sudo cp \*.deb /var/www/cloudstack/repo/binary
   $ cd /var/www/cloudstack/repo/binary
   $ sudo dpkg-scanpackages . /dev/null > Packages
   $ sudo gzip -9k Packages
   $ sudo apt-ftparchive release . > Release

.. note::

   You can safely ignore the warning about a missing override file.

Now you should have all of the DEB packages, ``Packages``,
``Packages.gz`` and ``Release`` in the ``binary`` directory and
available over HTTP. (You may want to use ``wget`` or ``curl``
to test this before moving on to the next step.)


Repository signing
~~~~~~~~~~~~~~~~~~

The following step is optional.

The repository we just created will work without cryptographic
signatures, but it's always better to sign your releases if you can.

Install GnuPG first:

.. parsed-literal::

   $ sudo apt-get install gpg

Set up a signing key if you don't have one yet.
If you already have a suitable key, skip this step.

.. parsed-literal::

   $ sudo gpg --default-new-key-algo rsa4096 --gen-key

Generate the repository signatures. Replace ${YOUR_KEY_ID} with the
key ID of the key you created above.

.. parsed-literal::

   $ sudo rm -fr Release.gpg InRelease
   $ sudo gpg --default-key ${YOUR_KEY_ID} -abs -o Release.gpg Release
   $ sudo gpg --default-key ${YOUR_KEY_ID} --clearsign -o InRelease Release
   $ sudo gpg --output KEY.gpg --armor --export ${YOUR_KEY_ID}

Store the ``Release.gpg`` and ``InRelease`` as well as KEY.gpg on your
HTTP server.


Configuring your machines to use the APT repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now that we have created the repository, you need to configure your
machine to make use of the APT repository. You can do this by adding a
repository file under ``/etc/apt/sources.list.d``. Use your preferred
editor to create ``/etc/apt/sources.list.d/cloudstack.list`` with this
line:

.. parsed-literal::

   deb http://<server.url>/cloudstack/repo/binary ./

If you signed your Release file with GnuPG, import the signing key
on your target system first.

.. parsed-literal::

   $ wget -q -O - http://<server.url>/cloudstack/repo/binary/KEY.gpg | sudo apt-key add -

.. note::
   In the previous lines the variable <server.url> must be replaced with the address of the repository

Now that you have the repository info in place, you'll want to run
another update so that APT knows where to find the CloudStack packages.

.. parsed-literal::

   $ sudo apt-get update

You can now move on to the instructions under Install on Ubuntu.


Building RPMs from Source
-------------------------

As mentioned previously in `“Prerequisites for building Apache CloudStack”
<#prerequisites-for-building-apache-cloudstack>`_, you will need to install
several prerequisites before you can build packages for CloudStack. Here we'll
assume you're working with a 64-bit build of CentOS or Red Hat Enterprise
Linux.

.. parsed-literal::

   # yum groupinstall "Development Tools"

.. parsed-literal::

   # yum install java-11-openjdk-devel genisoimage mysql mysql-server ws-commons-util MySQL-python python-setuptools createrepo
   # curl -sL https://rpm.nodesource.com/setup_12.x | sudo bash -
   # yum install nodejs

Next, you'll need to install build-time dependencies for CloudStack with
Maven. We're using Maven 3, so you'll want to grab `Maven 3.0.5 (Binary tar.gz)
<http://maven.apache.org/download.cgi>`_ and uncompress it in
your home directory (or whatever location you prefer):

.. parsed-literal::

   $ cd ~
   $ tar zxvf apache-maven-3.0.5-bin.tar.gz

.. parsed-literal::

   $ export PATH=~/apache-maven-3.0.5/bin:$PATH

Maven also needs to know where Java is, and expects the JAVA\_HOME
environment variable to be set:

.. parsed-literal::

   $ export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk.x86_64

Verify that Maven is installed correctly:

.. parsed-literal::

   $ mvn --version

You probably want to ensure that your environment variables will survive
a logout/reboot. Be sure to update ``~/.bashrc`` with the PATH and
JAVA\_HOME variables.

Building RPMs for CloudStack is fairly simple. Assuming you already have
the source downloaded and have uncompressed the tarball into a local
directory, you're going to be able to generate packages in just a few
minutes.

.. note::

   Packaging has changed. If you've created packages for CloudStack
   previously, you should be aware that the process has changed considerably
   since the project has moved to using Apache Maven. Please be sure to follow
   the steps in this section closely.


Generating RPMS
~~~~~~~~~~~~~~~

Now that we have the prerequisites and source, you will cd to the
`packaging/` directory.

.. parsed-literal::

   $ cd packaging/

Generating RPMs is done using the ``package.sh`` script:

.. parsed-literal::

   $ ./package.sh -d centos63

For other supported options(like centos7), run ``./package.sh --help``

That will run for a bit and then place the finished packages in
``dist/rpmbuild/RPMS/x86_64/``.

You should see the following RPMs in that directory:

.. parsed-literal::

   cloudstack-agent-|release|.el6.x86_64.rpm
   cloudstack-cli-|release|.el6.x86_64.rpm
   cloudstack-common-|release|.el6.x86_64.rpm
   cloudstack-management-|release|.el6.x86_64.rpm
   cloudstack-usage-|release|.el6.x86_64.rpm


Creating a yum repo
^^^^^^^^^^^^^^^^^^^

While RPMs is a useful packaging format - it's most easily consumed from
Yum repositories over a Network. The next step is to create a Yum Repo
with the finished packages:

.. parsed-literal::

   $ mkdir -p ~/tmp/repo

   $ cd ../..
   $ cp dist/rpmbuild/RPMS/x86_64/\*rpm ~/tmp/repo/

   $ createrepo /tmp/repo

The files and directories within ``~/tmp/repo`` can now be uploaded to a
web server and serve as a yum repository.


Configuring your systems to use your new yum repository
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now that your yum repository is populated with RPMs and metadata we need
to configure the machines that need to install CloudStack. Create a file
named ``/etc/yum.repos.d/cloudstack.repo`` with this information:

.. parsed-literal::

   [apache-cloudstack]
   name=Apache CloudStack
   baseurl=http://webserver.tld/path/to/repo
   enabled=1
   gpgcheck=0

Completing this step will allow you to easily install CloudStack on a
number of machines across the Network.

.. _building-noredist:

Building Non-OSS
----------------

If you need support for the VMware, NetApp, F5, NetScaler, SRX, or any
other non-Open Source Software (nonoss) plugins, you'll need to download
a few components on your own and follow a slightly different procedure
to build from source.

.. warning::

   Some of the plugins supported by CloudStack cannot be distributed with
   CloudStack for licensing reasons. In some cases, some of the required
   libraries/JARs are under a proprietary license. In other cases, the
   required libraries may be under a license that's not compatible with
   `Apache's licensing guidelines for third-party products
   <http://www.apache.org/legal/resolved.html#category-x>`_.

#. To build the Non-OSS plugins, you'll need to have the requisite JARs
   installed under the ``deps`` directory.

   Because these modules require dependencies that can't be distributed
   with CloudStack you'll need to download them yourself. Links to the
   most recent dependencies are listed on the `*How to build CloudStack*
   <https://cwiki.apache.org/confluence/display/CLOUDSTACK/How+to+build+CloudStack>`_
   page on the wiki.

#. You may also need to download
   `vhd-util <https://download.cloudstack.org/tools/>`_,
   which was removed due to licensing issues. You'll copy vhd-util to
   the ``scripts/vm/hypervisor/xenserver/`` directory.

#. Once you have all the dependencies copied over, you'll be able to
   build CloudStack with the ``noredist`` option:

.. parsed-literal::

   $ mvn clean
   $ mvn install -Dnoredist

#. Once you've built CloudStack with the ``noredist`` profile, you can
   package it using the `“Building RPMs from Source” <#building-rpms-from-source>`_
   or `“Building DEB packages” <#building-deb-packages>`_ instructions.

.. note::

   In case you are building debian packages via script ``packaging/build-deb.sh``, you will need to export the following configuration:

.. parsed-literal::

   $ export ACS_BUILD_OPTS="-Dnoredist -Dnonoss"
