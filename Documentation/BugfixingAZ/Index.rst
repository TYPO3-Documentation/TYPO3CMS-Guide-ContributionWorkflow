.. include:: ../Includes.txt
.. highlight:: shell

.. _Fixing-a-bug-A-Z:

================
Fixing a bug A-Z
================

So you want to fix a bug in TYPO3? **Great!** This document will guide you
through the process step by step.

.. note::

   We assume you have already reviewed the setup process so we won't be covering
   that here again.


.. _Bugfixing-Fix-the-code:

Fix the code
============

.. sidebar:: UnitTests

   Adding Unit Tests is a good idea at this point because it makes it a lot
   easier to ensure TYPO3 behaves consistently now and in the future.

This part is pretty straightforward. But be warned, there
are still a few dark places deep inside the TYPO3 core dating back to the
medieval times of PHP4. Yes, TYPO3 has been around for quite some time now. And
there is ancient code we didn't have to touch yet because it just works.

If you should encounter any problems or have questions, talk to us on Slack_ in
the `#typo3-cms-coredev` channel.


.. _Bugfixing-Coding-Guidelines:

Coding Guidelines
=================

.. attention::

   Make sure you are using the correct PHP codestyle. It is **PSR-2** at
   the time of writing and specified in the :ref:`TYPO3 Coding Guidelines
   <t3coreapi:cgl>`. Instruct your IDE to work against this standard,
   ask us if you need any assistance.


You will find more information about this and about the :ref:`appendix-cgl` of
other file types such as JavaScript in the Appendix.


There is information about how to set up with :ref:`PhpStorm with PSR-2
<phpstorm-setup-cgl>`.


.. _Bugfixing-Test-the-code:

Test the code
=============

It is a good idea to test the TYPO3 core with your fix to be sure that the
automatic tests, that are running on bamboo after you have pushed a patch to
the Gerrit review system, do not fail.

See :ref:`Testing the core <testing>` for a step-by-step guide using docker.

If no test fails it is safe to push your fix to Gerrit.

.. _Bugfixing-Adding-documentation:

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

Description of Changes
-----------------------

There are four different types of breaking changes. Choose one which fits your patch:

**Breaking Changes**: A patch moved or removed a specific part of core functionality 
that may break extensions if they use this part.

**:ref:`Deprecations <deprecations>`**: A patch deprecates a certain core functionality 
for a planned removal.

**Features:** A patch adds new functionality.

**Important Information:** Anything that does not fit the other categories but is 
important enough to require a Changelog entry.   

Mandatory sections of breaking changes
---------------------------------------

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

Check your rst file
--------------------

When you are done, you can use the following script to check that your rst file is ok. 
The script will check all files in `typo3/sysext/core/Documentation/Changelog`.

::

   Build/Scripts/validateRstFiles.php


.. _Bugfixing-Commit-and-push:

Commit and push
===============

When committing your changes decide whether you are creating *a
completely new patch* or instead you are improving *an existing one.* You can
change your local commit as often as you want to. Once you are happy with your
change, push it to Gerrit.


.. _Bugfixing-Set-a-Commit-Message:

Commit Message rules for TYPO3 CMS
----------------------------------

Please make sure that you read the :ref:`commitmessage` in the Appendix. 
Your code will not be merged if it does not follow the commit message 
rules.    

.. important::
   The section :ref:`commitmessage` is a must-read. Read it. Follow it.

For a bugfix, your commit message may look something like this:

.. code-block:: none

   [BUGFIX] Subject line of max 52 chars

   Some descriptions with line length of max. 72 characters

   Resolves: #12346
   Releases: master, 8.7
   

.. _Bugfixing-Create-a-new-patch:

Create a new patch
------------------

To create a totally new patch you have to attach a new commit message. A commit
message is new if it doesn't contain as `Change-Id: ...` line. The common
command to do so is::

   git commit -a

The :ref:`commit-msg hook <git-setup-commit-msg-hook>` automatically generates
the `Change-Id: ...` line and fills in a unique id.


.. _Bugfixing-Change-an-existing-patch:

Change an existing patch
------------------------

To improve an existing commit you have to keep a part of the old commit
message. Precisely, it is the `Change-Id: ...` line that you need to keep
unmodified. The common command to do so is::

   git commit -a --amend

The `--amend` option fills in the old commit message which you can then edit.
Change whatever you like but keep the `Change-ID: ...` line.

.. tip::

   Keep in mind that you can commit with --amend **as often as you want,**
   just make sure you keep the `Change-Id:` line intact.


.. _Bugfixing-Pushing-your-changes:

Pushing your changes
--------------------

Once you are happy with your changes, you can push them via::

   git push origin HEAD:refs/publish/master

Where ``master`` is the target, so ``master`` is current development trunk.

Use the following for TYPO3v8 LTS::

   git push origin HEAD:refs/publish/TYPO3_8-7

Use the following for TYPO3v7 LTS::

   git push origin HEAD:refs/publish/TYPO3_7-6


.. important::
   Pushing to a branch other than master only makes sense if the bug only
   exists on that branch and does not exist on master. Backporting of a
   fix to a branch is done by the core team member who merges the original
   fix to the master branch.


.. _Bugfixing-Use-Botty-on-Slack:

Use Botty on Slack
==================

Once your push to Gerrit_ goes through, you will receive a URL for your new
change. If you are on `Slack <https://typo3.slack.com>`__ you can now advertise
your new change in the
`#typo3-cms-coredev`
channel using the command::

   review:show [ReviewNumber or URL]


.. _Bugfixing-Wait-for-reviews:

Wait for reviews
================

It's time to sit back and await feedback on your changes. The review team process
dozens of requests each day, so expect a succinct response that is short and to the point.

Improve your patch
==================

It is not unusual for a patch to get comments requesting changes. If that happens,
please respond in a timely fashion. If things are unclear, ask in the `typo3-cms-coredev`
channel on Slack. 

When you change your patch, make sure you do not add another commit. Append to 
your original commit instead as described in :ref:`lifeOfAPatch`.


