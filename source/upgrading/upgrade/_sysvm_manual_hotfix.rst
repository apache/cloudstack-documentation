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

.. sub-section optionally included in upgrade notes.

.. Add following to file when including this manual hotfix
   .. _manual_hofix:

   Manual hotfix for systemvm upgrade
   ----------------------------------
   
   .. include:: _sysvm_restart.rst
.. End of include example

Some manual steps are required to upgrade of SystemVMs and Virtual Routers.

Following MySQL commands will update the Template ID used by Console Proxy VMs (CPVM)
and Secondary Storage VMs (SSVM). It will also change the default Template for
Virtual Router to *systemvm-<hypervisor>-4.4* Templates.


XenServer System VMs
^^^^^^^^^^^^^^^^^^^^

   Execute following MySQL queries in MySQL. 
   Please note ``<ID FROM COMMAND #1>`` from the first command

   #. Connect to the database:

      .. code-block:: bash

         mysql -h localhost -u root -p cloud

   #. Get the id of the new Template:

      .. code-block:: mysql

         select id,name from vm_template where name = 'systemvm-xenserver-4.4';

   #. Replace ``<ID FROM COMMAND #1>`` by the id from the previous command and execute following:

      .. code-block:: mysql
 
         update vm_template set type='SYSTEM' where id='<ID FROM COMMAND #1>';
         update vm_instance set vm_template_id = '<ID FROM COMMAND #1>' where type='ConsoleProxy' and hypervisor_type = 'xenserver';
         update vm_instance set vm_template_id = '<ID FROM COMMAND #1>' where type='SecondaryStorageVm' and hypervisor_type = 'xenserver';
         update configuration set value = 'systemvm-xenserver-4.4' where name = 'router.template.xen';


KVM SystemVMs
^^^^^^^^^^^^^

   Execute following MySQL queries in MySQL. 
   Please note ``<ID FROM COMMAND #1>`` from the first command

   #. Connect to the database:

      .. code-block:: bash

         mysql -h localhost -u root -p cloud

   #. Get the id of the new Template:

      .. code-block:: mysql   

         select id,name from vm_template where name = 'systemvm-kvm-4.4';

   #. Replace ``<ID FROM COMMAND #1>`` by the id from the previous command and execute following:

      .. code-block:: mysql

         update vm_template set type='SYSTEM' where id='<ID FROM COMMAND #1>';
         update vm_instance set vm_template_id = '<ID FROM COMMAND #1>' where type='ConsoleProxy' and hypervisor_type = 'KVM';
         update vm_instance set vm_template_id = '<ID FROM COMMAND #1>' where type='SecondaryStorageVm' and hypervisor_type = 'KVM';
         update configuration set value = 'systemvm-kvm-4.4' where name = 'router.template.kvm';


VMware SystemVMs
^^^^^^^^^^^^^^^^

   Execute following MySQL queries in MySQL. 
   Please note ``<ID FROM COMMAND #1>`` from the first command

   #. Connect to the database:

      .. code-block:: bash

         mysql -h localhost -u root -p cloud

   #. Get the id of the new Template:

      .. code-block:: mysql   

         select id,name from vm_template where name = 'systemvm-vmware-4.4';

   #. Replace ``<ID FROM COMMAND #1>`` by the id from the previous command and execute following:

      .. code-block:: mysql

         update vm_template set type='SYSTEM' where id='<ID FROM COMMAND #1>';
         update vm_instance set vm_template_id = '<ID FROM COMMAND #1>' where type='ConsoleProxy' and hypervisor_type = 'vmware';
         update vm_instance set vm_template_id = '<ID FROM COMMAND #1>' where type='SecondaryStorageVm' and hypervisor_type = 'vmware';
         update configuration set value = 'systemvm-vmware-4.4' where name = 'router.template.vmware';
