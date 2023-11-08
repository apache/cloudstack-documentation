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


User Services
=============

In addition to the physical and logical infrastructure of your cloud and
the CloudStack software and servers, you also need a layer of User
services so that people can actually make use of the cloud. This means
not just a User UI, but a set of options and resources that Users can
choose from, such as Templates for creating Instances, disk
storage, and more. If you are running a commercial service, you will be
keeping track of what services and resources Users are consuming and
charging them for that usage. Even if you do not charge anything for
people to use your cloud – say, if the Users are strictly internal to
your organization, or just friends who are sharing your cloud – you can
still keep track of what services they use and how much of them.


Service Offerings, Disk Offerings, Network Offerings, and Templates
-------------------------------------------------------------------

A User creating a new Instance can make a variety of choices about its
characteristics and capabilities. CloudStack provides several ways to
present Users with choices when creating a new Instance:

-  Service Offerings, defined by the CloudStack administrator, provide a
   choice of CPU speed, number of CPUs, RAM size, tags on the root disk,
   and other choices. See Creating a New Compute Offering.

-  Disk Offerings, defined by the CloudStack administrator, provide a
   choice of disk size and IOPS (Quality of Service) for primary data
   storage. See Creating a New Disk Offering.

-  Network Offerings, defined by the CloudStack administrator, describe
   the feature set that is available to end Users from the virtual
   router or external networking devices on a given guest network. See
   Network Offerings.

-  Templates, defined by the CloudStack administrator or by any
   CloudStack User, are the base OS images that the User can choose from
   when creating a new Instance. For example, CloudStack includes CentOS
   as a Template. See Working with Templates.

In addition to these choices that are provided for Users, there is
another type of service offering which is available only to the
CloudStack root administrator, and is used for configuring virtual
infrastructure resources. For more information, see Upgrading a Virtual
Router with System Service Offerings.















