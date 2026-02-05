..  include:: /Includes.rst.txt

..  index::
    single: CGL
    single: Coding Guidelines

..  _appendix-cgl:

=================
Coding Guidelines
=================

More information is found in the :ref:`Coding Guidelines <t3coreapi:cgl>`
section of the "TYPO3 Explained" manual (formerly known as "Core API").

This is just a very brief overview.

..  _appendix-cgl-php:

PHP
===

Make sure you are using the correct PHP code style. It is based on
the `TYPO3 Coding Standards <https://github.com/TYPO3/coding-standards>`__,
(which follows PER-CS1.0 / PSR-12 and transition into PER-CS2.0
at the time of this writing), and covered in the
:ref:`TYPO3 Coding Guidelines <t3coreapi:cgl>`.

See :ref:`PhpStorm setup: CGL <phpstorm-setup-cgl>` for information on how
to configure the correct coding style.

The Appendix contains information on scripts to check / fix coding
guideline issues: :ref:`cgl-fix-my-commit`

Most PHP coding guidelines can be automatically applied with the command:

..  code-block:: bash

    Build/Scripts/runTests.sh -s cgl

..  _appendix-cgl-javascript:

JavaScript
==========

The following rules should be applied for JavaScript:
`Airbnb JavaScript Style Guide <https://github.com/airbnb/javascript>`__

..  _appendix-cgl-typescript:

TypeScript
==========

The following rules should be applied for TypeScript:
`Excel Micro TypeScript Style Guide <https://github.com/excelmicro/typescript>`__.

..  _appendix-cgl-xliff:

Xliff files
===========

Language files are usually stored in a Folder Resources/Private/Language
in files with the ending *.xlf*. Xliff files are indented using 2 spaces. 
The following command normalizes your XLIFF files:

..  code-block:: bash

    Build/Scripts/runTests.sh -s normalizeXliff
    
Please also check :ref:`common-review-checks-xlf` for Xliff-specific things
to pay attention to.

..  _appendix-cgl-xliff-filename:

XLIFF file naming
-----------------

XLIFF files have historically been named with file names starting with
`locallang_`. Newly introduced XLIFF files should drop the `locallang_`
prefix and only be named according to their purpose, for example
`clipboard.xlf` or `db/tt_content.xlf`. Newly introduced file
names should use **snake_case**.

TCA-related XLIFF files should either be called `db.xlf` or be stored in a
folder named `db`, for example `db/tt_content.xlf`.

..  _appendix-cgl-xliff-reference:

Label reference naming
----------------------

Newly introduced label references should use *snake case*. Different parts of a
label reference can be separated by dots, for example:

..  code-block:: xml

    <trans-unit id="my_field.title">
        <source>My title</source>
    </trans-unit>
    <trans-unit id="my_field.description">
        <source>My description</source>
    </trans-unit>

Existing labels should not be mass-changed to snake case, as each changed label
must be retranslated into all languages.

..  _appendix-cgl-xliff-domain-syntax:

Utilizing "translation domain syntax"
-------------------------------------

With `Feature: #93334 - Translation Domain Mapping <https://docs.typo3.org/permalink/changelog:feature-93334-1729000000>`_
and `Feature: #107759 - TranslateViewHelper supports translation domain syntax <https://docs.typo3.org/permalink/changelog:feature-107759-1729433323>`_
the label localization within fluid template files and PHP code can be
shortened:

..  code-block:: html

    <f:translate key="form.legend" domain="core.messages" />
    <f:translate key="module.title" domain="core.module" />

..  code-block:: php

    $languageService->sL('backend.toolbar:save');
    
This syntax is preferred and should be utilized for any new code committed
to TYPO3 v14+ because of these reasons:

*   It is shorter, easier to read, has no odd `LLL:EXT:` magic notation
*   Applies conventions of Symfony translation usage in other frameworks
*   Allows better automatic extraction and analysis (CLI commands)
*   Allows for better deprecations and usage analysis

Detailed reasons are found in the mentioned changelogs.
