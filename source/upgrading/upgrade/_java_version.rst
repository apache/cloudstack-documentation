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

.. sub-section included in upgrade notes.

Java Version Requirement
------------------------

CloudStack |version| requires installation of Java 17 JRE for management server
and the KVM agent. On installing or upgrading cloudstack-management and/or
cloudstack-agent packages, please configure Java 17 as the default java
version using:

   .. parsed-literal::

      $ sudo alternatives --config java

Note: For Ubuntu distributions where the openjdk-17 packages are not available
from the main repositories, the JRE can be installed from an external PPA such
as openjdk-r. The PPA can be added before installation/upgrade:

   .. parsed-literal::

      $ sudo add-apt-repository ppa:openjdk-r/ppa
      $ sudo apt-get update

