.. include:: ../Includes.txt

.. highlight:: bash

.. _phpstorm-setup-xdebug:

===========
Debug TYPO3
===========

.. _debugging-with-phpstorm-and-xdebug:

.. index::
   single: Tools; Debugging With PhpStorm and Xdebug
   single: Debugging; With PhpStorm and Xdebug

Debugging With PhpStorm and Xdebug
==================================


.. youtube:: VtffB0CG1ok


In order to configure PhpStorm with Xdebug you need to do three things:

#. Install xdebug
#. Configure xdebug settings in your php.ini
#. Use the appropriate plugin in your browser
#. Configure PhpStorm


php.ini
-------

Example setup:

::

   xdebug.remote_enable = 1
   xdebug.remote_host = localhost
   xdebug.max_nesting_level = 1000

You should also configure the port (xdebug.remote_port) if that should differ from the default (9000).

Remember to restart your Webserver / php-fpm / Docker after you made your changes.

Install Plugin
--------------

Install plugin "Xdebug Helper" for your browser. To start debugging, click on the bug icon and select "Debug".


PhpStorm
--------

* Check `Run: Webserver Debug Validation`
* Start `Run: Start listing for PHP Debug Connections`
* Create some breakpoints

More Information
================

* `Configuring Xdebug with PhpStorm <https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html#integrationWithProduct>`__ (Jetbrains)
