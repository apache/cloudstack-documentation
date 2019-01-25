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


CloudStack Installation from GIT repo for Developers
====================================================

This guide is aimed at CloudStack developers who need to build the code.
These instructions are valid on a Ubuntu 12.04 and CentOS 6.4 systems
and were tested with the 4.2 release of Apache CloudStack. Instructions
adapted for Ubuntu 18.04 and CloudStack 4.11 are also available. Please
adapt them if you are on a different operating system or using a newer/older
version of CloudStack. This book is composed of the following sections:

#. Installation of the prerequisites

#. Compiling and installation from source

#. Using the CloudStack simulator

#. Installation with DevCloud the CloudStack sandbox

#. Building your own packages

#. The CloudStack API

#. Testing the AWS API interface


Prerequisites
-------------

In this section we'll look at installing the dependencies you'll need
for Apache CloudStack development.


On Ubuntu 12.04
~~~~~~~~~~~~~~~

First update and upgrade your system:

::

   apt-get update 
   apt-get upgrade

NTP might already be installed, check it with ``service ntp status``. If
it's not then install NTP to synchronize the clocks:

::

   apt-get install openntpd

Install ``openjdk``. As we're using Linux, OpenJDK is our first choice.

::

   apt-get install openjdk-7-jdk

Install ``tomcat6``, note that the new version of tomcat on
`Ubuntu <http://packages.ubuntu.com/precise/all/tomcat6>`__ is the
6.0.35 version.

::

   apt-get install tomcat6

Next, we'll install MySQL if it's not already present on the system.

::

   apt-get install mysql-server

Remember to set the correct ``mysql`` password in the CloudStack
properties file. Mysql should be running but you can check it's status
with:

::

   service mysql status

Developers wanting to build CloudStack from source will want to install
the following additional packages. If you dont' want to build from
source just jump to the next section.

Install ``git`` to later clone the CloudStack source code:

::

   apt-get install git

Install ``Maven`` to later build CloudStack

::

   apt-get install maven

This should have installed Maven 3.0, check the version number with
``mvn --version``

A little bit of Python can be used (e.g simulator), install the Python
package management tools:

::

   apt-get install python-pip python-setuptools

Finally install ``mkisofs`` with:

::

   apt-get install genisoimage

On Ubuntu 18.04
~~~~~~~~~~~~~~~

Run apt-get update to fetch the latest package list from the repo

::

   apt-get update

NTP might already be installed, check it with ``service ntp status``. If
it's not then install NTP to synchronize the clocks:

::

   apt-get install openntpd

Install ``openjdk``. As we're using Linux, OpenJDK is our first choice.

::

   apt-get install openjdk-8-jdk

Next, we'll install MySQL if it's not already present on the system.

::

   apt-get install mysql-server

Remember to set the correct ``mysql`` password in the CloudStack
properties file. Mysql should be running but you can check it's status
with:

::

   service mysql status

Developers wanting to build CloudStack from source will want to install
the following additional packages. If you dont' want to build from
source just jump to the next section.

Install ``git`` to later clone the CloudStack source code:

::

   apt-get install git

Install ``Maven`` to later build CloudStack

::

   apt-get install maven

This should have installed Maven 3.0, check the version number with
``mvn --version``

A little bit of Python can be used (e.g simulator), install the Python
package management tools:

::

   apt-get install python-pip python-setuptools

Finally install ``mkisofs`` with:

::

   apt-get install genisoimage

On CentOS 6.4
~~~~~~~~~~~~~

First update and upgrade your system:

::

   yum -y update
   yum -y upgrade

If not already installed, install NTP for clock synchornization

::

   yum -y install ntp

Install ``openjdk``. As we're using Linux, OpenJDK is our first choice.

::

   yum -y install java-1.7.0-openjdk-devel

Install ``tomcat6``, note that the version of tomcat6 in the default
CentOS 6.4 repo is 6.0.24, so we will grab the 6.0.35 version. The
6.0.24 version will be installed anyway as a dependency to cloudstack.

::

   wget https://archive.apache.org/dist/tomcat/tomcat-6/v6.0.35/bin/apache-tomcat-6.0.35.tar.gz
   tar xzvf apache-tomcat-6.0.35.tar.gz -C /usr/local

Setup tomcat6 system wide by creating a file
``/etc/profile.d/tomcat.sh`` with the following content:

::

   export CATALINA_BASE=/usr/local/apache-tomcat-6.0.35
   export CATALINA_HOME=/usr/local/apache-tomcat-6.0.35

Next, we'll install MySQL if it's not already present on the system.

::

   yum -y install mysql mysql-server

Remember to set the correct ``mysql`` password in the CloudStack
properties file. Mysql should be running but you can check it's status
with:

::

   service mysqld status

Install ``git`` to later clone the CloudStack source code:

::

   yum -y install git

Install ``Maven`` to later build CloudStack. Grab the 3.0.5 release from
the Maven `website <http://maven.apache.org/download.cgi>`__

::

   wget http://mirror.cc.columbia.edu/pub/software/apache/maven/maven-3/3.0.5/binaries/apache-maven-3.0.5-bin.tar.gz
   tar xzf apache-maven-3.0.5-bin.tar.gz -C /usr/local
   cd /usr/local
   ln -s apache-maven-3.0.5 maven

Setup Maven system wide by creating a ``/etc/profile.d/maven.sh`` file
with the following content:

::

   export M2_HOME=/usr/local/maven
   export PATH=${M2_HOME}/bin:${PATH}

Log out and log in again and you will have maven in your PATH:

::

   mvn --version

This should have installed Maven 3.0, check the version number with
``mvn --version``

A little bit of Python can be used (e.g simulator), install the Python
package management tools:

::

   yum -y install python-setuptools

To install python-pip you might want to setup the Extra Packages for
Enterprise Linux (EPEL) repo

::

   cd /tmp
   wget http://mirror-fpt-telecom.fpt.net/fedora/epel/6/i386/epel-release-6-8.noarch.rpm
   rpm -ivh epel-release-6-8.noarch.rpm

Then update you repository cache ``yum update`` and install pip
``yum -y install python-pip``

Finally install ``mkisofs`` with:

::

   yum -y install genisoimage


Installing version 4.8 from Source
----------------------------------

CloudStack uses git for source version control, if you know little about
`git <http://book.git-scm.com/>`__ is a good start. Once you have git
setup on your machine, pull the source with:

::

   git clone https://git-wip-us.apache.org/repos/asf/cloudstack.git

To build the latest stable release:

::

   git checkout 4.8

To compile Apache CloudStack, go to the cloudstack source folder and
run:

::

   mvn -Pdeveloper,systemvm clean install

If you want to skip the tests add ``-DskipTests`` to the command above. 
Do NOT use ``-Dmaven.test.skip=true`` because that will break the build.

You will have made sure to set the proper db password in
``utils/conf/db.properties``

Deploy the database next:

::

   mvn -P developer -pl developer -Ddeploydb

Run Apache CloudStack with jetty for testing. Note that ``tomcat`` maybe
be running on port 8080, stop it before you use ``jetty``

::

   mvn -pl :cloud-client-ui jetty:run

Log Into Apache CloudStack:

Open your Web browser and use this URL to connect to CloudStack:

::

   http://localhost:8080/client/

Replace ``localhost`` with the IP of your management server if need be.

.. note:: 
   If you have iptables enabled, you may have to open the ports used by 
   CloudStack. Specifically, ports 8080, 8250, and 9090.

You can now start configuring a Zone, playing with the API. Of course we
did not setup any infrastructure, there is no storage, no
hypervisors...etc. However you can run tests using the simulator. The
following section shows you how to use the simulator so that you don't
have to setup a physical infrastructure.


Using the Simulator
-------------------

CloudStack comes with a simulator based on Python bindings called
*Marvin*. Marvin is available in the CloudStack source code or on Pypi.
With Marvin you can simulate your data center infrastructure by
providing CloudStack with a configuration file that defines the number
of zones/pods/clusters/hosts, types of storage etc. You can then develop
and test the CloudStack management server *as if* it was managing your
production infrastructure.

Do a clean build:

::

   mvn -Pdeveloper -Dsimulator -DskipTests clean install

Deploy the database:

::

   mvn -Pdeveloper -pl developer -Ddeploydb
   mvn -Pdeveloper -pl developer -Ddeploydb-simulator

Install marvin. Note that you will need to have installed ``pip``
properly in the prerequisites step.

::

   pip install tools/marvin/dist/Marvin-|release|.tar.gz

Stop jetty (from any previous runs)

::

   mvn -pl :cloud-client-ui jetty:stop

Start jetty

::

   mvn -pl client jetty:run

Setup a basic zone with Marvin. In a separate shell://

::

   mvn -Pdeveloper,marvin.setup -Dmarvin.config=setup/dev/basic.cfg -pl :cloud-marvin integration-test

At this stage log in the CloudStack management server at
http://localhost:8080/client with the credentials admin/password, you
should see a fully configured basic zone infrastructure. To simulate an
advanced zone replace ``basic.cfg`` with ``advanced.cfg``.

You can now run integration tests, use the API etc...

Installing version 4.11 from Source
----------------------------------

CloudStack uses git for source version control, if you know little about
`git <http://book.git-scm.com/>`__ is a good start. Once you have git
setup on your machine, pull the source with:

::

   git clone https://git-wip-us.apache.org/repos/asf/cloudstack.git

To build the latest stable release:

::

   git checkout 4.11

Make sure you are using java 8. On Ubuntu you can run the following commands.
To list available java installations:

::

   sudo update-java-alternatives -l

To switch to java 8:

::

   sudo update-java-alternatives -s java-1.8.0-openjdk-amd64


To compile Apache CloudStack, go to the cloudstack source folder and
run:

::

   mvn -Pdeveloper,systemvm clean install

If you want to skip the tests add ``-DskipTests`` to the command above.
Do NOT use ``-Dmaven.test.skip=true`` because that will break the build.

The default installation of mysql is configured not to allow non root users to
connect as root. This can be changed by running the following commands:

::

   sudo -i mysql
   ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'
   exit

Before deploying the database you will have to make sure to set the proper db
passwords in ``utils/conf/db.properties``

Next, deploy the database:

::

   mvn -P developer -pl developer -Ddeploydb

Run Apache CloudStack with jetty for testing. Note that ``tomcat`` maybe
be running on port 8080, stop it before you use ``jetty``

::

   mvn -pl :cloud-client-ui jetty:run

Log Into Apache CloudStack:

Open your Web browser and use this URL to connect to CloudStack:

::

   http://localhost:8080/client/

Replace ``localhost`` with the IP of your management server if need be.

.. note::
   If you have iptables enabled, you may have to open the ports used by
   CloudStack. Specifically, ports 8080, 8250, and 9090.

You can now start configuring a Zone, playing with the API. Of course we
did not setup any infrastructure, there is no storage, no
hypervisors...etc. However you can run tests using the simulator. The
following section shows you how to use the simulator so that you don't
have to setup a physical infrastructure.


Using the Simulator
-------------------

CloudStack comes with a simulator based on Python bindings called
*Marvin*. Marvin is available in the CloudStack source code or on Pypi.
With Marvin you can simulate your data center infrastructure by
providing CloudStack with a configuration file that defines the number
of zones/pods/clusters/hosts, types of storage etc. You can then develop
and test the CloudStack management server *as if* it was managing your
production infrastructure.

Do a clean build:

::

   mvn -Pdeveloper -Dsimulator -DskipTests clean install

Deploy the database:

::

   mvn -Pdeveloper -pl developer -Ddeploydb
   mvn -Pdeveloper -pl developer -Ddeploydb-simulator

Install marvin. Note that you will need to have installed ``pip``
properly in the prerequisites step.

::

   pip install tools/marvin/dist/Marvin-|release|.tar.gz

Stop jetty (from any previous runs)

::

   mvn -pl :cloud-client-ui jetty:stop

Start jetty

::

   mvn -Dsimulator -Dorg.eclipse.jetty.annotations.maxWait=120 -pl cloud-client-ui jetty:run

Setup a basic zone with Marvin. In a separate shell://

::

   python tools/marvin/marvin/deployDataCenter.py -i setup/dev/advanced.cfg

At this stage log in the CloudStack management server at
http://localhost:8080/client with the credentials admin/password, you
should see a fully configured advanced zone infrastructure. To simulate a
basic zone replace ``advanced.cfg`` with ``basic.cfg``.

You can now run integration tests, use the API etc...

Using DevCloud
--------------

The Installing from source section will only get you to the point of
runnign the management server, it does not get you any hypervisors. The
simulator section gets you a simulated datacenter for testing. With
DevCloud you can run at least one hypervisor and add it to your
management server the way you would a real physical machine.

`DevCloud <https://cwiki.apache.org/confluence/display/CLOUDSTACK/DevCloud>`__
is the CloudStack sandbox, the standard version is a VirtualBox based
image. There is also a KVM based image for it. Here we only show steps
with the VirtualBox image. For KVM see the
`wiki <https://cwiki.apache.org/confluence/display/CLOUDSTACK/devcloud-kvm>`__.

\*\* DevCloud Pre-requisites

#. Install `VirtualBox <http://www.virtualbox.org>`__ on your machine

#. Run VirtualBox and under >Preferences create a *host-only interface*
   on which you disable the DHCP server

#. Download the DevCloud `image 
   <http://people.apache.org/~bhaisaab/cloudstack/devcloud/devcloud2.ova>`__

#. In VirtualBox, under File > Import Appliance import the DevCloud
   image.

#. Verify the settings under > Settings and check the ``enable PAE``
   option in the processor menu

#. Once the VM has booted try to ``ssh`` to it with credentials:
   ``root/password``

   ssh root@192.168.56.10


Adding DevCloud as an Hypervisor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Picking up from a clean build:

::

   mvn -Pdeveloper,systemvm clean install
   mvn -P developer -pl developer,tools/devcloud -Ddeploydb

At this stage install marvin similarly than with the simulator:

::

   pip install tools/marvin/dist/Marvin-|release|.tar.gz

Start the management server

::

   mvn -pl client jetty:run

Then you are going to configure CloudStack to use the running DevCloud
instance:

::

   cd tools/devcloud
   python ../marvin/marvin/deployDataCenter.py -i devcloud.cfg

If you are curious, check the ``devcloud.cfg`` file and see how the data
center is defined: 1 Zone, 1 Pod, 1 Cluster, 1 Host, 1 primary Storage,
1 Seondary Storage, all provided by Devcloud.

You can now log in the management server at
``http://localhost:8080/client`` and start experimenting with the UI or
the API.

Do note that the management server is running in your local machine and
that DevCloud is used only as a n Hypervisor. You could potentially run
the management server within DevCloud as well, or memory granted, run
multiple DevClouds.


Building Packages
-----------------

Working from source is necessary when developing CloudStack. As
mentioned earlier this is not primarily intended for users. However some
may want to modify the code for their own use and specific
infrastructure. The may also need to build their own packages for
security reasons and due to network connectivity constraints. This
section shows you the gist of how to build packages. We assume that the
reader will know how to create a repository to serve this packages. The
complete documentation is available in the :ref:`building_deb_packages` section.

To build debian packages you will need couple extra packages that we did
not need to install for source compilation:

::

   apt-get install python-mysqldb
   apt-get install debhelper

Then build the packages with:

::

   dpkg-buildpackage -uc -us

One directory up from the CloudStack root dir you will find:

::

   cloudstack_|release|_amd64.changes
   cloudstack_|release|.dsc
   cloudstack_|release|.tar.gz
   cloudstack-agent_|release|_all.deb
   cloudstack-awsapi_|release|_all.deb
   cloudstack-cli_|release|_all.deb
   cloudstack-common_|release|_all.deb
   cloudstack-docs_|release|_all.deb
   cloudstack-management_|release|_all.deb
   cloudstack-usage_|release|_all.deb

Of course the community provides a repository for these packages and you
can use it instead of building your own packages and putting them in
your own repo. Instructions on how to use this community repository are
available in the installation book.

.. _the-api:

The CloudStack API
------------------

The CloudStack API is a query based API using http that return results
in XML or JSON. It is used to implement the default web UI. This API is
not a standard like `OGF
OCCI <http://www.ogf.org/gf/group_info/view.php?group=occi-wg>`__ or
`DMTF CIMI <http://dmtf.org/standards/cloud>`__ but is easy to learn.
Mapping exists between the AWS API and the CloudStack API as will be
seen in the next section. Recently a Google Compute Engine interface was
also developed that maps the GCE REST API to the CloudStack API
described here. The API
`docs <http://cloudstack.apache.org/docs/api/>`__ are a good start to
learn the extent of the API. Multiple clients exist on
`github <https://github.com/search?q=cloudstack+client&ref=cmdform>`__
to use this API, you should be able to find one in your favorite
language. The reference documentation for the API and changes that might
occur from version to version is availble
`on-line <http://cloudstack.apache.org/docs/en-US/Apache_CloudStack/4.1.1/html/Developers_Guide/index.html>`__.
This short section is aimed at providing a quick summary to give you a
base understanding of how to use this API. As a quick start, a good way
to explore the API is to navigate the dashboard with a firebug console
(or similar developer console) to study the queries.

In a succint statement, the CloudStack query API can be used via http
GET requests made against your cloud endpoint (e.g
http://localhost:8080/client/api). The API name is passed using the
``command`` key and the various parameters for this API call are passed
as key value pairs. The request is signed using the access key and
secret key of the user making the call. Some calls are synchronous while
some are asynchronous, this is documented in the API
`docs <http://cloudstack.apache.org/docs/api/>`__. Asynchronous calls
return a ``jobid``, the status and result of a job can be queried with
the ``queryAsyncJobResult`` call. Let's get started and give an example
of calling the ``listUsers`` API in Python.

First you will need to generate keys to make requests. Going through the
dashboard, go under ``Accounts`` select the appropriate account then
click on ``Show Users`` select the intended users and generate keys
using the ``Generate Keys`` icon. You will see an ``API Key`` and
``Secret Key`` field being generated. The keys will be of the form:

::

   API Key : XzAz0uC0t888gOzPs3HchY72qwDc7pUPIO8LxC-VkIHo4C3fvbEBY_Ccj8fo3mBapN5qRDg_0_EbGdbxi8oy1A
   Secret Key: zmBOXAXPlfb-LIygOxUVblAbz7E47eukDS_0JYUxP3JAmknOYo56T0R-AcM7rK7SMyo11Y6XW22gyuXzOdiybQ

Open a Python shell and import the basic modules necessary to make the
request. Do note that this request could be made many different ways,
this is just a low level example. The ``urllib*`` modules are used to
make the http request and do url encoding. The ``hashlib`` module gives
us the sha1 hash function. It used to geenrate the ``hmac`` (Keyed
Hashing for Message Authentication) using the secretkey. The result is
encoded using the ``base64`` module.

::

   $python
   Python 2.7.3 (default, Nov 17 2012, 19:54:34) 
   [GCC 4.2.1 Compatible Apple Clang 4.1 ((tags/Apple/clang-421.11.66))] on darwin
   Type "help", "copyright", "credits" or "license" for more information.
   >>> import urllib2
   >>> import urllib
   >>> import hashlib
   >>> import hmac
   >>> import base64

Define the endpoint of the Cloud, the command that you want to execute,
the type of the response (i.e XML or JSON) and the keys of the user.
Note that we do not put the secretkey in our request dictionary because
it is only used to compute the hmac.

::

   >>> baseurl='http://localhost:8080/client/api?'
   >>> request={}
   >>> request['command']='listUsers'
   >>> request['response']='json'
   >>> request['apikey']='plgWJfZK4gyS3mOMTVmjUVg-X-jlWlnfaUJ9GAbBbf9EdM-kAYMmAiLqzzq1ElZLYq_u38zCm0bewzGUdP66mg'
   >>> secretkey='VDaACYb0LV9eNjTetIOElcVQkvJck_J_QljX_FcHRj87ZKiy0z0ty0ZsYBkoXkY9b7eq1EhwJaw7FF3akA3KBQ'

Build the base request string, the combination of all the key/pairs of
the request, url encoded and joined with ampersand.

::

   >>> request_str='&'.join(['='.join([k,urllib.quote_plus(request[k])]) for k in request.keys()])
   >>> request_str
   'apikey=plgWJfZK4gyS3mOMTVmjUVg-X-jlWlnfaUJ9GAbBbf9EdM-kAYMmAiLqzzq1ElZLYq_u38zCm0bewzGUdP66mg&command=listUsers&response=json'

Compute the signature with hmac, do a 64 bit encoding and a url
encoding, the string used for the signature is similar to the base
request string shown above but the keys/values are lower cased and
joined in a sorted order

::

   >>> sig_str='&'.join(['='.join([k.lower(),urllib.quote_plus(request[k].lower().replace('+','%20'))])for k in sorted(request.iterkeys())]) 
   >>> sig_str
   'apikey=plgwjfzk4gys3momtvmjuvg-x-jlwlnfauj9gabbbf9edm-kaymmailqzzq1elzlyq_u38zcm0bewzgudp66mg&command=listusers&response=json'
   >>> sig=hmac.new(secretkey,sig_str,hashlib.sha1).digest()
   >>> sig
   'M:]\x0e\xaf\xfb\x8f\xf2y\xf1p\x91\x1e\x89\x8a\xa1\x05\xc4A\xdb'
   >>> sig=base64.encodestring(hmac.new(secretkey,sig_str,hashlib.sha1).digest())
   >>> sig
   'TTpdDq/7j/J58XCRHomKoQXEQds=\n'
   >>> sig=base64.encodestring(hmac.new(secretkey,sig_str,hashlib.sha1).digest()).strip()
   >>> sig
   'TTpdDq/7j/J58XCRHomKoQXEQds='
   >>> sig=urllib.quote_plus(base64.encodestring(hmac.new(secretkey,sig_str,hashlib.sha1).digest()).strip())

Finally, build the entire string by joining the baseurl, the request str
and the signature. Then do an http GET:

::

   >>> req=baseurl+request_str+'&signature='+sig
   >>> req
   'http://localhost:8080/client/api?apikey=plgWJfZK4gyS3mOMTVmjUVg-X-jlWlnfaUJ9GAbBbf9EdM-kAYMmAiLqzzq1ElZLYq_u38zCm0bewzGUdP66mg&command=listUsers&response=json&signature=TTpdDq%2F7j%2FJ58XCRHomKoQXEQds%3D'
   >>> res=urllib2.urlopen(req)
   >>> res.read()
   {
      "listusersresponse" : { 
         "count":1 ,
         "user" : [  
            {
               "id":"7ed6d5da-93b2-4545-a502-23d20b48ef2a",
               "username":"admin",
               "firstname":"admin",
               "lastname":"cloud",
               "created":"2012-07-05T12:18:27-0700",
               "state":"enabled",
               "account":"admin",
               "accounttype":1,
               "domainid":"8a111e58-e155-4482-93ce-84efff3c7c77",
               "domain":"ROOT",
               "apikey":"plgWJfZK4gyS3mOMTVmjUVg-X-jlWlnfaUJ9GAbBbf9EdM-kAYMmAiLqzzq1ElZLYq_u38zCm0bewzGUdP66mg",
               "secretkey":"VDaACYb0LV9eNjTetIOElcVQkvJck_J_QljX_FcHRj87ZKiy0z0ty0ZsYBkoXkY9b7eq1EhwJaw7FF3akA3KBQ",
               "accountid":"7548ac03-af1d-4c1c-9064-2f3e2c0eda0d"
            }
         ]
      }
   }
                                                      

All the clients that you will find on github will implement this
signature technique, you should not have to do it by hand. Now that you
have explored the API through the UI and that you understand how to make
low level calls, pick your favorite client of use
`CloudMonkey <https://pypi.python.org/pypi/cloudmonkey/>`__. CloudMonkey
is a sub-project of Apache CloudStack and gives operators/developers the
ability to use any of the API methods. It has nice auto-completion and
help feature as well as an API discovery mechanism since 4.2.


Testing the AWS API interface
-----------------------------

While the native CloudStack API is not a standard, CloudStack provides a
AWS EC2 compatible interface. It has the great advantage that existing
tools written with EC2 libraries can be re-used against a CloudStack
based cloud. In the installation books we described how to run this
interface from installing packages. In this section we show you how to
compile the interface with ``maven`` and test it with Python boto
module.

Starting from a running management server (with DevCloud for instance),
start the AWS API interface in a separate shell with:

::

   mvn -Pawsapi -pl :cloud-awsapi jetty:run

Log into the CloudStack UI ``http://localhost:8080/client``, go to
*Service Offerings* and edit one of the compute offerings to have the
name ``m1.small`` or any of the other AWS EC2 instance types.

With access and secret keys generated for a user you should now be able
to use Python `Boto <http://docs.pythonboto.org/en/latest/>`__ module:

::

   import boto
   import boto.ec2

   accesskey="2IUSA5xylbsPSnBQFoWXKg3RvjHgsufcKhC1SeiCbeEc0obKwUlwJamB_gFmMJkFHYHTIafpUx0pHcfLvt-dzw"
   secretkey="oxV5Dhhk5ufNowey7OVHgWxCBVS4deTl9qL0EqMthfPBuy3ScHPo2fifDxw1aXeL5cyH10hnLOKjyKphcXGeDA"

   region = boto.ec2.regioninfo.RegionInfo(name="ROOT", endpoint="localhost")
   conn = boto.connect_ec2(aws_access_key_id=accesskey, aws_secret_access_key=secretkey, is_secure=False, region=region, port=7080, path="/awsapi", api_version="2012-08-15")

   images=conn.get_all_images()
   print images

   res = images[0].run(instance_type='m1.small',security_groups=['default'])

Note the new ``api_version`` number in the connection object and also
note that there was no user registration to make like in previous
CloudStack releases.


Conclusions
-----------

CloudStack is a mostly Java application running with Tomcat and Mysql.
It consists of a management server and depending on the hypervisors
being used, an agent installed on the hypervisor farm. To complete a
Cloud infrastructure however you will also need some Zone wide storage
a.k.a Secondary Storage and some Cluster wide storage a.k.a Primary
storage. The choice of hypervisor, storage solution and type of Zone
(i.e Basic vs. Advanced) will dictate how complex your installation can
be. As a quick start, you might want to consider KVM+NFS and a Basic
Zone.

If you've run into any problems with this, please ask on the
cloudstack-dev `mailing list </mailing-lists.html>`__.
