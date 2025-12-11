:navigation-title: How to deprecate

..  include:: /Includes.rst.txt

..  index::
    single: Deprecation

..  _deprecations:

========================================================================
How to deprecate classes, methods, arguments and hooks in the TYPO3 Core
========================================================================

TYPO3 Core development policy states that public API will not be changed
without a grace period where extension authors can adapt to the changes.
In that grace period a deprecation warning will be thrown. If you want to remove
or change functionality in the TYPO3 Core, it has to be deprecated first.

..  note::
    Upon deprecating or removing functionality the change must be added
    to the :ref:`Extension scanner <extension-scanner>` whenever possible.

..  note::
    It's not always possible to "deprecate" everything. In some cases,
    hard breaking changes must be introduced. These need to be addressed
    and discussed with much care beyond the scope of this chapter, and can
    only occur in new major versions of TYPO3 in the `X.0.x` focus release.

Here is how:

..  contents::

..  index::
    single: Deprecation; Deprecate a class

..  _deprecate-class:

Deprecate a class
=================

*   Add a :php:`@deprecated` annotation to the class doc comment
*   Deprecate the constructor - see next section about deprecating a method


..  index::
    single: Deprecation; Deprecate a method

..  _deprecate-method:

Deprecate method
================

*   Add a :php:`@deprecated` annotation to the method doc comment
*   Add a :php:`trigger_error` call to the method, describing the migration
    path and triggering an error of type :php:`E_USER_DEPRECATED`

..  code-block:: php

    trigger_error(
      'Content with <link> syntax was found, update your content to use the t3:// syntax, and migrate your content via the upgrade wizard in the install tool',
      E_USER_DEPRECATED
    );


..  index::
    single: Deprecation; Deprecate method arguments

..  _deprecate-method-arguments:

Deprecate method arguments
==========================

If you want to deprecate method arguments, check for argument existence and
trigger an error the same way you would for a method. If you want to deprecate
and remove an unused argument, use :php:`func_get_args()` or :php:`func_num_args()`
(see example below):

..  code-block:: php
    :emphasize-lines: 3,4,5

    public function TS_AtagToAbs($value)
    {
        if (func_num_args() > 1) {
            trigger_error('Second argument of TS_AtagToAbs() is not in use and is removed, however the argument in the callers code can be removed without side-effects.', E_USER_DEPRECATED);
        }
        // ...
    }


..  _make-class-properties-protected:

Make class properties protected
===============================

To reach full encapsulation of classes, the public access to properties should be removed.
The property access should be done by public methods only.

Public properties that should be protected can be migrated to protected or private and
wrapped with getters/setters as needed.

During a phase of deprecation, entries into the deprecation log are triggered, if an
extension accesses a previously public property. The code still keeps working until the
next major release, when the deprecation and public access fallback are removed from the code.

To deprecate usage of a (still) public property that should be changed to protected in
the future:

#.  Add the :php:`TYPO3\CMS\Core\Compatibility\PublicPropertyDeprecationTrait` trait to
    the class.
#.  Add the property :php:`$deprecatedPublicProperties` to the class and list all properties that
    should no longer be accessed from outside of the class.
#.  Make the property private/protected.

..  code-block:: diff

    +use TYPO3\CMS\Core\Compatibility\PublicPropertyDeprecationTrait;
    +
    class RecordHistory
    {
    +       use PublicPropertyDeprecationTrait;
    +
    +       /**
    +         * @var string[]
    +         */
    +        private $deprecatedPublicProperties = [
    +            'changeLog' => 'Using changeLog is deprecated and will not be possible anymore in TYPO3 v11.0. Use getChangeLog() instead.',
    +       ];
    +
            /**
             * @var array
             */
    -       public $changeLog = [];
    +       protected $changeLog = [];


..  _make-class-methods-protected:

Make class methods protected
============================

This works in a similar way as :ref:`make-class-properties-protected`: The trait
:php:`TYPO3\CMS\Core\Compatibility\PublicMethodDeprecationTrait` allows to make
public methods protected or private without breaking extensions.

This can be used in case the public methods may still be called by extensions.
This will then trigger a deprecation.

In order to make a method private or protected:

#.  Add the :php:`TYPO3\CMS\Core\Compatibility\PublicMethodDeprecationTrait` trait to
    the class.
#.  Add the property :php:`$deprecatedPublicMethods` to the class and list all methods that
    should no longer be accessed from outside of the class.
#.  Make the method private/protected.


..  code-block:: diff

    +use TYPO3\CMS\Core\Compatibility\PublicMethodDeprecationTrait;
    +
    class PageRepository
    {
    +       use PublicMethodDeprecationTrait;
    +
    +       /**
    +         * @var string[]
    +         */
    +        private $deprecatedPublicMethods = [
    +            'init' => 'init() is now called implicitly on object creation, and is not necessary anymore to be called explicitly. Calling init() will throw an error in TYPO3 v10.0.',
    +       ];
    +

    -       public function init($show_hidden)
    +       protected function init($show_hidden)



..  index::
    single: Deprecation; Deprecate a hook

..  _deprecate-hooks:

Deprecate a hook
================

As hooks provide extension points throughout the core, deprecating and removing
them should be carefully considered, but sometimes the placement of a hook doesn't
make sense anymore as the functionality around it changed or other hooks / mechanisms
replaced it's purpose. If you have to deprecate a hook, call :php:`trigger_error`
before the hook call:

..  code-block:: php
    :emphasize-lines: 3,4,5,6

    if (isset($GLOBALS['TYPO3_CONF_VARS']['SC_OPTIONS']['t3lib/class.t3lib_parsehtml_proc.php']['modifyParams_LinksDb_PostProc'])
        && is_array($GLOBALS['TYPO3_CONF_VARS']['SC_OPTIONS']['t3lib/class.t3lib_parsehtml_proc.php']['modifyParams_LinksDb_PostProc'])
    ) {
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


..  index::
    single: Deprecation; Deprecate methods still called by the core

..  _deprecate-used-methods:

Deprecate methods still called by the TYPO3 Core
================================================

If you want to deprecate a method that still has to be used by the core itself
to provide the functionality for the time being, you can achieve that by adding
a new method parameter that will prevent the deprecation warning message being
triggered and add that parameter to the callees in the core.

Example:

..  code-block:: php
    :emphasize-lines: 9,11,15,16,17

    /**
     * Transformation handler: 'ts_links' / direction: "rte"
     * Converting TYPO3-specific <link> tags to <a> tags
     *
     * This functionality is only used to convert legacy <link> tags to the new linking syntax using <a> tags,  and will
     * not be converted back to <link> tags anymore.
     *
     * @param string $value Content input
     * @param bool $internallyCalledFromCore internal option for calls where the Core is still using this function, to suppress method deprecations
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

..  _deprecate-language-reference:

Deprecate a language label reference
====================================

If you move or remove a language label from the Core, third-party extensions and
projects may still depend on it. Therefore, it is good practice to keep the original label
and mark it as deprecated with an `x-unused-since` attribute for XLIFF 1.2 or the
`subState="deprecated"` property for XLIFF 2.0 files:

..  tabs::

    ..  group-tab:: XLIFF 1.2

        ..  code-block:: xml
        
            <trans-unit id="CType_formlabel" x-unused-since="14.0">
                <source>Type</source>
            </trans-unit>

    ..  group-tab:: XLIFF 2.0

        ..  code-block:: xml

            <unit id="label5">
                <segment subState="deprecated">
                    <source>This is label #5 (deprecated in English)</source>
                </segment>
            </unit>

The label can then be completely removed in the next major TYPO3 version (the
label must not be referenced any longer in the Core.)

A deprecation warning is triggered the first time a deprecated label is written
to the cache. Subsequent resolutions of the same label use the cached entry and do
not trigger additional warnings until the cache is cleared.

Note that some label references use computed label strings, so check
these carefully before removal.

..  _move-xliff-file:

Move or rename XLIFF files
==========================

If you move or rename an XLIFF file, add a mapping to
:php:`TYPO3\CMS\Core\Localization\LocalizationFactory` in the ``MOVED_FILES``
constant. Remove all references to the old XLIFF file in the Core. The mapping
can be safely removed in the next major TYPO3 version.

More information
================

Changelogs

*   9.0 :doc:`Dealing with properties that become protected <ext_core:Changelog/9.0/Important-81330-DealingWithPropertiesThatAreMigratedToProtected>`
*   9.0 :doc:`Trait to migrate public access to protected by deprecation <ext_core:Changelog/9.0/Feature-81330-TraitToMigratePublicAccessToProtectedByDeprecation>`
*   9.4 :doc:`Trait to detect public deprecated methods: PublicMethodDeprecationTrait <ext_core:Changelog/9.4/Feature-85247-TraitToDetectPublicDeprecatedMethods>`
