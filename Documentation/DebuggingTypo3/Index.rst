..  include:: /Includes.rst.txt

..  highlight:: bash

..  _phpstorm-setup-xdebug:

===========
Debug TYPO3
===========

..  index::
    single: Tools; Debugging With PhpStorm and Xdebug
    single: Debugging; With PhpStorm and Xdebug

..  _debugging-with-phpstorm-and-xdebug:

Debugging With PhpStorm and Xdebug
==================================

..  youtube:: VtffB0CG1ok

In order to configure PhpStorm with Xdebug you need to do four things:

#.  Install xdebug
#.  Configure xdebug settings in your php.ini
#.  Use the appropriate plugin in your browser
#.  Configure PhpStorm


php.ini
-------

Example setup:

..  code-block:: ini
    :caption: php.ini

    xdebug.mode = debug
    xdebug.client_host = localhost
    xdebug.max_nesting_level = 1000

You should also configure the port (xdebug.client_port) if that should differ from the default (9003).

These are the settings of Xdebug 3. They replace the Xdebug 2 settings
`xdebug.remote_enable`, `xdebug.remote_host` and `xdebug.remote_port`, see the
`Xdebug upgrade guide <https://xdebug.org/docs/upgrade_guide>`__.

Remember to restart your Webserver / php-fpm / Docker after you made your changes.

Install Plugin
--------------

Install plugin "Xdebug Helper" for your browser. To start debugging, click on the bug icon and select "Debug".

PhpStorm
--------

*   Check `Run: Webserver Debug Validation`
*   Start `Run: Start Listening for PHP Debug Connections`
*   Create some breakpoints

More Information
================

*   `Configuring Xdebug with PhpStorm <https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html#integrationWithProduct>`__ (Jetbrains)
