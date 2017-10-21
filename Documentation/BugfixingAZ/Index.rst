.. include:: ../Includes.txt

.. _bugfix-index:

================
Fixing a bug A-Z
================

So you found a bug in TYPO3 (who would have thought there are any?) and want to fix it right away? **Great**. This document will
guide you through it step by step.

.. note::

   We assume you went through the setup process so we won't be covering that here.


Identify the issue
==================

Be up to date
   First of all, you should make sure that the bug does exist in the latest master branch. Do a ``git pull`` on your
   development environment, flush all caches, do a ``composer install``, just to be sure.

Remove side effects
   Work on a TYPO3 instance which is as clean as possible so you can rule out extensions messing with the TYPO3 core. If you
   need to set up an extension to illustrate the problem, make sure it is as free of side effects as possible.

Narrow down the problem
   Try different browsers, this will help the team (and you) a lot to provide a proper description of the problem.

Talk to the core team
   When in doubt, don't hesitate to talk to us on Slack_ in the ``typo3-cms-coredev`` channel.


Create an issue
===============

Head over to Forge_ and log in (if you aren't already). You can find the TYPO3 core issue tracker here: https://forge.typo3.org/projects/typo3cms-core/.

If you click "New issue" you will see a form with a couple of fields that are important. Let's go over these really quick.

Tracker
   The tracker is just Redmines term for the type of issue. The trackers you will be using the most are **Feature** and **Bug**.
   The others are mostly for internal organization (like Stories and Epics) and things which aren't really a feature or
   a bug... they are just tasks somebody needs to take care of.

Subject
   Pick a meaningful subject. Something like "GIFBUILDER broken" is very generic and doesn't help describing the problem.
   Just imagine how you would like to get a report for yourself :)

Description
   As usual, provide steps how to reproduce the problem. Redmine offers a lot of text formatting options: use them to make
   your report readable. If you attach **images** (which makes sense, because a screenshot says more than 1000 words), consider
   displaying it inline in your description using exclamation marks to wrap your filename in - this saves everybody a click
   and makes it easier to understand which image goes where. As you can imagine: provide a screenshot of the relevant parts
   of the image.

   Do **not** add screenshots of code, use the ``<pre><code>`` tags in Redmine so we can search for the lines of code via
   Forger.


Fix the code
============

.. sidebar:: UnitTests

   Adding Unit Tests is a good idea at this point because it makes it a lot easier to ensure TYPO3 behaves consistently
   now and in the future.

This is actually the part that is pretty straightforward. But be warned, they are still some dark places deep inside the
TYPO3 core dating back to the medieval times of PHP4 (yes, TYPO3 has been around for quite some time) which we didn't have
to touch yet, because they just work.

If you should encounter any problems or have questions, talk to us on Slack_ in the ``typo3-cms-coredev`` channel.

.. warning::

   Make sure you are using the correct PHP codestyle - which is **PSR-2** at the time of writing. Instruct your IDE to
   work against this standard, install PHP Codesniffer, ask us if you need any assistance.


Adding documentation
====================

.. sidebar:: Forger

   If you want to save yourself some time you can use the rst Helper at https://forger.typo3.org/utility/rst

   Select the type of rst snippet you want to create, enter your issue number and click the search button.

If your change makes it necessary to add to the official documentation you have to add a rst snippet to your change.
There are 4 different types of documentation snippets which have to follow a certain format and **always** need to go
into ``typo3/sysext/core/Documentation/Changelog/master``.

We will explain the mandatory sections a rst snippet needs to have below:

Breaking Changes
   #. **Description** - why things had to break backwards compatibility.

   #. **Impact** - how will the change affect your installation.

   #. **Affected Installations** - describe scenarios under which circumstances an TYPO3 install will be affected by this change.

   #. **Migration** - provide instructions what needs to be done to get things working again. Explicitly mention if no
      migration is possible.

:ref:`Deprecations<deprecations>`
   #. **Description** - why things had to be deprecated.

   #. **Impact** - how will the change affect your installation.

   #. **Affected Installations** - describe scenarios under which circumstances an TYPO3 install will be affected by this change.

   #. **Migration** - provide instructions what needs to be done to get things working again. Explicitly mention if no
      migration is possible.

Features
   #. **Description** - what can the new feature do.

   #. **Impact** - how users are affected by this new feature.

Important Information
   #. **Description** - describe what is so important it needed an rst snippet


Commit and Push
===============

.. highlight:: shell

When committing your changes decide about whether you are creating *a completely new patch* or whether
you are improving *an existing one.* You can change your local commit as often as you want to.
Once you are happy with your change, push it to Gerrit_ as described in :ref:`git-setup-pushing-your-changes`.

Create a new patch
------------------

To create a totally new patch you have to attach a new commit message. A commit message is new if it doesn't contain
as `Change-Id: ...` line. The common command to do so is::

   git commit -a

The pre-commit hook (:ref:`git-setup-precommithook`) automatically generates the `Change-Id: ...` line
and fills in a unique id.

Change an existing patch
------------------------

To improve an existing commit you have to keep a part of the old commit message.
Precisely, it's the `Change-Id: ...` line that you need to keep unmodified. The common command
to do so is::

   git commit -a --amend

The `--amend` option fills in the old commit message which you can then edit. Change whatever you like but keep
the `Change-ID: ...` line.

.. tip::

   Keep in mind that you can commit **as often as you want,**
   just make sure you keep the `Change-Id:` line intact.



Use Botty on Slack
==================

Once your push to Gerrit_ went through, you will get back the URL of your new change. If you are on Slack_ you can now
advertise your new change using the command ``review:show [ReviewNumber or URL]``. This will work only in public channels,
though.


Wait for reviews
================

Lean back, have a tea, put the battle-armor on and wait for feedback on your reviews.
