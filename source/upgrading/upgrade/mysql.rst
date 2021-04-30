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

Users who may upgrade their MySQL server after upgrading to Apache
CloudStack 4.15 or later, may need to run the following SQL query to
fix an issue with "cloud.nics" table's column type which may lead to
exception seen in the management server logs. Users who have already
upgraded their MySQL server prior to upgrading to Apache CloudStack
4.15 may not need this as this query runs as part of the 4.14.x to
4.15.0.0 database upgrade path.

.. note::
   The issue has not been seen in cases where the database was upgraded while on CloudStack version 4.14.

   .. parsed-literal::
ALTER TABLE nics MODIFY COLUMN update_time timestamp DEFAULT CURRENT_TIMESTAMP;

The issue is known to affect the following MySQL server versions:

 -  5.7.34 or later
 -  8+
