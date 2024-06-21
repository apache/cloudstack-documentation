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
These instructions are valid on a Ubuntu 22.04 and 24.04 systems
and were tested with the 4.19 release of Apache CloudStack. Community maintained
CloudStack self-learning course is also available at `CloudStack HackerBook
<https://github.com/shapeblue/hackerbook/tree/main>`__.

Please adapt them if you are on a different operating system or using a
newer/older version of CloudStack. This book is composed of the following
sections:

#. Installation of the prerequisites

#. Compiling and installation from source

#. Using the CloudStack Simulator

#. Using Appliance for development

#. Building your own packages

#. The CloudStack API

Prerequisites
-------------

In this section we'll look at installing the dependencies you'll need
for Apache CloudStack development.

To build and test CloudStack from source you will need the following
installed:
* jdk 11+ (openjdk-11-jdk)
* maven 3+
* git
* python3-pip
* python3-setuptools
* mkisofs
* MySql 8x Server

Example Ubuntu
~~~~~~~~~~~~~~

::

   sudo apt update
   sudo apt install git openssh-client openjdk-11-jdk maven mysql-client mysql-server nfs-kernel-server quota genisoimage python3 python3-pip

Note: ensure to install python 3.8/3.9/3.10, as required you can install
specific Python3 versions using pyenv. Similarly, Java versions can be installed
and managed using jenv.

Installing CloudStack from Source
----------------------------------

CloudStack uses git for source version control, if you know little about
`git <http://book.git-scm.com/>`__ is a good start. Once you have git
setup on your machine, pull the source with:

::

   git clone https://github.com/apache/cloudstack.git

To build a stable release, checkout the branch for that version:

::

   git checkout 4.19

Optional, you can install noredist/nonoss dependencies:

::

   git clone https://github.com/shapeblue/cloudstack-nonoss
   cd cloudstack-nonoss && bash -x install-non-oss.sh

To compile Apache CloudStack, go to the cloudstack source folder and
run:

::

   mvn -Pdeveloper,systemvm clean install

If you want to skip the tests add ``-DskipTests`` to the command above.
Do NOT use ``-Dmaven.test.skip=true`` because that will break the build. To
build noredist/nonoss add ``-Dnoredist`` flag to the command.

If you have set a root mysql password, you will need to adjust the password in
``utils/conf/db.properties``

Deploy the database next:

::

   mvn -P developer -pl developer -Ddeploydb

Run Apache CloudStack with jetty for testing

::

   mvn -pl :cloud-client-ui jetty:run

To build and run the UI, do this:

::

   curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -
   sudo apt install nodejs
   cd cloudstack/ui
   npm install
   npm run serve

Log Into Apache CloudStack:

Open your Web browser and use this URL to connect to CloudStack:

::

   http://localhost:5050 # this runs the UI
   http://localhost:8080/client/ # this is the API backend

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

CloudStack comes with a simulator for hosts, Instances and Network infrastructure,
allowing you to use the CloudStack management server without using real
servers.  It also comes with Marvin, which can create a set of
infrastructure based on a configuration file that defines the number
of zones/pods/clusters/hosts, types of storage etc.  Marvin combined with
the simulator enable you to develop and test the CloudStack management server
*as if* it was managing production infrastructure.

Stop jetty (from any previous runs, if running)

::

   mvn -pl :cloud-client-ui jetty:stop

Do a clean build with the simulator option enabled:

::

   mvn -Pdeveloper -Dsimulator -DskipTests clean install

Deploy the database (skip first line if you did this earlier):

::

   mvn -Pdeveloper -pl developer -Ddeploydb
   mvn -Pdeveloper -pl developer -Ddeploydb-simulator

Start jetty with the simulator enabled

::

   mvn -Dsimulator -pl :cloud-client-ui jetty:run

Setup a basic or advanced zone with Marvin. In a separate shell://

::

   python3 tools/marvin/marvin/deployDataCenter.py -i setup/dev/basic.cfg
   OR
   python3 tools/marvin/marvin/deployDataCenter.py -i setup/dev/advanced.cfg

At this stage log in the CloudStack management server UI at
http://localhost:5050 or using CLI with the API endpoint at
http://localhost:8080/client with the credentials admin/password, you should see
a fully configured zone infrastructure.

You can now run integration tests, use the API etc.

Using Appliance for development
-------------------------------

The Installing from source section will only get you to the point of
runnign the management server, it does not get you any hypervisors. The
simulator section gets you a simulated datacenter for testing. An appliance
based development such as using ``mbx`` can allow you to run at least one
hypervisor and add it to your management server the way you would a real physical machine.

MonkeyBox or `mbx <https://github.com/shapeblue/mbx>`__
enable VM/appliance-based CloudStack development. It is tested with Ubuntu and
uses KVM and prebuilt images to deploy QA and dev environments for anybody to
try out CloudStack with a range of hypervisors, local and NFS storage.

Please refer to the project for more details: https://github.com/shapeblue/mbx

Building Packages
-----------------

Working from source is necessary when developing CloudStack. As
mentioned earlier this is not primarily intended for users. However some
may want to modify the code for their own use and specific
infrastructure. The may also need to build their own packages for
security reasons and due to network connectivity constraints. This
section shows you the gist of how to build packages. We assume that the
reader will know how to create a repository to serve this packages. The
complete documentation is available in the :ref:`building_deb_packages`
section.

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
`docs <https://cloudstack.apache.org/api.html>`__ are a good start to
learn the extent of the API. Multiple clients exist on
`GitHub <https://github.com/search?q=cloudstack+client&ref=cmdform>`__
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
`docs <https://cloudstack.apache.org/api.html>`__. Asynchronous calls
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

All the clients that you will find on GitHub will implement this
signature technique, you should not have to do it by hand. Now that you
have explored the API through the UI and that you understand how to make
low level calls, pick your favorite client of use
`CloudMonkey <https://pypi.python.org/pypi/cloudmonkey/>`__. CloudMonkey
is a sub-project of Apache CloudStack and gives operators/developers the
ability to use any of the API methods. It has nice auto-completion and
help feature as well as an API discovery mechanism since 4.2.

Conclusions
-----------

CloudStack is a mostly Java application running with Jetty and Mysql.
It consists of a management server and depending on the hypervisors
being used, an agent installed on the hypervisor farm. To complete a
Cloud infrastructure however you will also need some Zone wide storage
a.k.a Secondary Storage and some Cluster wide storage a.k.a Primary
storage. The choice of hypervisor, storage solution and type of Zone
(i.e Basic vs. Advanced) will dictate how complex your installation can
be. As a quick start, you might want to consider KVM+NFS and a Basic
Zone.

If you've run into any problems with this, please ask on the
cloudstack-dev `mailing list <https://cloudstack.apache.org/mailing-lists.html>`__.
