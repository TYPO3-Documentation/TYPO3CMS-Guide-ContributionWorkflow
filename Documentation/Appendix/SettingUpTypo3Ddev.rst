.. include:: ../Includes.txt

.. highlight:: bash

.. _ddev:

.. _settting-up-typo3-with-ddev:

==========================
Setting up TYPO3 with DDEV
==========================

`DDEV <https://ddev.readthedocs.io>`__ provides several pre-configured
environments based on Docker.

Here is a description of how you can use DDEV to setup a working TYPO3
installation using the cloned master of the TYPO3 git repository.

You don't need to have a Webserver or Database running on your system.
Everything will be supplied by DDEV. In fact, if you do have a Webserver
or Database running on your machine, make sure there are no conflicts.
You can change the default ports DDEV uses (e.g. port 80 / 443 for Webserver)
in `.ddev/config.yaml` before you start it.

You can watch a video tutorial about setting up TYPO3 with DDEV, or go through steps outlined below.

.. youtube:: HZVMPoI9SIk


Setting up the prerequisites
============================

You will need to install docker and other
`ddev system requirements <https://ddev.readthedocs.io/en/latest/#system-requirements>`__.

Then install DDEV as described in the
`Installation <https://ddev.readthedocs.io/en/latest/#installation>`__
instructions.

In order to be able to build some assets (e.g. css, js files) you need to have `yarn` installed as `described here <https://yarnpkg.com/lang/en/docs/install/>`__.


Clone TYPO3
===========

Create a clone of the TYPO3 git repository as described in :ref:`git-clone`.


::

   mkdir t3master
   cd t3master
   git clone git://git.typo3.org/Packages/TYPO3.CMS.git .



Configure DDEV
==============


::

   ddev config


In order to change the PHP version, edit the configuration file `.ddev/config.yaml`. See supported version here: https://typo3.org/cms/roadmap/

::

   php_version: "7.3"

Start DDEV
==========

::

   ddev start
   

.. _ddev-composer-install:

Install dependencies via composer
=================================

This runs inside the container and thus uses your configured PHP version.

::

   ddev composer install



Check for database credentials
==============================

Let DDEV dump information:

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

.. hint::
   Creating FIRST_INSTALL is probably not necessary. Check to see if the database exists.
   ddev describe should give you enough information for that.

Now, create a file `FIRST_INSTALL`:

::

   touch FIRST_INSTALL


Setup your TYPO3 installation
=============================

Now load the URL as shown by `ddev start` in your browser with the path
`/typo3` appended to it. Typically this will be
http://t3master.ddev.local/typo3.

You will now be guided through the basic installation steps by TYPO3.

If you use the HTTPS url you may get a "Privacy error" or something similar from your browser. You will need to get your browser to ignore this warning (e.g. `Advanced:Proceed to t3master.ddev.local (unsafe)`, depends on browser).

The warning is due to the fact that self-signed certificates are being used.

If you are getting a `trustedHostsPattern` error on initial access, try accessing the HTTP domain first.

Additional setup
================

Be sure to add the .ddev directory to your local gitignore (e.g. :file:`.git/info/exclude`).

Shutdown DDEV
=============

When you are done you can do::

   ddev stop
   
or::   


   ddev remove

`ddev remove` does not remove the database. For a list of commands see::

   ddev help


.. hint::
   If you don't run "ddev stop" or "ddev remove" before shutting down or restarting docker
   the database might get corrupt and "ddev start" won't work anymore with the error::
      Failed to start <projectname>: db service health check timed out
   **keep in mind, this will remove your data entirely**

   try running::

      ddev remove --remove-data

   and::

      ddev start

   See https://github.com/drud/ddev/issues/748


Resources
=========

Remember, you can use the Slack channels to ask for help! Follow the general convention for the channels: not too chatty, get straight to the point and ask, be nice. Register for the `TYPO3 slack workspace <https://forger.typo3.com/slack>`__ if you have not done so already.

Slack channels
--------------

* **#ddev**
* **#typo3-cms-coredev** : Only for core development, ask general TYPO3 support questions in **#typo3-cms**


DDEV documentation
------------------

* `Get Started with DDEV <https://www.drud.com/get-started/>`__
* `DDEV System requirements <https://ddev.readthedocs.io/en/latest/#system-requirements>`__
* `General DDEV installation <https://ddev.readthedocs.io/en/latest/#installation>`__
* `DDEV TYPO3 Quickstart <https://ddev.readthedocs.io/en/latest/users/cli-usage/#typo3-quickstart>`__
* `DDEV commands <https://ddev.readthedocs.io/en/latest/users/cli-usage>`__


* `TYPO3 GmbH Blog post: DDEV adds support for TYPO3 CMS <https://typo3.com/blog/ddev-adds-support-for-typo3-cms/>`__
