.. include:: ../Includes.txt
.. highlight:: shell

.. _bugfix-index:

================
Fixing a bug A-Z
================

So you found a bug in TYPO3. Who would have thought there bugs? And you want to
fix them right away? **Great!** This document will guide you through the
process step by step.

.. note::

   We assume you already went through the setup process so we won't be covering 
   that here again.


Identify the issue
==================

Be up to date
   First of all, you should make sure that the bug does exist in the latest
   master branch. Do a `git pull` on your development environment, flush all
   caches, do a `composer install`, just to be sure.

Remove side effects
   Work on a TYPO3 instance which is as clean as possible so you can rule out
   that extensions are messing with the TYPO3 core. If you need to set up an
   extension to illustrate the problem, make sure it is as free of side effects
   as possible.

Narrow down the problem
   Try different browsers, this will help you and the team a lot to provide a
   proper description of the problem.

Talk to the core team
   When in doubt, don't hesitate to talk to us on Slack_ in the
   `#typo3-cms-coredev` channel.


Create an issue
===============

Head over to Forge_. Log in if you aren't already. You can find the TYPO3
core issue tracker at `Forge projects typo3cms-core
<https://forge.typo3.org/projects/typo3cms-core/>`__.

If you click "New issue" you will see a form with a couple of fields that are
important. Let's go over these really quick.

Tracker
   The tracker is just Redmines term for the type of issue. The trackers you
   will be using the most are **Feature** and **Bug**. The others, like
   "Stories" and "Epics", are mostly for internal organization and things which
   aren't really a feature or a bug. They just denote tasks that somebody needs
   to take care of.

Subject
   Pick a meaningful subject. Something like "GIFBUILDER broken" is very
   generic and doesn't describe the problem specificly. Just imagine how you
   would like to get a report yourself :)

Description
   As usual, provide the steps to reproduce the problem. Redmine offers a lot
   of text formatting options: Use them to make your report readable!

   A screenshot says more than 1000 words. So consider attaching **images**
   and, preferably add them **inline** (like `!image.png!`) so that they are
   shown **within** the text where they do belong.

   Do **not** add screenshots of code but use `<pre>` and `<code>` tags instead
   so that the code can be searched for.


Fix the code
============

.. sidebar:: UnitTests

   Adding Unit Tests is a good idea at this point because it makes it a lot
   easier to ensure TYPO3 behaves consistently now and in the future.

This is actually the part that is pretty straightforward. But be warned, there
are still a few dark places deep inside the TYPO3 core dating back to the
medieval times of PHP4. Yes, TYPO3 has been around for quite some time now. And
there is ancient code we didn't have to touch yet because it just works.

If you should encounter any problems or have questions, talk to us on Slack_ in
the `#typo3-cms-coredev` channel.

.. attention::

   Make sure you are using the correct PHP codestyle. It is **PSR-2** at
   the time of writing and specified in the :ref:`TYPO3 Coding Guidelines
   <t3coreapi:cgl>`. Instruct your IDE to work against this standard,
   install PHP Codesniffer, ask us if you need any assistance.


Test the code
=============

It is a good idea to test the TYPO3 core with your fix to be sure that the
automatic tests, that are running on bamboo after you have pushed a patch to
the Gerrit review system, do not fail.

The best for doing so is to run the tests locally with the same setup Bamboo
uses. All you need for this is `Docker installed locally.
<https://www.docker.com/get-docker>`__

You have to load the necessary PHP container from `Bitbucket T3COM bamboo-
remote-agent <https://bitbucket.typo3.com/projects/T3COM/repos/bamboo-remote-agent/browse>`__.
There are a lot of containers for testing with different PHP versions and
different databases and the functional tests. As an example, if you want to run
the unit tests for current master you have to load the php72 container::

   docker pull typo3gmbh/php72:latest

Then start the container like this. It leaves the bash shell open::

   docker run -it --rm \
      --name=typo3_core_test \
      -v <absolute local path where your typo3 checkout is>:/srv/tmp/cms \
      typo3gmbh/php72:latest \
      /sbin/my_init -- bash

At the bash prompt it takes three commands to run the unit tests::

   export HOME=/root
   cd /srv/tmp/cms
   bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/UnitTests.xml

If no test fails it is save to push your fix to Gerrit.

Running the functional tests is almost the same. It is just the phpunit command
that looks a bit different. For the mysql setup use::

   export typo3DatabaseName="func" \
          typo3DatabaseUsername="funcu" \
          typo3DatabasePassword="funcp" \
          typo3DatabaseHost="localhost" \
          typo3InstallToolPassword="klaus" \
          && bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/FunctionalTests.xml

When you want to test against other databases like PostgreSQL or MSSQL you will
find the database credentials inside the :file:`Build` folder of the TYPO3
core in the file :file:`Build/bamboo/src/main/java/core/AbstractCoreSpec.java`.

Search for 'typo3DatabaseUsername' in this Java file to find the definitions of
the different database credentials.

.. hint::

   Be sure to have a cup of coffee, a good book or other things to be done to
   span the waiting time. Functional tests will take a lot more time than unit
   tests. Depending on the power of your local machine you can expect about 45
   minutes or more.


Adding documentation
====================

.. sidebar:: Forger

   If you want to save yourself some time you can use the rst Helper at
   https://forger.typo3.org/utility/rst

   Select the type of rst snippet you want to create, enter your issue number
   and click the search button.

If your change makes it necessary to update the official documentation you have
to add a rst snippet describing your change. There are four different types of
documentation snippets which have to follow a certain format and **always**
need to go into :file:`typo3/sysext/core/Documentation/Changelog/master/`.

These are the mandatory sections that a rst snippet needs to have:

Breaking Changes
   #. **Description** - why things had to break backwards compatibility.

   #. **Impact** - how will the change affect your installation.

   #. **Affected Installations** - describe scenarios under which circumstances
      a TYPO3 install will be affected by this change.

   #. **Migration** - provide instructions what needs to be done to get things
      working again. Explicitly mention if no migration is possible.

:ref:`Deprecations <deprecations>`
   #. **Description** - why things had to be deprecated.

   #. **Impact** - how will the change affect your installation.

   #. **Affected Installations** - describe scenarios under which circumstances
      an TYPO3 install will be affected by this change.

   #. **Migration** - provide instructions what needs to be done to get things
      working again. Explicitly mention if no migration is possible.

Features
   #. **Description** - what can the new feature do.

   #. **Impact** - how users are affected by this new feature.

Important Information
   #. **Description** - describe what is so important it needed an rst snippet


Commit and Push
===============

When committing your changes decide about whether you are creating *a
completely new patch* or whether you are improving *an existing one.* You can
change your local commit as often as you want to. Once you are happy with your
change, push it to Gerrit_ as described in :ref:`git-setup-pushing-your-changes`.


Create a new patch
------------------

To create a totally new patch you have to attach a new commit message. A commit
message is new if it doesn't contain as `Change-Id: ...` line. The common
command to do so is::

   git commit -a

The :ref:`pre-commit hook <git-setup-precommithook>` automatically generates
the `Change-Id: ...` line and fills in a unique id.


Change an existing patch
------------------------

To improve an existing commit you have to keep a part of the old commit
message. Precisely, it is the `Change-Id: ...` line that you need to keep
unmodified. The common command to do so is::

   git commit -a --amend

The `--amend` option fills in the old commit message which you can then edit.
Change whatever you like but keep the `Change-ID: ...` line.

.. tip::

   Keep in mind that you can commit **as often as you want,**
   just make sure you keep the `Change-Id:` line intact.



Use Botty on Slack
==================

Once your push to Gerrit_ went through, you will get back the URL of your new
change. If you are on Slack_ you can now advertise your new change using the
command `review:show [ReviewNumber or URL]`. Note that the command works in
public channels only.


Wait for reviews
================

Lean back, have a tea, put the battle-armor on and wait for feedback on your
reviews.
