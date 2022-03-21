.. include:: /Includes.rst.txt

.. index::
   single: Gerrit; Submit a Change
   single: Submit a Change

.. _coreMergers-review:

===============================
Review a patch as a Core Merger
===============================

.. include:: /_includes/CoreMergers.rst.txt

Please see :ref:`reviewPatch` for general information on how to review a
patch.

.. figure:: /Images/External/Gerrit/CoreMergers/VoteCoreMerger.png
   :class: with-shadow

   Vote by clicking the :guilabel:`Reply` button


.. _Gerrit-Vote-plus-1:

Voting +1
=========

.. _Gerrit-Practical-considerations:

Practical considerations
------------------------

The Core Merger who gave an early +1 should try and go back to
transform the +1 into a +2
after a second review came in, if applicable.

Each newly pushed patch requires a complete new round of voting before it can
be submitted. So everyone that reviewed once is invited to re-vote as soon as
a new patch is pushed. Using Gerrit's Patch History feature allows to quickly
see what has changed from the already reviewed patch to the new one.

Consider these rules when comparing patches:

*  If the patch was re-pushed due to the comments, check the diff between the
   versions of the patch.
*  If the patch needed to be rebased onto current main, the change set might
   contain the changes due to rebasing. So better check the diff between base
   and most recent version in this case.

.. _Gerrit-Vote-plus-2:

Voting +2
=========

.. figure:: /Images/External/Gerrit/CoreMergers/Vote-plus-2.png
   :class: with-shadow

Ready to merge
--------------

A Core Merger can give a +2 vote on *Code Review* and *Verified* if
there is already a positive vote by another Core Merger.

.. _Gerrit-No-brainers:
.. _Gerrit-Low-brainers:

Low brainers
-------------

A Core Merger can give a +2 and submit right away in case of "low-brainers"
(what used to be called "FYI").

A Core Merger can give a +2 and wait a bit before submitting
(used to be called "FYI24", "FYI48", ...).

.. _Gerrit-Vote-minus-2:

Voting -2
=========

.. figure:: /Images/External/Gerrit/CoreMergers/Vote-minus-2.png
   :class: with-shadow

A :guilabel:`-2` vote by a Core Merger blocks a patch from merging.
In contrast to -1, a -2 is a **veto**. Use with care. With a -2, you
are taking responsibility of the patch and basically stating that it will not
be done until you actively remove your negative vote.

To date, we have had no real problem with someone giving -2 and then
not acting responsibly. It would be great if it stays this way.
