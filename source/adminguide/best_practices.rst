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
   

Best Practices
==============

This section provides the best practices to follow for your cloud.

The following are some of the best practices:

-  Configure 'api.allowed.source.cidr.list' at cloud level or an account
   level to limit source IPs where the API requests are allowed from.
   
-  Setup fail2ban or similar tools to avoid any brute-force attempts
   for any operations.
