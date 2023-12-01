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


User Data and Meta Data
~~~~~~~~~~~~~~~~~~~~~~~

The user-data service on a Shared or Isolated Network can be provided through the
Virtual Router or through an attached iso called the Config drive.

User Data and Meta Data Via Virtual Router
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


CloudStack provides API access to attach up to 32KB of user data to a
deployed Instance. Deployed Instances also have access to metadata via the
virtual router.

User data can be accessed once the IP address of the virtual router is
known. Once the IP address is known, use the following steps to access
the user data:

#. Run the following command to find the virtual router.

   .. code:: bash
      # cat /var/lib/dhclient/dhclient-eth0.leases | grep dhcp-server-identifier | tail -1
#. Access user data by running the following command using the result of
   the above command

   .. code:: bash
      # curl http://10.1.1.1/latest/user-data
Meta Data can be accessed similarly, using a URL of the form
http://10.1.1.1/latest/meta-data/{metadata type}. (For backwards
compatibility, the previous URL http://10.1.1.1/latest/{metadata type}
is also supported.) For metadata type, use one of the following:

-  service-offering. A description of the Instance service offering

-  availability-zone. The Zone name

-  local-ipv4. The guest IP of the Instance

-  local-hostname. The hostname of the Instance

-  public-ipv4. The first public IP for the router. (E.g. the first IP
   of eth2)

-  public-hostname. This is the same as public-ipv4

-  instance-id. The Instance name

User Data and Meta Data via Config Drive
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Config drive is an ISO file that is mounted as a cd-rom on a user Instance and
contains related userdata, metadata (incl. ssh-keys) and
password files.

Enable config drive
~~~~~~~~~~~~~~~~~~~
To use the config drive the Network offering must have the “ConfigDrive”
provider selected for the userdata service.

If the networkoffering uses ConfigDrive for userdata and the Template is
password enabled, the password string for the Instance is placed in the
vm_password.txt file and it is included in the ISO.

ConfigDrive availability
~~~~~~~~~~~~~~~~~~~~~~~~
At Instance start the config drive ISO is attached on the 2nd cd/dvd drive of the
user Instance, such that any other ISO image (e.g. boot image or vmware tools)
is mounted on 1st cd/dvd drive. This means existing functionality of
supporting 1 cd rom drive is still available.

At password reset or update of user data, the Config Drive ISO
will be rebuilt. The existing ISO is mounted on a temporary directory,
password, userdata or ssh-keys are updated and a new ISO is built from the
updated directory structure.

In case of a password reset, the new password will be picked-up at Instance start.
To access the updated userdata, the user needs to remount the config drive ISO.

When an Instance is stopped, the ConfigDrive network element will trigger the
Secondary Storage VM to remove the ISO from the secondary storage.
If the config drive is stored on primary storage, the network element will
trigger the host to remove the ISO.

The config drive ISO can be stored on primary storage by setting the global
setting vm.configdrive.primarypool.enabled to true. This is currently only
supported with use of the KVM Hypervisor.

Supporting ConfigDrive
~~~~~~~~~~~~~~~~~~~~~~

Extra data is added to the Instance profile to enable the creation of the config drive:

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

    - vm_password_md5checksum (for windows Instances)

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
