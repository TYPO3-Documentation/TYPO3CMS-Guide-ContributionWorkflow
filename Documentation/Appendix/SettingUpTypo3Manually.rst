.. include:: ../Includes.txt

.. highlight:: bash

.. _setting-up-typo3-manually:

=========================
Setting up TYPO3 manually
=========================

Prerequisites
=============

You will need a Webserver, PHP and database on your system. Look at the page `System requirements
<https://typo3.org/typo3-cms/overview/requirements/>`__ and also check out the specific system
requirements for the current master branch on the `Download TYPO3 <https://typo3.org/download/>`__
page.

You will need to set up the prerequisites for your operating system. Look at the following for guidance:

* :ref:`setting-up-typo3-manually-linux`


Clone TYPO3
===========

Create a clone of git as described in :ref:`git-clone`, run :ref:`composer-install` and
optionally :ref:`yarn-build`.


::

   git clone git://git.typo3.org/Packages/TYPO3.CMS.git .
   composer install



Create the database
===================

We are assuming, the database should be called t3coredev and you will
access it with username `typo3` and password `somepassword` from localhost.

::

   mysql> CREATE DATABASE t3coredev CHARACTER SET utf8 COLLATE utf8_general_ci;
   mysql> CREATE USER `typo3`@`localhost` identified by `somepassword`;
   mysql> GRANT ALL ON t3coredev.* TO `typo3`@`localhost`;

Create FIRST_INSTALL
====================

In your htdocs directory:

::

   touch FIRST_INSTALL


Continue ...
============

You can now access the TYPO3 installation wizard by going to, e.g.
http://t3coredev/typo3/. Follow the instructions of the installation
wizard.
