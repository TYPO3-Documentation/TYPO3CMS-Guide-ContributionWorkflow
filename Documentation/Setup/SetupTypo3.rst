.. include:: ../Includes.txt

.. highlight:: bash

.. _setup-typo3:

============================
Setup the TYPO3 installation
============================


.. important::

   If you are setting TYPO3 up with DDEV, you can skip this page and jump straight to

   .. rst-class:: horizbuttons-primary-m

   - :ref:`ddev`

.. index::
   single: Code Contribution Workflow; git clone

.. _setup-typo3-git-clone:
.. _git-clone:

git clone
=========

Switch into your **empty** htdocs directory of choice and clone a fresh master of TYPO3:: 

   git clone git://github.com/typo3/typo3 .


.. _git-guis:

Git GUIs
========

If you rather like to work with your favorite Git GUI, we compiled a list of the ones used throughout the core team
here.

* :ref:`SourceTree on Windows<windows-clonewithsourcetree>`
* SourceTree on OSX
* :ref:`Git Tower on OSX<gittower-osx>`
* `GitKraken <https://www.gitkraken.com>`__





.. index::
   single: Code Contribution Workflow; composer install

.. _composer-install:

composer install
================

*-- required* (unless run `composer install` from container solution, such as DDEV,
see :ref:`composer-install`)

.. tip::

   If you plan to use a Docker based container solution for setting up your
   TYPO3 installation (for example using :ref:`DDEV <ddev>`),
   you can perform the step `composer install` later and let it run
   :ref:`inside your Docker container <ddev-composer-install>`.

Information about :ref:`setting up Composer <prerequisites-composer>` is found in previous chapter.

Composer cannot detect the TYPO3 version of your cloned project because there is none. Before you run 
`composer install` you need to export the `COMPOSER_ROOT_VERSION environment variable <https://getcomposer.org/doc/03-cli.md#composer-root-version>`__.
Here you need to set a full version string matching the TYPO3 version of your clone.

Example::

   # cd <cloned project>
   export COMPOSER_ROOT_VERSION=11.0.0

Run composer install in the same directory you cloned the master repository to.
This may take several minutes::

   # cd <cloned project>
   composer install



.. index::
   single: Code Contribution Workflow; yarn install

.. _yarn-build:

yarn install
============

.. tip::

   This step is not necessary to setup a working environment. You may however
   want to test this step because you might be needing it later if you make
   changes in the frontend SCSS or TypeScript files in :file:`Build/Sources`.
   If not, skip to :ref:`setup-typo3-installation`.

Go to the `Build` folder of your TYPO3 install root directory.
Install all dependencies with `yarn install`.
Wait for the the end of the install progress.
Type `yarn build` for the build process.

::

   cd Build
   yarn install
   yarn build
   cd ..


.. _yarn-tasks:

yarn tasks
----------

The following is a list of available build targets (see package.json for an
up-to-date list). You will only be needing these if you want to do something
specific. Usually, it should suffice to use `yarn install` and `yarn build`.

-   `yarn build` - Compile everything.
-   `yarn build-css` - Compile SCSS to CSS.
-   `yarn lint` -  Test your SCSS and ts files.
-   `yarn build-js` - Compile JavaScript.
-   `yarn format` - Resolve Style issues.
-   `yarn update` - Update dependencies (Use this if you are **really** sure what you're doing).

.. _setup-typo3-installation:

Setting up a Working TYPO3 Installation
=======================================

You will now need to use your git clone to setup a working installation
of TYPO3. There are many different ways how you can do this. We
provide a few examples in the Appendix:

* :ref:`ddev`
* :ref:`setting-up-typo3-manually`
