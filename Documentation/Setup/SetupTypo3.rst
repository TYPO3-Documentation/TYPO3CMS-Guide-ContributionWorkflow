.. include:: ../Includes.txt

.. highlight:: bash


.. _setup-typo3:

============================
Setup the TYPO3 installation
============================

.. _git-clone:

git clone
=========

Switch into your **empty** htdocs directory of choice and clone a fresh master of TYPO3. Run ``composer install`` after that::

   git clone git://git.typo3.org/Packages/TYPO3.CMS.git .


If you rather like to work with your favorite Git GUI, we compiled a list of the ones used throughout the core team
here.

* :ref:`SourceTree on Windows<windows-clonewithsourcetree>`
* SourceTree on OSX
* :ref:`Git Tower on OSX<gittower-osx>`
* :ref:`GitKraken <https://www.gitkraken.com>`

.. _composer-install:

composer install
================

::

   composer install

.. _yarn-build:

yarn install
============

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
