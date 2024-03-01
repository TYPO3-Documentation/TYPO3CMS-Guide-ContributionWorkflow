.. include:: /Includes.rst.txt

.. highlight:: bash


.. index::
   single: DDEV
   single: Setup; DDEV

.. _ddev:
.. _settting-up-typo3-with-ddev:

.. warning::

   This guide explains the setup of TYPO3 for the core contribution with DDEV.
   Follow the :ref:`quick installation guide <t3start:installation_index>`
   to install TYPO3 using Composer for a project.


=======================================
TYPO3 Core contribution setup with DDEV
=======================================

`DDEV <https://ddev.readthedocs.io>`__ provides several pre-configured
environments based on Docker.

Here is a description of how you can use DDEV to setup a working TYPO3
installation using the cloned TYPO3 CMS Git repository.

You don't need to have a Webserver, a Database or PHP running on your system.
Everything will be supplied by DDEV. In fact, if you do have a Webserver
or Database running on your machine, make sure there are no conflicts (e.g.
change the ports in the :ref:`ddev config <ddev-configure>`).

Prerequisites
=============

*  Install Docker and other
   `ddev system requirements <https://ddev.readthedocs.io/en/latest/#system-requirements>`__.

*  Install DDEV as described in the
   `Installation <https://ddev.readthedocs.io/en/latest/#installation>`__
   instructions.

.. note::

   Composer and npm can run inside of DDEV, so there is no need to set them up locally.

*  You have cloned the TYPO3 git repository as described in :ref:`git-clone` and
   have switched to the directory which contains the local Git repository.

.. _ddev-configure:

Configure DDEV
==============

For the TYPO3 CMS core latest (main branch) DDEV v1.16.5 or later is suggested to have the correct setup included

::

   ddev config

DDEV should suggest the correct defaults and you just need to press ENTER::

   > Project name (t3coredev):

   > Docroot Location (current directory):

   > Found a typo3 codebase at /var/www/t3coredev.
   > Project Type [backdrop, drupal6, drupal7, drupal8, drupal9, laravel, magento, magento2, php, typo3, wordpress] (typo3):

Change configuration
====================

In order to make further changes to the configuration, use ddev config as shown below
or edit the configuration file :file:`.ddev/config.yaml` manually.

.. code-block:: shell

    # Set correct PHP version:
    ddev config --php-version="8.2"

    # Add necessary packages for the npm build process,
    # (only needed if you are working on assets):
    ddev config --nodejs-version="18"
    ddev config --webimage-extra-packages="automake,build-essential"

Optionally, set a new HTTP/HTTPS port to avoid conflicts with local defaults.
Error message:
Failed to start t3coredev: Unable to listen on required ports, port 80 is already in use,

.. code-block:: yaml

   ddev config --router-http-port="8090"
   ddev config --router-https-port="8443"

Start DDEV
==========

.. code-block:: bash

   ddev start

DDEV should now show a URL under which the site can be reached::

   > TYPO3 does not seem to have been set up yet, missing LocalConfiguration.php (/var/www/t3coredev/typo3conf/LocalConfiguration.php)
   > Generating AdditionalConfiguration.php file for database connection.
   > Successfully started t3coredev
   > Project can be reached at http://t3coredev.ddev.site http://127.0.0.1:32773

Ignore the warning about missing :file:`LocalConfiguration.php` for now. We will take
care of that below.

.. _ddev-composer-install:

Build
=====

It is recommended to run tasks such as :bash:`composer install` etc. via the
:ref:`runTests.sh <runTests_sh>` script. We provide the direct commands in some
places - in case there is good reason to run the commands directly. But, if you
need the direct commands, you are encouraged to look them up
using the instructions in :ref:`run-tests-directly-without-docker`.

.. tabs::

   .. group-tab:: runTests.sh

      .. code-block:: bash

         Build/Scripts/runTests.sh -s composerInstall

   .. group-tab:: DDEV

      .. code-block:: bash

         ddev composer install


The following is not necessary for the initial build, but once you change some assets (for example
Typescript, SCSS files), you must build them. You might like to try this
now:

.. tabs::

   .. group-tab:: runTests.sh

      .. code-block:: bash

         Build/Scripts/runTests.sh -s buildCss
         Build/Scripts/runTests.sh -s buildJavascript

   .. group-tab:: DDEV

      .. code-block:: bash

         ddev exec "cd Build && npm ci"
         ddev exec "cd Build && npm run build"


The first command is required once, the second (build) command is required after
every change of a resource file.

Be aware that until TYPO3 v11.5 yarn was used.

.. seealso::

   * `Using Developer Tools with DDEV-Local <https://ddev.readthedocs.io/en/stable/users/basics/developer-tools/>`__


DDEV describe
=============

Let DDEV dump information:

.. code-block:: bash

   ddev describe

Displays information about the project, its URLs and access to phpMyAdmin, MailHog and the MySQL database.

FIRST_INSTALL
=============

Create a file `FIRST_INSTALL`:

.. code-block:: bash

   touch FIRST_INSTALL


Setup your TYPO3 installation
=============================

Now load the URL by running the command `ddev launch`.

You will now be guided through the basic installation steps by TYPO3.

.. tip::

   If you use the HTTPS url you may get a "Privacy error" or something similar from your browser.
   You will need to get your browser to ignore this warning (e.g. `Advanced:Proceed to t3coredev.ddev.local
   (unsafe)`, depends on browser).

   The warning is due to the fact that self-signed certificates are being used.

   If you are getting a `trustedHostsPattern` error on initial access, try accessing the HTTP domain first.

Additional setup
================

Be sure to add the .ddev directory to your local gitignore (e.g. :file:`.git/info/exclude`).

Shutdown DDEV
=============

When you are done you can do::

   ddev stop

For a list of commands see::

   ddev help

Next step
=========

If you are in the middle of setting up a TYPO3 installation for core development, continue with

.. rst-class:: horizbuttons-primary-m

- :ref:`after-setup-typo3`.


Resources
=========

Remember, you can use the Slack channels to ask for help! Follow the general convention for the channels: not too chatty, get straight to the point and ask, be nice. Register for the `TYPO3 slack workspace <https://forger.typo3.com/slack>`__ if you have not done so already.

Slack channels
--------------

* **#ddev**
* **#typo3-cms-coredev** : Only for core development, ask general TYPO3 support questions in **#typo3-cms**


DDEV documentation
------------------

* `Get Started with DDEV <https://ddev.com/get-started/>`__
* `DDEV System requirements <https://ddev.readthedocs.io/en/latest/#system-requirements>`__
* `General DDEV installation <https://ddev.readthedocs.io/en/latest/#installation>`__
* `DDEV TYPO3 Quickstart <https://ddev.readthedocs.io/en/stable/users/quickstart/#typo3>`__
* `DDEV commands <https://ddev.readthedocs.io/en/stable/users/basics/cli-usage/>`__


* `TYPO3 GmbH Blog post: DDEV adds support for TYPO3 CMS <https://typo3.com/blog/ddev-adds-support-for-typo3-cms/>`__
