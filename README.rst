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


Apache CloudStack
=================

Apache CloudStack is an Apache project, see <http://cloudstack.apache.org> for
more information.


Website
=============

These guides can be viewed online at http://docs.cloudstack.apache.org/


Translation
===========

Clean the build

::

   make clean

Generate the .pot files

::

   make gettext

Generate the .tx/config files with:

::

   sphinx-intl update-txconfig-resources --pot-dir source/locale/pot --transifex-project-name apache-cloudstack-installation-rtd --locale-dir source/locale

Push the .pot files to transifex with:

::

   tx push -s

Download the translated strings, for example Japanese (ja):

::

   tx pull -l ja

Build the translated docs:

::

   sphinx-intl build --locale-dir source/locale
   make -e SPHINXOPTS="-D language='ja'" html


Feedback
========

Please send feedback to the mailing list at <dev@cloudstack.apache.org>,
or the JIRA at <https://issues.apache.org/jira/browse/CLOUDSTACK>.


Contributing to the documentation
=================================

Initial setup of your fork
--------------------------

In your browser, navigate to: https://github.com/apache/cloudstack-documentation

Fork this repository by clicking on the 'Fork' button on the top right hand side.  The fork will happen and you will be taken to your own fork of the repository.  On the right hand side of the page of your fork, under 'HTTPS clone URL', copy the URL to your clipboard by clicking the the clipboard just right of the URL.

On your computer, follow these steps to setup a local repository for working on the documentation:

.. code:: bash

   $ git clone https://github.com/YOUR_ACCOUNT/cloudstack-documentation.git
   $ cd cloudstack-docs-install
   $ git remote add upstream https://github.com/apache/cloudstack-documentation.git
   $ git checkout main
   $ git fetch upstream
   $ git merge upstream/main


Making changes
--------------

It is important that you create a new branch to make changes on and that you do not change the `main` branch (other than to pull in changes from `upstream/main`).  In this case I will assume you will be creating a branch called `dev` to make your changes in.  This `dev` branch will be created on your local repository and will then be pushed to your forked repository on GitHub where you will create a Pull Request for the changes to be committed into the official documentation.

It is good practice to create a new branch each time you want to contribute to the documentation and only track the changes for that pull request in this branch.

.. code:: bash

   $ git checkout -b dev
   (make your changes)
   $ git add .
   $ git commit -a -m "commit message for your changes"

.. note:: 
   The `-b` specifies that you want to create a new branch called `dev`.  You only specify `-b` the first time because you are creating a new branch.  Once the `dev` branch exists, you can later switch to it with only `git checkout dev`.


Merging `upstream/main` into your `dev` branch
------------------------------------------------

It is important that you maintain an up-to-date `main` branch in your local repository.  This is done by merging in the `upstream/main` (the official documentation repository) into your local repository.  You will want to do this before you start working on a feature as well as right before you submit your changes as a pull request.  You can also do this process periodically while you work on your changes to make sure you are working off the most recent version of the documentation.

This process will do the following:

#. Checkout your local `main` branch

#. Synchronize your local `main` branch with the `upstream/main` so you have all the latest changes from the official docs

#. Merge the latest changes from the official docs into your `dev` branch so it is up-to-date with the latest changes

.. code:: bash

   $ git checkout main
   $ git fetch upstream
   $ git merge upstream/main
   $ git checkout dev
   $ git pull . main

.. note:: Now your `dev` branch is up-to-date with all the recent changes in the `upstream/main`.


Making a pull request on GitHub to contribute your changes
----------------------------------------------------------

When you are happy with your changes and you want to contribute them, you will be creating a Pull Request on GitHub to do so.  This is done by pushing your changes to your forked repository (usually called 'origin') and then initiating a pull request.

.. note:: Make sure you have merged `upstream/main` into your `dev` branch before you do this.

.. code:: bash

   $ git push origin main
   $ git push origin dev

Now that the `dev` branch has been pushed to your GitHub repository, you can initiate the pull request.  

To initiate the pull request, do the following:

#. Navigate your browser to your forked repository: https://github.com/YOUR_ACCOUNT/cloudstack-documentation

#. Click the new button called 'Compare & pull request' that showed up just above the main area in your forked repository

#. Enter a good description of the work you have done and then click 'Send pull request'

If you are requested to make modifications to your proposed changes, make the changes locally on your `dev` branch, re-push the changes and submit the pull request again.


Cleaning up after a successful pull request
-------------------------------------------

Once the `dev` branch has been committed into the `upstream/main` branch, your local `dev` branch and the `origin/dev` branch are not needed anymore.  If you want to make additional documentation changes, restart the process with a new branch.

.. note:: Make sure that your changes are in `upstream/main` before you delete your `dev` and `origin/dev` branches!

You can delete these deprecated branches with the following:

.. code:: bash

   $ git checkout main
   $ git branch -D dev
   $ git push origin :dev
