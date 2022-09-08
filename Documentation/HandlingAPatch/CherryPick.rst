.. include:: /Includes.rst.txt

.. highlight:: bash

.. index::
   single: Code Contribution Workflow; Cherry pick a patch
   single: Git; Cherry pick a patch

.. _cherry-pick-a-patch:

===================
Cherry-pick a patch
===================

In order to test a patch or make additional changes on it, you will need
to cherry-pick it from the review system into your local git repository.


.. important::

   Make sure to always get the latest patch set of the current review.
   You can check this by looking at the **Patch Sets** menu left of the
   :guilabel:`Download` button. If the link :guilabel:`Go to latest patch set`
   is not shown, you know you picked the latest patch set.


.. rst-class:: bignums-xxl

1. Find the review on Gerrit

   see :ref:`Find-a-review`

2. Select the latest patchset and click download

   If the recent patchset is not shown, select it first:

   .. image:: /Images/External/Gerrit/HandlingAPatch/gerrit-go-to-latest-patchset.png
      :class: with-shadow

   Then click on :guilabel:`Download`:

   .. image:: /Images/External/Gerrit/HandlingAPatch/gerrit-download.png
      :class: with-shadow

3. Click on copy next to the line for "Cherry pick"

   This copies the command to the clipboard.

   .. image:: /Images/External/Gerrit/HandlingAPatch/gerrit-cherry-pick.png
      :class: with-shadow

4. Clean up your local repository

   Save your local changes beforehand, if you have any.
   
   .. code-block:: bash

      git stash save 'comment-your-changes'

   .. code-block:: bash

      git reset --hard origin/main
      git pull

5. Execute the command (git cherry-pick)

   In your shell, paste the copied command and execute it. Example::

      git fetch https://review.typo3.org/Packages/TYPO3.CMS refs/changes/47/56947/11 && git cherry-pick FETCH_HEAD

6. Cleanup your TYPO3 installation

   Depending on the changes made by the patch, you may have to apply some changes
   to your TYPO3 installation: see :ref:`cleanup-typo3`.

