.. include:: /Includes.rst.txt

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

You have cloned the TYPO3 git repository as described in :ref:`git-clone` and
are in the directory which contains the local Git repository:

.. code-block:: shell
    :caption: shell command

    cd /var/www/t3coredev

Create the database
===================

We are assuming you are using MySQL 8.0 and the database should be called t3coredev and you will
access it with username `typo3` and password `somepassword` from localhost.

..  code-block:: sql
    :caption: database command

    mysql> CREATE DATABASE t3coredev CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;
    mysql> CREATE USER `typo3`@`localhost` identified by `somepassword`;
    mysql> GRANT ALL ON t3coredev.* TO `typo3`@`localhost`;

.. note::

   For MySQL versions lower than 8.0 or MariaDB use the collation utf8mb4_general_ci.

Create FIRST_INSTALL
====================

.. code-block:: shell
    :caption: shell command in /var/www/t3coredev

    touch FIRST_INSTALL


Installation wizard
===================

You can now access the TYPO3 installation wizard by loading the page in the
browser with the configured URL, e.g. http://t3coredev. This should redirect
to http://t3coredev/typo3/install.php.

Follow the instructions of the installation wizard.
