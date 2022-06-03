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

.. code-block:: bash
   :caption: shell command

   sudo apt-get install apache2
   sudo a2enmod deflate rewrite headers mime expires



PHP 7.4
-------

.. code-block:: bash
   :caption: shell command

   sudo apt-get install libapache2-mod-php7.4 php7.4-cli \
   php7.4-common php7.4-curl php7.4-gd php7.4-imap php7.4-intl \
   php7.4-json php7.4-mbstring php7.4-mysql php7.4-opcache \
   php7.4-readline php7.4-soap php7.4-xml php7.4-zip

.. important::
   Make sure you use the correct PHP version for your TYPO3 version.

Make some changes to php.ini (or appropriate file in :file:`conf.d`) and reload:

.. code-block:: bash
   :caption: php.ini (or other PHP config filename)

   max_execution_time = 240
   max_input_vars = 1500


Restart Webserver:

.. code-block:: bash
   :caption: shell command

   sudo service apache2 restart


MySQL Server
------------

.. code-block:: bash
   :caption: shell command

   sudo apt-get install mysql-server

ImageMagick
-----------


.. code-block:: bash
   :caption: shell command

   sudo apt-get install imagemagick



Create a basic site for your installation
-----------------------------------------

Edit a sitefile, make sure it will point to the correct htdocs directory:

.. code-block:: apacheconf
   :caption: /etc/apache2/sites-available/t3coredev.conf

   <VirtualHost *:80>
      ServerAdmin youremail@yourdomain
      ServerName t3coredev
      DocumentRoot /var/www/t3coredev
      ErrorLog ${APACHE_LOG_DIR}/error.log
      CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>


Enable it:

.. code-block:: bash
   :caption: shell command

   sudo a2ensite t3coredev
   sudo service apache2 reload


Create a domain in your /etc/hosts
----------------------------------

.. code-block:: linux-config
   :caption: /etc/hosts

   127.0.0.1 localhost t3coredev


You will now be able to access your TYPO3 installation via http://t3coredev/typo3/ and it will greet you with an error message, because it is not configured yet

Next step
=========

Proceed with :ref:`setting-up-typo3-manually`.
