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


Set username and email
======================

You need to instruct git to work with your name and email address. Make sure the email address is the one you used when
:ref:`setting up your TYPO3 account<TYPO3Account>`::

   git config user.name "Your Name"
   git config user.email "your-email@example.com"

By default, git config sets the local configuration (same as using `--local` option for `git config`), meaning the configuration will be written to the configuration file in your repository (.git/config). If your name and email address is already set in your global git settings (in your home directory, e.g. `~/.gitconfig`) and is the same as the one for typo3.org / gerrit, you don't have to explicitly do this for each repository.

Check your git configuration::

    git config -l


Set autosetuprebase
===================

In order to avoid weird merges in your local repository when pulling in new commits from typo3.org, we encourage everybody
to set the autosetuprebase option, such that your local commits are always rebased on top of the official code::

   git config branch.autosetuprebase remote


.. _setup-git-commit-hook:

Install your commit hooks
=========================

.. _git-setup-commit-msg-hook:

commit-msg hook
---------------

.. important::
   The commit-msg hook is mandatory. It must be installed before you commit
   your changes. The hook will not prevent you from committing. It will
   complain about a messed up commit message, though. In case you forgot
   to write a correct commit message, you can always amend your last commit
   message to correct it.


Activate the hook::

   # ensure folder exists
   mkdir -p .git/hooks

   # copy
   cp Build/git-hooks/commit-msg .git/hooks/commit-msg

   # make executable
   chmod +x .git/hooks/commit-msg

.. note::
   You do not need the mkdir unless the .git/hooks directory doesn't exist. 
   It does not do any harm to execute it in any case though. 

You can read about the why and where of this hook :ref:`here <appendix-commit-hook>`.


.. _git-setup-precommithook:

pre-commit hook
---------------

.. important::
   The pre-commit hook is not supported on Windows.

.. note::
   The pre-commit hook is optional. It is not required for creating commits,
   but it will assist you in detecting problems with not correctly formatted
   files which will later cause the automatic tests to fail.

Again, you can copy the pre-commit hook from the build directory. This is not
available prior to the 8.7 branch::

   # ensure folder exists
   mkdir -p .git/hooks

   # copy
   cp Build/git-hooks/unix+mac/pre-commit .git/hooks/

   # make executable
   chmod +x .git/hooks/pre-commit

The pre-commit hook will check that all PHP files that will be committed
conform to the TYPO3 Coding Guidelines. If this is not the case, the
hook will display an error message. It will not automatically repair
any files though. You must do this yourself and afterwards amend your
commit::

   git commit -a --amend

There are scripts available for fixing Coding Guideline issues, see :ref:`cgl-fix-my-commit`.


Setting up your remote
======================

You must instruct Git to push to Gerrit_ instead of the original repository. It acts as a kind of facade in front of Git::

   git config url."ssh://<YOUR_TYPO3_USERNAME>@review.typo3.org:29418".pushInsteadOf git://git.typo3.org


Other resources
===============

See :ref:`git cheat sheet <cheat-sheet-git>` for more git commands.

We have compiled a list of more information for you in the :ref:`Appendix<appendix>` section.
