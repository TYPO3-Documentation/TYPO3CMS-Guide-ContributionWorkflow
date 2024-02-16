.. include:: /Includes.rst.txt

.. index::
   single: CGL
   single: Coding Guidelines

.. _appendix-cgl:

=================
Coding Guidelines
=================

More information is found in the :ref:`Coding Guidelines <t3coreapi:cgl>`
section of the "TYPO3 Explained" manual (formerly known as "Core API").

This is just a very brief overview.


PHP
===

Make sure you are using the correct PHP codestyle. It is based on
the `TYPO3 Coding Standards <https://github.com/TYPO3/coding-standards>`__,
(which follows PER-CS1.0 / PSR-12 and transition into PER-CS2.0
at the time of this writing), and covered in the
:ref:`TYPO3 Coding Guidelines <t3coreapi:cgl>`.

See :ref:`PhpStorm setup: CGL <phpstorm-setup-cgl>` for information on how
to configure the correct coding style.

The Appendix contains information on scripts to check / fix coding
guideline issues: :ref:`cgl-fix-my-commit`

JavaScript
==========

The following rules should be applied for JavaScript:
`Airbnb JavaScript Style Guide <https://github.com/airbnb/javascript>`__


TypeScript
==========

The following rules should be applied for TypeScript:
`Excel Micro TypeScript Style Guide <https://github.com/excelmicro/typescript>`__.

Xliff files
===========

Language files are usually stored in a Folder Resources/Private/Language
in files with the ending *.xlf*. While no tabs are allowed to indent
in PHP files, you should edit Xliff files using tabs.

