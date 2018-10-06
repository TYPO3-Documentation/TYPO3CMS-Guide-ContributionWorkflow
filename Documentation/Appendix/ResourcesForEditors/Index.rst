.. include:: ../../Includes.txt

.. _resources-for-editors:

==================================
Information for editing this guide
==================================

Here, we list some resources that are useful when editing this manual:

General information
===================

* :ref:`h2document:start` (official guide)

Resources for this guide
========================

* :ref:`Linktargets <Linktargets>`  (labels for cross-referencing)
* `warnings.txt <https://docs.typo3.org/typo3cms/ContributionWorkflowGuide/_buildinfo/warnings.txt>`__
  (list of warnings)
* `Issues on Github <https://github.com/TYPO3-Documentation/TYPO3CMS-Guide-ContributionWorkflow/issues>`__

Best practices for editing this guide
=====================================

Images
------

Example: :ref:`GerritAccount`

Hints for creating images
~~~~~~~~~~~~~~~~~~~~~~~~~

Do not create huge fullscreen images. If an image contains too much information,
try to highlight the significant information by usinng boxes, text, numbers and / or
arrows in the image.

Add a white border inside the image if it helps the image to stand out from the text.

Hints for adding images
~~~~~~~~~~~~~~~~~~~~~~~

When adding images, always set a shadow in rest:

.. code-block:: rest

   .. image:: _assets/gerrit-new-ui2.png
      :class: with-shadow

If it helps with readability on screen, limit the size of the image.

