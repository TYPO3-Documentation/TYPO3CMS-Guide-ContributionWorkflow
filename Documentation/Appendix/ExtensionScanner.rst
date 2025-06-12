..  include:: /Includes.rst.txt
..  index:: Extension scanner
..  _extension-scanner:

=================
Extension scanner
=================

Whenever functionality is :ref:`deprecated <deprecations>` or removed by
a breaking change it should be added to the Extension Scanner as either a weak or
strong match.

When changing Core API, Core developers should monitor the extension scanner and add matcher
configurations where possible. This is typically the case if PHP API was changed and the patch comes with
a deprecation or breaking ReST file to document the change.


..  index:: Extension scanner; Changelog connection

Connection to the changelog reStructuredText files
==================================================

All changelog type reStructuredText (reST) files since Core version 9 have to
be tagged with one of the three tags :rst:`FullyScanned`,
:rst:`PartiallyScanned` or :rst:`NotScanned`. In particular, the
:rst:`FullyScanned` tag is used by the extension scanner to mark instances as
"not affected by this change", as such they should be added with care and only
if the scanner configuration matches all changes mentioned in the reST file.

If only parts of the reST file are covered, :rst:`PartiallyScanned` has to be
added and the reST file should mention which parts are and are not covered.
If the scanner does not cover a reST file at all then :rst:`NotScanned` can
be added.

..  code-block:: rst
    :caption: Last line of a fully scanned reST file in the changelog

    ..  index:: Frontend, FullyScanned, ext:frontend

If a reST file is renamed the file may be covered in a matcher configuration
which then needs to be adapted as well. The reST files are not bound to
specific directories in the matcher configuration so moving a reST file
to a different location within the :file:`Changelog` directory has no effect.

..  index:: Extension Scanner; Configuration

Extension scanner PHP configuration
===================================

The match configurations can be found below the following path:
:file:`EXT:install/Configuration/ExtensionScanner`. Choose the file that
is related to your change and add the removed functionality to the extension
scanner match configuration. As a key we use the fully qualified name.

Example: Deprecate a class
--------------------------

..  code-block:: php
    :caption: EXT:install/Configuration/ExtensionScanner/Php/ClassNameMatcher.php

    'TYPO3\CMS\Frontend\Http\UrlProcessorInterface' => [
        'restFiles' => [
            'Deprecation-96641-UnusedHookRelatedUrlProcessorInterface.rst',
        ],
    ],

Example: Drop an argument from a method
------------------------------------------

..  code-block:: php
    :caption: EXT:install/Configuration/ExtensionScanner/Php/MethodArgumentDroppedMatcher.php

    'TYPO3\CMS\Core\Authentication\BackendUserAuthentication->checkAuthMode' => [
        'maximumNumberOfArguments' => 3,
        'restFiles' => [
            'Breaking-97265-SimplifiedAccessModeSystem.rst',
        ],
    ],


About the PHP part of the extension scanner
===========================================

The PHP part of the extension scanner is based on the library
`nikic/php-parser <https://github.com/nikic/PHP-Parser>`__. This library creates an
`abstract syntax tree <https://en.wikipedia.org/wiki/Abstract_syntax_tree>`__ from any given
compilable PHP file. It comes with a traverser for recursive iteration over the tree that
implements a visitor pattern, own visitors can be added. A single "matcher" is a visitor added
to the traverser. A default visitor resolves all shortened namespaced class usages to their
fully qualified name, which is a great help for our matchers.

This basically means: The whole AST is traversed exactly once for each PHP file and all matchers
are called for each node. Matches can then decide if they match a configured deprecation or breaking
scenario.

All matchers are covered by unit tests and a fixture that shows what exactly is matched. Studying the
fixture can be a good way to understand the matcher.

Matchers are systematically named: for method calls there is a usually one variant for dynamic and
one for static calls. If for example a static method changed its argument signature by removing
an argument then the according matcher class is :php:`TYPO3\CMS\Install\ExtensionScanner\Php\MethodArgumentDroppedStaticMatcher`.

Single matcher configurations are pretty obvious, new ones should be added at the end. When adding
matcher configurations it should be verified the match it is not already covered by some other matcher
(possibly in another reST file).
