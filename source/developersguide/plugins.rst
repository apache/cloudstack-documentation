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


Plugins
=======

Storage Plugins
---------------

This section gives an outline of how to implement a plugin to integrate
a third-party storage provider. For details and an example, you will
need to read the code.

.. note:: Example code is available at: `plugins/storage/volume/sample`

Third party storage providers can integrate with CloudStack to provide
either primary storage or secondary storage. For example, CloudStack
provides plugins for Amazon Simple Storage Service (S3) or OpenStack
Object Storage (Swift). The S3 plugin can be used for any object storage
that supports the Amazon S3 interface.

Additional third party object storages that do not support the S3
interface can be integrated with CloudStack by writing plugin software that
uses the object storage plugin framework. Several new interfaces are
available so that storage providers can develop vendor-specific plugins
based on well-defined contracts that can be seamlessly managed by
CloudStack.

Artifacts such as Templates, ISOs and Snapshots are kept in storage
which CloudStack refers to as secondary storage. To improve scalability and
performance, as when a number of hosts access secondary storage
concurrently, object storage can be used for secondary storage. Object
storage can also provide built-in high availability capability. When
using object storage, access to secondary storage data can be made
available across multiple zones in a region. This is a huge benefit, as
it is no longer necessary to copy Templates, Snapshots etc. across zones
as would be needed in an environment using only zone-based NFS storage.

The user enables a storage plugin through the UI. A new dialog box
choice is offered to select the storage provider. Depending on which
provider is selected, additional input fields may appear so that the
user can provide the additional details required by that provider, such
as a user name and password for a third-party storage account.


Overview of How to Write a Storage Plugin
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To add a third-party storage option to CloudStack, follow these general
steps (explained in more detail later in this section):

#. Implement the following interfaces in Java:

   -  DataStoreDriver

   -  DataStoreLifecycle

   -  DataStoreProvider

   -  VMSnapshotStrategy (if you want to customize the Instance Snapshot
      functionality)

#. Hardcode your plugin's required additional input fields into the code
   for the Add Secondary Storage or Add Primary Storage dialog box.

#. Place your .jar file in `plugins/storage/volume/` or
   `plugins/storage/image/`.

#. Edit `/client/tomcatconf/componentContext.xml.in`.

#. Edit `client/pom.xml`.


Implementing DataStoreDriver
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DataStoreDriver contains the code that CloudStack will use to provision the
object store, when needed.

You must implement the following methods:

-  getTO()

-  getStoreTO()

-  createAsync()

-  deleteAsync()

The following methods are optional:

-  resize()

-  canCopy() is optional. If you set it to true, then you must implement
   copyAsync().


Implementing DataStoreLifecycle
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DataStoreLifecycle contains the code to manage the storage operations
for ongoing use of the storage. Several operations are needed, like
create, maintenance mode, delete, etc.

You must implement the following methods:

-  initialize()

-  maintain()

-  cancelMaintain()

-  deleteDataStore()

-  Implement one of the attach\*() methods depending on what scope you
   want the storage to have: attachHost(), attachCluster(), or attachZone().


Implementing DataStoreProvider
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DataStoreProvider contains the main code of the data store.

You must implement the following methods:

-  getDatastoreLifeCycle()

-  getDataStoreDriver()

-  getTypes(). Returns one or more types of storage for which this data
   store provider can be used. For secondary object storage, return
   IMAGE, and for a Secondary Staging Store, return ImageCache.

-  configure(). First initialize the lifecycle implementation and the
   driver implementation, then call registerDriver() to register the new
   object store provider instance with CloudStack.

-  getName(). Returns the unique name of your provider; for example,
   this can be used to get the name to display in the UI.

The following methods are optional:

-  getHostListener() is optional; it's for monitoring the status of the host.


Implementing VMSnapshotStrategy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

VMSnapshotStrategy has the following methods:

-  takeVMSnapshot()

-  deleteVMSnapshot()

-  revertVMSnapshot()

-  canHandle(). For a given Instance Snapshot, tells whether this
   implementation of VMSnapshotStrategy can handle it.


Place the .jar File in the Right Directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For a secondary storage plugin, place your .jar file here:

::

   plugins/storage/image/

For a primary storage plugin, place your .jar file here:

::

   plugins/storage/volume/


Edit Configuration Files
~~~~~~~~~~~~~~~~~~~~~~~~

First, edit the following file tell CloudStack to include your .jar file.
Add a line to this file to tell the CloudStack Management Server that it
now has a dependency on your code:

::

   client/pom.xml

Place some facts about your code in the following file so CloudStack can
run it:

::

   /client/tomcatconf/componentContext.xml.in

In the section “Deployment configurations of various adapters,” add
this:

::

   <bean>id=”some unique ID” class=”package name of your implementation of DataStoreProvider”</bean>

In the section “Storage Providers,” add this:

::

   <property name=”providers”>
      <ref local=”same ID from the bean tag's id attribute”>
   </property>


Minimum Required Interfaces
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The classes, interfaces, and methods used by CloudStack from the Amazon Web
Services (AWS) Java SDK are listed in this section. An object storage
that supports the S3 interface is minimally required to support the
below in order to be compatible with CloudStack.


Interface AmazonS3
^^^^^^^^^^^^^^^^^^

http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/services/s3/AmazonS3.html

.. cssclass:: table-striped table-bordered table-hover

+------------------+---------------------------------------------------------+
| Modifier and     | Method and Description                                  |
| Type             |                                                         |
+==================+=========================================================+
| Bucket           | createBucket(String bucketName)                         |
|                  |                                                         |
|                  | Creates a new Amazon S3 bucket with the specified name  |
|                  | in the default (US) region, Region.US\_Standard.        |
+------------------+---------------------------------------------------------+
| void             | deleteObject(String bucketName, String key)             |
|                  |                                                         |
|                  | Deletes the specified object in the specified bucket.   |
+------------------+---------------------------------------------------------+
| ObjectMetadata   | getObject(GetObjectRequest getObjectRequest,            |
|                  | File destinationFile)                                   |
|                  |                                                         |
|                  | Gets the object metadata for the object stored in       |
|                  | Amazon S3 under the specified bucket and key, and saves |
|                  | the object contents to the specified file.              |
+------------------+---------------------------------------------------------+
| S3Object         | getObject(String bucketName, String key)                |
|                  |                                                         |
|                  | Gets the object stored in Amazon S3 under the specified |
|                  | bucket and key.                                         |
+------------------+---------------------------------------------------------+
| URL              | generatePresignedUrl(String bucketName, String key,     |
|                  | Date expiration, HttpMethod method)                     |
|                  |                                                         |
|                  | Returns a pre-signed URL for accessing an Amazon S3     |
|                  | resource.                                               |
+------------------+---------------------------------------------------------+
| void             | deleteBucket(String bucketName)                         |
|                  |                                                         |
|                  | Deletes the specified bucket.                           |
+------------------+---------------------------------------------------------+
| List<Bucket>     | listBuckets()                                           |
|                  |                                                         |
|                  | Returns a list of all Amazon S3 buckets that the        |
|                  | authenticated sender of the request owns.               |
+------------------+---------------------------------------------------------+
| ObjectListing    | listObjects(String bucketName, String prefix)           |
|                  |                                                         |
|                  | Returns a list of summary information about the objects |
|                  | in the specified bucket.                                |
+------------------+---------------------------------------------------------+
| PutObjectResult  | putObject(PutObjectRequest putObjectRequest)            |
|                  |                                                         |
|                  | Uploads a new object to the specified Amazon S3 bucket. |
+------------------+---------------------------------------------------------+
| PutObjectResult  | putObject(String bucketName, String key, File file)     |
|                  |                                                         |
|                  | Uploads the specified file to Amazon S3 under the       |
|                  | specified bucket and key name.                          |
+------------------+---------------------------------------------------------+
| PutObjectResult  | putObject(String bucketName, String key,                |
|                  | InputStream input, ObjectMetadata metadata)             |
|                  |                                                         |
|                  | Uploads the specified input stream and object metadata  |
|                  | to Amazon S3 under the specified bucket and key name.   |
+------------------+---------------------------------------------------------+
| void             | setEndpoint(String endpoint)                            |
|                  |                                                         |
|                  | Overrides the default endpoint for this client.         |
+------------------+---------------------------------------------------------+
| void             | setObjectAcl(String bucketName, String key,             |
|                  | CannedAccessControlList acl)                            |
|                  |                                                         |
|                  | Sets the CannedAccessControlList for the specified      |
|                  | object in Amazon S3 using one of the pre-configured     |
|                  | CannedAccessControlLists.                               |
+------------------+---------------------------------------------------------+

*Class TransferManager*

http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/services/s3/transfer/TransferManager.html

.. cssclass:: table-striped table-bordered table-hover

+------------------+---------------------------------------------------------+
| Modifier and     | Method and Description                                  |
| Type             |                                                         |
+==================+=========================================================+
| Upload           | upload(PutObjectRequest putObjectRequest)               |
|                  |                                                         |
|                  | Schedules a new transfer to upload data to Amazon S3.   |
+------------------+---------------------------------------------------------+

*Class PutObjectRequest*

http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/services/s3/model/PutObjectRequest.html

.. cssclass:: table-striped table-bordered table-hover

+------------------+---------------------------------------------------------+
| Modifier and     | Method and Description                                  |
| Type             |                                                         |
+==================+=========================================================+
| Upload           | upload(PutObjectRequest putObjectRequest)               |
|                  |                                                         |
|                  | Schedules a new transfer to upload data to Amazon S3.   |
+------------------+---------------------------------------------------------+

