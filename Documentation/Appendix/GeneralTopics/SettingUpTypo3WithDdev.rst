.. include:: ../../Includes.txt

.. highlight:: bash

.. _ddev:

==========================
Setting up TYPO3 with DDEV
==========================

`Ddev <https://ddev.readthedocs.io>`__ provides several pre-configured
development environments based on Docker. You can use an existing
TYPO3 environment and adapt it to your needs.

Here is a description of how you can use DDEV to setup a working TYPO3
installation using the cloned master.

You don't need to have a Webserver or Database running on your system.
Everything will be supplied by ddev. In fact, if you do have a Webserver
or Database running on your machine, make sure there are no conflicts.
You can change the default ports ddev uses (e.g. port 80 / 443 for Webserver)
in `.ddev/config.yaml` before you start it.

Setting up the prerequisites
============================

You will need to install docker and other `System requirements <https://ddev.readthedocs.io/en/latest/#system-requirements>`__.

Then install ddev as described in the `Installation <https://ddev.readthedocs.io/en/latest/#installation>` instructions.

clone TYPO3
===========

Change to the directory, where your TYPO3 installation should exist and
clone the TYPO3 repository as described in :ref:`setup-typo3`.

::

   git clone git://git.typo3.org/Packages/TYPO3.CMS.git .
   composer install
   cd Build
   yarn install
   yarn build
   cd ..


Configure ddev
==============


::

   ddev config


Now edit the configuration file `.ddev/config.yaml` and make sure you
change the PHP version to the required version (in TYPO3 9 master
this is PHP 7.2).

::

   php_version: "7.2"

Start ddev
==========

::

   ddev start


Check for database credentials
==============================

Let ddev dump information:

::

   ddev describe

You will need username, password, Database name, host and port of the
MySQL credentials to setup your TYPO3 installation, e.g.

::

   MySQL Credentials
   -----------------
   Username:     	db
   Password:     	db
   Database name:	db
   Host:         	db
   Port:         	3306

FIRST_INSTALL
=============

Now, create a file `FIRST_INSTALL`:

::

   touch FIRST_INSTALL


Setup your TYPO3 installation
=============================

Now load the URL as shown by `ddev start` in your browser with the path
`/typo3` appended to it. Typically this will be
http://ddev.dev.local/typo3.

You will now be guided through the basic installation steps by TYPO3.


