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


Deploying CloudStack with Ansible
=================================

What is Ansible
---------------

Ansible is a deployment and configuration management tool similar in
intent to Chef and Puppet. It allows (usually) DevOps teams to
orchestrate the deployment and configuration of their environments
without having to re-write custom scripts to make changes.

Like Chef and Puppet, Ansible is designed to be idempotent. This means
that you determine the state you want a host to be in and Ansible will
decide if it needs to act in order to achieve that state.


There’s already Chef and Puppet, so what’s the fuss about Ansible?
------------------------------------------------------------------

Let’s take it as a given that configuration management makes life much
easier (and is quite cool), Ansible only needs an SSH connection to the
hosts that you’re going to manage to get started. While Ansible requires
Python 2.4 or greater on the host you’re going to manage in order to
leverage the vast majority of its functionality, it is able to connect
to hosts which don’t have Python installed in order to then install
Python, so it’s not really a problem. This greatly simplifies the
deployment procedure for hosts, avoiding the need to pre-install agents
onto the clients before the configuration management can take over.

Ansible will allow you to connect as any user to a managed host (with
that user’s privileges) or by using public/private keys – allowing fully
automated management.

There also doesn’t need to be a central server to run everything, as
long as your playbooks and inventories are in-sync you can create as
many Ansible servers as you need (generally a bit of Git pushing and
pulling will do the trick).

Finally – its structure and language is pretty simple and clean. I’ve
found it a bit tricky to get the syntax correct for variables in some
circumstances, but otherwise I’ve found it one of the easier tools to
get my head around.


So let’s see something
----------------------

For this example we’re going to create an Ansible server which will then
deploy a CloudStack server. Both of these servers will be CentOS 6.4
Instances.


Installing Ansible
------------------

Installing Ansible is blessedly easy. We generally prefer to use CentOS
so to install Ansible you run the following commands on the Ansible
server.

::
 
   # rpm -ivh http://www.mirrorservice.org/sites/dl.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
   # yum install -y ansible

And that’s it.

*(There is a commercial version which has more features such as callback
to request configurations and a RESTful API and also support. The
installation of this is different)*

By default Ansible uses /etc/ansible to store your playbooks, I tend to
move it, but there’s no real problem with using the default location.
Create yourself a little directory structure to get started with. The
documentation recommends something like this:


Playbooks
---------

Ansible uses playbooks to specify the state in which you wish the target
host to be in to be able to accomplish its role. Ansible playbooks are
written in YAML format.


Modules
-------

To get Ansible to do things you specify the hosts a playbook will act
upon and then call modules and supply arguments which determine what
Ansible will do to those hosts.

To keep things simple, this example is a cut-down version of a full
deployment. This example creates a single management server with a local
MySQL server and assumes you have your secondary storage already
provisioned somewhere. For this example I’m also not going to include
securing the MySQL server, configuring NTP or using Ansible to configure
the networking on the hosts either. Although normally we’d use Ansible
to do exactly that.

The pre-requisites to this CloudStack build are:

-  A CentOS 6.4 host to install CloudStack on

-  An IP address already assigned on the ACS management host

-  The ACS management host should have a resolvable FQDN (either through
   DNS or the host file on the ACS management host)

-  Internet connectivity on the ACS management host


Planning
--------

The first step I use is to list all of the tasks I think I’ll need and
group them or split them into logical blocks. So for this deployment of
CloudStack I’d start with:

-  Configure selinux

-  (libselinux-python required for Ansible to work with selinux enabled
   hosts)

-  Install and configure MySQL

-  (Python MySQL-DB required for Ansible MySQL module)

-  Install cloud-client

-  Seed secondary storage

Ansible is built around the idea of hosts having roles, so generally you
would group or manage your hosts by their roles. So now to create some
roles for these tasks

I’ve created:

-  cloudstack-manager

-  mysql

First up we need to tell Ansible where to find our CloudStack management
host. In the root Ansible directory there is a file called ‘hosts’
(/etc/Ansible/hosts) add a section like this:

::

   [acs-manager]
   xxx.xxx.xxx.xxx

where xxx.xxx.xxx.xxx is the ip address of your ACS management host.


MySQL
-----

So let’s start with the MySQL server.  We’ll need to create a task
within the mysql role directory called main.yml. The ‘task’ in this case
to have MySQL running and configured on the target host. The contents of
the file will look like this:

::

   -name: Ensure mysql server is installed

   yum: name=mysql-server state=present

   - name: Ensure mysql python is installed

   yum: name=MySQL-python state=present


   - name: Ensure selinux python bindings are installed

   yum: name=libselinux-python state=present

   - name: Ensure cloudstack specfic my.cnf lines are present

   lineinfile: dest=/etc/my.cnf regexp=’$item’ insertafter=”symbolic-links=0″ line=’$item’ 

   with\_items:

   – skip-name-resolve

   – default-time-zone=’+00:00′

   – innodb\_rollback\_on\_timeout=1

   – innodb\_lock\_wait\_timeout=600

   – max\_connections=350

   – log-bin=mysql-bin

    – binlog-format = ‘ROW’


   - name: Ensure MySQL service is started

   service: name=mysqld state=started

   - name: Ensure MySQL service is enabled at boot

   service: name=mysqld enabled=yes

    

   - name: Ensure root password is set

   mysql\_user: user=root password=$mysql\_root\_password host=localhost

   ignore\_errors: true

   - name: Ensure root has sufficient privileges

   mysql\_user: login\_user=root login\_password=$mysql\_root\_password user=root host=% password=$mysql\_root\_password priv=\*.\*:GRANT,ALL state=present

This needs to be saved as `/etc/ansible/roles/mysql/tasks/main.yml`

As explained earlier, this playbook in fact describes the state of the
host rather than setting out commands to be run. For Instance, we
specify certain lines which must be in the my.cnf file and allow Ansible
to decide whether or not it needs to add them.

Most of the modules are self-explanatory once you see them, but to run
through them briefly;

The ‘yum’ module is used to specify which packages are required, the
‘service’ module controls the running of services, while the
‘mysql\_user’ module controls mysql user configuration. The ‘lineinfile’
module controls the contents in a file.

 We have a couple of variables which need declaring.  You could do that
within this playbook or its ‘parent’ playbook, or as a higher level
variable. I’m going to declare them in a higher level playbook. More on
this later.

 That’s enough to provision a MySQL server. Now for the management
server.

 
CloudStack Management server service
------------------------------------

For the management server role we create a main.yml task like this:

::

   - name: Ensure selinux python bindings are installed

     yum: name=libselinux-python state=present


   - name: Ensure the Apache Cloudstack Repo file exists as per Template

     template: src=cloudstack.repo.j2 dest=/etc/yum.repos.d/cloudstack.repo


   - name: Ensure selinux is in permissive mode

     command: setenforce permissive


   - name: Ensure selinux is set permanently

     selinux: policy=targeted state=permissive


   -name: Ensure CloudStack packages are installed

     yum: name=cloud-client state=present


   - name: Ensure vhdutil is in correct location

     get\_url: url=http://download.cloudstack.org/tools/vhd-util dest=/usr/share/cloudstack-common/scripts/vm/hypervisor/xenserver/vhd-util mode=0755


Save this as `/etc/ansible/roles/cloudstack-management/tasks/main.yml`

Now we have some new elements to deal with. The Ansible Template module
uses Jinja2 based templating.  As we’re doing a simplified example here,
the Jinja Template for the cloudstack.repo won’t have any variables in
it, so it would simply look like this:

::

   [cloudstack]
   name=cloudstack
   baseurl=http://download.cloudstack.org/rhel/4.2/
   enabled=1
   gpgcheck=0

This is saved in 
`/etc/ansible/roles/cloudstack-manager/templates/cloudstack.repo.j2`

That gives us the packages installed, we need to set up the database. To
do this I’ve created a separate task called setupdb.yml

::

   - name: cloudstack-setup-databases
   command: /usr/bin/cloudstack-setup-databases cloud:{{mysql\_cloud\_password }}@localhost –deploy-as=root:{{mysql\_root\_password }}

   - name: Setup CloudStack manager
   command: /usr/bin/cloudstack-setup-management


Save this as: `/etc/ansible/roles/cloudstack-management/tasks/setupdb.yml`

As there isn’t (as yet) a CloudStack module, Ansible doesn’t inherently
know whether or not the databases have already been provisioned,
therefore this step is not currently idempotent and will overwrite any
previously provisioned databases.

There are some more variables here for us to declare later.

 
System VM Templates:
--------------------

Finally we would want to seed the system VM Templates into the secondary
storage.  The playbook for this would look as follows:

::

   - name: Ensure secondary storage mount exists
     file: path={{ tmp\_nfs\_path }} state=directory


   - name: Ensure  NFS storage is mounted
     mount: name={{ tmp\_nfs\_path }} src={{ sec\_nfs\_ip }}:{{sec\_nfs\_path }} fstype=nfs state=mounted opts=nolock


   - name: Seed secondary storage
     command:
   /usr/share/cloudstack-common/scripts/storage/secondary/cloud-install-sys-tmplt -m {{ tmp\_nfs\_path }} -u http://download.cloud.com/templates/4.2/systemvmtemplate-2013-06-12-master-kvm.qcow2.bz2 -h kvm -F

     command:
   /usr/share/cloudstack-common/scripts/storage/secondary/cloud-install-sys-tmplt -m {{ tmp\_nfs\_path }} -u http://download.cloud.com/templates/4.2/systemvmtemplate-2013-07-12-master-xen.vhd.bz2 -h xenserver -F

     command:
   /usr/share/cloudstack-common/scripts/storage/secondary/cloud-install-sys-tmplt -m {{ tmp\_nfs\_path }} -u http://download.cloud.com/templates/4.2/systemvmtemplate-4.2-vh7.ov -h vmware -F


Save this as `/etc/ansible/roles/cloudstack-manager/tasks/seedstorage.yml`

Again, there isn’t a CloudStack module so Ansible will always run this
even if the secondary storage already has the Templates in it.

 
Bringing it all together
------------------------

Ansible can use playbooks which run other playbooks, this allows us to
group these playbooks together and declare variables across all of the
individual playbooks. So in the Ansible playbook directory create a file
called deploy-cloudstack.yml, which would look like this:

::

   -hosts: acs-manager

    vars:

       mysql\_root\_password: Cl0ud5tack
       mysql\_cloud\_password: Cl0ud5tack
       tmp\_nfs\_path: /mnt/secondary
       sec\_nfs\_ip: IP\_OF\_YOUR\_SECONDARY\_STORAGE
       sec\_nfs\_path: PATH\_TO\_YOUR\_SECONDARY\_STORAGE\_MOUNT


    roles:

      – mysql
      – cloudstack-manager

    tasks:

      – include: /etc/ansible/roles/cloudstack-manager/tasks/setupdb.yml
      – include: /etc/ansible/roles/cloudstack-manager/tasks/seedstorage.yml


Save this as `/etc/ansible/deploy-cloudstack.yml`  inserting the IP
address and path for your secondary storage and changing the passwords
if you wish to.

To run this go to the Ansible directory (cd /etc/ansible ) and run:

::

   # ansible-playbook deploy-cloudstack.yml -k

‘-k’ tells Ansible to ask you for the root password to connect to the
remote host.

Now log in to the CloudStack UI on the new management server.


How is this example different from a production deployment?
-----------------------------------------------------------

In a production deployment, the Ansible playbooks would configure
multiple management servers connected to the source/replica replicating MySQL
databases along with any other infrastructure components required and
deploy and configure the hypervisor hosts. We would also have a
dedicated file describing the hosts in the environment and a dedicated
file containing variables which describe the environment.

The advantage of using a configuration management tool such as Ansible
is that we can specify components like the MySQL database VIP once and
use it multiple times when configuring the MySQL server itself and other
components which need to use that information.


Acknowledgements
----------------

Thanks to Shanker Balan for introducing me to Ansible and a load of
handy hints along the way.
