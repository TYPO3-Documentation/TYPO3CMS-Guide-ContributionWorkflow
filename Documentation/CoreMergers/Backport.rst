.. include:: ../Includes.txt

.. index::
   single: Gerrit; Backport a Change
   single: Backport a Change

.. _coreMergers-backport:
.. _lifeOfAPatch-backport:


=================
Backport a Change
=================

.. include:: /_includes/CoreMergers.rst.txt


Before you start, wait until the review process has been successfully completed for the most
recent affected branch.

Use Gerrit for the cherry-pick
==============================

First try to use the Gerrit cherry-pick feature for automatic backporting.

.. rst-class:: bignums-xxl

#. Cherry pick into a branch

   .. figure:: /Images/External/Gerrit/CoreMergers/Backport1.png
      :class: with-shadow

      Cherry picking via Gerrit

#. Choose branch and adjust commit message

   In the following modal, you can select the branch to backport. Existing
   branches are shown by autocomplete.

   Remove from the commit message everything below the Change-ID because the
   information about former reviewers is not needed for the cherry pick. Make sure
   that you **don't alter the Change-ID** but remove every line (also empty ones)
   below it. After doing so hit the :guilabel:`Cherry Pick` button.


   .. figure:: /Images/External/Gerrit/CoreMergers/Backport2.png
      :class: with-shadow

      Adjust the commit message and click :guilabel:`Cherry Pick`

#. Review backport patch

   This creates a new Change on Gerrit that needs to be reviewed and
   merged once more.

   .. figure:: /Images/External/Gerrit/CoreMergers/Backport3.png
      :class: with-shadow

      A new change based on another branch is created. It has the status
      "Active" once more.

#. Merge the backport

   If the backport is a :ref:`Low brainer <Gerrit-low-brainers>` you can vote
   :guilabel:`+2` and continue to merge the backport. Otherwise it should be
   reviewed by at least one other Core Merger.


   .. figure::  /Images/External/Gerrit/CoreMergers/Backport4.png
      :class: with-shadow

      Merging the backport

Manual backport
===============

If the automatic backport fails, you need to manually cherry-pick the patch to the target branch. (e.g. cherry-pick the
master patch onto your local (up to date) 10.4 branch) You will most likely need to adjust the code for the older branch.

Edit the commit message to comply to the guidelines again. (e.g. remove the Reviewed-* and Tested-* lines added by Gerrit)

.. important::
   The Change-Id must be left unchanged, otherwise Gerrit is not able to link the backport to its original change!

Push the review back to Gerrit.

On Gerrit the original patch will show the cherry-pick as a related patch.
