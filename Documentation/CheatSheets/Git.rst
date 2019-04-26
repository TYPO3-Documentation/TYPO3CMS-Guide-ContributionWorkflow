.. include:: ../Includes.txt

.. highlight:: bash

.. _cheat-sheet-git:

====================================
Git Cheat Sheet for Core Development
====================================

This is a short list of commands. If you are not familiar with the
workflow yet, make sure you follow the link at the beginning of
each section and read the detailed description.

The following commands assume you are in the working directory of the TYPO3 core repository.

.. _cheat-sheet-git-clone:

git clone
=========

Clone latest master into current directory::

   git clone git://git.typo3.org/Packages/TYPO3.CMS.git .

.. _cheat-sheet-git-setup:

Setup
=====

For detailed setup instructions, please see: :ref:`Setting-up-your-Git-environment`

Workflow - common commands
==========================

For details see :ref:`Fixing-a-bug-A-Z`

Reset repo to last remote commit in (remote) master::

   git reset --hard origin/master && git pull origin master

Stage and commit all changes::

   git commit -a

Is the same as::

   git add .
   git commit

Stage and commit all changes to already existing commit::

   git commit -a --amend

Push changes to remote master on gerrit (default method)::

   git push origin HEAD:refs/for/master

.. note::
   Pushing to `refs/publish` is deprecated, we now push to `refs/for`.


Workflow - drafts
=================

Push changes to remote master on gerrit as **draft**::

   git push origin HEAD:refs/drafts/master


*When pushing as draft, the pushed patch will only be visible to you
and those who you add as a reviewer. It also does not start any
automated tests or builds on the TYPO3 testing infrastructure.*

.. _cheat-sheet-git-other-branches:

Workflow -other branches
========================

Show all branches::

   git branch -a

Checkout 9.5 branch::

   git checkout 9.5

Checkout 8.7 branch::

   git checkout TYPO3_8-7


.. important::
   Pushing to a branch other than master only makes sense if the bug only
   exists on that branch and does not exist on master. Backporting of a
   fix to a branch is done by the core team member who merges the original
   fix to the master branch.


Long story short: In most cases, **push to master**. The rest is being taken
care of by core team members!

Push 9.5 branch::

   git push origin HEAD:refs/for/9.5

Push 8.7 branch::

   git push origin HEAD:refs/for/TYPO3_8-7

Push 7.6 branch::

   git push origin HEAD:refs/for/TYPO3_7-6


Workflow - commit msg
=====================

Details: :ref:`commitmessage`

Example commit message for a bugfix:

.. code-block:: text

   [BUGFIX] Subject line

   Description

   Resolves: #12345
   Releases: master, 9.5

Other keywords:

.. code-block:: text

   [BUGFIX]
   [FEATURE]
   [DOCS]
   [TASK]
   [!!!][FEATURE]
   [WIP][TASK]

* subject < 52 chars
* other lines <= 72 chars


Workflow - Undoing / fixing things
==================================

Throw away all changes since last commit::

   git reset HEAD --hard

Unstage a file (remove file from index, but keep in working dir)::

   git reset <path>

Change author for last commit::

   git commit --amend --author "Some Name <some@email>"


Squash last 2 commits:

   This is very handy, in case you accidentally created a new commit
   instead of adding to an existing commit (with `git commit --amend`).

   * All changes have been committed or stashed
   * Run the following command:

   ::

      git rebase -i HEAD~2

   * In the editor, replace 'pick' with 'squash' in the line describing the latest commit


References
==========

See also these not TYPO3 specific cheat sheets for git if you are not very familiar with git:

* `cheat sheet for git
  <https://services.github.com/on-demand/downloads/github-git-cheat-sheet/>`__
* `"git - the simple guide" by Roger Dudler <http://rogerdudler.github.io/git-guide/>`__
