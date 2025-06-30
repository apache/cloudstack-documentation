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
   

Custom Actions
--------------

In addition to standard instance operations, extensions support custom actions. These can be configured via UI in the extension details view or the addCustomAction API. The extension binary or script must implement handlers for these action names and process any provided parameters.

   |add-custom-action.png|

Description, allowed role types, parameters, success/error messages, configuration details, timeout can be defined during creation or update.
Alowed role types can be one or more of Admin, Resource Admin, Domain Admin, User.
Success and error messages will be used and returned during action execution. They allow string expansion and the following can be used to customise messages:

   - {{actionName}} for showing name of the action
   - {{extensionName}} for showing name of the extension
   - {{resourceName}} for showing name of the resource

An example usage can be - "Successfully completed {{actionName}} for {{resourceName}} using {{extensionName}}".
Configuration details can be key-value pairs which will be passed to the extension during action execution.
Timeout value can be configured to adjust wait time for action completion.

A single parameter can have the following details:

   - **name**: Name of the parameter.

   - **type**: Type of the parameter. It can be one of the following: BOOLEAN, DATE, NUMBER, STRING

   - **validationformat**: Validation format for the parameter value. Supported only for NUMBER and STRING type. For NUMBER, it can be NONE or DECIMAL. For STRING, it can be NONE, EMAIL, PASSWORD, URL, UUID.

   - **valueoptions**: Options for the value of the parameter. This is allowed only for NUMBER and STRING type.


Running Custom Action
^^^^^^^^^^^^^^^^^^^^^

All enabled custom actions can then be triggered for a resource of the type the action is defined for or provided while running, using the **Run Action** view or runCustomAction API.

   |run-custom-action.png|


.. Images


.. |add-custom-action.png| image:: /_static/images/add-custom-action.png
.. |run-custom-action.png| image:: /_static/images/run-custom-action.png
.. |run-custom-action-instance.png| image:: /_static/images/run-custom-action-instance.png
