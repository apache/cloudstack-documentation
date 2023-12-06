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


The Cloudian Connector Plugin
=============================

Introduction to the Cloudian Connector Plugin
---------------------------------------------

The Cloudian (HyperStore) Connector is a native CloudStack plugin that allow
integration between Apache CloudStack and Cloudian Management Console (CMC). The
Connector integrates Cloudian S3 Storage into the CloudStack Management GUI and
allows administrators to easily give their CloudStack users access to and manage
their own S3 storage areas.

Compatibility
~~~~~~~~~~~~~

The following table shows the compatiblity of Cloudian Connector with CloudStack.

.. cssclass:: table-striped table-bordered table-hover

+---------------------+----------------------+-------------------------+
| Connector Version   | CloudStack version   | Cloudian Compatibility  |
+=====================+======================+=========================+
| 4.9_6.2-1           | 4.9                  | Version 6.2 and onwards |
+---------------------+----------------------+-------------------------+
| 4.11+               | 4.11+                | Version 6.2 and onwards |
+---------------------+----------------------+-------------------------+

Table: Support Matrix

.. note::
   Starting CloudStack 4.11, the Connector will be part of the CloudStack
   release and will not need to be externally installed.

Connector Overview
------------------

Single-Sign-On Integration
~~~~~~~~~~~~~~~~~~~~~~~~~~

The connector plugin adds a Cloudian Storage button to the CloudStack UI. This
button is available for all users on the bottom left of the menu.

.. figure:: /_static/images/cloudian-tab.png
   :align: center
   :alt: a screenshot of an enabled Cloudian Connector

When a user clicks this button, a new window or tab (depending on the web
browser preferences) is opened for the HyperStore CMC GUI. The CloudStack user
is automatically logged in to CMC as the correctly mapped HyperStore user using
Single-Sign-On (SSO).

With the connector enabled, when the user clicks ‘Log Out’ in the CloudStack UI
this first logs the user out of CloudStack and then redirects the page to log
out any logged-in Cloudian user out of CMC GUI and finally redirects the page to
the CloudStack login page.

Single-Sign-On is a technique where CloudStack and HyperStore are configured to
trust each other. This is achieved by configuring both HyperStore and the
CloudStack connector with the same SSO Shared Key. The CloudStack connector
creates a special login URL for CMC which it signs using this shared key. Upon
receiving the special signed login URL, CMC validates the request by comparing
the signature to its own copy of the shared key and the user is automatically
logged in.

User Mapping and Provisioning/De-provisioning
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack domains are mapped to Cloudian Groups. CloudStack Accounts within
those domains are mapped to Cloudian users. The Cloudian user and group are
created on demand if it doesn’t already exist when the CloudStack user accesses
CMC through the Cloudian Storage button. When Accounts and domains are created
or removed in CloudStack, they automatically create or remove users or groups in
CMC.

.. cssclass:: table-striped table-bordered table-hover

+---------------------+----------------------------+
| CloudStack Entity   | Equivalent Cloudian Entity |
+=====================+============================+
| Account             | User                       |
+---------------------+----------------------------+
| Domain              | Group                      |
+---------------------+----------------------------+

Table: Mapping Between Cloudian and CloudStack

.. note::
   Adding groups or users directly through Cloudian does not add
   corresponding CloudStack Domains or Accounts. The integration is driven
   completely from the CloudStack side.

Special Admin User Mapping
~~~~~~~~~~~~~~~~~~~~~~~~~~

The special CloudStack admin is are mapped to a special HyperStore Admin user
account which defaults to the user id admin. As the admin user on HyperStore is
configurable, there is a configuration option to control this mapping. This
mapping dictates which HyperStore user is automatically logged in using SSO when
the CloudStack admin user clicks "Cloudian Storage".

.. note::
   The Cloudian Admin user default is called admin. Older versions of
   Cloudian used to use admin@cloudian.com.

DNS Resolution Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The CloudStack Management Server will need to be access the Cloudian admin
service. The Cloudian admin service is commonly run on the same nodes as your
Cloudian S3 servers. The admin service is used to provision and deprovision
Cloudian users and groups automatically by CloudStack.

Additionally, your CloudStack users will need to be able to resolve your CMC
server hostname on their desktops so that they can access CMC.

Example domain names that should resolve:

.. cssclass:: table-striped table-bordered table-hover

+---------------------+----------------------+------------------------------+
| Resolvable Name     | Required By          | Description                  |
+=====================+======================+==============================+
| mgmt.abc-cloud.com  | User's browser       | CloudStack Management Server |
+---------------------+----------------------+------------------------------+
| cmc.abc-cloud.com   | User's browser       | Cloudian CMC                 |
+---------------------+----------------------+------------------------------+
| admin.abc-cloud.com | Management Server    | Cloudian Admin Server        |
+---------------------+----------------------+------------------------------+

Table: DNS Name Resolution Example


Configuring the Cloudian Connector
----------------------------------

Prerequisites
~~~~~~~~~~~~~

Cloudian ships with SSO disabled by default. You will need to enable it on each
CMC server. Additionally, you will need to choose a unique SSO shared key that
you will also configure in the CloudStack connector further below.

Edit Puppet config to enable SSO on all CMC servers:

   ::

     # vi /etc/cloudian-[version]-puppet/modules/cmc/templates/mts-ui.properties.erb
       sso.enabled=true
       sso.shared.key=YourSecretKeyHere


.. note::
   Once configured in Puppet, you should roll out to each CMC server and
   restart CMC services. Please refer to the HyperStore documentation for how to
   do this.

Connector Configuration
~~~~~~~~~~~~~~~~~~~~~~~

The main way to configure, enable and disable the connector is using the
CloudStack global setting. The global settings provide an easy way to configure
the connector and synchronize setting across multiple management server(s). The
following global setting can be accessed and changed using the CloudStack UI:

.. cssclass:: table-striped table-bordered table-hover

+------------------------------+------------------------------------------------+
| Global Setting               | Description                                    |
+==============================+================================================+
| cloudian.connector.enabled   | Setting to enable/disable the plugin           |
+------------------------------+------------------------------------------------+
| cloudian.admin.host          | The Cloudian admin server host                 |
+------------------------------+------------------------------------------------+
| cloudian.admin.port          | The Cloudian admin server port, usually 19443  |
|                              | (https) or 18081 (http)                        |
+------------------------------+------------------------------------------------+
| cloudian.admin.protocol      | The Cloudian admin server protocol, http/https |
+------------------------------+------------------------------------------------+
| cloudian.validate.ssl        | Whether to validate SSL certificate of Cloudian|
|                              | admin service while making API calls           |
+------------------------------+------------------------------------------------+
| cloudian.admin.user          | Basic auth user name for Cloudian admin server |
+------------------------------+------------------------------------------------+
| cloudian.admin.password      | Basic auth password for Cloudian admin server  |
+------------------------------+------------------------------------------------+
| cloudian.api.request.timeout | The admin API request timeout in seconds       |
+------------------------------+------------------------------------------------+
| cloudian.cmc.admin.user      | The user id of the CMC admin that maps to      |
|                              | CloudStack admin user                          |
+------------------------------+------------------------------------------------+
| cloudian.cmc.host            | The Cloudian Management Console hostname       |
+------------------------------+------------------------------------------------+
| cloudian.cmc.port            | The Cloudian Management Console port           |
+------------------------------+------------------------------------------------+
| cloudian.cmc.protocol        | The Cloudian Management Console protocol       |
+------------------------------+------------------------------------------------+
| cloudian.sso.key             | The shared secret as configured in Cloudian CMC|
+------------------------------+------------------------------------------------+

Table: Cloudian Connector Global Settings

.. note::
   Change in only ‘cloudian.connector.enabled’ setting requires restarting of
   all the CloudStack management server(s), rest of the setting can be changed
   dynamically without requiring to restart the CloudStack management server(s).

Enabling the Cloudian Connector
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Cloudian Connector comes disabled by default, enabling the connector is the
last step. You should have already configured the Cloudian Connector global
settings. To enable the connector, ensure that the global setting
"cloudian.connector.enabled" is set to true. Finally, restart each of the
management server(s) to reload and enable the connector.

For example, here is how you can restart the CloudStack management server
installed on CentOS7:

   ::

     # systemctl restart cloudstack-management


Troubleshooting
~~~~~~~~~~~~~~~~

Most of the trouble you may run into will be configuration related.

There are a few things which can go wrong for SSO. Here are the most common
problems and things to check:

-  Does the global settings cloudian.cmc.admin.user point to the correct Cloudian
   (admin) user?

-  Is SSO configured and enabled on Cloudian HyperStore CMC?

-  Check for errors in the CMC log file.

-  Are both CloudStack and HyperStore CMC configured with the same cloudian.sso.key?

-  Check the /var/log/cloudstack/management/management-server.log file and
   search for errors relating to SSO.

-  Try access the CMC host directly from the problem users host using the
   configured cloudian.cmc.host, cloudian.cmc.port and cloudian.cmc.protocol
   configured in the CloudStack global settings.

-  If you log out of the management server and log in again, does the Cloudian
   Storage button work?


Adding/Deleting Domains or Accounts fails: These operations use the Cloudian
Admin Server. It's likely that something has changed with the connection or the
admin server is down. Check list:

-  Is the admin server alive and listening?

-  Try access the admin server host directly from the problem users host using
   the configured cloudian.admin.host, cloudian.admin.port and
   cloudian.admin.protocol configured in the CloudStack global settings. Check the
   configured auth settings cloudian.admin.user and cloudian.admin.password.

-  If you’re experiencing timeout issues, trying changing the API timeout value
   defined in cloudian.api.request.timeout global setting.

-  Look for errors in the admin log file /var/log/cloudian/cloudian-admin.log.


------------


Cloudian as CloudStack Secondary Storage
----------------------------------------

This section is a supplementary guide for CloudStack and describes how to
configure CloudStack to use Cloudian HyperStore as Secondary Storage. Please
also review CloudStack’s documentation (Getting Started Guide) for configuring
and using S3 as Secondary Storage.

CloudStack, as of version 4.2.1, can utilize Cloudian HyperStore as S3 Secondary
Storage out of the box. There is no need for any modifications or to install any
connectors. Secondary Storage is used to store ISOs, Templates, Snapshots and
Volumes.

.. note::
   CloudStack still requires an NFS Secondary Storage Staging Server with is
   mentioned in the requirements below.

Requirements:

-  CloudStack 4.5+ (installed/configured and running)
-  Cloudian HyperStore 5.0 or greater (installed/configured and running)

NFS Secondary Storage Staging Server Requirement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The use of S3 as Secondary Storage for CloudStack also requires an NFS server.
The NFS server is required because the various hypervisors cannot yet talk
directly to S3 but instead talk through the standard file system API. As such,
CloudStack requires an NFS staging server which the Hypervisors use to read and
write data from/to. The NFS storage requirements for the staging server are
small however as space is only required while objects are staged (moving)
between the S3 server and the Instances.


DNS Name Resolution Requirement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

All CloudStack Management Servers, System VMs and customer Instances (if required)
must be able to resolve your S3 bucket names. Usually, if you already have
Cloudian installed and running in your environment, this is already working.
At a minimum the following names should resolve to the correct IP addresses
using the DNS server that your Management Server and System VMs are using.

.. cssclass:: table-striped table-bordered table-hover

+---------------------+------------------------------+
| Example Name        | DNS Name Types               |
+=====================+==============================+
| s3.mycloud.com      | Cloudian S3 Endpoint         |
+---------------------+------------------------------+
| sec.s3.mycloud.com  | Bucket for Secondary Storage |
+---------------------+------------------------------+
| s3-admin.mycloud.com| Cloudian Admin Server        |
+---------------------+------------------------------+

Table: Example Domain Names that should Resolve on CloudStack Servers

Adding Cloudian as CloudStack Secondary Storage
-----------------------------------------------

Setup a Cloudian User and Bucket for Secondary Storage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

S3 Secondary Storage stores the CloudStack Templates, Snapshots etc in a
dedicated S3 Bucket. To properly configure CloudStack you will need to know the
S3 Bucket name and how to access your S3 Server (the S3 endpoint, access key and
secret key).

Below, we will create a dedicated Cloudian user and a dedicated bucket which we
will assign for use as Secondary Storage.

Create a dedicated user/group:

-  Login to the Cloudian Management Console (CMC) as the Cloudian admin user.

-  Create a new group called cloudstack. Any group name is ok.

-  Create a new user called cloudstack in the cloudstack group. Any user name is ok.


Create a dedicated bucket:

-  Login to CMC as the cloudstack user created above.

-  Create a bucket called secondary. Any bucket name will do.

-  On the top menu bar on the right hand side, use the drop down menu under your
   user name to select Security Credentials and copy and paste your Access and
   Secret Keys to a note for later use. CloudStack will need these when you attach
   Cloudian as Secondary Storage in a later step below.

Open Up Access to your S3 Network from Secondary Storage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If your S3 server is on a different Network to your Secondary Storage VM, you
will need to open up access to the S3 Network. This also allows users to
download Templates from their S3 object store areas.

.. figure:: /_static/images/cloudian-ss_globalopt.png
   :align: center
   :alt: a screenshot of changing global settings

.. note::
   Editing the Global Settings requires you to restart the management server(s).

Add an NFS Secondary Storage Staging Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As mentioned previously, S3 Secondary Storage currently requires the use of an
NFS Secondary Staging Server. Add NFS Secondary Storage Staging Server:

-  Login to CloudStack Management Server as the admin user.

-  Navigate to Infrastructure → Secondary Storage.

-  Click Select View and select Secondary Staging Store.

-  Click Add Secondary Staging Store.

-  Configure the zone, server and path for your desired secondary staging store.
   For example nfs.mycloud.com and /export/staging.

.. figure:: /_static/images/cloudian-s3_ss_cache.png
   :align: center
   :alt: a screenshot of adding secondary staging store

Attach Cloudian as Secondary Storage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack supports using either S3 or NFS as Secondary Storage but not both.
The below instructions assume you are not using Secondary Storage on NFS and
that you can delete it to add the S3 storage.

.. note::
  Already using NFS for Secondary Storage with CloudStack? You need to migrate
  your Secondary Storage. Refer to CloudStack’s instructions for migrating
  existing NFS Secondary Storage to an S3 object storage. CloudStack 4.5 onwards
  supports migrating data via special commands which are described in the Getting
  Started Guide in a section titled Upgrading from NFS to Object Storage.

Adding S3 Secondary Storage:

-  Login to CloudStack Management Server as the admin user.

-  Navigate to Infrastructure → Secondary Storage.

-  If it exists, select and delete any existing NFS Secondary Storage server
   setting. NOTE: Do not do this if you want to migrate existing NFS secondary
   storage to S3. Instead, see warning above.

-  Click the Add Secondary Storage button. This will open up a pop-up form which
   you can fill out similarly to below.

.. figure:: /_static/images/cloudian-s3_ss_config.png
   :align: center
   :alt: a screenshot of configuring S3 secondary storage

.. note::
   CloudStack doesn’t currently allow you to re-edit the S3 configuration so take
   time to double check what you enter. If you make a mistake the only options
   currently are either a) delete and recreate the storage or b) directly edit the
   entry in the database.

When you have finished adding Cloudian as Secondary Storage in the previous
steps, CloudStack will populate the new secondary storage with the system and
default Templates. This can take some time do download as the Templates are
quite big.

.. note::
   You can check if the system Template and the default Template have properly
   downloaded to the new secondary storage by navigating to Templates, selecting a
   Template, clicking on the Zones tab and checking its Status is Ready 100%
   Downloaded.

.. note::
   Should you continue to have problems, sometimes it is necessary to restart
   the Secondary Storage VM. You can do this by navigating to Infrastructure,
   System VMs, selecting and rebooting the Secondary Storage VM.

CloudStack should now ready to use Cloudian HyperStore for S3 Secondary Storage.

Revision History
----------------

-  Fri Oct 6 2017 Rohit Yadav rohit.yadav@shapeblue.com Documentation
   created for 4.11.0 version of the Cloudian Connector Plugin
