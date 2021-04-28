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

|MySQL upgrade problems|
   When upgrading newer CloudStack versions on older MySQL versions, some of the upgrade scripts may not apply fully on the database and some changes will be missing in the resulting installation. 

   Some versions of MySQL may not apply a SQL statement such as below which can be executed manually by the admin post-upgrade:
   .. parsed-literal::
ALTER TABLE nics MODIFY COLUMN update_time timestamp DEFAULT CURRENT_TIMESTAMP;

   After the upgrade of CLoudStack and while on one of those versions MySQL, an upgrade to a higher version of MySQL will lead to a broken system.
   The only remedie know is to apply those columns after the MySQL upgrade.
