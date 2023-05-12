.. include:: /Includes.rst.txt

.. highlight:: bash



.. index::
   single: Code Contribution Workflow; Git Setup
   single: Tools; Git
   single: Git; Setup
   single: Setup; Git

.. _Setting-up-your-Git-environment:

=========
Git Setup
=========

.. note::

   If you are working on a previously cloned, older repository, you can skip
   this page but may need to make the following changes to your Git setup:

   *  :ref:`migrate-master-main`
   *  :ref:`migrateToGithub`

These steps will walk you through your basic Git setup when working with TYPO3.

.. index::
   single: Code Contribution Workflow; git clone
   single: git; git clone

.. _setup-typo3-git-clone:
.. _git-clone:

git clone
=========

Create a directory for your TYPO3 core installation and change into it, e.g.:

.. code-block:: bash
   :caption: shell command

   mkdir /var/www/t3coredev
   cd /var/www/t3coredev

Clone the TYPO3 CMS core repository:

.. code-block:: bash
   :caption: shell command

   git clone git@github.com:typo3/typo3 .



.. index::
   single: Code Contribution Workflow; git setup username and email
   single: Git Setup; username and email

.. _set-username-and-email:

Set Username and Email
======================

*-- required* (unless this is already setup globally, see `git config --global -l`)

You need to instruct git to work with your name and email address. Make sure the email address and user name are the same as those you used when
:ref:`setting up your TYPO3 account<TYPO3Account>`:

.. code-block:: bash
   :caption: shell command


   git config user.name "Your Name"
   git config user.email "your-email@example.org"



.. index::
   single: Code Contribution Workflow; git setup rebase
   single: Git Setup; rebase

.. _set-autosetuprebase:

Set autosetuprebase
===================

*-- required*

In order to avoid weird merges in your local repository when pulling in new commits from typo3.org, we encourage everybody
to set the autosetuprebase option, such that your local commits are always rebased on top of the official code:

.. code-block:: bash
   :caption: shell command

   git config branch.autosetuprebase remote


.. index::
   single: Code Contribution Workflow; Git Hooks
   single: Git Setup; Git Hooks
   single: Setup; Git Hooks

.. _setup-git-commit-hook:
.. _git-setup-commit-msg-hook:


Install Your Commit Hooks
=========================

There are two git hooks available for TYPO3 development:

* :ref:`commit-msg-hook`: required
* :ref:`pre-commit-hook`: optional, currently not available for Windows

To set them up, do the following:

commit-msg Hook
---------------

*-- required*

Activate the hook by copying the sample file to :file:`.git/hooks/commit-msg`:

.. code-block:: bash
   :caption: shell command

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

*-- optional*

The pre-commit hook runs on Linux and MacOS. To use the pre-commit hook on Windows you can use a tool like the `Git BASH <https://gitforwindows.org/>`__.

Activate the hook by copying the sample file to :file:`.git/hooks/pre-commit`:

.. code-block:: bash
   :caption: shell command

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

For Linux / MacOS:

.. code-block:: bash
   :caption: shell command

   composer gerrit:setup

This will "install" the :file:`commit-msg` hook and :file:`pre-commit` hook.

More information: :ref:`custom-composer-commands`.



.. index::
   single: Code Contribution Workflow; git setup remote

.. _git-setup-remote:

Setting up Your Remote
======================

*-- required*

You must instruct Git to push to Gerrit_ instead of the original repository. It acts as a kind of facade in front of Git:

.. code-block:: bash
   :caption: shell command

   git config remote.origin.pushurl ssh://<YOUR_TYPO3_USERNAME>@review.typo3.org:29418/Packages/TYPO3.CMS.git


This will instruct Git to push using the
`refs/for namespace <https://gerrit-review.googlesource.com/Documentation/concept-refs-for-namespace.html>`__
when you do `git push`:

.. code-block:: bash
   :caption: shell command

   git config remote.origin.push +refs/heads/main:refs/for/main


.. index::
   single: Code Contribution Workflow; Commit Message Template
   single: Git Setup; Commit Message Template

.. _committemplate:

Setting up a Commit Message Template
====================================

*-- optional*

If you follow these instructions, whenever you create a new commit,
Git will use the template to create the commit message, which you can
then modify in your editor. So use this, to make it easier for you to
fill out the required information.

First, create a file, for example :file:`~/.gitmessage.txt`.

.. code-block:: text
   :caption: ~/.gitmessage.txt

   [BUGFIX|TASK|FEATURE]

   Resolves: #
   Releases: main, 12.4

Make Git use this file as a template for the commit message:

.. code-block:: bash
   :caption: shell command

   git config commit.template ~/.gitmessage.txt


For additional information about how to write a proper commit message
see :ref:`commitmessage`.


.. _git-show-config:

Show Configuration
==================

*-- optional*

Show current configuration:

.. code-block:: bash
   :caption: shell command

   git config -l

The result should look like this:

.. code-block:: none
   :caption: result

   ...
   remote.origin.url=git@github.com:typo3/typo3
   remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
   branch.main.remote=origin
   branch.main.merge=refs/heads/main
   branch.autosetuprebase=remote
   remote.origin.pushurl=ssh://<YOUR_TYPO3_USERNAME>@review.typo3.org:29418/Packages/TYPO3.CMS.git
   commit.template=/path/to/.gitmessage.txt
   ...

Or, compare the :file:`.git/config` file inside the repository:

.. code-block:: ini
   :caption: .git/config

    [core]
       repositoryformatversion = 0
       filemode = true
       bare = false
       logallrefupdates = true
    [remote "origin"]
        url = git@github.com:typo3/typo3
        fetch = +refs/heads/*:refs/remotes/origin/*
        pushurl = ssh://<TYPO3_USER_NAME>@review.typo3.org:29418/Packages/TYPO3.CMS.git
    [branch "main"]
       remote = origin
       merge = refs/heads/main
    [branch]
       autosetuprebase = remote
    [commit]
       template = /path/to/.gitmessage.txt


Other resources
===============

* :ref:`Troubleshooting`
* See :ref:`git cheat sheet <cheat-sheet-git>` for more git commands.
* We have compiled a list of more information for you in the :ref:`Appendix<appendix>` section.
