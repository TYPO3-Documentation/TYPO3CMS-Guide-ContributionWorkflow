.. include:: /Includes.rst.txt

.. index::
   single: Code Contribution Workflow; Finding Reviews

.. _Find-a-review:

=======================
Find a review on Gerrit
=======================

For finding an existing review (patch), there are several possibilities. Use whatever
is most convenient for you or what fits your needs.

.. index::
   single: Tools; Forger Finding Reviews
   single: Review; Finding Reviews

.. _forger_reviews:

Forger
======

In any case, you can use `Forger <https://forger.typo3.com>`__ to
search for the review.

Examples:

* select `Reviews : All <https://forger.typo3.com/gerrit/status>`__
  to view and filter for reviews
* `Sprints Reviews <https://forger.typo3.com/sprint/reviews>`__
  to see a board
  of all open patches by type (Bugs, Tasks, Features)

.. image:: /Images/External/Forger/forger-review-board.svg
   :class: with-shadow

* `Sprints TYPO3-Core <https://forger.typo3.com/sprint/core>`__
  to see a board
  of all open core issues by type (Next patchlevel, Regressions)


Email notification
==================

If you are in any way involved in the review (e.g. you are author,
reviewer or you made changes), you will get a notification about
it to your email address. The notification contains a link.



.. index::
   single: Tools; Gerrit Your Changes
   single: Review; Own Changes

.. _gerrit-your-changes:

Gerrit: Your Changes
====================

For your own patches, go to `Gerrit <https://review.typo3.org>`__
and select Your: Changes.

.. image:: /Images/External/Gerrit/HandlingAPatch/gerrit-your-patches.png
   :class: with-shadow



.. index::
   single: Tools; Gerrit Open Changes
   single: Review; Open Changes

.. _gerrit-open-changes:

Gerrit: Open Changes
====================

Select `Changes : Open <https://review.typo3.org/q/status:open>`__ to
get the latest changes or changes with recent modifications.



.. index::
   single: Tools; Gerrit Search
   single: Review; Search

.. _gerrit-search:

Gerrit: Search
==============

Or use the search box on `Gerrit <https://review.typo3.org>`__

GitHub: Links to Gerrit
=======================

Each commit to the TYPO3 Git repository comes with some metadata
linking issue and patch reviews, for example:

..  code-block::

   [TASK] Provide PSR-7 Request in PolicyMutatedEvent
   
   For additional context does the PolicyMutatedEvent
   now provide the current PSR-7 Request.

   Resolves: #104141
   Releases: main, 12.4
   Change-Id: I1817366e77f20f6c43eef0ee209fbb419e7237e2
   Reviewed-on: https://review.typo3.org/c/Packages/TYPO3.CMS/+/84913
   Tested-by: Lorem Ipsum <example@example.com>
   Reviewed-by: Lorem Ipsum <example@example.com>
   Tested-by: core-ci <typo3@example.com>

The line `Resolves` contains the Forge issue id.
The line `Reviewed-on` contains the link to the gerrit patch.

Forge
=====

Once a patch has been pushed for an issue, the corresponding issue
on `Forge <https://forge.typo3.org>`__ will contain comments with the
topic "Updated by Gerrit Code Review ..." and a link to the review on Gerrit.
