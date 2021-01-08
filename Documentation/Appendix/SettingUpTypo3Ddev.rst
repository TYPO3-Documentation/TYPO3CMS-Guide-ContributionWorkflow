.. include:: ../Includes.txt

.. highlight:: bash


.. index::
   single: DDEV
   single: Setup; DDEV

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

You will need to install Docker and other
`ddev system requirements <https://ddev.readthedocs.io/en/latest/#system-requirements>`__.

Then install DDEV as described in the
`Installation <https://ddev.readthedocs.io/en/latest/#installation>`__
instructions.

.. note::

   Composer and yarn can run inside of DDEV, so there is no need to set them up locally.


Clone TYPO3
===========

Create a clone of the TYPO3 git repository as described in :ref:`git-clone`::

   mkdir t3master
   cd t3master
   git clone git://git.typo3.org/Packages/TYPO3.CMS.git .



Configure DDEV
==============

For the master branch ddev v1.16.5 or later is suggested to have the correct setup included.

::

   ddev config

DDEV should suggest the correct defaults and you just need to press ENTER::

   > Project name (t3master):

   > Docroot Location (current directory):

   > Found a typo3 codebase at /var/www/t3master.
   > Project Type [backdrop, drupal6, drupal7, drupal8, drupal9, laravel, magento, magento2, php, typo3, wordpress] (typo3):


In order to be able to use composer inside ddev, edit the configuration file `.ddev/config.yaml`::

   composer_version: "2"


Start DDEV
==========

::

   ddev start
   
DDEV should now show a URL under which the site can be reached::

   > TYPO3 does not seem to have been set up yet, missing LocalConfiguration.php (/var/www/t3master/typo3conf/LocalConfiguration.php)
   > Generating AdditionalConfiguration.php file for database connection.
   > Successfully started t3master
   > Project can be reached at http://t3master.ddev.site http://127.0.0.1:32773

Ignore the warning about missing :file:`LocalConfiguration.php` for now, we will take
care of that below.

.. _ddev-composer-install:

Install dependencies via composer
=================================

This runs inside the container and thus uses your configured Composer version::

   ddev composer install


It is not necessary for the initial build, but once you change some assets (e.g.
Typescript, SCSS files), you should build with yarn. You might like to try this
now::

   ddev exec "cd Build && yarn install"
   ddev exec "cd Build && yarn build"

The first command is required once, the second (build) command is required after
every change of a resource file.

.. seealso::

   * `Using Developer Tools with DDEV-Local <https://ddev.readthedocs.io/en/stable/users/developer-tools/>`__


DDEV describe
=============

Let DDEV dump information::

   ddev describe

You may need some of this later.

FIRST_INSTALL
=============

Create a file `FIRST_INSTALL`::

   touch FIRST_INSTALL


Setup your TYPO3 installation
=============================

Now load the URL as shown by `ddev start` or `ddev describe` in your browser, e.g.
http://t3master.ddev.site.

You will now be guided through the basic installation steps by TYPO3.

.. tip::

   If you use the HTTPS url you may get a "Privacy error" or something similar from your browser.
   You will need to get your browser to ignore this warning (e.g. `Advanced:Proceed to t3master.ddev.local
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

- :ref:`Setting-up-your-Git-environment`.


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
