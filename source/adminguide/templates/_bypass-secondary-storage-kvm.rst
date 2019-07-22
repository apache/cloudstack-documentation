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


.. _bypass-secondary-storage-kvm:

Bypassing Secondary Storage For KVM templates
--------------------------------------------

CloudStack provides an optional way to register and use templates on KVM.

Instead of registering a template and use secondary storage as cache, it is possible to bypass secondary storage on KVM templates registration. At deployment time, the template is downloaded directly to primary storage avoiding the copy from secondary storage.

Supported protocols: HTTP/HTTPS, NFS and metalinks. The protocol is obtained from the template URL.

To enable this option for a template:

#. In the left navigation bar, click Templates.

#. Click Register Template.

#. Select KVM as hypervisor:

   |kvm-direct-download.png|

   -  **Direct Download**. It will be shown in the UI when KVM is selected as hypervisor. Choose Yes for enabling the bypassing secondary storage option.

   -  **Checksum**. Optional field. If this field is populated, the checksum is compared to the downloaded template checksum when the template is downloaded to primary storage at deployment time.

After the template is registered, it is automatically available for VM deployments.

Uploading certificates for direct downloads
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For HTTPS direct downloads, the KVM hosts on a zone should need certificates.

CloudStack provides some APIs to handle certificates for direct downloads:

- Upload a certificate to hosts in 'Up' state in a zone with id = ZONE_ID:

   .. code:: bash

         upload templatedirectdownloadcertificate hypervisor=KVM name=CERTIFICATE_ALIAS zoneid=ZONE_ID certificate=CERTIFICATE_FORMATTED

   where:
      - CERTIFICATE_FORMATTED is the string format of a X509 certificate
      - CERTIFICATE_ALIAS is the alias which will be used to import the certificate on each KVM host

   **Note:**. These certificates are imported into the /etc/cloudstack/agent/cloud.jks keystore on each KVM host.

- Revoke a certificate from every host in 'Up' state in a zone with id = ZONE_ID:
   
   .. code:: bash

         revoke templatedirectdownloadcertificate hypervisor=KVM name=CERTIFICATE_ALIAS zoneid=ZONE_ID

- It is also possible to revoke a certificate from a specific host within a zone:

   .. code:: bash

         revoke templatedirectdownloadcertificate hypervisor=KVM name=CERTIFICATE_ALIAS zoneid=ZONE_ID hostid=HOST_ID

- After a certificate is revoked from a host within a zone, it can be re-uploaded to the host:

   .. code:: bash

         upload templatedirectdownloadcertificate hypervisor=KVM name=CERTIFICATE_ALIAS zoneid=ZONE_ID certificate=CERTIFICATE_FORMATTED hostid=HOST_ID

Certificates for direct downloads synchronization task
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Certificates are uploaded to the running hosts in a zone at a certain moment. However, the number of running hosts may change and new hosts added to the zone may not include the certificate uploaded to the rest of the hosts.

CloudStack provides a way to synchronize certificates across all the running hosts on each zone. The global setting 'direct.download.certificate.background.task.interval' defines the interval in which the synchronization task will run. This task will:

- Iterate through each enabled zone
- Get the running hosts in a zone
- Check which hosts need the certificates which have been already uploaded to other hosts
- Upload missing certificates to hosts
