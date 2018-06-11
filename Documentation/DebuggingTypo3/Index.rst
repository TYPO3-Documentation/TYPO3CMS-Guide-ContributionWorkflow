.. include:: ../Includes.txt

.. highlight:: bash

.. _phpstorm-setup-xdebug:


===============
Debugging TYPO3
===============

Debugging TYPO3 with PhpStorm and Xdebug
========================================


.. youtube:: VtffB0CG1ok


In order to configure PhpStorm with Xdebug you need to do three things:

1. Configure xdebug settings in your php.ini
2. Use the appropriate plugin in your browser
3. Configure PhpStorm


php.ini
-------

Example setup:

::

   xdebug.remote_enable = 1
   xdebug.remote_host = <your ip adress or hostname>
   xdebug.max_nesting_level = 1000


Remember to restart your Webserver / php-fpm after you made your changes.

Install plugin
--------------

Install plugin "Xdebug Helper" for your browser. To start debugging, click on the bug icon and select "Debug".


PhpStorm
--------

* Check `Run: Webserver Debug Validation`
* Start `Run: Start listing for PHP Debug Connections`
* Create some breakpoints
