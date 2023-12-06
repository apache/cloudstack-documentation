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


Host Hyper-V Installation
-------------------------

If you want to use Hyper-V hypervisor to run Guest Instances,
install Hyper-V on the hosts in your cloud. The instructions in this
section doesn't duplicate Hyper-V Installation documentation. It
provides the CloudStack-specific steps that are needed to prepare a
Hyper-V host to work with CloudStack.


System Requirements for Hyper-V Hypervisor Hosts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Supported Operating Systems for Hyper-V Hosts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  Windows Server 2012 R2 Standard

-  Windows Server 2012 R2 Datacenter

-  Hyper-V 2012 R2


Minimum System Requirements for Hyper-V Hosts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  1.4 GHz 64-bit processor with hardware-assisted virtualization.

-  800 MB of RAM

-  32 GB of disk space

-  Gigabit (10/100/1000baseT) Ethernet adapter


Supported Storage
^^^^^^^^^^^^^^^^^

-  Primary Storage: Server Message Block (SMB) Version 3, Local

-  Secondary Storage: SMB


Preparation Checklist for Hyper-V
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For a smoother installation, gather the following information before you
start:

.. cssclass:: table-striped table-bordered table-hover

+------------+----------+------------------------------------------------------+
| Hyper-V    | Value    | Description                                          |
| Requiremen |          |                                                      |
| ts         |          |                                                      |
+============+==========+======================================================+
| Server     | Hyper-V  | After the Windows Server 2012 R2 installation,       |
| Roles      |          | ensure that Hyper-V is selected from Server Roles.   |
|            |          | For more information, see `Installing                |
|            |          | Hyper-V <http://technet.microsoft.com/en-us/library/ |
|            |          | jj134187.aspx#BKMK_Step2>`__.                        |
+------------+----------+------------------------------------------------------+
| Share      | New      | Ensure that folders are created for Primary and      |
| Location   | folders  | Secondary storage. The SMB share and the hosts       |
|            | in the   | should be part of the same domain.                   |
|            | /Share   |                                                      |
|            | director | If you are using Windows SMB share, the location of  |
|            | y        | the file share for the Hyper-V deployment will be    |
|            |          | the new folder created in the \\Shares on the        |
|            |          | selected volume. You can create sub-folders for both |
|            |          | CloudStack Primary and Secondary storage within the     |
|            |          | share location. When you select the profile for the  |
|            |          | file shares, ensure that you select SMB Share        |
|            |          | -Applications. This creates the file shares with     |
|            |          | settings appropriate for Hyper-V.                    |
+------------+----------+------------------------------------------------------+
| Domain and |          | Hosts should be part of the same Active Directory    |
| Hosts      |          | domain.                                              |
+------------+----------+------------------------------------------------------+
| Hyper-V    | Full     | Full control on the SMB file share.                  |
| Users      | control  |                                                      |
+------------+----------+------------------------------------------------------+
| Virtual    |          | If you are using Hyper-V 2012 R2, manually create an |
| Switch     |          | external virtual switch before adding the host to    |
|            |          | CloudStack. If the Hyper-V host is added to the Hyper-V |
|            |          | manager, select the host, then click Virtual Switch  |
|            |          | Manager, then New Virtual Switch. In the External    |
|            |          | Network, select the desired NIC adapter and click    |
|            |          | Apply.                                               |
|            |          |                                                      |
|            |          | If you are using Windows 2012 R2, virtual switch is  |
|            |          | created automatically.                               |
+------------+----------+------------------------------------------------------+
| Virtual    |          | Take a note of the name of the virtual switch. You   |
| Switch     |          | need to specify that when configuring CloudStack        |
| Name       |          | physical network labels.                             |
+------------+----------+------------------------------------------------------+
| Hyper-V    |          | -  Add the Hyper-V domain users to the Hyper-V       |
| Domain     |          |    Administrators group.                             |
| Users      |          |                                                      |
|            |          | -  A domain user should have full control on the SMB |
|            |          |    share that is exported for primary and secondary  |
|            |          |    storage.                                          |
|            |          |                                                      |
|            |          | -  This domain user should be part of the Hyper-V    |
|            |          |    Administrators and Local Administrators group on  |
|            |          |    the Hyper-V hosts that are to be managed by       |
|            |          |    CloudStack.                                          |
|            |          |                                                      |
|            |          | -  The Hyper-V Agent service runs with the           |
|            |          |    credentials of this domain user account.          |
|            |          |                                                      |
|            |          | -  Specify the credential of the domain user while   |
|            |          |    adding a host to CloudStack so that it can manage    |
|            |          |    it.                                               |
|            |          |                                                      |
|            |          | -  Specify the credential of the domain user while   |
|            |          |    adding a shared SMB primary or secondary storage. |
|            |          |                                                      |
+------------+----------+------------------------------------------------------+
| Migration  | Migratio | Enable Migration.                                    |
|            | n        |                                                      |
+------------+----------+------------------------------------------------------+
| Migration  | Delegati | If you want to use Live Migration, enable            |
|            | on       | Delegation. Enable the following services of other   |
|            |          | hosts participating in Live Migration: CIFS and      |
|            |          | Microsoft Virtual System Migration Service.          |
+------------+----------+------------------------------------------------------+
| Migration  | Kerberos | Enable Kerberos for Live Migration.                  |
+------------+----------+------------------------------------------------------+
| Network    | Allow    | Allow access for Dial-in connections.                |
| Access     | access   |                                                      |
| Permission |          |                                                      |
| for        |          |                                                      |
| Dial-in    |          |                                                      |
+------------+----------+------------------------------------------------------+


Hyper-V Installation Steps
~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Download the operating system from `Windows Server 2012 R2
   <http://technet.microsoft.com/en-us/windowsserver/hh534429>`_.

#. Install it on the host as given in `Install and Deploy Windows Server 2012
   R2 <http://technet.microsoft.com/library/hh831620>`_.

#. Post installation, ensure that you enable Hyper-V role in the server.

#. If no Active Directory domain exists in your deployment, create one
   and add users to the domain.

#. In the Active Directory domain, ensure that all the Hyper-v hosts are
   added so that all the hosts are part of the domain.

#. Add the domain user to the following groups on the Hyper-V host:
   Hyper-V Administrators and Local Administrators.


Installing the CloudStack Agent on a Hyper-V Host
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Hyper-V Agent helps CloudStack perform operations on the Hyper-V
hosts. This Agent communicates with the Management Server and controls
all the Instances on the host. Each Hyper-V host must have the Hyper-V
Agent installed on it for successful interaction between the host and
CloudStack. The Hyper-V Agent runs as a Windows service. Install the
Agent on each host using the following steps.

CloudStack Management Server communicates with Hyper-V Agent by using
HTTPS. For secure communication between the Management Server and the
host, install a self-signed certificate on port 8250.

.. note::
   The Agent installer automatically perform this operation. You have not
   selected this option during the Agent installation, it can also be done
   manually as given in step 1.

#. Create and add a self-signed SSL certificate on port 8250:

   #. Create A self-signed SSL certificate:

      .. parsed-literal::

         # New-SelfSignedCertificate -DnsName apachecloudstack -CertStoreLocation Cert:\LocalMachine\My

      This command creates the self-signed certificate and add that to
      the certificate store ``LocalMachine\My``.

   #. Add the created certificate to port 8250 for https communication:

      .. parsed-literal::

         netsh http add sslcert ipport=0.0.0.0:8250 certhash=<thumbprint> appid="{727beb1c-6e7c-49b2-8fbd-f03dbe481b08}"

      Thumbprint is the thumbprint of the certificate you created.

#. Build the CloudStack Agent for Hyper-V as given in `Building CloudStack
   Hyper-V Agent <https://cwiki.apache.org/confluence/display/CLOUDSTACK/Creating+Hyperv+Agent+Installer>`__.

#. As an administrator, run the installer.

#. Provide the Hyper-V admin credentials when prompted.

   When the agent installation is finished, the agent runs as a service
   on the host machine.


Physical Network Configuration for Hyper-V
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You should have a plan for how the hosts will be cabled and which
physical NICs will carry what types of traffic. By default, CloudStack
will use the device that is used for the default route.

If you are using Hyper-V 2012 R2, manually create an external virtual
switch before adding the host to CloudStack. If the Hyper-V host is
added to the Hyper-V manager, select the host, then click Virtual Switch
Manager, then New Virtual Switch. In the External Network, select the
desired NIC adapter and click Apply.

If you are using Windows 2012 R2, virtual switch is created
automatically.


Storage Preparation for Hyper-V (Optional)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack allows administrators to set up shared Primary Storage and
Secondary Storage that uses SMB.

#. Create a SMB storage and expose it over SMB Version 3.

   For more information, see `Deploying Hyper-V over SMB
   <http://technet.microsoft.com/en-us/library/jj134187.aspx>`_.

   You can also create and export SMB share using Windows. After the
   Windows Server 2012 R2 installation, select File and Storage Services
   from Server Roles to create an SMB file share. For more information,
   see `Creating an SMB File Share Using Server Manager
   <http://technet.microsoft.com/en-us/library/jj134187.aspx#BKMK_Step3>`_.

#. Add the SMB share to the Active Directory domain.

   The SMB share and the hosts managed by CloudStack need to be in the
   same domain. However, the storage should be accessible from the
   Management Server with the domain user privileges.

#. While adding storage to CloudStack, ensure that the correct domain,
   and credentials are supplied. This user should be able to access the
   storage from the Management Server.
