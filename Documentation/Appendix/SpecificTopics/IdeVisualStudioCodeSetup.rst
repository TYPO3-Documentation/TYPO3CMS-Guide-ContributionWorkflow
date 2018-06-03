.. include:: ../../Includes.txt


.. _vscode-setup:

=============================
Setting up Visual Studio Code
=============================

Here are some hints and examples, what you can do to setup Visual Studio Code.

Conventions on this page
========================

If you need to select something from the menu in Visual Studio Code, menu items
are displayed like this: `File: Settings: ....`

Installation
============

* The latest stable version you can find at https://code.visualstudio.com/Download
* If you prefer using the Insider Builds use https://code.visualstudio.com/insiders

Quick setup
===========

Press :kbd:`ctrl` + :kbd:`shift` + :kbd:`X` and type `typo3-pack` to find the
`TYPO3 Extension Pack` which installs a selection of useful extensions for
the contribution to TYPO3. Then click `Install` to install all of it.

Alternatifly use `code --install-extension gilbertsoft.typo3-pack` respectifly
`code-insiders --install-extension gilbertsoft.typo3-pack` at the command
prompt.




General setup
=============

`File: Settings: Languages & Frameworks: PHP`

* `PHP Language Level`: choose appropriate version
* `CLI Interpreter`: choose appropriate version

.. image:: _assets/phpstorm-settings-language+frameworks-php.png
   :align: center
   :alt: Setup Visual Studio Code PHP settings


.. _vscode-setup-cgl:

Coding Guidelines
=================

Make sure your IDE is setup properly to comply with the
:ref:`Coding Guidelines for TYPO3 (CGL) <t3coreapi:cgl>`. For example,
(following PSR-2) space characters (not tabs) are used to indent source
code. See
:ref:`Whitespace and indentation <t3coreapi:cgl-general-requirements-for-php-files>`
for more information.


.. hint::
   Please also note that there is an .editorconfig file in the TYPO3 core repository.
   See http://EditorConfig.org for more information.

PHP files
---------

`File: Settings: Editor: Code Style : PHP : Set From : Predefined Style`

Choose PSR-1 / PSR-2


.. image:: _assets/phpstorm-settings-codestyle-php-setfrom.png
   :align: center
   :alt: Setup Visual Studio Code Predefined Code Style


In order to test this, use `Code: Reformat Code` to reformat a PHP file


More information
-----------------

You can find more information on the :ref:`Coding Guidelines section in the Appendix
<appendix-cgl>`.

.. _vscode-setup-plugins:

Optional Plugins
================

Here are some Plugins, you might use when developing TYPO3. DynamicReturnTypePlugin
and Php Inspections are not TYPO3 specific, but will show possible errors and 
are strongly recommended when developing for the TYPO3 core.

.. hint::
   None of these Plugins are mandatory, check out what might be useful for yourself!

Install Plugins: `File: Settings: Plugins`


* `DynamicReturnTypePlugin
  <https://plugins.jetbrains.com/plugin/7251-dynamicreturntypeplugin>`__ :
  With this Plugin, return types for some functions can be configured
  dynamically. For example, if you use `GeneralUtility::makeInstance`,
  the expected return type is determined from the first parameter
  passed to the function. The configuration file for this plugin is
  `dynamicReturnTypeMeta.json
  <https://github.com/TYPO3/TYPO3.CMS/blob/master/dynamicReturnTypeMeta.json>`__
* `Php Inspections (EA Extended)
  <https://plugins.jetbrains.com/plugin/7622-php-inspections-ea-extended->`__ :
  Static Code Analysis tool for PHP
* `Fluid plugin <https://plugins.jetbrains.com/plugin/9469-fluid-plugin--free-version>`__ 
  (sgalinski)
* `TypoScript plugin
  <https://plugins.jetbrains.com/plugin/7463-typoscript-plugin>`__ (sgalinski)
* :ref:`phpstorm-gerritplugin`
* `TYPO3 CMS Plugin
  <https://plugins.jetbrains.com/plugin/9496-typo3-cms-plugin>`__
* `TYPO3 XLIFF Utility
  <https://plugins.jetbrains.com/plugin/8098-typo3-xliff-utility>`__


.. _vscode-setup-testing:

Setting up Visual Studio Code for the Testing Framework
=======================================================

First setup the Testing Framework. Replace <YOUR_WEBROOT> with your path
to the web directory. You must use absolute
paths for this.

`File: Settings: Languages & Frameworks: PHP: Test Frameworks`:

* Use composer autoloader
* `Path to script`: <YOUR_WEBROOT>/vendor/autoload.php
* Test runner: Defaut configuration file:
  <YOUR_WEBROOT>/vendor/typo3/testing-framework/Resources/Core/Build/UnitTests.xml
* Test Runner: Default bootstrap file:
  <YOUR_WEBROOT>/vendor/typo3/testing-framework/Resource/Core/Build/UnitTestsBootstrap.php


.. image:: _assets/phpstorm-settings-testing-framework.png
   :align: center
   :alt: Setup Testing Framework

If this is setup correctly, it will be possible to run your unit tests
from within the IDE.


Other Resources
===============

* https://wiki.typo3.org/Development/PHPStorm_Settings
