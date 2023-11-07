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

.. _about-password-key-encryption:

About Password and Key Encryption
---------------------------------

CloudStack stores several sensitive passwords and secret keys that are
used to provide security. These values are always automatically
encrypted:

-  Database secret key

-  Database password

-  SSH keys

-  Compute node root password

-  VPN password

-  User API secret key

-  VNC password

CloudStack uses the Java Simplified Encryption (JASYPT) library. The
data values are encrypted and decrypted using a database secret key,
which is stored in one of CloudStack’s internal properties files along
with the database password. The other encrypted values listed above,
such as SSH keys, are in the CloudStack internal database.

Of course, the database secret key itself can not be stored in the open
– it must be encrypted. How then does CloudStack read it? A second
secret key must be provided from an external source during Management
Server startup. This key can be provided in one of two ways: loaded from
a file or provided by the CloudStack administrator. The CloudStack
database has a configuration setting that lets it know which of these
methods will be used. If the encryption type is set to "file," the key
must be in a file in a known location. If the encryption type is set to
"web," the administrator runs the utility
com.cloud.utils.crypt.EncryptionSecretKeySender, which relays the key to
the Management Server over a known port.

The encryption type, database secret key, and Management Server secret
key are set during CloudStack installation. They are all parameters to
the CloudStack database setup script (cloudstack-setup-databases). The
default values are file, password, and password. It is, of course,
highly recommended that you change these to more secure keys.


Changing the Default Password Encryption
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Passwords are encoded when creating or updating Users. CloudStack allows
you to determine the default encoding and authentication mechanism for
admin and User logins. Two new configurable lists have been
introduced—userPasswordEncoders and userAuthenticators.
userPasswordEncoders allows you to configure the order of preference for
encoding passwords, whereas userAuthenticators allows you to configure
the order in which authentication schemes are invoked to validate User
passwords.

Additionally, the plain text User authenticator has been modified not to
convert supplied passwords to their md5 sums before checking them with
the database entries. It performs a simple string comparison between
retrieved and supplied login passwords instead of comparing the
retrieved md5 hash of the stored password against the supplied md5 hash
of the password because clients no longer hash the password. The
following method determines what encoding scheme is used to encode the
password supplied during User creation or modification.

When a new User is created, the User password is encoded by using the
first valid encoder loaded as per the sequence specified in the
``UserPasswordEncoders`` property in the ``ComponentContext.xml`` or
``nonossComponentContext.xml`` files. The order of authentication
schemes is determined by the ``UserAuthenticators`` property in the same
files. If Non-OSS components, such as VMware environments, are to be
deployed, modify the ``UserPasswordEncoders`` and ``UserAuthenticators``
lists in the ``nonossComponentContext.xml`` file, for OSS environments,
such as XenServer or KVM, modify the ``ComponentContext.xml`` file. It
is recommended to make uniform changes across both the files. When a new
authenticator or encoder is added, you can add them to this list. While
doing so, ensure that the new authenticator or encoder is specified as a
bean in both these files. The administrator can change the ordering of
both these properties as preferred to change the order of schemes.
Modify the following list properties available in
``client/tomcatconf/nonossComponentContext.xml.in`` or
``client/tomcatconf/componentContext.xml.in`` as applicable, to the
desired order:

.. sourcecode:: xml

   <property name="UserAuthenticators">
      <list>
         <ref bean="SHA256SaltedUserAuthenticator"/>
         <ref bean="MD5UserAuthenticator"/>
         <ref bean="LDAPUserAuthenticator"/>
         <ref bean="PlainTextUserAuthenticator"/>
      </list>
   </property>
   <property name="UserPasswordEncoders">
      <list>
         <ref bean="SHA256SaltedUserAuthenticator"/>
         <ref bean="MD5UserAuthenticator"/>
         <ref bean="LDAPUserAuthenticator"/>
         <ref bean="PlainTextUserAuthenticator"/>
      </list>
   </property>

In the above default ordering, SHA256Salt is used first for
``UserPasswordEncoders``. If the module is found and encoding returns a
valid value, the encoded password is stored in the User table's password
column. If it fails for any reason, the MD5UserAuthenticator will be
tried next, and the order continues. For ``UserAuthenticators``,
SHA256Salt authentication is tried first. If it succeeds, the User is
logged into the Management server. If it fails, md5 is tried next, and
attempts continues until any of them succeeds and the User logs in . If
none of them works, the User is returned an invalid credential message.

