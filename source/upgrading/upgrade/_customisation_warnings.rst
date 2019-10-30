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

CloudStack Customisations
--------------------------

There are a number of ways in which administrators can customise CloudStack.  During an
upgrade, a number of these could be overridden.  Therefore steps should be taken to ensure
that they can be restored after the upgrade is completed.


Guest OS mappings
##################

A new CloudStack release often brings compatibility with new hypervisors, and therefore 
new Guest OS mappings. An API is provided to manually add guest OSes and the
relevant hypervisor mappings, however, there is a high probability that manually 
added guest OSes and/or mappings would conflict with guest OSes and/or mappings
added as part of a version upgrade.

It is therefore essential to remove any Guest OS mappings that were manually added 
in order to ensure a successful upgrade.  If need be, any custom Guest OS mappings 
still 'missing' after an upgrade can be re-added after the upgrade.
That means that any custom added rows in the *guest_os*, *guest_os_hypervisor*, 
*guest_os_details* and *guest_os_category* database tables, should be removed 
prior to the upgrade, and added later if needed.

.. warning::
      Manually added guest OS mappings can cause the upgrade process to fail.


Customised CSS
###############

If you have altered the CSS files in order to customise the appearance of the CloudStack UI,
you should make a backup copy as the installed CSS files are likely to be overwritten during
any upgrade.

You should inspect a 'diff' of your customised css files and the new versions, and then
reapply your changes to the new files as the new versions may contain changes to better display existing
elements or have new entries to support new UI elements.

Plugins
#######

If you have 3rd party plugins installed, you should backup your plugins directories and the
plugins.js file.  While the plugins directories *should* remain untouched, the plugins.js
file is likely to be overwritten.

3rd Party Integrations
#######################

CloudStack is put through extensive regression testing during a release cycle, however 
the numerous 3rd party integrations which are available cannot all be tested by the 
community nor indeed may the community know about many of them. Therefore it is essential
that you verify that your integrations will continue to work after an upgrade through thorough
testing and checking with the vendor/supplier of your integrations.

