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

Guest OS mappings
--------------------------

New CloudStack release usually brings new Guest OS mappings, so it is
important to remove any Guest OS mappings that were manually added 
by the cloud operator, in order to ensure a successful upgrade.
If needed, those custom Guest OS mappings can be added after the upgrade.
That means that any custom added rows in the *guest_os*, *guest_os_hypervisor*, 
*guest_os_details* and *guest_os_category*, should be removed prior to the upgrade,
and added later if needed.

.. note::
      Manually added guest OS mappings will usually break the upgrade process.
