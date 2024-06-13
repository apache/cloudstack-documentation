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


Webhooks allow external services to be notified when certain events happen.
CloudStack allows provisioning webhooks for all account roles and for various
scopes.
This allows users to consume event notifications without any external services
such as an event streaming platforms.

Webhooks can be managed using both API and UI. CloudStack provides following
APIs for webhhoks:

   .. cssclass:: table-striped table-bordered table-hover

   ====================== ===========================
   API                    Description
   ====================== ===========================
   createWebhook          Creates a Webhook
   listWebhooks           Lists Webhooks
   updateWebhook          Updates a Webhook
   deleteWebhook          Deletes a Webhook
   listWebhookDeliveries  Lists Webhook deliveries
   deleteWebhookDelivery  Deletes Webhook delivery(s)
   executeWebhookDelivery Executes a Webhook delivery
   ====================== ===========================

In the UI, webhooks can be managed under *Tools > Webhhooks* menu.

   |webhooks.png|


Creating a webhook
~~~~~~~~~~~~~~~~~~

Any CloudStack user having createWebhook API access can create a new webhook
for the event notifications.

To create a webhook:

#. Log in to the CloudStack UI.

#. In the left navigation bar, click Tools and choose Webhooks.

#. Click Create Webhook.

#. In the dialog, make the following choices:

   -  **Name**. Any desired name for the webhook.

   -  **Description**. A short description of the webhook.

   -  **Scope**. (Available only for ROOT admins or domain admins). Scope
      of the webhook. The value can be Local, Domain or Global.
      Local - only events associated with the owner account will be notified.
      Domain - events associated with domain will be notified.
      Global - all events will be notified. This is available only for ROOT
      admin account.
      For a normal user account, webhooks can be created with Local scope
      only.

   -  **Domain**. An optional domain for the Webhook. If the account parameter
      is used, domain must also be used.

   -  **Account**. An optional account for the webhook. Must be used with
      domain.

   -  **Payload URL**. The payload URL of the Webhook. All events for the
      webhook will posted on this URL.

   -  **SSL Verification**. An otional parameter to specify whether the HTTP
      POST requests for event notications must be sent with strict SSL
      verification request when a HTTPS payload URL is used.

   -  **Secret Key**. An option secret key parameter which can be used to sign
      the HTTP POST requests for event notifications with HMAC.

   -  **Enabled**. To specify whether the webhook be created with enabled or
      disabled state

   |create-webhook.png|


Working with webhook deliveries
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CloudStack attempts webhook deliveries using a thread pool with given retries.
The following global configuration can be used to configure thread pool size
for deliveries:

   - **webhook.delivery.thread.pool.size**: Size of the thread pool for webhook
     deliveries.


Also, the number attempts for a particular event notification and the timeout
for one particular attempt can be configured using the following domain-level
configurations:

   - **webhook.delivery.retries**: Number of tries to be made for a webhook
     delivery.

   - **webhook.delivery.timeout**: Wait timeout (in seconds) for a webhook
     delivery attempt.

.. note::
   The onus of dealing with the duplicate event deliveries lies with the payload
   server or application. During delivery, when the server doesn't respond in a
   timely manner or returns a failure CloudStack will re-attempt the delivery of
   the event, based on the above global settings, irrespective of the fact whether
   the server already received the event in any previous attempts.


CloudStack allows retrieving recent deliveries for a webhook with details such
as event, headers, payload, respose, success, duration, etc.
In the UI, these can be accessed under Recent deliveries tab in the Webhook
detail view.
The user can redeliver an existing delivery. To check the working of the
webhook consumer test deliveries can made. Test deliveries are not recorded
by CloudStack.

   |webhook-deliveries.png|

The administrator can configure storage of webhook deliveries using the
following global configurations:

   - **webhook.deliveries.limit**: Limit for number of deliveries to keep
     in DB per webhook. Default value is 10.

   - **webhook.deliveries.cleanup.interval**: Interval (in seconds) for
     cleaning up webhook deliveries. Default value is 3600 or 1 hour.

   - **webhook.deliveries.cleanup.initial.delay**:  Initial delay (in seconds)
     for webhook deliveries cleanup task. Default value is 180.

Based on the above configurations CloudStack will purge older deliveries in
the database using a repeatedly running task.

For a webhook delivery, CloudStack sends a HTTP POST request with event data
as the payload. The following custom headers are sent with the request:

   -  **X-CS-Event-ID**. Event ID for which the webhook delivery is made.

   -  **X-CS-Event**. Event for for which the webhook delivery is made.

   -  **User-Agent**. In the format - *CS-Hookshot/<ACCOUNT_ID>*. Here
      ACCOUNT_ID is the ID of the account which trigerred the event.

   -  **X-CS-Signature**. HMAC SHA256 signature created using the webhook
      secret key and the delivery payload. It is sent only when secret key
      is specified for the webhook.


Working with HTTPS webhook payload URL with self-signed certificate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Generate a self signed certificate for the server, make sure to mention the IP address of the server when it prompts.

   .. parsed-literal::

      openssl req -x509 -newkey rsa:4096 -nodes -out cert.pem -keyout key.pem -days 365

#. Copy the genereated cert.pem to the management server(s).

#. Import the certificate for JDK on the management server(s)

   .. parsed-literal::

      cp /etc/java/java-17-openjdk/java-17-openjdk-17.0.10.0.7-2.0.1.el8.x86_64/lib/security/cacerts /etc/java/java-17-openjdk/java-17-openjdk-17.0.10.0.7-2.0.1.el8.x86_64/lib/security/jssecacerts

      keytool -importcert -file /root/kiran/cert.pem -alias webhook -keystore /etc/java/java-17-openjdk/java-17-openjdk-17.0.10.0.7-2.0.1.el8.x86_64/lib/security/jssecacerts -storepass changeit

4. Test the webhook.



.. Images


.. |webhooks.png| image:: /_static/images/webhooks.png
.. |create-webhook.png| image:: /_static/images/create-webhook.png
.. |webhook-deliveries.png| image:: /_static/images/webhook-deliveries.png






