.. include:: /Includes.rst.txt
.. highlight:: shell

.. index::
   single: Code Contribution Workflow; Create Patch

.. _Fixing-a-bug-A-Z:
.. _core-contrib-quickstart:
.. _quickstart-create-a-patch:


==============
Create a Patch
==============

**Quick links:**

.. rst-class:: horizbuttons-primary-m

- :ref:`git setup <Setting-up-your-Git-environment>`
- :ref:`git cheat sheet <cheat-sheet-git>`
- :ref:`Commit Message rules <commitmessage>`
- :ref:`Deprecations <deprecations>`
- :ref:`Testing <testing>`
- :ref:`Adding-documentation`

So you want to fix a bug or add a new feature to TYPO3? **Great!**

.. tip::

   If you
   should encounter any problems or have questions, talk to us on
   https://typo3.slack.com in the **#typo3-cms-coredev** channel
   (see :ref:`appendix-slack-intro`).


.. _Bugfixing-prerequisites:
.. _Bugfixing-Fix-the-code:
.. _fix-the-code:

Step by Step Walkthrough
========================

You should have a cloned Git repository with a working TYPO3 installation
as described in :ref:`setup <setup>` (or via the
:ref:`Quick start guide <quickstart>`). Especially the
:ref:`Git setup <Setting-up-your-Git-environment>` is required.

.. rst-class:: bignums-xxl

#. Create an Issue on Forge

   More information: :ref:`bugreporting-index`

   Every patch must have a matching issue on
   `Forge <https://forge.typo3.org/projects/typo3cms-core/issues>`__,
   so create an issue now or submit
   a patch for an existing issue.


#. Make your changes to the code, add documentation, tests

   This part is pretty straightforward. But be warned, there
   are still a few dark places deep inside the TYPO3 core dating back to the
   medieval times of PHP4. Yes, TYPO3 has been around for quite some time now. And
   there is ancient code we didn't have to touch yet because it just works.

   Make sure to look at :ref:`deprecations` in the Appendix for information
   about how to deprecate things if you need to make changes to the public API.

   For new features, breaking changes and deprecations, it is necessary to :ref:`add
   information to the changelog <changelog>`.

   If you change SCSS, JavaScript or TypeScript files, you can :ref:`build <build>`
   locally.

   Add Unit Tests or Functional Tests for new functionality, refine existing tests
   if necessary. Tests are important because they ensure that
   TYPO3 will behave consistently now and in the future.

   See :ref:`Testing the core <testing>` in TYPO3 Explained for more information
   about writing and running tests.

   Once you have finalized your patch, check out the :ref:`common-review-checks`
   for a list of what kind of review checks people may perform on your contribution.
   Stay ahead of the game and address those yourself first.

#. Commit your changes

   Please make sure that you read the :ref:`commitmessage` in the Appendix.
   Your code will not be merged if it does not follow the commit message
   rules.

   .. important::
      The section :ref:`commitmessage` is a must-read. Read it. Follow it.

   For a bugfix, your commit message may look something like this:

   .. code-block:: text
      :caption: commit message

      [BUGFIX] Subject line of max 52 chars

      Some descriptions with line length of max. 72 characters

      Resolves: #12346
      Releases: main, 12.4

   Only create one commit. Do not create a branch. Work on main.

   .. code-block:: bash
      :caption: shell command

      git commit -a

   The :ref:`commit-msg hook <pre-commit-hook>` will do some sanity
   checks and add a line starting with `Change-Id:`.


   If you have activated the :ref:`pre-commit hook <pre-commit-hook>`
   it will loudly complain if something does not conform to the coding guidelines.

   In that case, use the :ref:`runTests.sh <runTestsShCgl>` script to to fix CGL
   issues.

   After you have created your commit, you can still make changes by
   amending to your commit:

   .. code-block:: bash
      :caption: shell command

      git commit -a --amend

   .. tip::

      Keep in mind that you can commit with --amend **as often as you want,**
      just make sure you keep the `Change-Id:` line intact.

#. Push to Gerrit

   To submit the patch to Gerrit, issue the following command:

   .. code-block:: bash
      :caption: shell command

      git push origin HEAD:refs/for/main

   If you have setup the default as described in :ref:`git-setup-remote`
   it is sufficient to use:

   .. code-block:: bash
      :caption: shell command

      git push

   In case you want to push a "Work in progress", check out:
   :ref:`git-work-in-progress`.

   If Gerrit accepts your push, it responds with the following messages:

   .. code-block:: none
      :caption: result

      remote: New Changes:
      remote:   https://review.typo3.org/<gerrit-id>
      remote:
      To ssh://<username>@review.typo3.org:29418/Packages/TYPO3.CMS.git
       * [new branch]      HEAD -> refs/for/<release-branch>

   If you see an error, check out the :ref:`Git Troubleshooting <git-troubleshooting>`
   section.

   You can visit the link to https://review.typo3.org to see your patch in Gerrit.

   The Continuous Integration service, running on GitLab Pipelines, will automatically
   be executed in the background and perform checks and tests on your patch.
   Failing tests will be linked to that instance, where jobs can also be retried
   (given sufficient permissions when being logged in to GitLab).

   Advanced users / core team only: See
   :ref:`cheat sheet: other branches <cheat-sheet-git-other-branches>`
   for pushing to other branches.

#. Optional: Advertise review on Slack channel

.. _announce-slack:
   Once your push to Gerrit_ goes through, you will receive a URL for your new
   change. If you are on `Slack <https://typo3.slack.com>`__ you can now advertise
   your new change in the **#typo3-cms-coredev** channel. You can get a preformatted
   line of your change to post in the channel by clicking the copy button next to the title in Gerrit_:

   .. image:: /Images/External/Forge/copy-slack-link.png
      :class: with-shadow

   This is not something, you will do for every review. As a first contributor
   it is recommended to mention that you are new to the process.

Now, it's time to sit back and await feedback on your changes. The review team process
dozens of requests each day, so expect a succinct response that is short and to the point.
You will get notified by email, if there is activity on your patch in Gerrit
(e.g. votes, comments, new patchsets, merge etc.).

Check out the section :ref:`reviewPatch` for more about this process, in which you can
also be involved!

It is not unusual for a patch to get comments requesting changes. If that happens,
please respond in a timely fashion and improve your review. If things are unclear,
ask in the **#typo3-cms-coredev** channel on https://typo3.slack.com.


Helpful links
=============

* `Gerrit <https://review.typo3.org>`__ Review server
* `Forge <https://forge.typo3.org>`__ Issue tracker
* `Forger <https://forger.typo3.com>`__ Search for reviews and issues
* `Slack <https://slack.typo3.org>`__ chat system

Next Steps
==========

You will find some more information about the review process in the chapter
:ref:`lifeOfAPatch`. The following pages are especially relevant
for new contributors:

* :ref:`new-contributors-tips`
* :ref:`Working-with-Gerrit` describes the review tool Gerrit.
* :ref:`Find-a-review` is helpful if you don't know how to find your patch on Gerrit.
* Gerrit works with up- and downvoting patches. A patch must get a specific number of
  upvotes before it can be merged. :ref:`lifeOfAPatch-review` gives
  an introduction to how this works.
* When you make additional changes to your patch, make sure you do not add another
  commit. Append to your original commit instead as described in
  :ref:`lifeOfAPatch-improve-patch`.
* Before starting to work on a new, unrelated patch you need to run the :ref:`cleanup-tasks`.
