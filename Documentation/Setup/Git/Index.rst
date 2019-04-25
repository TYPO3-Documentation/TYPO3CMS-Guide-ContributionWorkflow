.. include:: ../../Includes.txt

.. highlight:: bash

.. _Setting-up-your-Git-environment:

===============================
Setting up your Git environment
===============================

These steps will walk you through your basic Git setup when working with TYPO3.

Prerequisites
=============

* If you want to get an introduction to how our workflow works, :ref:`head over here<workflow-explained>`
* We expect you have a fully-fledged web development setup at hand. If you are not sure, though, :ref:`take a look here <prerequisites>`.
* Make sure, you have cloned the TYPO3 source as described previously in :ref:`setup-typo3-git-clone`::

      git clone git://git.typo3.org/Packages/TYPO3.CMS.git .
      composer install


Set username and email
======================

You need to instruct git to work with your name and email address. Make sure the email address and user name are the same as those you used when
:ref:`setting up your TYPO3 account<TYPO3Account>`::

   git config user.name "Your Name"
   git config user.email "your-email@example.com"

Set autosetuprebase
===================

In order to avoid weird merges in your local repository when pulling in new commits from typo3.org, we encourage everybody
to set the autosetuprebase option, such that your local commits are always rebased on top of the official code::

   git config branch.autosetuprebase remote


.. _setup-git-commit-hook:
.. _git-setup-commit-msg-hook:

Install Your Commit Hooks
=========================

There are two git hooks available for TYPO3 development:

* :ref:`commit-msg-hook`: mandatory
* :ref:`pre-commit-hook`: optional, currently not available for Windows

To set them up, do the following:

commit-msg Hook
---------------

Activate the hook by copying the sample file to :file:`.git/hooks/commit-msg`::

   # ensure folder exists
   mkdir -p .git/hooks

   # copy
   cp Build/git-hooks/commit-msg .git/hooks/commit-msg

   # make executable
   chmod +x .git/hooks/commit-msg

.. note::

   You usually do not need the `mkdir` or the `chmod`. It does not do any harm to
   execute it in any case though.

More information: :ref:`commit-msg-hook`


pre-commit Hook
---------------

The pre-commit hook runs on Linux and MacOS. It is not required for core development.

Activate the hook by copying the sample file to :file:`.git/hooks/pre-commit`::

   # ensure folder exists
   mkdir -p .git/hooks

   # copy
   cp Build/git-hooks/unix+mac/pre-commit .git/hooks/

   # make executable
   chmod +x .git/hooks/pre-commit

More information: :ref:`pre-commit-hook`


Alternative: Setup With Composer
--------------------------------

As an alternative for copying the hook scripts manually, you can use the following composer command:

For Linux / MacOS::

   composer gerrit:setup

This will "install" the :file:`commit-msg` hook and :file:`pre-commit` hook.

More information: :ref:`custom-composer-commands`.

Setting up your remote
======================

You must instruct Git to push to Gerrit_ instead of the original repository. It acts as a kind of facade in front of Git::

   git config url."ssh://<YOUR_TYPO3_USERNAME>@review.typo3.org:29418".pushInsteadOf git://git.typo3.org



.. _committemplate:

Setting up a Commit Message Template
====================================

This is optional! If you do not wish to setup a commit message template,
continue with the next step:  :ref:`forger-index`.

If you follow these instructions, whenever you create a new commit,
Git will use the template to create the commit message, which you can
then modify in your editor. So use this, to make it easier for you to
fill out the required information.

First, create a file, for example in :file:`~/.gitmessage.txt`.

.. code-block:: none

   [BUGFIX|TASK|FEATURE]

   Resolves: #
   Releases: master, 9.5

Make Git use this file as a template for the commit message::

   git config commit.template ~/.gitmessage.txt


For additional information about how to write a proper commit message
see :ref:`commitmessage`.

Show Configuration
==================

Show current configuration::

  git config -l


Other resources
===============

See :ref:`git cheat sheet <cheat-sheet-git>` for more git commands.

We have compiled a list of more information for you in the :ref:`Appendix<appendix>` section.
