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

There are two types of host tags:

- (Explicit) host tags: the host tags are managed by CloudStack, including the flexible host tags. Cloud operator can set, update, and delete host tags via CloudStack API or GUI.
- Implicit host tags: the host tags are not managed by CloudStack API. For more information, see section `“Implicit host tags” <host_and_storage_tags.html#id1>`_.

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

.. _strict-host-tags:
Strict Host Tags
-----------------
During certain operations, such as changing the compute offering or starting or
live migrating an instance to a specific host, CloudStack may ignore the host
tags. This behavior is intentional and is designed to provide flexibility in
resource allocation. However, in some cases, this can lead to instances being
deployed on undesired hosts.

To address this, CloudStack introduces an add-on feature that allows administrators
to enforce tag checks during these operations. By specifying the required tags
in the global configuration `vm.strict.host.tags`, CloudStack will ensure that
the specified tags must match during the operations. If any of the specified
tags do not match, the operation will fail.

If `resource.limit.host.tags` are defined and
`vm.strict.resource.limit.host.tag.check` is set to true, the tags defined in
`resource.limit.host.tags` are included with the `vm.strict.host.tags`.

.. list-table:: Strict host tags related global settings
   :header-rows: 1

   * - Parameter
     - Default
     - Description
   * - ``vm.strict.host.tags``
     - empty
     - A comma-separated list of tags which must match during operations like
       modifying the compute offering for an instance, and starting or live
       migrating an instance to a specific host.
   * - ``vm.strict.resource.limit.host.tag.check``
     - `true`
     - If set to true, tags specified in `resource.limit.host.tags` are also
       included in `vm.strict.host.tags`.

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
-------------
When defining tags for a resource (a host, for example), offerings with those tags will be directed to that resource. However, offerings without tags can also be targeted to it. So, even after adding tags to a resource with the intention of making it exclusive to certain types of offerings, this exclusivity can be ignored.

Furthermore, the standard tag system only allows the user to enter a simple list of tags, without the possibility of creating more complex rules, such as checking whether the offering has certain pairs of tags.

To overcome these situations, ACS allows hosts and storages to have tags that are rules written in JavaScript, also known as flexible tags. With flexible tags, the role of tag targeting is reversed, that is, instead of the host or storage needing to have the offering's tag for targeting to be carried out, the offering will need to have the tag of the resource to which it will be directed. This inversion means that offerings without tags cannot be directed to any resource. This way, operators can have finer control over the targeting of VMs and volumes within the environment.

Configuring flexible tags on hosts is carried out through the ``updateHost`` API, entering the rule in the ``hosttags`` field. On the other hand, configuring flexible tags in the storages is done using the ``updateStoragePool`` API, informing the rule in the ``tags`` field. For the informed tag to be effectively interpreted as JavaScript, you must declare the ``istagarule`` parameter as true whenever you use one of the APIs presented.

It is worth mentioning that the compute offering or disk offering tags are injected in list format. Thus, when validating an offering with tags ``A, B``, during processing, there will be the variable ``tags``, where ``tags[0]`` will be tag A, and ``tags[1]`` will be tag B.

It's also important to mention that flexible tags are not compatible with quota's activation rules.

Implicit Host Tags
------------------
In Apache CloudStack 4.19 and prior, cloud operators are only able to set tags of host via Cloudstack API or on CloudStack GUI.

Implicit host tags feature is supported since Apache CloudStack 4.20. With the feature, Cloud operators can easily set the
implicit host tags per host based on the server configurations. For example, based on the following hardware devices and
softwares which can be fetched by commands, scripts or tools:

- CPU architecture and model
- Network card type and speed
- Hard disk type and raid type
- GPU model
- OS distribution and version

To set it, please add the following line to /etc/cloudstack/agent/agent.properties and restart cloudstack-agent.

.. parsed-literal::
   host.tags=<implicit host tags separated by comma>

Cloud operators can also get the information and set the implicit host tags by automation tools (chef, ansible, puppet, etc).

.. note::
   - Implicit host tags are only configurable on KVM hosts. They are not managed by CloudStack API.

   - Implicit host tags are not compatible with flexible host tags.

   - Flexible host tags and host tags managed by CloudStack API are explicit tags.

   - Explicit and implicit host tags have no difference in VM instance deployment and migration.
