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
requirements for the current main branch on the `Download TYPO3 <https://typo3.org/download/>`__
page.

You will need to set up the prerequisites for your operating system. Look at the following for guidance:

* :ref:`setting-up-typo3-manually-linux`


Clone TYPO3
===========

Create a clone of git as described in :ref:`git-clone`, run :ref:`composer-install` and
optionally :ref:`yarn-build`.


::

   git clone git@github.com:typo3/typo3 .
   composer install



Create the database
===================

We are assuming your are using MySQL 8.0 and the database should be called t3coredev and you will
access it with username `typo3` and password `somepassword` from localhost.

::

   mysql> CREATE DATABASE t3coredev CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;
   mysql> CREATE USER `typo3`@`localhost` identified by `somepassword`;
   mysql> GRANT ALL ON t3coredev.* TO `typo3`@`localhost`;

.. note::

   For MySQL versions lower than 8.0 or MariaDB use the collation utf8mb4_general_ci.

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
