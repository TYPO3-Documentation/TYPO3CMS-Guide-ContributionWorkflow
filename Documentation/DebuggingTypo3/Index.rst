.. include:: ../Includes.txt

.. highlight:: bash

.. _phpstorm-setup-xdebug:

===============
Debugging TYPO3
===============

Debugging TYPO3 with Phpstorm and Xdebug
========================================


.. youtube:: VtffB0CG1ok


In order to configure Phpstorm with Xdebug you need to do 3 things:

1. Configure xdebug settings in php.ini
2. Use appropriate plugin with your browser
3. Configure Phpstorm


php.ini
-------

Example setup:

::

   xdebug.remote_enable = 1
   xdebug.remote_host = <ip>
   xdebug.max_nesting_level = 1000


Remember to restart your Webserver / php-fpm after you made your changes.

Install plugin
--------------

Install plugin "Xdebug Helper" for your browser. To start debugging, click the bug and select "Debug".


Phpstorm
--------

* Check `Run: Webserver Debug Validation`
* Start `Run: Start listing for PHP Debug Connections`