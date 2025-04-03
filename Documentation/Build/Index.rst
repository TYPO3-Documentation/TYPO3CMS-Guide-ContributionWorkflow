.. include:: /Includes.rst.txt

.. highlight:: bash

.. index::
   single: Code Contribution Workflow; Build
   single: Build
   single: SCSS
   single: TypeScript
.. _build:

===============
Building assets
===============

This page explains building assets like JavaScript and CSS files.

For the most part, the TypeScript, JavaScript and SCSS sources are contained in
:file:`Build/Sources`. These are compiled to target files, usually located in:

* CSS: :file:`typo3/sysext/*/Resources/Public/Css`
* JavaScript: :file:`typo3/sysext/*/Resources/Public/JavaScript`

If you make changes to the source files, you can build locally using
:ref:`runTests.sh <runTests_sh>`:

.. code-block:: bash

   Build/Scripts/runTests.sh -s build

Note you can also use `npm` + `nvm` locally, if you are proficient with setting this up locally.

It is also possible to lint the files locally:

.. code-block:: bash

   Build/Scripts/runTests.sh -s lintScss
   Build/Scripts/runTests.sh -s lintTypescript

Remember to commit the compiled files alongside any patches, they are part
of the monorepo.
