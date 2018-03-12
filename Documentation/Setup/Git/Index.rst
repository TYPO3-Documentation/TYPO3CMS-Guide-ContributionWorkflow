.. include:: ../../Includes.txt

.. highlight:: bash

.. _git-setup:

===============================
Setting up your Git environment
===============================

.. toctree::
   :maxdepth: 1

   CommitMessageFormat

These steps will walk you through your basic Git setup when working with TYPO3.


.. tip::

   If you want to get an introduction to how our workflow works, :ref:`head over here<workflow-explained>`

.. note::

   We expect you have a fully-fledged web development setup at hand.

   If you are not sure, though, :ref:`take a look here <prerequisites>`.


Make sure, you have cloned the TYPO3 source as described previously.


::

      git clone git://git.typo3.org/Packages/TYPO3.CMS.git .

Add your TYPO3.org account to your git configuration
====================================================

You need to instruct git to work with your name and email address. Make sure the email address is the one you used when
:ref:`setting up your TYPO3 account<TYPO3Account>`.


::

   git config user.name "Your Name"
   git config user.email "your-email@example.com"


In order to avoid weird merges in your local repository when pulling in new commits from typo3.org, we encourage everybody
to set the autosetuprebase option, such that your local commits are always rebased on top of the official code::

   git config branch.autosetuprebase remote

.. _commit-hook:

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


Make sure that the directory .git/hooks exists first:

::

   mkdir .git/hooks


::

   cp Build/git-hooks/commit-msg .git/hooks/commit-msg
   chmod +x .git/hooks/commit-msg


You can read about the why and where of this hook :ref:`here<appendix-commit-hook>`.

pre-commit hook
---------------

Again, you can copy the pre-commit hook from the build directory. This is not
available prior to the 8.7 branch.

.. note::
   The pre-commit hook is optional. It is not required for creating commits,
   but it will assist you in detecting problems with not correctly formatted
   files which will later cause the automatic tests to fail.


::

   cp Build/git-hooks/unix+mac/pre-commit .git/hooks/
   chmod +x .git/hooks/pre-commit


The pre-commit hook will check that all PHP files that will be committed
conform to the TYPO3 Coding Guidelines. If this is not the case, the
hook will display an error message. It will not automatically repair
any files though. You must do this yourself and afterwards amend your
commit:

::

   git commit -a --amend


.. important::
   The pre-commit hook is not supported on Windows.


There are scripts available for fixing Coding Guideline issues, see :ref:`cgl-fix-my-commit`.


Setting up your remote
======================

You can instruct Git to push to Gerrit_ instead of the original repository. It acts as a kind of facade in front of Git::

   git config url."ssh://<YOUR_TYPO3_USERNAME>@review.typo3.org:29418".pushInsteadOf git://git.typo3.org


Other resources
===============

We have compiled a list of helpful examples for you in the :ref:`Appendix<appendix>` section.
