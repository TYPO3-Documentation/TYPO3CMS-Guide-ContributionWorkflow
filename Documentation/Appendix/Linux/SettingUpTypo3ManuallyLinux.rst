.. include:: ../../Includes.txt

.. highlight:: bash

.. _setting-up-typo3-manually-linux:

=====================================
Setting up TYPO3 manually under Linux
=====================================

Prerequisites
=============

You will need a Webserver, PHP and database on your system. Look at the page `System requirements
<https://typo3.org/typo3-cms/overview/requirements/>`__ and check out the specific system
requirements for the current master branch on the `Download TYPO3 <https://typo3.org/download/>`__
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
  


PHP 7.2
-------

::

   sudo apt-get install libapache2-mod-php7.2 php7.2-cli \
   php7.2-common php7.2-curl php7.2-gd php7.2-imap php7.2-intl \
   php7.2-json php7.2-mbstring php7.2-mysql php7.2-opcache \
   php7.2-readline php7.2-soap php7.2-xml php7.2-zip

.. important::
   Make sure you use the correct PHP version for your TYPO3 version. For the current master TYPO3 9, this is PHP 7.2.

Make some changes to php.ini and reload::

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

make sure it will point to the correct htdocs directory:

::

   <VirtualHost *:80>
      ServerAdmin youremail@yourdomain
      ServerName t3coredev
      DocumentRoot /var/www/t3coredev
      ErrorLog ${APACHE_LOG_DIR}/error.log
      CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>


Enable it

::

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
