.. include:: ../Includes.txt

.. highlight:: bash

.. index::
   single: Git; Git Cheat Sheet
   single: Cheat Sheets; Git Cheat Sheet

.. _cheat-sheet-git:

===============
Git Cheat Sheet
===============

This is a short list of commands. If you are not familiar with the
workflow yet, make sure you follow the link at the beginning of
each section and read the detailed description.

The following commands assume you are in the working directory of the TYPO3 core repository.

.. _cheat-sheet-git-clone:

git clone
=========

Clone TYPO3 CMS Git repository into current directory::

   git clone git@github.com:typo3/typo3 .

.. _cheat-sheet-git-setup:

Setup
=====

For detailed setup instructions, please see: :ref:`Setting-up-your-Git-environment`

Workflow - common commands
==========================

For details see :ref:`Fixing-a-bug-A-Z`

Reset repo to last remote commit in (remote) main branch::

   git reset --hard origin/main && git pull origin main

Stage and commit all changes::

   git commit -a

Is the same as::

   git add .
   git commit

Stage and commit all changes to already existing commit::

   git commit -a --amend

Push changes to remote main branch on gerrit (default method)::

   git push

This assumes, you have correctly configured your remote as described in
:ref:`git-setup-remote`. If not, you must explicitly push using the
`refs/for namespace <https://gerrit-review.googlesource.com/Documentation/concept-refs-for-namespace.html>`__::

   git push origin HEAD:refs/for/main

.. note::
   Pushing to `refs/publish` is deprecated, we now push to `refs/for`.

.. _git-work-in-progress:

Workflow - work in progress
===========================

In case you want to push a "Work in progress", use the following instead::

      git push origin HEAD:refs/for/main%wip

You can also configure Gerrit to always mark your pushes as WIP. In order to do this
head over to https://review.typo3.org/settings/ and configure "Set new
changes" to "work in progress" by default".

See: https://gerrit-review.googlesource.com/Documentation/user-upload.html#wip

.. _cheat-sheet-git-other-branches:

Workflow -other branches
========================

Show all branches::

   git branch -a

Checkout 10.4 branch::

   git checkout 10.4

Checkout 9.5 branch::

   git checkout 9.5


.. important::
   Pushing to a branch other than main only makes sense if the bug only
   exists on that branch and does not exist on main. Backporting of a
   fix to a branch is done by the core team member who merges the original
   fix to the main branch.


Long story short: In most cases, **push to main**. The rest is being taken
care of by core team members!

Push 10.4 branch::

   git push origin HEAD:refs/for/10.4

Push 9.5 branch::

   git push origin HEAD:refs/for/9.5


Workflow - commit msg
=====================

Details: :ref:`commitmessage`

Example commit message for a bugfix:

.. code-block:: text

   [BUGFIX] Subject line

   Description

   Resolves: #12345
   Releases: main, 10.4

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


Squash last 2 commits::

   git rebase -i HEAD~2

In the editor, replace 'pick' with 'squash' in the line describing the latest commit

This is very handy, in case you accidentally created a new commit
instead of adding to an existing commit (with `git commit --amend`). This way,
you can merge the last 2 commits and the commit messages.


References
==========

See also these not TYPO3 specific cheat sheets for git if you are not very familiar with git:

* `cheat sheet for git
  <https://services.github.com/on-demand/downloads/github-git-cheat-sheet/>`__
  (in several languages)
* `"git - the simple guide" by Roger Dudler <http://rogerdudler.github.io/git-guide/>`__
* `"Oh, shit, git!" by Katie Sylor-Miller <https://ohshitgit.com/>`__ is basically a cheat sheet for Git, but
  focuses mostly on fixing things that went wrong.

To learn more about the internal working of Git, check out these resources:

* `Git Internals in the Pro Git book <https://git-scm.com/book/en/v1/Git-Internals>`__
