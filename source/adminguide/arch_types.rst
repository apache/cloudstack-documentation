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


Hosts/Cluster Arch Types Allocation
===================================

Since CloudStack 4.20.0, it is possible to add AMD 64 bits and ARM 64 bits clusters (and hosts). A single zone can contain clusters (and hosts) of different arch types (multi-arch zones). 

When a multi-arch zone is selected for VM deployment, CloudStack allows the users to filter the templates/ISOs by their arch type.

|deploy-vm-arch-types.png|

Once a template/ISO is selected, only the clusters (and hosts) matching the arch type will be considered for the VM allocation

.. |deploy-vm-arch-types.png| image:: /_static/images/deploy-vm-arch-types.png
   :alt: Filtering templates and ISOs by arch types

