.. include:: /Includes.rst.txt

.. highlight:: bash

.. index::
   single: Linux
   single: Setup; Linux

.. _setting-up-typo3-manually-linux:

=====================================
Setting up TYPO3 manually under Linux
=====================================

Prerequisites
=============

You will need a Webserver, PHP and database on your system. Look at the page `System requirements
<https://typo3.org/typo3-cms/overview/requirements/>`__ and check out the specific system
requirements for the current main branch on the `Download TYPO3 <https://typo3.org/download/>`__
page.

Just as a minimal example, this is a list of packages you might want to
install on a Debian flavored Linux system (e.g. Ubuntu).


.. important::
   This is a very simple, minimal setup. You might want to use Nginx instead or php-fpm with Apache.

Setup
=====

Apache Webserver
-----------------

::

   sudo apt-get install apache2
   sudo a2enmod deflate rewrite headers mime expires



PHP
---

.. note::

   You may have to add a PPA (ondrej/php) to get the latest PHP version. If
   you are not familiar with doing that, consider using :ref:`DDEV <ddev>`.

Install the latest PHP version for the core development branch (see
`composer.json <https://github.com/TYPO3/typo3/blob/main/composer.json>`__ in
TYPO3 repository on GitHub), including the required PHP extensions listed
in :ref:`System requirements <t3start:system-requirements>`.

::

   sudo apt-get install libapache2-mod-<version> php<version>-cli ...

Make some changes to php.ini and reload. Also refer to the
:ref:`System requirements <t3start:system-requirements>` for the recommended
values, but you may want to increase the values for your development environment.

Make some changes to php.ini and reload::

   memory_limit = 512M
   max_execution_time = 240
   max_input_vars = 1500


Restart Webserver::

   sudo service apache2 restart


MySQL Server
------------

::

   sudo apt-get install mysql-server

ImageMagick
-----------


::

   sudo apt-get install imagemagick



Create a basic site for your installation
-----------------------------------------

Edit a sitefile, e.g. `/etc/apache2/sites-available/t3coredev.conf`

make sure it will point to the correct htdocs directory::

   <VirtualHost *:80>
      ServerAdmin youremail@yourdomain
      ServerName t3coredev
      DocumentRoot /var/www/t3coredev
      ErrorLog ${APACHE_LOG_DIR}/error.log
      CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>


Enable it::

   sudo a2ensite t3coredev
   sudo service apache2 reload


Create a domain in your /etc/hosts
----------------------------------

/etc/hosts:

::

   127.0.0.1 localhost t3coredev


You will now be able to access your TYPO3 installation via http://t3coredev/typo3/ and it will greet you with an error message, because it is not configured yet

Next step
=========

Proceed with :ref:`setting-up-typo3-manually`.
