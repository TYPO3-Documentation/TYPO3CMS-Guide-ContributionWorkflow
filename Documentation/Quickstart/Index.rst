.. include:: ../Includes.txt

.. highlight:: bash

.. _core-contrib-quickstart:

===========
Quick start
===========

Quick start for creating a patch. 

.. important::

   The quick start is a very fast walkthrough with very little explanation.
   If you get stuck or need more information, click on the "More information"
   link at the beginning of each section.

   Or skip quick start and begin with :ref:`workflow-explained` for an in-depth
   walkthrough.


.. rst-class:: bignums-xxl

1. Signup

   More information: :ref:`TYPO3-Guide-ContributionWorkflow-Account`

   * Signup for a `typo3.org account <https://my.typo3.org/index.php?id=2>`__
   * Signup for `Slack <https://my.typo3.org/index.php?id=35>`__, join the
     `#typo3-cms-coredev` channel

2. Setup ssh key for Gerrit

   More information: :ref:`GerritAccount`

   Log in to `Gerrit <https://review.typo3.org>`__, click on Settings and upload your
   ssh key

3. Setup your git environment

   More information: :ref:`Setting-up-your-Git-environment`

   git clone::

      git clone git://git.typo3.org/Packages/TYPO3.CMS.git .

   Setup name and email (same as you used for typo3.org), replace `"Your name"` and `"your-email@example.com"` here)::

      git config user.name "Your Name"
      git config user.email "your-email@example.com"


   Setup autosetuprebase::

      git config branch.autosetuprebase remote

   Setup commit hook::

      cp Build/git-hooks/commit-msg .git/hooks/commit-msg

   Push to Gerrit (replace `<YOUR_TYPO3_USERNAME>` here)::

      git config url."ssh://<YOUR_TYPO3_USERNAME>@review.typo3.org:29418".pushInsteadOf git://git.typo3.org

4. Run composer and yarn

   More information: :ref:`composer-install`

   Inside your cloned TYPO3 repository, run composer::

      composer install

   Run yarn::

      cd Build
      yarn install
      yarn build
      cd ..


5. Setup your TYPO3 installation

   More information: :ref:`setup-typo3-installation`

6. Setup your IDE to adhere to the coding guidelines

   More information: :ref:`setup-ide`

   Use the :file:`.editorconfig` in the TYPO3 core directory to setup your IDE.

7. Create an Issue on Forge

   More information: :ref:`bugreporting-index`

   Every patch must have a matching issue on
   `Forge <https://forge.typo3.org/projects/typo3cms-core/issues>`__,
   so create an issue now or submit
   a patch for an existing issue.

8. Create your patch

   More information: :ref:`Fixing-a-bug-A-Z`

   Create your patch, make sure you add tests and :ref:`run existing tests <testing>`.
   Add :ref:`documentation <Bugfixing-Adding-documentation>`
   for breaking changes and new features.

9. Commit and push

   More information: :ref:`Bugfixing-Create-a-new-patch`

   First, read :ref:`commitmessage`.

   Then, commit and push::

      git commit -a
      git push origin HEAD:refs/publish/master

10. Finally, announce your review on Slack

   Login to `Slack <https://typo3.slack.org>`__ and in the `#typo3-cms-coredev`
   announce your new patch by using the `botty <https://wiki.typo3.org/T3Bot>`__
   command::

      review:show [ReviewNumber or URL]

   This is not something you would do for every patch, but for your first one
   it is recommended. Please mention that you are a new contributor.

.. important::

   If someone makes comments on your review in `Gerrit <https://review.typo3.org>`__,
   look at the comments and try to improve your patch.

Do not get discouraged if your patch is downvoted, commented on and not merged right
away! Find a way to improve it. Ask in the **#typo3-cms-coredev** channel
in `Slack <https://typo3.slack.com>`__, if things are unclear.

Refer to :ref:`lifeOfAPatch` for information about how to push a new patchset.

