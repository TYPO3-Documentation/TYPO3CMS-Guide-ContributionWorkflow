.. include:: ../Includes.txt

.. highlight:: bash

.. _cheat-sheet-git:

==========================================
git cheat sheet for Core development
==========================================

.. attention::
   This is a short list of commands. If you are not familiar with the
   workflow yet, make sure you follow the link at the beginning of 
   each section and read the detailed description.

See also this general `cheat sheet for git 
<https://services.github.com/on-demand/downloads/github-git-cheat-sheet/>`__
if you are not very familiar with git. 

git clone
=========

Clone latest master into current directory::

   git clone git://git.typo3.org/Packages/TYPO3.CMS.git .

.. _cheat-sheet-git-setup:

Setup
=====

Details: :ref:`Setting-up-your-Git-environment`

.. attention::

   The following commands assume you are in the working directory of the TYPO3
   core repository.

Set username and email in repository configuration (implicit --local)::

   git config user.name "Your Name"
   git config user.email "your-email@example.com"

Set autosetuprebase::

   git config branch.autosetuprebase remote

Copy commit-msg hook::

   cp Build/git-hooks/commit-msg .git/hooks/commit-msg

Push to gerrit

* **replace** `<YOUR_TYPO3_USERNAME>` with your Gerrit / typo3.org user name!

::

   git config url."ssh://<YOUR_TYPO3_USERNAME>@review.typo3.org:29418".pushInsteadOf git://git.typo3.org

Optional: Set a commit message template::

   git config commit.template ~/.gitmessage.txt

This command uses the file ~/.gitmessage.txt as git message tepmlate. 
For additional information about how to set up a proper gitmessage 
see :ref:`committemplate`

Workflow - common commands
==========================

For details see :ref:`Bugfixing-Commit-and-push`

Change to directory with .git for this to work.

Reset repo to last remote commit in master::

   git reset --hard origin/master && git pull origin master

Stage and commit all changes::

   git commit -a

or::

   git add .
   git commit

Stage and commit all changes to already existing commit::

   git commit -a --amend

Push changes to remote master on gerrit::

   git push origin HEAD:refs/publish/master

Workflow - commit msg
=====================

Details: :ref:`commitmessage`

Example commit message for a bugfix::

   [BUGFIX] Subject line
   
   Description

   Resolves: #12345
   Releases: master, 8.7

Other keywords::

   [BUGFIX]
   [FEATURE]
   [DOCS]
   [TASK]
   [!!!][FEATURE]
   [WIP][TASK]

* subject < 52 chars
* other lines <= 72 chars


Workflow - other branches
=========================

Show all branches::

   git branch -a

Checkout 8.7 branch::

   git checkout TYPO3_8-7

Push 8.7 branch::

   git push origin HEAD:refs/publish/TYPO3_8-7

Push 7.6 branch::

   git push origin HEAD:refs/publish/TYPO3_7-6

Workflow - Undoing / fixing things
==================================

Throw away all changes since last commit::

   git reset HEAD --hard

Unstage a file (remove file from index, but keep in working dir)::

   git reset <path>

Change author for last commit::

   git commit --amend --author "Some Name <some@email>"
