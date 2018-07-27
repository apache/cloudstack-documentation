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

Java 8 JRE on Ubuntu
--------------------

CloudStack |version| requires installation of Java 8 JRE from an external PPA
such as openjdk-r for Ubuntu distributions where the openjdk-8 packages are not
available from the main repositories such as on Ubuntu 14.04. The PPA can be
added before installation/upgrade:

   .. parsed-literal::

      $ sudo add-apt-repository ppa:openjdk-r/ppa
      $ sudo apt-get update

Users can also choose to install Java 8 distribution from Oracle, or `Xulu-8 <http://repos.azulsystems.com/>`_ OpenJDK distribution from Azul.
