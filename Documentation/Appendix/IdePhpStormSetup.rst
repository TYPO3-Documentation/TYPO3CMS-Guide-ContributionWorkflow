.. include:: ../Includes.txt


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

.. image:: _assets/phpstorm-settings-language+frameworks-php.png
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
`.editorconfig <https://git.typo3.org/Packages/TYPO3.CMS.git/blob/HEAD:/.editorconfig>`__
file in the TYPO3 core repository.
See http://EditorConfig.org for more information. Use the `EditorConfig plugin
<https://plugins.jetbrains.com/plugin/7294-editorconfig>`__ for PhpStorm.

If you use the :file:`.editorconfig` file (which is included in the TYPO3 core), some
standard formatting rules are already setup automatically (e.g. indent with 
4 spaces for PHP files).

However, the rules defined in :file:`.editorconfig` are very minimal, so at
least set up PhpStorm to comply with PSR-1 / PSR-2 for PHP as described next.

PHP files
---------

Set **Predefined Style** in PhpStorm: 
:guilabel:`File > Settings > Editor > Code Style > PHP > Set From > Predefined Style`

Choose PSR-1 / PSR-2


.. image:: _assets/phpstorm-settings-codestyle-php-setfrom.png
   :align: center
   :alt: Setup PhpStorm Predefined Code Style


In order to test this, use `Code: Reformat Code` to reformat a PHP file.


More information
-----------------

You can find more information on the :ref:`Coding Guidelines section in the Appendix
<appendix-cgl>`.

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
  <https://github.com/TYPO3/TYPO3.CMS/blob/master/dynamicReturnTypeMeta.json>`__
* `Php Inspections (EA Extended)
  <https://plugins.jetbrains.com/plugin/7622-php-inspections-ea-extended->`__ :
  Static Code Analysis tool for PHP
* `reStructuredText plugin <https://plugins.jetbrains.com/plugin/7124-restructuredtext-support>`__:
  This will show you errors in your reStructuredText files (file ending .rst)
  when you are editing the core changelog or are updating the documentation
  for a system extension.
  
Optional Plugins
----------------
  
* `Fluid plugin <https://plugins.jetbrains.com/plugin/9469-fluid-plugin--free-version>`__ 
  (sgalinski)
* `TypoScript plugin
  <https://plugins.jetbrains.com/plugin/7463-typoscript-plugin>`__ (sgalinski)
* :ref:`phpstorm-gerritplugin`
* `TYPO3 CMS Plugin
  <https://plugins.jetbrains.com/plugin/9496-typo3-cms-plugin>`__
* `TYPO3 XLIFF Utility
  <https://plugins.jetbrains.com/plugin/8098-typo3-xliff-utility>`__


.. _phpstorm-setup-testing:

Setting up  PhpStorm for the Testing Framework
==============================================

First setup the Testing Framework. Replace <YOUR_WEBROOT> with your path
to the web directory. You must use absolute
paths for this.

Setup **Test Frameworks** in PhpStorm:
:guilabel:`File > Settings > Languages & Frameworks > PHP: Test Frameworks`:

(:kbd:`ctrl + alt + s` opens :guilabel:`File > Settings`)

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

* `Susanne Moog: "PhpStorm—a Short Review" <https://typo3.org/article/phpstorm-a-short-review/>`__ (on typo3.org, 17th April, 2019)
