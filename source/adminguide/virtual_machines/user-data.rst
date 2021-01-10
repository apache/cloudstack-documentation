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

CloudStack provides APIs to attach up to 32KB of user-data to a deployed VM.

There are two CloudStack APIs that can be used to store user-data:
`deployVirtualMachine <http://cloudstack.apache.org/docs/api/apidocs-4.14/user/deployVirtualMachine.html>`_
and
`updateVirtualMachine <http://cloudstack.apache.org/docs/api/apidocs-4.14/user/updateVirtualMachine.html>`_
They both support the parameter ``userdata=``. The value for this parameter
must be a `base64 <https://www.base64encode.org/>`_-encoded multi-part MIME
message. See further below for an example of what this should look like.

HTTP GET parameters are limited to a length of 2048 bytes, but it is possible
to store larger user-data blobs by sending them in the body via HTTP POST
instead of GET.

From inside the VM, the user-data is accessible via the virtual router,
if the UserData service is enabled on the network offering.

If you are using the DNS service of the virtual router, a special hostname
called `data-server.` is provided, that will point to a valid user-data server.

Otherwise you have to determine the virtual router address via other means,
such as DHCP leases. Be careful to scan all routers if you have multiple
networks attached to a VM, in case not all of them have the UserData service
enabled.

User-data is available from the URL ``http://data-server./latest/user-data``
and can be fetched via curl or other HTTP client.

It is also possible to fetch VM metadata from the same service, via the URL
``http://data-server./latest/{metadata type}``.  For backwards compatibility,
the previous URL ``http://data-server./latest/{metadata type}`` is also supported.

For metadata type, use one of the following:

-  ``service-offering``. A description of the VMs service offering

-  ``availability-zone``. The Zone name

-  ``local-ipv4``. The guest IP of the VM

-  ``local-hostname``. The hostname of the VM

-  ``public-ipv4``. The first public IP for the router.

-  ``public-hostname``. This is the same as public-ipv4

-  ``instance-id``. The instance name of the VM


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

User-data is not included with the normal VM state for historic reasons.
To read out the base64-encoded user-data via the API, use the `getVirtualMachineUserData <http://cloudstack.apache.org/docs/api/apidocs-4.14/user/getVirtualMachineUserData.html>`_
API call:

.. code:: bash

   cmk get virtualmachineuserdata virtualmachineid=8fd996b6-a102-11ea-ba47-23394b299ae9


Using cloud-init
~~~~~~~~~~~~~~~~

`cloud-init <https://cloudinit.readthedocs.org/en/latest>`_ can be used to access
and interpret user-data inside virtual machines. If you install cloud-init into your
VM templates, it will allow you to store SSH keys and user passwords on each new
VM deployment automatically (:ref:`adding-password-management-to-templates` and `using ssh keys <virtual_machines.html#using-ssh-keys-for-authentication>`_).

#. Install cloud-init package into a VM template:

   .. code:: bash

      # yum install cloud-init
        or
      $ sudo apt-get install cloud-init

#. Create a datasource configuration file in the VM template: ``/etc/cloud/cloud.cfg.d/99_cloudstack.cfg``

   .. code:: yaml

      datasource:
        CloudStack: {}
        None: {}
      datasource_list:
        - CloudStack


Custom user-data example
~~~~~~~~~~~~~~~~~~~~~~~~

This example uses cloud-init to automatically update all OS packages on the first launch.

#. Create user-data, wrapped into a multi-part MIME message and encoded in base64:

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
   
#. Deploy a VM with this user-data:

.. code:: bash

   cmk deploy virtualmachine name=..... userdata=Q29udGVudC1UeXBlOiBtdWx0aXBhcnQvbWl4ZWQ7IGJvdW5kYXJ5PSIvLyIKTUlNRS1WZXJzaW9uOiAxLjAKCi0tLy8KQ29udGVudC1UeXBlOiB0ZXh0L2Nsb3VkLWNvbmZpZzsgY2hhcnNldD0idXMtYXNjaWkiCk1JTUUtVmVyc2lvbjogMS4wCkNvbnRlbnQtVHJhbnNmZXItRW5jb2Rpbmc6IDdiaXQKQ29udGVudC1EaXNwb3NpdGlvbjogYXR0YWNobWVudDsgZmlsZW5hbWU9ImNsb3VkLWNvbmZpZy50eHQiCgojY2xvdWQtY29uZmlnCgojIFVwZ3JhZGUgdGhlIGluc3RhbmNlIG9uIGZpcnN0IGJvb3QKIyAoaWUgcnVuIGFwdC1nZXQgdXBncmFkZSkKIwojIERlZmF1bHQ6IGZhbHNlCiMgQWxpYXNlczogYXB0X3VwZ3JhZGUKcGFja2FnZV91cGdyYWRlOiB0cnVlCg==


Disclaimer
~~~~~~~~~~

Refer to the `cloud-init CloudStack datasource <http://cloudinit.readthedocs.org/en/latest/topics/datasources.html#cloudstack>`_
documentation for latest capabilities. cloud-init and the cloud-init CloudStack
datasource are not supported by Apache CloudStack community.
