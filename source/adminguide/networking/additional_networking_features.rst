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

##############################
Additional Networking Features
##############################

*******************************
KVM Libvirt Hook Script Include
*******************************

Feature Overview:
=================

-  This feature applies to KVM hosts.
-  KVM utilised under CloudStack uses the standard Libvirt hook script behaviour as outlined in the Libvirt documentation page `hooks`_.
-  During the install of the KVM CloudStack agent, the Libvirt hook script "/etc/libvirt/hooks/qemu", referred to as the qemu script hereafter is installed. 
-  This is a python script that carries out network management tasks every time a VM is started, stopped or migrated, as per the Libvirt hooks specification.
-  Custom network configuration tasks can be done at the same time as the qemu script is called.
-  Since the tasks in question are user-specific, they cannot be included in the CloudStack-provided qemu script.

-  The Libvirt documentation page `qemu`_ describes the parameters that can be passed to the qemu script, based on what actions KVM and Libvirt are carrying out on each VM: 'prepare', 'start', 'started', 'stopped', 'release', 'migrate', 'restore', 'reconnect' and 'attach'.

The KVM Libvirt Hook script allows for:
=======================================

#. The inclusion and execution of custom scripts to perform additional networking configuration tasks.
#. The included custom scripts can be bash scripts and/or python scripts.
#. Each custom script's start-up and return commands are captured and logged.
#. There are no limits to the number of custom scripts that can be included or called.

Usage:
======

-  The cloudstack-agent package will install the qemu script in the /etc/libvirt/hooks directory of Libvirt.
-  The Libvirt documentation page `arguments`_ describes the arguments that can be passed to the qemu script. 
-  The input arguments are: 

    #. Name of the object involved in the operation, or '-' if there is none. For example, the name of a guest being started.
    #. Name of the operation being performed. For example, 'start' if a guest is being started.
    #. Sub-operation indication, or '-' if there is none.
    #. An extra argument string, or '-' if there is none.

-  The operation argument is based on what actions KVM and Libvirt are carrying out on each VM: 'prepare', 'start', 'started', 'stopped', 'release', 'migrate', 'restore', 'reconnect', 'attach'.

-  If an invalid operation argument is received, the qemu script will log the fact, not execute any custom scripts and exit.

-  All input arguments that are passed to the qemu script will also be passed to each custom script. 

-  For each of the above actions, the qemu script will find and run scripts by the name "<action>_<custom script name>" in a custom include path /etc/libvirt/hooks/custom/. Custom scripts that do not follow this naming convention will be ignored and not be executed.

-  In addition to the Libvirt standard actions, the qemu script will also find and run custom scripts with an "all" prefixed to the script name. For example: "all_<custom script name>". These custom scripts will run every time the qemu script is called with a valid Libvirt action.
-  In the case of multiple custom scripts, they will be executed in sorted (alphabetical) order. The alphabetical ordering will use the file name part after the prefix and underscore have been removed from the file name. For example, if there are two custom script files in the directory: all_cde.sh, migrate_abc.py; they will be sorted and executed in this order: migrate_abc.py, all_cde.sh.
-  Custom scripts can either be bash scripts and/or python scripts.
-  Custom scripts must be executable by the underlying host operating system. Non-executable scripts will be logged and ignored.
-  Each custom script's start-up and return commands will be captured and logged.
-  During execution of a custom script, the standard out (stdout) and standard error (stderr) outputs of the custom script will be logged (appended) to /var/log/libvirt/qemu-hook.log. If the custom script needs to log anything, it can also use this file for logging purposes.
-  There is a timeout setting in the qemu script that counts down at the start of every execution of a custom script. If the custom script is still executing after the timeout time has elapsed, the custom script will be gracefully terminated.

Timeout Configuration:
======================

-  The timeout setting called "timeoutSeconds", at the top of the qemu script, has a default timeout setting of 10 minutes, expressed as 10 * 60 seconds, and can be manually modified if a different timeout is required.
-  To configure a different timeout, do the following:

    #. Navigate to the /etc/libvirt/hooks/ folder.
    #. Open the qemu script in an editor.
    #. Find the "timeoutSeconds" timeout setting.
    #. Change the 10 * 60 value to a preferred timeout value. For example 20 * 60, for a 20-minute timeout.

Custom Script Naming for a Specific VM Action:
==============================================

-  For a custom script that needs to be executed at the end of a specific VM action, do the following: 

    #. Navigate to the custom script that needs to be executed for a specific action.
    #. Rename the file by prefixing to the filename the specific action name followed by an underscore. For example, if a custom script is named abc.sh, then prefix 'migrate' and an underscore to the name to become migrate_abc.sh.


Custom Script Naming for All VM Actions:
==============================================

-  For a custom script that needs to be executed at the end of all VM actions, do the following:

    #. Navigate to the custom script that needs to be executed for all actions.
    #. Rename the file by prefixing 'all' to the filename, followed by an underscore.  For example, if a custom script is named def.py, then prefix 'all' and an underscore to the name to become all_def.py.

Custom Script Execution Configuration:
==============================================

-  Grant each custom script execute permissions so that the underlying host operating system can execute them:

    #. Navigate to the custom script that needs to be executable.
    #. Grant the custom script execute permissions.

-  Place the custom scripts in the custom include folder /etc/libvirt/hooks/custom/ so that the qemu script will be able to find and execute them:

    #. Make sure that the /etc/libvirt/hooks/custom/ folder is created and that it has the correct access permissions.
    #. Navigate to the custom scripts that need to be copied.
    #. Copy the scripts to the /etc/libvirt/hooks/custom/ folder.


-  In shell custom scripts include #!/bin/bash in the first line of the file so that the script will be executed with bash.
-  In Python custom scripts include #!/usr/bin/python in the first line of the file so that the script will be executed with python.

.. _`hooks`: https://libvirt.org/hooks.html
.. _`qemu`: https://libvirt.org/hooks.html#qemu
.. _`arguments`: https://libvirt.org/hooks.html#arguments
