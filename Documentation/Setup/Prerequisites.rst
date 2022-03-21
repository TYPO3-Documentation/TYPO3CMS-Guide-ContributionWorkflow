.. include:: /Includes.rst.txt

.. highlight:: bash

.. _prerequisites:

==============================
Prerequisites and Useful Tools
==============================

.. note::

   If you are using DDEV to setup your TYPO3 installation, it is not necessary to install
   the tools locally (e.g. Composer, yarn). They will be supplied by DDEV and you can run
   them inside the container.

   In that case you can skip right to :ref:`DDEV <settting-up-typo3-with-ddev>`.

Here's a list of the tools we use in the TYPO3 project:


* :ref:`Composer <prerequisites-composer>`
* :ref:`Yarn <prerequisites-yarn>`
* :ref:`Grunt <prerequisites-grunt>`


If some of these are new for you, take a few minutes to read up about what they
do for us. Maybe they prove useful in your everyday work as well.
You can find installation tutorials in the :ref:`Appendix <appendix>` section.



.. index::
   single: Tools; Composer

.. _prerequisites-composer:

Composer
========

*-- required (depends)*

If you use a container solution, such as DDEV, you can run composer install from inside
the container, see :ref:`composer-install`.


.. sidebar:: Composer

   You can learn a lot more about composer on their website https://getcomposer.org/.
   Also, look at :ref:`composer` in the Appendix for some
   information specific to the TYPO3 core contribution toolchain.

Composer is a dependency manager for PHP.

Follow the
installation instructions from https://getcomposer.org. Afterwards, you should
have a working executable `composer` available.

Verify composer is working::

   $ composer --version

Setting up Your Frontend Build Toolchain.
=========================================

*-- required (depends)*

Yarn and Grunt are not required for setting up a working TYPO3 installation. You
will need them however if you plan to create patches which require changing frontend
files. See :ref:`yarn build <yarn-build>` for more information on this.



.. index::
   single: Tools; Yarn

.. _prerequisites-yarn:

Yarn
----

TYPO3 itself does not need yarn to run, but yarn is something similar to composer, but for the world outside of PHP.
We will be mainly using yarn to get helpful tools like Grunt and Bower.

Install on MacOS
~~~~~~~~~~~~~~~~

1. install the packagemanager homebrew::

      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

2. install yarn::

      brew install yarn


Installer for Windows and MacOS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Go to https://yarnpkg.com/lang/en/docs/install/#windows-tab

2. Download the package and install


Linux
~~~~~

1. Go to https://yarnpkg.com/lang/en/docs/install/#linux-tab

2. Download the package and install

For additional infos see https://yarnpkg.com


Install all Required Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The later section :ref:`yarn-build` will explain how to set
everything up in your TYPO3 working directory.



.. index::
   single: Tools; Grunt

.. _prerequisites-grunt:

Grunt
=====

.. sidebar:: Grunt

   You can learn more about Grunt on their website http://gruntjs.com/.

Grunt is a JavaScript-based task runner. While this does not sound very expressive at first this is basically, what grunt
does - it runs tasks for us.

In our case grunt compiles CSS, minifies and concatenates JavaScript files, runs syntax checks and a couple of
other useful things. The good news is that TYPO3 comes with a predefined set of tasks that grunt will run, so you don't
have to take care of all the busywork underneath.
