:orphan:
:navigation-title: Create patch - Intention
.. include:: /Includes.rst.txt

.. index::
   single: Patch

.. _quickstart-intent:

Quick Start: Create a patch - Intention
=======================================

For this part of the guide to be effective, we establish our intent.

This could be many things:

*  **Fix a bug** in one of the TYPO3 Core Extensions
*  Introduce a **new feature**
*  Fix mistakes or add content in the **Documentation** of any of the Core Extensions
*  Enhance **tests** for certain functionality
*  Raise or add **dependencies** within TYPO3
*  Adjust the **TYPO3 Build** or **Testing Pipeline**
*  Make changes to the **TypeScript/SCSS build** of TYPO3

For the sake of clarity, let's pick a simple example:

    I found a bug in the TYPO3 record editing backend (FormEngine) for
    the `JsonElement` input (TCA type `json`). With a new HTML5 spec,
    all Json presentations need a new attribute called `input-format="json"`
    to be set.

For this you have already discovered the TYPO3 Core file
:file:`typo3/sysext/backend/Classes/Form/Element/JsonElement.php`,
which has this code at `line 188`:

..  code:: php

        $editorHtml = '
            <typo3-t3editor-codemirror ' . GeneralUtility::implodeAttributes($codeMirrorConfig, true, true) . '>
                <textarea ' . GeneralUtility::implodeAttributes($attributes, true, true) . '>' . htmlspecialchars($itemValue) . '</textarea>
                <input type="hidden" name="target" value="0" />
                <input type="hidden" name="effectivePid" value="' . htmlspecialchars((string)($this->data['effectivePid'] ?? '0')) . '" />
            </typo3-t3editor-codemirror>';
    } else {
        $attributes['class'] = implode(' ', array_merge(explode(' ', $attributes['class']), ['formengine-textarea', 't3js-enable-tab']));
        $resultArray['javaScriptModules'][] = JavaScriptModuleInstruction::create('@typo3/backend/form-engine/element/json-element.js');
        $editorHtml = '
            <typo3-formengine-element-json recordFieldId="' . htmlspecialchars($fieldId) . '">
                <textarea ' . GeneralUtility::implodeAttributes($attributes, true, true) . '>' . htmlspecialchars($itemValue) . '</textarea>
            </typo3-formengine-element-json>';
    }

We change this code into:

..  code:: php
    :emphasize-lines: 3,12

        $editorHtml = '
            <typo3-t3editor-codemirror ' . GeneralUtility::implodeAttributes($codeMirrorConfig, true, true) . '>
                <textarea input-format="json" ' . GeneralUtility::implodeAttributes($attributes, true, true) . '>' . htmlspecialchars($itemValue) . '</textarea>
                <input type="hidden" name="target" value="0" />
                <input type="hidden" name="effectivePid" value="' . htmlspecialchars((string)($this->data['effectivePid'] ?? '0')) . '" />
            </typo3-t3editor-codemirror>';
    } else {
        $attributes['class'] = implode(' ', array_merge(explode(' ', $attributes['class']), ['formengine-textarea', 't3js-enable-tab']));
        $resultArray['javaScriptModules'][] = JavaScriptModuleInstruction::create('@typo3/backend/form-engine/element/json-element.js');
        $editorHtml = '
            <typo3-formengine-element-json recordFieldId="' . htmlspecialchars($fieldId) . '">
                <textarea input-format="json" ' . GeneralUtility::implodeAttributes($attributes, true, true) . '>' . htmlspecialchars($itemValue) . '</textarea>
            </typo3-formengine-element-json>';

Note that we added :html:`input-format="json"` in the marked lines.

After we patched the file, we can manually check it has the wanted effect.

To contribute this patch and to meet the TYPO3 quality criteria, this change
needs to be covered by a Unit or Functional Test (see
:ref:`Testing <t3coreapi:testing>` and :ref:`Using runTests.sh <t3contribute:runTests_sh>`).

Since testing is vital to TYPO3, we add a test for our code change above.

By browsing through the existing TYPO3 testing directories, we often find
tests that can be adapted for the change we make. In this case, there's
:file:`typo3/sysext/backend/Tests/Unit/Form/Element/JsonElementTest.php`
which already performs a test:

..  code:: php

        self::assertStringContainsString('<typo3-formengine-element-json', $result['html']);
        self::assertStringContainsString('placeholder="placeholder"', $result['html']);
        self::assertStringContainsString('&quot;foo&quot;: &quot;bar&quot;', $result['html']);

        // ...

        self::assertStringContainsString('<typo3-t3editor-codemirror', $result['html']);
        self::assertStringContainsString('placeholder="placeholder"', $result['html']);
        self::assertStringContainsString('&quot;foo&quot;: &quot;bar&quot;', $result['html']);

In most cases you need to create a distinct test method for patches you make,
but in this case we can take the easy route and just append our expectation:

..  code:: php
    :emphasize-lines: 4,11

        self::assertStringContainsString('<typo3-formengine-element-json', $result['html']);
        self::assertStringContainsString('placeholder="placeholder"', $result['html']);
        self::assertStringContainsString('&quot;foo&quot;: &quot;bar&quot;', $result['html']);
        self::assertStringContainsString('input-format="json"', $result['html']);

        // ...

        self::assertStringContainsString('<typo3-t3editor-codemirror', $result['html']);
        self::assertStringContainsString('placeholder="placeholder"', $result['html']);
        self::assertStringContainsString('&quot;foo&quot;: &quot;bar&quot;', $result['html']);
        self::assertStringContainsString('input-format="json"', $result['html']);

After the change, we can verify our test works:

..  code:: bash

    ./Build/Scripts/runTests.sh -p 8.3 -s unit typo3/sysext/backend/Tests/Unit/Form/Element/JsonElementTest.php

with an output like:

..  code:: text

    PHPUnit 11.2.5 by Sebastian Bergmann and contributors.

    Runtime:       PHP 8.3.8
    Configuration: ~/TYPO3-contrib/Build/phpunit/UnitTests.xml

    ..                                                                  2 / 2 (100%)

    Time: 00:00.021, Memory: 14.00 MB

    OK (2 tests, 14 assertions)

    ###########################################################################
    Result of unit
    Container runtime: docker
    PHP: 8.3
    SUCCESS
    ###########################################################################

If you take our patched file :file:`typo3/sysext/backend/Classes/Form/Element/JsonElement.php`
again and accidentally replace `input-type="json"` with `input-type="jason"` and
re-execute the test, you will see it will properly report a failure.

..  hint::

    If a patch is not only a bugfix but has an important impact or a new feature,
    it needs Documentation alongside the patch. See :ref:`Adding Documentation <t3contribute:Adding-documentation>`,
    this is beyond the scope of this chapter.

This concludes stating an intent for contributing a patch and you have a modified
file plus a test to contribute. Continue on :ref:`quickstart-patch`!

