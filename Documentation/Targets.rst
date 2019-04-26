:orphan:
.. include:: Includes.txt

.. _linktargets:

===========
Linktargets
===========

This page is only relevant for documentation contributors editing or linking
to this manual.

This section :ref:`Targets-for-Cross-Referencing` lists all the
link targets in this manual. The link targets can be used for
linking from this manual or from other manuals.

How to Link With Intersphinx Mechanism
======================================

If you place a `.. _This-is-ABC:` in front of a headline,
you are defining a linktarget that you can later link to
(from the same manual)::

   :ref:`This-is-ABC`


If you link from another manual, you need to prepend the
shortcut for this manual, e.g. `t3contribute`::

   :ref:`t3contribute:This-is-ABC`

For this to work, you must define the intersphinx shortcut
in the file :ref:`Settings.cfg <h2document:settings-cfg>`
in the manual you are linking from, e.g.:

.. code-block:: none

   [intersphinx_mapping]

   t3contribute     = https://docs.typo3.org/typo3cms/ContributionWorkflowGuide/

More information: :ref:`About Intersphinx
<h2document:intersphinx>` and :ref:`h2document:cheat-sheet-intersphinx`
in "ReST & Sphinx Cheat Sheet".

.. _Targets-for-Cross-Referencing:

Labels for Cross-Referencing
============================

.. ref-targets-list::

