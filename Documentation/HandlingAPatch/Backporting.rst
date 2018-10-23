.. include:: ../Includes.txt

.. _lifeOfAPatch-backport:

===================================
Backport a change to other branches
===================================

.. note::

   This is an informative section targeted towards members of the core team only.


First wait until the review process was successfully completed for the most recent affected branch.

Use Gerrit for the cherry-pick
==============================

First try to use the Gerrit cherry-pick feature for automatic backporting.

.. image:: _assets/gerrit_cherrypick_1.png
   :width: 400px

In the following modal, you can easily select the branch, you want to cherry pick to, by just typing partial information.

.. image:: _assets/gerrit_cherrypick_2.png
   :width: 400px

Remove from the commit message everything below the Change-ID because the information about former reviewers is not needed
for the cherry pick. Make sure that you **don't alter the Change-ID** but remove every line (also empty ones) below it. After doing so hit the "Cherry Pick Change" button.

.. image:: _assets/gerrit_cherrypick_3.png
   :width: 400px

Manual backport
===============

If the automatic backporting fails, you need to manually cherry-pick the patch to the target branch. (e.g. cherry-pick the
master patch onto your local (up to date) TYPO3_6-2 branch) You will most likely need to adjust the code for the older branch.

Edit the commit message to comply to the guidelines again. (e.g. remove the Reviewed-* and Tested-* lines added by Gerrit)
**Keep the Change-Id though!**

Push the review back to Gerrit.

On Gerrit the original patch will show the cherry-pick as a related patch.