.. include:: ../Includes.txt

.. _rebase:

======
Rebase
======


.. include:: ../_includes/NewPageInfo.rst.txt

.. _rebase-intro:

What is rebase?
===============

Simply speaking, git reapplies commits on top of another
base tip (as explained in the
`Pro Git book <https://git-scm.com/docs/git-rebase>`__).

When you start your patch, it will be based on a specific
commit. Meanwhile, other commits are merged and the TYPO3 codebase
changes. Your patch will still be based on an older version
of the source.


.. code-block:: none

   remote | local | commits
   ------------------------

     +                 x : latest commit
     |
     |
     +                 d
     |
     +                 c
     |       +         b : your commit
     |       |
     +--------         a : parent of your commit
     |
     +

When you rebase, your change, will be **reapplied** to a
different commit (typically the latest one) and your patch
will be based on the latest version.

There are other applications for rebase (e.g. squash commits),
but this is the one relevant for the TYPO3 Contribution Workflow, so
this is what we mean when we talk about rebase.

Do not let information on the Web confuse you: Usually
it is assumed that someone is working on a different branch
(feature branch). In our commit model, we always work on one
branch (master) and we only create one commit for a change.

.. _when-should-you-rebase:

When should you rebase?
=======================

When you are working on a patch, you can regularly rebase
in order to get the latest changes.

You can also do it before you run tests and push your change.

In fact, it is good practice to do this!


.. _how-to-rebase:

How do you rebase?
==================


The following assumes, there are not yet any merge conflicts. If
there are merge conflicts, you must resolve them as you rebase
/ merge / cherry-pick. See the section :ref:`resolve-merge-conflicts`.

.. _rebase-with-gerrit-button:

Method 1: Use Rebase button on Gerrit
-------------------------------------

**Prerequisites:**

  If you have already pushed your change to Gerrit, you can use the
  Rebase button.

  This is only possible, if there are not yet any merge conflicts.

**Do it:**

   Load your patch in the browser, click on "Rebase" and then
   "Rebase on top of the master branch".



.. _rebase-with-git-pull:

Method 2: git pull --rebase
---------------------------

This is a command-line method. You can do this regularly while
working on your patch.

**Prerequisites:**

   This command assumes, you are currently working on your patch
   in your local git repository and you have a clean working
   directory, meaning you committed your changes.

**Do it:**

   ::

      git pull --rebase origin master

   (which is the pull command you already know, with the
   additional option `--rebase`.)

   or

   ::

      git fetch
      git rebase origin/master

**What does it do:**

  From the manpage: "... rebase the current branch on top of the
  upstream branch after fetching." (upstream is origin/master)

   Remember, git pull (internally) does a `git fetch` and then `git merge`.
   With this command, git does a `git fetch` and then a `git rebase`
   using the upstream branch (latest master branch).

**More information:**

   * `StackOverflow: Difference between git pull and git pull --rebase
     <https://stackoverflow.com/questions/18930527/difference-between-git-pull-and-git-pull-rebase>`__



