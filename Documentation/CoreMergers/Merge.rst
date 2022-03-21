.. include:: /Includes.rst.txt

.. index::
   single: Gerrit; Submit a Change
   single: Submit a Change

.. _coreMergers-merge:
.. _lifeOfAPatch-Merging-Patches:

==============
Merge patches
==============

.. include:: /_includes/CoreMergers.rst.txt


.. _lifeOfAPatch-Merging-Patches-Prerequisites:

The merging process
===================


.. rst-class:: bignums-xxl

#. Prerequisites

   A patch can only be merged if it has received a :ref:`+ 2<Gerrit-Vote-plus-2>`
   vote from a Core Merger. A :guilabel:`+2` can be given by the second
   Core Merger to review the patch positively.

   Merging gets blocked by a :guilabel:`-2` vote.

#. Submit the patch

   You can merge by clicking the :guilabel:`Submit` button. The Core Merger
   to merge the patch also has to do
   the :ref:`Backporting <coreMergers-backport>` if the submit-message requests
   for a backport.

   .. figure:: /Images/External/Gerrit/CoreMergers/Merging1.png
      :class: with-shadow

      The :guilabel:`Submit` button on a patch in status :guilabel:`Ready
      to submit`.

#. The patch is successfully merged

   When the merging is successful, the Change looks like this:

   .. figure:: /Images/External/Gerrit/CoreMergers/Merging2.png
      :class: with-shadow

      The patch in status :guilabel:`Merged`.

#. Backport if necessary

   If required in the commit message, do the
   :ref:`backport <coreMergers-backport>` next.

#. How to revert a submitted change

   There is a :guilabel:`Revert` button available now. Please stick to the
   :ref:`revert workflow<coreMergers-revert>` if reverting a change should
   become necessary.
