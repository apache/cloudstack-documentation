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

Custom Hypervisor Installation
------------------------------

CloudStack allows adapting a new hypervisor plugin that may be developed privately.

The new hypervisor type is internally named Custom to the CloudStack services.


The setting ‘hypervisor.custom.display.name’ allows administrators to set the display name of the hypervisor type.
The display name will be shown in the CloudStack UI and API.

    - In case the ‘hypervisor.list’ setting contains the display name of the new hypervisor type, the setting value is automatically updated after the ‘hypervisor.custom.display.name’ setting is updated.


The custom hypervisor type supports:

    - Direct downloads (the ability to download templates into primary storage from the hypervisor hosts without using secondary storage)
    - Local storage (use hypervisor hosts local storage as primary storage)
    - Template format: RAW format (the templates to be registered on the new hypervisor type must be in RAW format)

The UI is also extended to display the new hypervisor type and the supported features listed above.
