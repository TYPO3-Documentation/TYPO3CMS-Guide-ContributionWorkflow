.. include:: ../Includes.txt
.. highlight:: shell

.. _Fixing-a-bug-A-Z:
.. _core-contrib-quickstart:
.. _quickstart-create-a-patch:

.. index::
   single: Code Contribution Workflow; Create Patch

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

This chapter will guide you through the process step by step. If you
should encounter any problems or have questions, talk to us on
https://typo3.slack.com in the **#typo3-cms-coredev** channel
(see :ref:`appendix-slack-intro`).


.. _Bugfixing-prerequisites:
.. _Bugfixing-Fix-the-code:
.. _fix-the-code:

Step by Step Walkthrough
========================

.. rst-class:: bignums-xxl


1. Setup accounts

   * Signup for a `typo3.org account <https://my.typo3.org/index.php?id=2>`__
   * Signup for `Slack <https://my.typo3.org/index.php?id=35>`__, join the
     `#typo3-cms-coredev` channel

   More information: :ref:`TYPO3-Guide-ContributionWorkflow-Account`

   * Log in to `Gerrit <https://review.typo3.org>`__, click on Settings and upload your
     ssh key
   More information: :ref:`GerritAccount`

2. Setup your git environment

   More information: :ref:`Setting-up-your-Git-environment`

   git clone::

      git clone git://git.typo3.org/Packages/TYPO3.CMS.git .

   Setup name and email (same as you used for typo3.org), replace `"Your name"` and `"your-email@example.com"` here)::

      git config user.name "Your Name"
      git config user.email "your-email@example.com"


   Setup autosetuprebase::

      git config branch.autosetuprebase remote

   Setup commit-msg hook::

      cp Build/git-hooks/commit-msg .git/hooks/commit-msg

   Push to Gerrit (replace `<YOUR_TYPO3_USERNAME>` here)::

      git config url."ssh://<YOUR_TYPO3_USERNAME>@review.typo3.org:29418".pushInsteadOf git://git.typo3.org


3. Run composer and yarn

   More information: :ref:`composer-install`

   Inside your cloned TYPO3 repository, run composer::

      composer install

   Run yarn::

      cd Build
      yarn install
      yarn build
      cd ..


4. Setup your TYPO3 installation

   More information: :ref:`setup-typo3-installation`

   Setup your TYPO3 installation usig the git cloned TYPO3 source (as described above).


5. Setup your IDE to adhere to the coding guidelines

   More information: :ref:`setup-ide`

   Use the :file:`.editorconfig` in the TYPO3 core directory to setup your IDE.
   As :file:`.editorconfig` only contains minimal rules, it is a good idea to
   additionally setup your IDE to use PSR-1 / PSR-2 for PHP files.

6. Create an Issue on Forge

   More information: :ref:`bugreporting-index`

   Every patch must have a matching issue on
   `Forge <https://forge.typo3.org/projects/typo3cms-core/issues>`__,
   so create an issue now or submit
   a patch for an existing issue.


7. Make your changes to the code, add documentation, tests

   This part is pretty straightforward. But be warned, there
   are still a few dark places deep inside the TYPO3 core dating back to the
   medieval times of PHP4. Yes, TYPO3 has been around for quite some time now. And
   there is ancient code we didn't have to touch yet because it just works.

   Make sure to look at :ref:`deprecations` in the Appendix for information
   about to deprecate things if you need to make changes to the public API.

   For new features, breaking changes and deprecations, it is necessary to :ref:`add
   information to the changelog <changelog>`.

   Add Unit Tests or Functional Tests for new functionality, refine existing tests
   if necessary. Tests are important because they ensure that
   TYPO3 will behave consistently now and in the future.

   See :ref:`Testing the core <testing>` in TYPO3 Explained for more information
   about writing and running tests.

8. Commit your changes

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

9. Push to Gerrit

   To submit the patch to Gerrit, issue the following command::

      git push origin HEAD:refs/for/master


   In case you want to push a "Work in progress", check out:
   :ref:`git-work-in-progress`.

   If Gerrit accepts your push, it responds with the following messages:

   .. code-block:: bash

      remote: New Changes:
      remote:   https://review.typo3.org/<gerrit-id>
      remote:
      To ssh://<username>@review.typo3.org:29418/Packages/TYPO3.CMS.git
       * [new branch]      HEAD -> refs/for/<release-branch>

   If you see an error, check out the :ref:`Git Troubleshooting <git-troubleshooting>`
   section.

   You can visit the link to https://review.typo3.org to see your patch in Gerrit.
   
   If the automatically starting pre-merge build fails due to an error on Bamboo which
   isn't caused by your patch (e.g. time out) you can restart it on
   `Intercept <https://intercept.typo3.com/admin/bamboo/core>`__.
   

   Advanced users / core team only: See
   :ref:`cheat sheet: other branches <cheat-sheet-git-other-branches>`
   for pushing to other branches.

10. Optional: Use Botty on Slack and wait for reviews

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

.. tip::

   Look at the page :ref:`aliases` for some sample aliases which might help to
   simplify your workflow.

Helpful links
=============

* `Gerrit <https://review.typo3.org>`__ Review server
* `Forge <https://forge.typo3.org>`__ Issue tracker
* `Forger <https://forger.typo3.org>`__ Search for reviews and issues
* `Slack <https://slack.typo3.org>`__ chat system

Next Steps
==========

* :ref:`improving-a-patch` in this guide for next steps in improving your patch or reviewing other patches
