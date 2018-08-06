.. include:: ../Includes.txt

.. _deprecations:

========================================================================
How to deprecate classes, methods, arguments and hooks in the TYPO3 core
========================================================================

TYPO3 core development policy states that public API will not be changed
without a grace period where extension authors can adapt to the changes.
In that grace period a deprecation warning will be thrown. If you want to remove
or change functionality in the TYPO3 core, it has to be deprecated first.

Here is how:

Deprecate a class
=================

 * Add a :php:`@deprecated` annotation to the class doc comment
 * Deprecate the constructor - see next section about deprecating a method

Deprecate method
================

 * Add a :php:`@deprecated` annotation to the method doc comment
 * Add a :php:`trigger_error` call to the method, describing the migration
   path and triggering an error of type :php:`E_USER_DEPRECATED`

.. code-block:: php

   trigger_error(
      'Content with <link> syntax was found, update your content to use the t3:// syntax, and migrate your content via the upgrade wizard in the install tool',
      E_USER_DEPRECATED
   );

Deprecate method arguments
==========================

If you want to deprecate method arguments, check for argument existence and
trigger an error the same way you would for a method. If you want to deprecate
and remove an unused argument, use :php:`func_get_args()` for arguments existence
(see example below):

.. code-block:: php
   :emphasize-lines: 3,4,5

   public function TS_AtagToAbs($value)
   {
      if (func_get_args() > 1) {
         trigger_error('Second argument of TS_AtagToAbs() is not in use and is removed, however the argument in the callers code can be removed without side-effects.', E_USER_DEPRECATED);
      }
      // ...
   }


Deprecate a hook
================

As hooks provide extension points throughout the core, deprecating and removing
them should be carefully considered, but sometimes the placement of a hook doesn't
make sense anymore as the functionality around it changed or other hooks / mechanisms
replaced it's purpose. If you have to deprecate a hook, call :php:`trigger_error`
before the hook call:

.. code-block:: php
   :emphasize-lines: 3,4,5,6

   if (isset($GLOBALS['TYPO3_CONF_VARS']['SC_OPTIONS']['t3lib/class.t3lib_parsehtml_proc.php']['modifyParams_LinksDb_PostProc'])
      && is_array($GLOBALS['TYPO3_CONF_VARS']['SC_OPTIONS']['t3lib/class.t3lib_parsehtml_proc.php']['modifyParams_LinksDb_PostProc'])) {
      trigger_error(
         'The hook "t3lib/class.t3lib_parsehtml_proc.php->modifyParams_LinksDb_PostProc" will be removed in TYPO3 v10, use LinkService syntax to modify links to be stored in the database.',
         E_USER_DEPRECATED
      );
      $parameters = [
         'currentBlock' => $v,
         'linkInformation' => $linkInformation,
         'url' => $linkInformation['href'],
         'attributes' => $tagAttributes
      ];
      foreach ($GLOBALS['TYPO3_CONF_VARS']['SC_OPTIONS']['t3lib/class.t3lib_parsehtml_proc.php']['modifyParams_LinksDb_PostProc'] as $className) {
         $processor = GeneralUtility::makeInstance($className);
         $blockSplit[$k] = $processor->modifyParamsLinksDb($parameters, $this);
      }
   }


Deprecate methods still called by the TYPO3 Core
================================================

If you want to deprecate a method that still has to be used by the core itself
to provide the functionality for the time being, you can achieve that by adding
a new method parameter that will prevent the deprecation warning message being
triggered and add that parameter to the callees in the core.

Example:

.. code-block:: php
   :emphasize-lines: 9,11,15,16,17

   /**
    * Transformation handler: 'ts_links' / direction: "rte"
    * Converting TYPO3-specific <link> tags to <a> tags
    *
    * This functionality is only used to convert legacy <link> tags to the new linking syntax using <a> tags, and will
    * not be converted back to <link> tags anymore.
    *
    * @param string $value Content input
    * @param bool $internallyCalledFromCore internal option for calls where the Core is still using this function, to supress method deprecations
    * @return string Content output
    * @deprecated will be removed in TYPO3 v10, only ->TS_AtagToAbs() should be called directly, <link> syntax is deprecated
    */
   public function TS_links_rte($value, $internallyCalledFromCore = null)
   {
      if ($internallyCalledFromCore === null) {
         trigger_error('This method will be removed in TYPO3 v10, use TS_AtagToAbs() directly and do not use <link> syntax anymore', E_USER_DEPRECATED);
      }
      $hasLinkTags = false;
      $value = $this->TS_AtagToAbs($value);
      // ...
   }
