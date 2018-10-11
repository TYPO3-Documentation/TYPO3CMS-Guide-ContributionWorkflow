.. include:: ../Includes.txt

.. _rebase:

========================
Rebase & Merge conflicts
========================

.. important::

   This page is work in progress. It is not complete, and
   not all information here has yet been verified.

   Please help to make it better by clicking "Edit me on
   GitHub" and adding your changes.

   For more information, see :ref:`h2document:docs-contribute`.


Occasionally, if your patch has been pushed to Gerrit a while
ago and has not been merged yet, you may be asked to rebase.

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

When you rebase, your changes, will be **reapplied** to a
different commit (typically the latest one) and your patch
will be based on the latest version.

There are other applications for rebase (e.g. squash commits),
but this is the one relevant for the Contribution Guide, so
this is what we mean when we talk about rebase.

Do not let information on the internet confuse you: Usually
it is assumed that someone is working on a different branch
(feature branch). In our commit model, we always work on one
branch (master). See :ref:`workflow-explained` to recapitulate.

When should you rebase?
=======================

In case of merge conflicts
--------------------------

If your patch has merge conflicts. Gerrit as well as Forger will
show you:

**Gerrit:** Load your patch page in the browser.

.. image:: _assets/gerrit_merge_conflict.png
   :class: box-shadow


**Forger:** Open one of the `ReviewSprint <https://forger.typo3.com/sprint/reviews>`__
views on Forger.

.. image:: _assets/forger_merge_conflicts.png
   :class: box-shadow


Regularly
---------

When you are working on a patch, you can regularly rebase
in order to get the lastest changes.

How do you rebase?
==================

Method 1: git pull --rebase
---------------------------

The simplest method, if there are not yet any merge conflicts:

If you are already working on your patch, meaning your latest
commit is your patch commit and your working directory is clean::

   git pull --rebase


Remember, git pull usually does a `git fetch` and then `git merge`. With this command,
you will do a `git fetch` and then a rebase.


Method 2: Rebase on parent and resolve merge conflicts
------------------------------------------------------

If there are already merge conflicts, and even cherry-picking the patch
is not possible because of errors, try the following:

.. rst-class:: bignums

1. Reset to a clean state (make sure you saved your work first!)

   .. code-block:: bash

      git reset --hard origin/master
      git pull

2. Fetch the change


   Perform the copy-pasted command from Gerrit without the cherry-pick part), e.g.

   .. code-block:: bash

      git fetch https://review.typo3.org/Packages/TYPO3.CMS refs/changes/70/PATCH-NUMBER/PATCHSET-NUMBER

3. Checkout parent (previous commit) of your patch (yes, the `^` is important!)

   .. code-block:: bash

      git reset --hard FETCH_HEAD^

4. Cherry pick the patch (onto the parent commit)

   .. code-block:: bash

      cherry-pick FETCH_HEAD

   If there were no errors or problems, you can continue.

5. Rebase

   .. code-block:: bash

      git fetch
      git rebase origin/master

6. If no merge conflicts, you are done.

7. If merge conflicts, resolve them.


   Your output should show you something like ...


   .. code-block:: none

      git rebase origin/master
      First, rewinding head to replay your work on top of it...
      Applying: [WIP][BUGFIX] Change datatype of hash fields in index_words table
      Using index info to reconstruct a base tree...
      M	typo3/sysext/indexed_search/Classes/Domain/Repository/IndexSearchRepository.php
      M	typo3/sysext/indexed_search/Classes/Indexer.php
      M	typo3/sysext/indexed_search/Classes/Utility/IndexedSearchUtility.php
      M	typo3/sysext/indexed_search/ext_tables.sql
      M	typo3/sysext/install/Classes/Updates/AbstractUpdate.php
      M	typo3/sysext/install/Classes/Updates/ExtensionManagerTables.php
      M	typo3/sysext/install/ext_localconf.php
      Falling back to patching base and 3-way merge...
      Auto-merging typo3/sysext/install/ext_localconf.php
      Auto-merging typo3/sysext/install/Classes/Updates/ExtensionManagerTables.php
      CONFLICT (content): Merge conflict in typo3/sysext/install/Classes/Updates/ExtensionManagerTables.php
      Auto-merging typo3/sysext/install/Classes/Updates/AbstractUpdate.php
      CONFLICT (content): Merge conflict in typo3/sysext/install/Classes/Updates/AbstractUpdate.php
      Auto-merging typo3/sysext/indexed_search/ext_tables.sql
      Auto-merging typo3/sysext/indexed_search/Classes/Utility/IndexedSearchUtility.php
      Auto-merging typo3/sysext/indexed_search/Classes/Indexer.php
      Auto-merging typo3/sysext/indexed_search/Classes/Domain/Repository/IndexSearchRepository.php
      error: Failed to merge in the changes.
      Patch failed at 0001 [WIP][BUGFIX] Change datatype of hash fields in index_words table
      Use 'git am --show-current-patch' to see the failed patch

      Resolve all conflicts manually, mark them as resolved with
      "git add/rm <conflicted_files>", then run "git rebase --continue".
      You can instead skip this commit: run "git rebase --skip".
      To abort and get back to the state before "git rebase", run "git rebase --abort".


   Relevant are the **CONFLICT** lines, you must resolve all conflicts
   (see :ref:`resolve-merge-conflicts` for these files
   and then do this for every file (as git has already told you to in the output):

   .. code-block:: bash

      git add <path as shown above>

8. Finally, do the rebase:

   .. code-block:: bash

      git rebase --continue

9. And, as usual (see :ref:`lifeOfAPatch-improve-patch`):

   .. code-block:: bash

      git commit --amend
      git push origin HEAD:refs/publish/master



.. _what-are-merge-conflicts:

What are merge conflicts?
=========================

Usually, git does a good job of merging several changes in one file.

However, there are occasions where git does not know what to do, because
one change *conflicts* with another.

You will always have several possibilities:

#. Use change 1

#. Use change 2

#. Use a combination which you manually combine.



Example
-------


Original file:

.. code-block:: none

   111
   222


Change 1

.. code-block:: none

   111
   aaa
   222

Change 2

.. code-block:: none

  111
  bbb
  222


Git cannot resolve this automatically, because it is ambigous. What should
the result be?

Result 1

.. code-block:: none

  111
  aaa
  bbb
  222


Result 2

.. code-block:: none

  111
  bbb
  aaa
  222


The merge conflict will show:

.. code-block:: none

   111
   <<<<<<< HEAD
   bbb
   =======
   aaa
   >>>>>>> aaa
   222



.. _resolve-merge-conflicts:

How to resolve merge conflicts?
===============================

If you see an output like this:

.. code-block:: none

   CONFLICT (content): Merge conflict in typo3/sysext/install/Classes/Updates/ExtensionManagerTables.php

You must resolve the conflict for all these files. There are several ways to do this.

Most editors or IDEs assist you in doing this. Check the information for your IDE.

If you want to do it manually, look for all occurences of `<<<<<<<`. These are markers. They are used
as follows (as in example above):

The merge conflict will show:

.. code-block:: none

   111
   <<<<<<< HEAD
   bbb
   =======
   aaa
   >>>>>>> aaa
   222

#. Beginning of conflict: `<<<<<<<`, after that name of branch for version 1 (here: HEAD)

#. Separation: `=======` Marks end of version1 and beginning of version2

#. End of conflict: `>>>>>>` and then name of branch version 2.


There may be more than one conflict in a file!

When you are done, add the file and then continue, e.g. if you were rebasing:

.. code-block:: bash

   git add <path1>
   git add <path2>
   git rebase --continue



