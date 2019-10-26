.. include:: ../Includes.txt

.. highlight:: bash

.. _cherry-pick-a-patch:

.. index::
   single: Code Contribution Workflow; Cherry pick a patch
   single: Git; Cherry pick a patch

===================
Cherry-pick a patch
===================

In order to test a patch or make additional changes on it, you will need
to cherry-pick it from the review-system into your local git repository.


.. important::

   Make sure to always get the latest patch set of the current review. You can check this by looking at the **Patch Sets**
   menu left of the **Download Button**. The left and right numbers should always be the same, so you know you picked the
   latest patch set. You can also click on **Go to latest patch set**.


.. rst-class:: bignums-xxl

1. Find the review on Gerrit

   see :ref:`Find-a-review`

2. Select the latest patchset and click download

   .. image:: _assets/gerrit-go-to-latest-patchset.png
      :class: with-shadow

   .. image:: _assets/gerrit-download.png
      :class: with-shadow

3. Click on copy next to the line for "Cherry pick"

   This copies the command to the clipboard.

   .. image:: _assets/gerrit-cherry-pick.png
      :class: with-shadow

4. Clean up your local repository

   .. code-block:: bash

      git reset --hard origin/master
      git pull

5. Execute the command (git cherry-pick)

   In your shell, paste the copied command and execute it. Example::

      git fetch https://review.typo3.org/Packages/TYPO3.CMS refs/changes/47/56947/11 && git cherry-pick FETCH_HEAD

6. Cleanup your TYPO3 installation

   Depending on the changes made by the patch, you may have to apply some changes
   to your TYPO3 installation: see :ref:`cleanup-typo3`.

