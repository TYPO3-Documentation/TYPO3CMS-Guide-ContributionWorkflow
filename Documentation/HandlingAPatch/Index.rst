.. include:: ../Includes.txt

.. _lifeOfAPatch:
.. _improving-a-patch:

===================================
Handle and Improve a Patch (Gerrit)
===================================

.. note::

   This chapter assumes your environment is set up properly as described in
   :ref:`Contribution Walkthrough Environment Setup<setup>`


This chapter focuses on handling an existing patch, by reviewing it, modifying
it, reverting it etc. If you want to create a new patch, look at :ref:`Fixing-a-bug-A-Z`.


The code contribution workflow is based on patches and patchsets.
A patch can be updated multiple times, adding a new patchset on top.
Every patch contains a single commit. If changes are made to a patch, the already existing
commit is changed (:code:`git commit --amend`). How to do this is explained in
:ref:`lifeOfAPatch-improve-patch`

To make sure, every patch applied to the TYPO3 codebase meets highest standards,
every patch must be reviewed. Only after at least 2 people have tested the patch
and at least 2 people have verified it (one of them must be a member of the core team), can
the patch be merged (for more details on voting, see :ref:`gerrit-voting`.

Additionally, a suite of tests (unit, functional and acceptance) will
automatically run on every patch (set), the results being shown as a +1 or
-1 by typo3.com.




.. toctree::
   :titlesonly:

   GerritBasics
   FindAReview
   CherryPick
   CleanupTypo3
   ChangeAPatch
   Rebase
   ResolveMergeConflicts
   Review
   Backporting
   Revert

