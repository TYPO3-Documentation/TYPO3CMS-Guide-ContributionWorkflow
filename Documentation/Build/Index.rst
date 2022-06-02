. include:: /Includes.rst.txt

.. highlight:: bash

.. index::
   single: Code Contribution Workflow; Build
   single: Build
   single: SCSS
   single: TypeScript
.. _build:

=====
Build
=====

This page explains building JavaScript and CSS files.

For the most part, the TypeScript, JavaScript and SCSS sources are contained in
:file:`Build/Sources`. These are converted into target files, usually located in:

* CSS: :file:`typo3/sysext/*/Resources/Public/Css`
* JavaScript: :file:`typo3/sysext/*/Resources/Public/JavaScript`

If you make changes to the source files, you can build locally using
:ref:`runTests.sh <runTests_sh>`:

.. code-block:: bash

   Build/Scripts/runTests.sh -s buildCss
   Build/Scripts/runTests.sh -s buildJavascript

It is also possible to lint the files locally:

.. code-block:: bash

   Build/Scripts/runTests.sh -s lintScss
   Build/Scripts/runTests.sh -s lintTypescript
