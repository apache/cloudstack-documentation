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


User-Data and Meta-Data
-----------------------

Users can register userdata in CloudStack and refer the registered userdata while
deploying or editing or reset userdata on an instance. The userdata content can also be
directly provided while deploying the instance. Userdata content length can be up to 32kb.

To register a new userdata:

#. Log in to the CloudStack UI.

#. In the left navigation bar, click Compute and then User Data.

#. Click Register a userdata.

#. In the dialog, make the following choices:

   -  **Name**: Any desired name for the userdata.

   -  **Userdata**: Plain userdata content. CloudStack UI does base64 encoding.

   -  **Userdata parameters**: Comma separated list of variables which (if any) declared
      in userdata content.

   -  **Domain**: An optional domain for the userdata.

   -  **Account**: An optional account for the userdata.

.. image:: /_static/images/register_userdata.png
   :width: 400px
   :align: center
   :alt: Regiser userdata dialog box

If userdata content has variables declared in it, user can register the Userdata
with userdata parameters.

For example, if userdata content is like below having a custom variable "variable1"

   .. code:: bash

      ## template: jinja
      #cloud-config
      runcmd:
         - echo 'TestVariable {{ ds.meta_data.variable1 }}' >> /tmp/variable
         - echo 'Hostname {{ ds.meta_data.public_hostname }}' > /tmp/hostname

Userdata has to be registered with userdata parameter "variable1" like below

.. image:: /_static/images/register_userdata_with_variables.png
   :width: 400px
   :align: center
   :alt: Regiser userdata with variables dialog box

If the variables in userdata content are of a predefined metadata like "public_hostname"
or "instance_id", then userdata parameters should not declare these variables. That is
the reason in the above example "public_hostname" is not declared.

There are three CloudStack APIs that can be used to provide user-data to instance:
deployVirtualMachine, updateVirtualMachine and resetUserDataForVirtualMachine.
These APIs accepts parameters ``userdataid`` and ``userdatadetails``.
userdatadetails is to specify the custom values for the variables which are declared
in userdata in a key value parameter map details.

.. image:: /_static/images/deployvm_userdata.png
   :width: 400px
   :align: center
   :alt: Provide userdata id or userdata text dialog box

If the userdata contains variables that are declared during registration then those values
has to be specified like below,

.. image:: /_static/images/deployvm_userdata_with_variables.png
   :width: 400px
   :align: center
   :alt: Provide userdata id or userdata with variables text dialog box

These details will be saved as meta-data file(s) in both config drive and virtual router,
which in turn support jinja based instance meta-data feature of cloud-init,
refer to https://cloudinit.readthedocs.io/en/latest/topics/instancedata.html.

These APIs also support the parameter ``userdata=`` to provide the userdata content
directly. The value for this parameter must be a `base64 <https://www.base64encode.org/>`_-encoded
multi-part MIME message. See further below for an example of what this should look like.

The registered UserData can be linked to a Template or ISO on registration/upload/editing
using linkUserDataToTemplate API. The same API can be used to unlink the mapping of userdata and Template.

While linking userData to a Template/ISO userdata override policy has to be specified.
Following are the override policies available: 

Allow Override: Allow users to override UserData for the Template during instance deployment or on reset.
                This is the default override policy if not specified 

Deny Override: Override of UserData isn’t allowed during instance deployment or on reset.

Append Only: Don’t allow users to override linked UserData but allow users to pass userdata content 
             or ID that should be appended to the linked UserData of the Template. When the users pass userdata it is appended to the Template userdata in the form of a multipart MIME message

This is how it looks like in Template/ISO register/upload/edit forms.

.. image:: /_static/images/userdata_template_link.png
   :width: 400px
   :align: center
   :alt: Linking userdata to template/ISO

Based on these override policies, "Add Instance" UI form provides relevant options to either
override or append. If it is "Deny Override" then "Add Instance" will not allow adding user specific userdata

Storing and accessing userdata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

HTTP GET parameters are limited to a length of 2048 bytes, but it is possible
to store larger user-data blobs by sending them in the body via HTTP POST
instead of GET.

From inside the instance, the user-data is accessible via the virtual router,
if the UserData service is enabled on the network offering.

If you are using the DNS service of the virtual router, a special hostname
called `data-server.` is provided, that will point to a valid user-data server.

Otherwise you have to determine the virtual router address via other means,
such as DHCP leases. Be careful to scan all routers if you have multiple
networks attached to an instance, in case not all of them have the UserData service
enabled.

User-data is available from the URL ``http://data-server./latest/user-data``
and can be fetched via curl or other HTTP client.

It is also possible to fetch instance metadata from the same service, via the URL
``http://data-server./latest/{metadata type}``.  For backwards compatibility,
the previous URL ``http://data-server./latest/{metadata type}`` is also supported.

For metadata type, use one of the following:

-  ``service-offering``. A description of the instances service offering

-  ``availability-zone``. The Zone name

-  ``local-ipv4``. The guest IP of the instance

-  ``local-hostname``. The hostname of the instance

-  ``public-ipv4``. The first public IP for the router.

-  ``public-hostname``. This is the same as public-ipv4

-  ``instance-id``. The instance name of the instance


Determining the virtual router address without DNS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If can't or don't want to use the virtual router's DNS service, it's also
possible to determine the user-data server from a DHCP lease.

#. Run the following command to find the virtual router.

   .. code:: bash

      # cat /var/lib/dhcp/dhclient.eth0.leases | grep dhcp-server-identifier | tail -1

#. Access the data-server via its IP

   .. code:: bash

      # curl http://10.1.1.1/latest/user-data


Fetching user-data via the API
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

User-data is not included with the normal instance state for historic reasons.
To read out the base64-encoded user-data via the API, use the `getVirtualMachineUserData <https://cloudstack.apache.org/docs/api/apidocs-4.14/user/getVirtualMachineUserData.html>`_
API call:

.. code:: bash

   cmk get virtualmachineuserdata virtualmachineid=8fd996b6-a102-11ea-ba47-23394b299ae9


Using cloud-init
~~~~~~~~~~~~~~~~

`cloud-init <https://cloudinit.readthedocs.org/en/latest>`_ can be used to access
and interpret user-data inside Instances. If you install cloud-init into your
Instance Templates, it will allow you to store SSH keys and user passwords on each new
Instance deployment automatically (:ref:`adding-password-management-to-templates` and `using ssh keys <virtual_machines.html#using-ssh-keys-for-authentication>`_).

#. Install cloud-init package into an Instance Template:

   .. code:: bash

      # yum install cloud-init
        or
      $ sudo apt-get install cloud-init

#. Create a datasource configuration file in the Instance Template: ``/etc/cloud/cloud.cfg.d/99_cloudstack.cfg``

   .. code:: yaml

      datasource_list: [ CloudStack, None ]

For more information, see `Cloud-init integration <templates/_cloud_init.html#linux-with-cloud-init>`_

Custom user-data example
~~~~~~~~~~~~~~~~~~~~~~~~

This example uses cloud-init to automatically update all OS packages on the first launch.

#. Register the following user-data in CloudStack. If APIs are used to register userdata or to
   provide direct userdata text then userdata needs to be wrapped into a multi-part MIME message
   and encoded in base64:

   .. code:: bash

      base64 <<EOF
      Content-Type: multipart/mixed; boundary="//"
      MIME-Version: 1.0

      --//
      Content-Type: text/cloud-config; charset="us-ascii"
      MIME-Version: 1.0
      Content-Transfer-Encoding: 7bit
      Content-Disposition: attachment; filename="cloud-config.txt"

      #cloud-config

      # Upgrade the instance on first boot
      # (ie run apt-get upgrade)
      #
      # Default: false
      # Aliases: apt_upgrade
      package_upgrade: true
      EOF
   
#. Deploy an instance with this user-data either by providing the UUID of the registerd userdata
   or by providing base64 encoded userdata:

   .. code:: bash

      cmk deploy virtualmachine name=..... userdata=Q29udGVudC1UeXBlOiBtdWx0aXBhcnQvbWl4ZWQ7IGJvdW5kYXJ5PSIvLyIKTUlNRS1WZXJzaW9uOiAxLjAKCi0tLy8KQ29udGVudC1UeXBlOiB0ZXh0L2Nsb3VkLWNvbmZpZzsgY2hhcnNldD0idXMtYXNjaWkiCk1JTUUtVmVyc2lvbjogMS4wCkNvbnRlbnQtVHJhbnNmZXItRW5jb2Rpbmc6IDdiaXQKQ29udGVudC1EaXNwb3NpdGlvbjogYXR0YWNobWVudDsgZmlsZW5hbWU9ImNsb3VkLWNvbmZpZy50eHQiCgojY2xvdWQtY29uZmlnCgojIFVwZ3JhZGUgdGhlIGluc3RhbmNlIG9uIGZpcnN0IGJvb3QKIyAoaWUgcnVuIGFwdC1nZXQgdXBncmFkZSkKIwojIERlZmF1bHQ6IGZhbHNlCiMgQWxpYXNlczogYXB0X3VwZ3JhZGUKcGFja2FnZV91cGdyYWRlOiB0cnVlCg==

   .. code:: bash

      cmk deploy virtualmachine name=..... userdataid=<Userdata UUID>

.. note:: When using multipart userdata, cloud-init expects userdata format of one particular type only in one multipart section.

Disclaimer
~~~~~~~~~~

Refer to the `cloud-init CloudStack datasource <http://cloudinit.readthedocs.org/en/latest/topics/datasources.html#cloudstack>`_
documentation for latest capabilities. cloud-init and the cloud-init CloudStack
datasource are not supported by Apache CloudStack community.
