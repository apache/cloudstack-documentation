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


Host and Storage Tags
======================

Host tags and storage tags, despite the name, are not related to resource tags ( see section :ref:`resource-tags` ); they are a feature to direct resource allocation, such as which host the VM will be deployed on or which storage the volume will be created on. There are several reasons for using tags (such as directing the volume to better quality storage, according to the offering).
    
Host tags
---------
Host tags are responsible for directing VMs to compatible hosts. They are validated with the host tags informed in the compute offerings or in the system offerings.

To explain the behavior of host tags, some examples will be demonstrated with two hosts (Host1 and Host2):

#. Tag setup:
    * Host1: h1
    * Host2: h2
    * Offering: h1
    When a VM is created with the offering, the deployment will be carried out on Host1, as it is the one that has the tag compatible with the offering.

#. Tag setup:
    * Host1: h1
    * Host2: h2,h3
    * Offering: h3
    Hosts and offerings accept a list of tags, with comma (,) being their separator. So in this example, Host2 has the h2 and h3 tags. When a VM is created with the offering, the deployment will be carried out on Host2, as it is the one that has the tag compatible with the offering.

#. Tag setup:
    * Host1: h1
    * Host2: h2,h3
    * Offering: (no tag)
    When the offering does not have tags, it will be possible to deploy the VM on any host.

#. Tag setup:
    * Host1: (no tag)
    * Host2: h2
    * Offering: h3
    None of the hosts have compatible tags and it will not be possible to deploy a VM with the offering. However, CloudStack ignores this behavior when a host is manually selected.

Storage tags
------------
Storage tags are responsible for directing volumes to compatible primary storage. They are validated with the storage tags entered in the disk offerings or system offerings.

To explain the behavior of storage tags, some examples will be demonstrated:

#. Tag setup:
    * Storage: A
    * Offering: A,B
    Storage and offering accept a list of tags, with the comma (,) being their separator. Therefore, in this example, the offering has tags A and B. In this example, it will not be possible to allocate the volume, as all the offering tags must exist in the storage. Although the storage has the A tag, it does not have the B tag.

#. Tag setup:
    * Storage: A,B,C,D,X
    * Offering: A,B,C
    In this example, it will be possible to allocate the volume, as all the offering tags exist in the storage.

#. Tag setup:
    * Storage: A, B, C
    * Offering: (no tag)
    In this example, it will be possible to allocate the volume, as the offering does not have any tag requirements.

#. Tag setup:
    * Storage: (no tag)
    * Offering: D,E
    In this example, it will not be possible to allocate the volume, as the storage does not have tags, therefore it does not meet the offering requirements.

In short, if the offering has tags, the storage will need to have all the tags for the volume to be allocated. If the offering does not have tags, the volume can be allocated, regardless of whether the storage has a tag or not.

Flexible Tags
--------------
When defining tags for a resource (a host, for example), offerings with those tags will be directed to that resource. However, offerings without tags can also be targeted to it. So, even after adding tags to a resource with the intention of making it exclusive to certain types of offerings, this exclusivity can be ignored.

Furthermore, the standard tag system only allows the user to enter a simple list of tags, without the possibility of creating more complex rules, such as checking whether the offering has certain pairs of tags.

To overcome these situations, ACS allows hosts and storages to have tags that are rules written in JavaScript, also known as flexible tags. With flexible tags, the role of tag targeting is reversed, that is, instead of the host or storage needing to have the offering's tag for targeting to be carried out, the offering will need to have the tag of the resource to which it will be directed. This inversion means that offerings without tags cannot be directed to any resource. This way, operators can have finer control over the targeting of VMs and volumes within the environment.

Configuring flexible tags on hosts is carried out through the ``updateHost`` API, entering the rule in the ``hosttags`` field. On the other hand, configuring flexible tags in the storages is done using the ``updateStoragePool`` API, informing the rule in the ``tags`` field. For the informed tag to be effectively interpreted as JavaScript, you must declare the ``istagarule`` parameter as true whenever you use one of the APIs presented.

It is worth mentioning that the compute offering or disk offering tags are injected in list format. Thus, when validating an offering with tags ``A, B``, during processing, there will be the variable ``tags``, where ``tags[0]`` will be tag A, and ``tags[1]`` will be tag B.

It's also important to mention that flexible tags are not compatible with quota's activation rules.
