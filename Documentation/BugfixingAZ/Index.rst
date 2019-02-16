.. include:: ../Includes.txt
.. highlight:: shell

.. _Fixing-a-bug-A-Z:

=======================
Create & submit a patch
=======================

**Quick links:**

.. rst-class:: horizbuttons-primary-m

- :ref:`git setup <Setting-up-your-Git-environment>`
- :ref:`git cheat sheet <cheat-sheet-git>`
- :ref:`Commit Message rules <commitmessage>`
- :ref:`Deprecations <deprecations>`
- :ref:`Testing <testing>`
- :ref:`Adding-documentation`

So you want to fix a bug or add a new feature to TYPO3? **Great!**

This chapter will guide you through the process step by step. If you
should encounter any problems or have questions, talk to us on
https://typo3.slack.com in the **#typo3-cms-coredev** channel
(for more information on Slack, see :ref:`appendix-slack-intro`).


.. _Bugfixing-prerequisites:

Prerequisites
=============

We assume, you have followed all steps in the **intro & setup** chapters.If
not, use :ref:`quickstart-create-a-patch` to guide you through
the entire process.

Also, an **issue** must exist for the patch you want to create. Every patch
must refer to at least one corresponding issue. If there is no issue
yet, create one now by going to https://forge.typo3.org/.
(see :ref:`create-an-issue` for more information).


.. _Bugfixing-Fix-the-code:
.. _fix-the-code:

Step by step walkthrough
========================

.. rst-class:: bignums-xxl

1. Make your changes to the code

   This part is pretty straightforward. But be warned, there
   are still a few dark places deep inside the TYPO3 core dating back to the
   medieval times of PHP4. Yes, TYPO3 has been around for quite some time now. And
   there is ancient code we didn't have to touch yet because it just works.

   Make sure to look at :ref:`deprecations` in the Appendix for information
   about to deprecate things if you need to make changes to the public API.

2. Add tests

   Add Unit Tests or Functional Tests for new functionality, refine existing tests
   if necessary. Tests are important because they ensure that
   TYPO3 will behave consistently now and in the future.

   See :ref:`t3coreapi:testing-writing-unit` in TYPO3 Explained for more information
   about writing Unit Tests.

3. Optional: Run tests

   See :ref:`Testing the core <testing>` for a step-by-step guide using docker.

4. Add documentation

   For new features, breaking changes and deprecations, it is necessary to :ref:`add
   information to the changelog <changelog>`.

5. Use the commit message rules

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
   
6. Commit

   Only create one commit. Do not create a branch. Work on master.

   .. code-block:: bash

      git commit -a

   The :ref:`commit-msg hook <git-setup-commit-msg-hook>` will do some sanity
   checks and add a line starting with `Change-Id:`.


   If you have activated the :ref:`pre-commit hook <git-setup-precommithook>`
   it will loudly complain if something does not conform to the coding guidelines.

   In that case, use the :ref:`cgl-fix-my-commit` script to to fix CGL issues
   (it uses `php-cs-fixer <https://github.com/FriendsOfPHP/PHP-CS-Fixer>`__).

   After you have created your commit, you can still make changes by
   amending to your commit::

      git commit -a --amend

   .. tip::

      Keep in mind that you can commit with --amend **as often as you want,**
      just make sure you keep the `Change-Id:` line intact.

7. Optional: Check your commit history

   Before you submit your patch for review, check what you are going to push::

      git log origin/master..HEAD

   You must only see one commit (for the basic workflow described in this guide).

8. Push to Gerrit

   To submit the patch to Gerrit, issue the following command::

      git push origin HEAD:refs/for/master


   If Gerrit accepts your push, it responds with the following messages:

   .. code-block:: bash

      remote: New Changes:
      remote:   https://review.typo3.org/<gerrit-id>
      remote:
      To ssh://<username>@review.typo3.org:29418/Packages/TYPO3.CMS.git
       * [new branch]      HEAD -> refs/for/<release-branch>

   You can visit the link to https://review.typo3.org to see your patch in Gerrit.

   Advanced users / core team only: See
   :ref:`cheat sheet: other branches <cheat-sheet-git-other-branches>`
   for pushing to other branches.

9. Optional: Use Botty on Slack and wait for reviews

   Once your push to Gerrit_ goes through, you will receive a URL for your new
   change. If you are on `Slack <https://typo3.slack.com>`__ you can now advertise
   your new change in the **#typo3-cms-coredev** channel using the command::

      review:show [ReviewNumber or URL]

   This is not something, you will do for every review. As a first contributor
   it is recommended to mention that you are new to the process. 
   
   Now, it's time to sit back and await feedback on your changes. The review team process
   dozens of requests each day, so expect a succinct response that is short and to the point.

   You will get notified by email, if there is activity on your patch in Gerrit
   (e.g. votes, comments, new patchsets, merge etc.).


It is not unusual for a patch to get comments requesting changes. If that happens,
please respond in a timely fashion and improve your review. If things are unclear, 
ask in the **#typo3-cms-coredev** channel on https://typo3.slack.com.

When you change your patch, make sure you do not add another commit. Append to 
your original commit instead as described in :ref:`lifeOfAPatch-improve-patch`.


Helpful links
=============

* `Gerrit <https://review.typo3.org>`__ Review server
* `Forge <https://forge.typo3.org>`__ Issue tracker
* `Forger <https://forger.typo3.org>`__ Search for reviews and issues
* `Slack <https://slack.typo3.org>`__ chat system

More information
================

* :ref:`t3coreapi:testing-writing-unit` in TYPO3 explained
* :ref:`improving-a-patch` in this guide for next steps in improving your patch or reviewing other patches

