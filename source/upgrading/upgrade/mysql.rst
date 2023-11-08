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

MySQL upgrade problems
======================

With certain MySQL versions (see below), issues have been seen with "cloud.nics" table's 
column type (which was not updated properly during CloudStack upgrades, due to MySQL limitations),
which eventually may lead to exception seen in the management server logs, causing Users to
not be able to start any VM.

The following SQL statement needs to be manually executed in order to fix such issue:

   .. parsed-literal::
ALTER TABLE nics MODIFY COLUMN update_time timestamp DEFAULT CURRENT_TIMESTAMP;

The issue is known to affect the following MySQL server versions:

 -  5.7.34 or later
 -  8+
