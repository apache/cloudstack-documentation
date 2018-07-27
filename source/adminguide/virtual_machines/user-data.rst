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

CloudStack provides API access to attach up to 2KB of data after base64 encoding
to a deployed VM. Using HTTP POST(via POST body), you can send up to 32K of data
after base64 encoding. Deployed VMs also have access to instance metadata via
the virtual router.

Create virtual machine thru the API: `deployVirtualMachine <http://cloudstack.apache.org/docs/api/apidocs-4.5/user/deployVirtualMachine.html>`_
using the parameter ``userdata=`` to include user-data formated in
`base64 <https://www.base64encode.org/>`_.

Accessed user-data from VM. Once the IP address of the virtual router is
known, use the following steps to retrieve user-data:

#. Run the following command to find the virtual router.

   .. code:: bash

      # cat /var/lib/dhclient/dhclient-eth0.leases | grep dhcp-server-identifier | tail -1

#. Access user-data by running the following command using the result of
   the above command

   .. code:: bash

      # curl http://10.1.1.1/latest/user-data

Meta Data can be accessed similarly, using a URL of the form
``http://10.1.1.1/latest/meta-data/{metadata type}``. (For backwards
compatibility, the previous URL ``http://10.1.1.1/latest/{metadata type}``
is also supported.) For metadata type, use one of the following:

-  ``service-offering``. A description of the VMs service offering

-  ``availability-zone``. The Zone name

-  ``local-ipv4``. The guest IP of the VM

-  ``local-hostname``. The hostname of the VM

-  ``public-ipv4``. The first public IP for the router. (E.g. the first IP
   of eth2)

-  ``public-hostname``. This is the same as public-ipv4

-  ``instance-id``. The instance name of the VM


Using Cloud-Init
~~~~~~~~~~~~~~~~

`Cloud-Init <https://cloudinit.readthedocs.org/en/latest>`_ can be use to access
an interpret user-data from virtual machines. Cloud-Init be installed into 
templates and also require CloudStack password and sshkey scripts (:ref:`adding-password-management-to-templates` and `using ssh keys <virtual_machines.html#using-ssh-keys-for-authentication>`_). User password management and 
``resetSSHKeyForVirtualMachine`` API are not yet supported by cloud-init.

#. Install cloud-init package into a template:

   .. code:: bash

      # yum install cloud-init
        or
      $ sudo apt-get install cloud-init

#. Create datasource configuration file: ``/etc/cloud/cloud.cfg.d/99_cloudstack.cfg``

   .. code:: yaml

      datasource:
        CloudStack: {}
        None: {}
      datasource_list:
        - CloudStack


user-data example
~~~~~~~~~~~~~~~~~

This example use cloud-init to Upgrade Operating-System of the newly created VM:

.. code:: yaml 

   #cloud-config
   
   # Upgrade the instance on first boot
   # (ie run apt-get upgrade)
   #
   # Default: false
   # Aliases: apt_upgrade
   package_upgrade: true


base64 formated:

.. code:: bash

   I2Nsb3VkLWNvbmZpZw0KDQojIFVwZ3JhZGUgdGhlIGluc3RhbmNlIG9uIGZpcnN0IGJvb3QNCiMgKGllIHJ1biBhcHQtZ2V0IHVwZ3JhZGUpDQojDQojIERlZmF1bHQ6IGZhbHNlDQojIEFsaWFzZXM6IGFwdF91cGdyYWRlDQpwYWNrYWdlX3VwZ3JhZGU6IHRydWUNCg==

Refer to `Cloud-Init CloudStack datasource <http://cloudinit.readthedocs.org/en/latest/topics/datasources.html#cloudstack>`_
documentation for latest capabilities. Cloud-Init and Cloud-Init CloudStack
datasource are not supported by Apache CloudStack community.

