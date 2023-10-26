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


.. _adding-password-management-to-templates:

Adding Password Management to Your Templates
--------------------------------------------

CloudStack provides an optional password reset feature that allows users
to set a temporary admin or root password as well as reset the existing
admin or root password from the CloudStack UI.

To enable the Reset Password feature, you will need to download an
additional script to patch your Template. When you later upload the
Template into CloudStack, you can specify whether reset admin/root
password feature should be enabled for this Template.

The password management feature works always resets the account password
on Instance boot. The script does an HTTP call to the virtual router to
retrieve the account password that should be set. As long as the virtual
router is accessible the guest will have access to the account password
that should be used. When the user requests a password reset the
management server generates and sends a new password to the virtual
router for the account. Thus an Instance reboot is necessary to effect
any password changes.

If the script is unable to contact the virtual router during Instance
boot it will not set the password but boot will continue normally.


Linux OS Installation
~~~~~~~~~~~~~~~~~~~~~

Use the following steps to begin the Linux OS installation:

#. Download the latest version of the cloud-set-guest-password script from the repository:

   -  `https://github.com/apache/cloudstack/blob/main/setup/bindir/cloud-set-guest-password.in 
      <https://github.com/apache/cloudstack/blob/main/setup/bindir/cloud-set-guest-password.in>`_

#. Rename the file:

   .. code:: bash

      mv cloud-set-guest-password.in cloud-set-guest-password

#. Copy this file to /etc/init.d.

   On some Linux distributions, copy the file to ``/etc/rc.d/init.d``.

#. Run the following command to make the script executable:

   .. code:: bash

      chmod +x /etc/init.d/cloud-set-guest-password

#. Depending on the Linux distribution, continue with the appropriate
   step.

   On Fedora, CentOS/RHEL, and Debian, run:

   .. code:: bash

      chkconfig --add cloud-set-guest-password


Windows OS Installation
~~~~~~~~~~~~~~~~~~~~~~~

Download the installer, CloudInstanceManager.msi, from the `Download
page <http://sourceforge.net/projects/cloudstack/files/Password%20Management%20Scripts/CloudInstanceManager.msi/download>`_
and run the installer in the newly created Windows Instance.
