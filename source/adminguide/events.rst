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
   

Event Notification
==================

An event is essentially a significant or meaningful change in the state
of both virtual and physical resources associated with a cloud
environment. Events are used by monitoring systems, usage and billing
systems, or any other event-driven workflow systems to discern a pattern
and make the right business decision. In CloudStack an event could be a
state change of virtual or physical resources, an action performed by an
user (action events), or policy based events (alerts).


Event Logs
----------

There are two types of events logged in the CloudStack Event Log.
Standard events log the success or failure of an event and can be used
to identify jobs or processes that have failed. There are also long
running job events. Events for asynchronous jobs log when a job is
scheduled, when it starts, and when it completes. Other long running
synchronous jobs log when a job starts, and when it completes. Long
running synchronous and asynchronous event logs can be used to gain more
information on the status of a pending job or can be used to identify a
job that is hanging or has not started. The following sections provide
more information on these events..


Notification
------------

Event notification framework provides a means for the Management Server
components to publish and subscribe to CloudStack events. Event
notification is achieved by implementing the concept of event bus
abstraction in the Management Server.

A new event for state change, resource state change, is introduced as
part of Event notification framework. Every resource, such as user Instance,
volume, NIC, network, public IP, Snapshot, and Template, is associated
with a state machine and generates events as part of the state change.
That implies that a change in the state of a resource results in a state
change event, and the event is published in the corresponding state
machine on the event bus. All the CloudStack events (alerts, action
events, usage events) and the additional category of resource state
change events, are published on to the events bus.

Implementations
~~~~~~~~~~~~~~~
An event bus is introduced in the
Management Server that allows the CloudStack components and extension
plug-ins to subscribe to the events by using the Advanced Message
Queuing Protocol (AMQP) client. In CloudStack, a default implementation
of event bus is provided as a plug-in that uses the RabbitMQ AMQP
client. The AMQP client pushes the published events to a compatible AMQP
server. Therefore all the CloudStack events are published to an exchange
in the AMQP server.

Additionally, both an in-memory implementation and an Apache Kafka
implementation are also available.

Use Cases
~~~~~~~~~

The following are some of the use cases:

-  Usage or Billing Engines: A third-party cloud usage solution can
   implement a plug-in that can connects to CloudStack to subscribe to
   CloudStack events and generate usage data. The usage data is consumed
   by their usage software.

-  AMQP plug-in can place all the events on the a message queue, then a
   AMQP message broker can provide topic-based notification to the
   subscribers.

-  Publish and Subscribe notification service can be implemented as a
   pluggable service in CloudStack that can provide rich set of APIs for
   event notification, such as topics-based subscription and
   notification. Additionally, the pluggable service can deal with
   multi-tenancy, authentication, and authorization issues.


AMQP Configuration
~~~~~~~~~~~~~~~~~~~

As a CloudStack administrator, perform the following one-time
configuration to enable event notification framework. At run time no
changes can control the behaviour.

#. Create the folder ``/etc/cloudstack/management/META-INF/cloudstack/core``

#. Inside that folder, open ``spring-event-bus-context.xml``.

#. Define a bean named ``eventNotificationBus`` as follows:

   -  name : Specify a name for the bean.

   -  server : The name or the IP address of the RabbitMQ AMQP server.

   -  port : The port on which RabbitMQ server is running.

   -  username : The username associated with the Account to access the
      RabbitMQ server.

   -  password : The password associated with the username of the
      Account to access the RabbitMQ server.

   -  exchange : The exchange name on the RabbitMQ server where
      CloudStack events are published.

      A sample bean is given below:

      .. code:: bash

         <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
         http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
         http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
         http://www.springframework.org/schema/context
         http://www.springframework.org/schema/context/spring-context-3.0.xsd">
            <bean id="eventNotificationBus" class="org.apache.cloudstack.mom.rabbitmq.RabbitMQEventBus">
               <property name="name" value="eventNotificationBus"/>
               <property name="server" value="127.0.0.1"/>
               <property name="port" value="5672"/>
               <property name="username" value="guest"/>
               <property name="password" value="guest"/>
               <property name="exchange" value="cloudstack-events"/>
            </bean>
         </beans>

      The ``eventNotificationBus`` bean represents the
      ``org.apache.cloudstack.mom.rabbitmq.RabbitMQEventBus`` class.
      
      If you want to use encrypted values for the username and password, you have to include a bean to pass those
      as variables from a credentials file.

      A sample is given below

      .. code:: bash

         <beans xmlns="http://www.springframework.org/schema/beans"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xmlns:context="http://www.springframework.org/schema/context"
                xmlns:aop="http://www.springframework.org/schema/aop"
                xsi:schemaLocation="http://www.springframework.org/schema/beans
                 http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
                 http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
                 http://www.springframework.org/schema/context
                 http://www.springframework.org/schema/context/spring-context-3.0.xsd"
         >

            <bean id="eventNotificationBus" class="org.apache.cloudstack.mom.rabbitmq.RabbitMQEventBus">
               <property name="name" value="eventNotificationBus"/>
               <property name="server" value="127.0.0.1"/>
               <property name="port" value="5672"/>
               <property name="username" value="${username}"/>
               <property name="password" value="${password}"/>
               <property name="exchange" value="cloudstack-events"/>
            </bean>

            <bean id="environmentVariablesConfiguration" class="org.jasypt.encryption.pbe.config.EnvironmentStringPBEConfig">
               <property name="algorithm" value="PBEWithMD5AndDES" />
               <property name="passwordEnvName" value="APP_ENCRYPTION_PASSWORD" />
            </bean>

            <bean id="configurationEncryptor" class="org.jasypt.encryption.pbe.StandardPBEStringEncryptor">
               <property name="config" ref="environmentVariablesConfiguration" />
            </bean>

            <bean id="propertyConfigurer" class="org.jasypt.spring3.properties.EncryptablePropertyPlaceholderConfigurer">
               <constructor-arg ref="configurationEncryptor" />
               <property name="location" value="classpath:/cred.properties" />
            </bean>
         </beans>


      Create a new file in the same folder called ``cred.properties`` and the specify the values for username and password as jascrypt encrypted strings

      Sample, with ``guest`` as values for both fields:

      .. code:: bash

         username=nh2XrM7jWHMG4VQK18iiBQ==
         password=nh2XrM7jWHMG4VQK18iiBQ==


#. Restart the Management Server.

Kafka Configuration
~~~~~~~~~~~~~~~~~~~

As a CloudStack administrator, perform the following one-time
configuration to enable event notification framework. At run time no
changes can control the behaviour.

#. Create an appropriate configuration file in ``/etc/cloudstack/management/kafka.producer.properties``
   which contains valid kafka configuration properties as documented in http://kafka.apache.org/documentation.html#newproducerconfigs
   The properties may contain an additional ``topic`` property which if not provided will default to ``cloudstack``.
   While ``key.serializer`` and ``value.serializer`` are usually required for a producer to correctly start, they may be omitted and
   will default to ``org.apache.kafka.common.serialization.StringSerializer``.

#. Create the folder ``/etc/cloudstack/management/META-INF/cloudstack/core``

#. Inside that folder, open ``spring-event-bus-context.xml``.

#. Define a bean named ``eventNotificationBus`` with a single ``name`` attribute, A sample bean is given below:

   .. code:: xml

       <beans xmlns="http://www.springframework.org/schema/beans"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xmlns:context="http://www.springframework.org/schema/context"
              xmlns:aop="http://www.springframework.org/schema/aop"
              xsi:schemaLocation="http://www.springframework.org/schema/beans
                                  http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
                                  http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
                                  http://www.springframework.org/schema/context
                                  http://www.springframework.org/schema/context/spring-context-3.0.xsd">
          <bean id="eventNotificationBus" class="org.apache.cloudstack.mom.kafka.KafkaEventBus">
            <property name="name" value="eventNotificationBus"/>
          </bean>
        </beans>

#. Restart the Management Server.


Standard Events
---------------

The events log records three types of standard events.

-  INFO. This event is generated when an operation has been successfully
   performed.

-  WARN. This event is generated in the following circumstances.

   -  When a network is disconnected while monitoring a Template
      download.

   -  When a Template download is abandoned.

   -  When an issue on the storage server causes the volumes to fail
      over to the mirror storage server.

-  ERROR. This event is generated when an operation has not been
   successfully performed


Long Running Job Events
-----------------------

The events log records three types of standard events.

-  INFO. This event is generated when an operation has been successfully
   performed.

-  WARN. This event is generated in the following circumstances.

   -  When a network is disconnected while monitoring a Template
      download.

   -  When a Template download is abandoned.

   -  When an issue on the storage server causes the volumes to fail
      over to the mirror storage server.

-  ERROR. This event is generated when an operation has not been
   successfully performed


Event Log Queries
-----------------

Database logs can be queried from the user interface. The list of events
captured by the system includes:

-  Instance creation, deletion, and on-going management
   operations

-  Virtual router creation, deletion, and on-going management operations

-  Template creation and deletion

-  Network/load balancer rules creation and deletion

-  Storage volume creation and deletion

-  User login and logout


Deleting and Archiving Events and Alerts
----------------------------------------

CloudStack provides you the ability to delete or archive the existing
alerts and events that you no longer want to implement. You can
regularly delete or archive any alerts or events that you cannot, or do
not want to resolve from the database.

You can delete or archive individual alerts or events either directly by
using the Quickview or by using the Details page. If you want to delete
multiple alerts or events at the same time, you can use the respective
context menu. You can delete alerts or events by category for a time
period. For example, you can select categories such as **USER.LOGOUT**,
**VM.DESTROY**, **VM.AG.UPDATE**, **CONFIGURATION.VALUE.EDI**, and so
on. You can also view the number of events or alerts archived or
deleted.

In order to support the delete or archive alerts, the following global
parameters have been added:

-  **alert.purge.delay**: The alerts older than specified number of days
   are purged. Set the value to 0 to never purge alerts automatically.

-  **alert.purge.interval**: The interval in seconds to wait before
   running the alert purge thread. The default is 86400 seconds (one
   day).

.. note:: 
   Archived alerts or events cannot be viewed in the UI or by using the
   API. They are maintained in the database for auditing or compliance
   purposes.


Permissions
~~~~~~~~~~~

Consider the following:

-  The root admin can delete or archive one or multiple alerts or
   events.

-  The domain admin or end user can delete or archive one or multiple
   events.


Procedure
~~~~~~~~~

#. Log in as administrator to the CloudStack UI.

#. In the left navigation, click Events.

#. Perform either of the following:

   -  To archive events, click Archive Events, and specify event type
      and date.

   -  To archive events, click Delete Events, and specify event type and
      date.

#. Click OK.


Webhooks
--------

.. include:: events/webhooks.rst
