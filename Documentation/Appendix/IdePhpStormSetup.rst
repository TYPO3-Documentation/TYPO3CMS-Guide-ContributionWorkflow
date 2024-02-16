.. include:: /Includes.rst.txt

.. index::
   single: PhpStorm; PhpStorm Setup
   single: Setup; PhpStorm

.. _phpstorm-setup:

===============
PhpStorm: Setup
===============

Here are some hints and examples, what you can do to setup PhpStorm.

Conventions on this page
========================

If you need to select something from the menu in PhpStorm, menu items
are displayed like this: :guilabel:`File > Settings > ....`

General setup
=============

:guilabel:`File > Settings > Languages & Frameworks > PHP`

(:kbd:`ctrl + alt + s` opens :guilabel:`File > Settings`)

* `PHP Language Level`: choose appropriate version
* `CLI Interpreter`: choose appropriate version

.. image:: /Images/External/Phpstorm/phpstorm-settings-language+frameworks-php.png
   :align: center
   :alt: Setup PhpStorm PHP settings


.. _phpstorm-setup-cgl:

Coding Guidelines
=================

Make sure your IDE is setup properly to comply with the
:ref:`Coding Guidelines for TYPO3 (CGL) <t3coreapi:cgl>`.

.. _phpstorm-setup-cgl-editorconfig:

EditorConfig
------------

Please note that there is an
`.editorconfig <https://github.com/typo3/typo3/blob/main/.editorconfig>`__
file in the TYPO3 core repository.
See http://EditorConfig.org for more information. Use the `EditorConfig plugin
<https://plugins.jetbrains.com/plugin/7294-editorconfig>`__ for PhpStorm.

If you use the :file:`.editorconfig` file (which is included in the TYPO3 core), some
standard formatting rules are already setup automatically (e.g. indent with
4 spaces for PHP files).

The rules defined in :file:`.editorconfig` are very minimal and
it is suggested to see the :ref:`TYPO3 Coding Guidelines <t3coreapi:cgl>`
for more information and toolchain configuration. Please read 
`PhpStorm documentation on using PHP CS Fixer <https://www.jetbrains.com/help/phpstorm/using-php-cs-fixer.html#installing-configuring-php-cs-fixer>`__
for information on how to use the provided
`config.php <https://github.com/TYPO3/typo3/blob/main/Build/php-cs-fixer/config.php>`__
within PhpStorm.

For a quick start, you can Howevern use the following PhpStorm code
style to comply with PSR-12, which is the most recent recommendation
at the time of this writing that PhpStorm provides a preset for:

PHP files
---------

Set **Predefined Style** in PhpStorm:
:guilabel:`File > Settings > Editor > Code Style > PHP > Set From > Predefined Style`

Choose :guilabel:`PSR-12`.

In order to test this, use `Code: Reformat Code` to reformat a PHP file.


More information
-----------------

You can find more information on the :ref:`Coding Guidelines section in the Appendix
<appendix-cgl>`.


.. index::
   single: PhpStorm; PhpStorm Plugins

.. _phpstorm-setup-plugins:

Plugins for PhpStorm
====================

Here are some plugins, you might use when developing TYPO3. DynamicReturnTypePlugin
and Php Inspections are not TYPO3 specific, but will show possible errors and
are strongly recommended when developing for the TYPO3 core.

.. hint::
   None of these plugins are mandatory, check out what might be useful for yourself!

Install plugins in PhpStorm
---------------------------

#. Open Settings: :guilabel:`File > Settings` (:kbd:`ctrl + alt + s`)
#. Select :guilabel:`Plugins`
#. Start typing name of plugin and select a match
#. Click on :guilabel:`Install`.

Recommended Plugins
-------------------

* `EditorConfig plugin <https://plugins.jetbrains.com/plugin/7294-editorconfig>`__
* `DynamicReturnTypePlugin
  <https://plugins.jetbrains.com/plugin/7251-dynamicreturntypeplugin>`__ :
  With this Plugin, return types for some functions can be configured
  dynamically. For example, if you use `GeneralUtility::makeInstance`,
  the expected return type is determined from the first parameter
  passed to the function. The configuration file for this plugin is
  `dynamicReturnTypeMeta.json
  <https://github.com/typo3/typo3/blob/main/dynamicReturnTypeMeta.json>`__
* `Php Inspections (EA Extended)
  <https://plugins.jetbrains.com/plugin/7622-php-inspections-ea-extended->`__ :
  Static Code Analysis tool for PHP
* `reStructuredText plugin <https://plugins.jetbrains.com/plugin/7124-restructuredtext-support>`__:
  This will show you errors in your reStructuredText files (file ending .rst)
  when you are editing the core changelog or are updating the documentation
  for a system extension.
* `PHPUnit Enhancement <https://plugins.jetbrains.com/plugin/9674-phpunit-enhancement>`__
  This helps with code-completion and navigation in combination with unit tests
  and Prophecy (among other things).

Optional Plugins
----------------

* `Fluid plugin <https://plugins.jetbrains.com/plugin/11151-fluid--enterprise>`__
  (sgalinski)
* `TypoScript plugin
  <https://plugins.jetbrains.com/plugin/11243-typoscript--enterprise>`__ (sgalinski)
* :ref:`phpstorm-gerritplugin`
* `TYPO3 CMS Plugin
  <https://plugins.jetbrains.com/plugin/9496-typo3-cms-plugin>`__
* `TYPO3 XLIFF Utility
  <https://plugins.jetbrains.com/plugin/8098-typo3-xliff-utility>`__


.. index::
   single: PhpStorm; Setup Testing Framework
   single: Testing; Setup PhpStorm

.. _phpstorm-setup-plugins_testing_framework:

Setting up  PhpStorm for the Testing Framework
==============================================

*Optional*

.. note::

   It is recommended to use the script :ref:`runTests.sh <runTests_sh>` for
   running tests. Alternatively, if you wish to run the unit tests within
   PhpStorm, you can set them up this way.


First setup the Testing Framework. Replace <YOUR_WEBROOT> with your path
to the web directory. You must use absolute
paths for this.

Setup **Test Frameworks** in PhpStorm:
:guilabel:`File > Settings > Languages & Frameworks > PHP: Test Frameworks`:

(:kbd:`ctrl + alt + s` opens :guilabel:`File > Settings`)

* Use composer autoloader
* `Path to script`: <YOUR_WEBROOT>/vendor/autoload.php
* Test runner: Defaut configuration file:
  <YOUR_WEBROOT>/Build/phpunit/UnitTests.xml
* Test Runner: Default bootstrap file:
  <YOUR_WEBROOT>/Build/phpunit/UnitTestsBootstrap.php


.. image:: /Images/External/Phpstorm/phpstorm-settings-testing-framework.png
   :align: center
   :alt: Setup Testing Framework

If this is setup correctly, it will be possible to run your unit tests
from within the IDE.


Other Resources
===============

* `Susanne Moog: "PhpStorm—a Short Review" <https://typo3.org/article/phpstorm-a-short-review/>`__ (on typo3.org, 17th April, 2019)
