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
 

The CloudStack API is a low level API that has been used to implement
the CloudStack web UIs. It is also a good basis for implementing other
popular APIs such as EC2/S3 and emerging DMTF standards.

Many CloudStack API calls are asynchronous. These will return a Job ID
immediately when called. This Job ID can be used to query the status of
the job later. Also, status calls on impacted resources will provide
some indication of their state.

The API has a REST-like query basis and returns results in XML or JSON.

See `the Developer’s Guide <https://cwiki.apache.org/confluence/display/CLOUDSTACK/Development+101>`_
and `the API Reference <https://cloudstack.apache.org/api.html>`_.


Provisioning and Authentication API
-----------------------------------

CloudStack expects that a customer will have their own user provisioning
infrastructure. It provides APIs to integrate with these existing
systems where the systems call out to CloudStack to add/remove users..

CloudStack supports pluggable authenticators. By default, CloudStack
assumes it is provisioned with the user’s password, and as a result
authentication is done locally. However, external authentication is
possible as well. For example, see Using an LDAP Server for User
Authentication.


User Data and Meta Data via Config Drive
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Config drive is an ISO file that is mounted as a cd-rom on a user VM and
contains the user VM related userdata, metadata (incl. ssh-keys) and
password files.

Enable config drive
~~~~~~~~~~~~~~~~~~~
To use the config drive the network offering must have the “ConfigDrive”
provider selected for the userdata service.

If the networkoffering uses ConfigDrive for userdata and the template is
password enabled, the password string for the VM is placed in the
vm_password.txt file and it is included in the ISO.

ConfigDrive availability
~~~~~~~~~~~~~~~~~~~~~~~~
At VM start the config drive ISO is attached on the 2nd cd/dvd drive of the
user instance, such that any other ISO image (e.g. boot image or vmware tools)
is mounted on 1st cd/dvd drive. This means existing functionality of
supporting 1 cd rom drive is still available.

At password reset or update of user data, Secondary Storage VM will rebuild the
ConfigDrive ISO image. That is the existing ISO is mounted on a temporary directory,
password, userdata or ssh-keys are updated and a new ISO is built from the
updated directory structure.

In case of a password reset, the new password will be picked-up at VM start.
To access the updated userdata, the user needs to remount the config drive ISO.

When a VM is stopped, the ConfigDrive network element will trigger the
Secondary Storage VM to remove the ISO from the secondary storage.

The config drive ISO can be stored on primary storage by setting the global
setting vm.configdrive.primarypool.enabled to true. This is currently only
supported with use of the KVM Hypervisor.

Supporting ConfigDrive
~~~~~~~~~~~~~~~~~~~~~~

Extra data is added to the VM profile to enable the creation of the config drive:

VMdata - a list of String arrays representing [“directory”, “filename”, “content”] on the ConfigDrive device.

- <mountdir>/cloudstack

  - /metadata:

    - availability-zone.txt

    - instance-id.txt

    - service-offering.txt

    - cloud-identifier.txt

    - local-hostname.txt

    - vm-id.txt

    - public-keys.txt

  - /password

    - vm_password.txt

    - vm_password_md5checksum (for windows VM’s)

- <mountdir>/openstack/version/:

  - user_data (=hardlink to <mountdir>/cloudstack/user_data/user_data.txt)

    - vendor_data.json

    - meta_data.json

    - Network_data.json

  - label, which is configurable in global settings:

    - name : vm.configdrive.label

    - default: config-2

For more detailed information about the Config Drive implementation refer to
the `Wiki Article
<https://cwiki.apache.org/confluence/display/CLOUDSTACK/Using+ConfigDrive+for+Metadata%2C+Userdata+and+Password#:~:text=CLOUDSTACK%2D9813%20%2D%20(),%2Dkeys)%20and%20password%20files>`_