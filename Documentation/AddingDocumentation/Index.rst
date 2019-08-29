.. include:: ../Includes.txt

.. _Bugfixing-Adding-documentation:
.. _Adding-documentation:

=================
Add Documentation
=================

**Quick links:**

.. rst-class:: horizbuttons-primary-m

- :ref:`h2document:Formatting-with-reST`
- :ref:`h2document:format-rest-cgl`
- :ref:`h2document:rest-cheat-sheet`
- :ref:`h2document:rendering-docs-quickstart`


The documentation `Changelog <https://docs.typo3.org/typo3cms/extensions/core/latest/>`__
and documentation for
`system extensions <https://docs.typo3.org/typo3cms/SystemExtensions/Index.html>`__
is maintained in the core.

.. _changelog:

Changelog
=========

Some patches require a .rst (reStructuredText) Changelog file describing the change.
Not all patches
need an entry in the Changelog. Check the list below. Also see the current
`Changelog <https://docs.typo3.org/typo3cms/extensions/core/latest/>`__
for some examples.

Every file may optionally contain tags, but it must contain at least a
NotScanned, PartiallyScanned or FullyScanned tag for the extension scanner.
See :ref:`t3coreapi:extension-scanner` in TYPO3 Explained for more 
information.

If you use the Forger reST File Generator, it will take care of this.

reST File Generator
-------------------

.. tip::

   If you want to save yourself some time you can use the rst Helper at
   https://forger.typo3.com/utilities/rst

This is strongly recommended because the tool will generate correctly
formatted files. You can always add more to the .rst file directly later.

Select the type of rst snippet you want to create, enter your issue number
and click the search button. Select appropriate tags.

When you are done, copy the generated text and create a file with the same
name as suggested in the generator.


Types of Changes
----------------

There are four different types of changes
which have to follow a certain format and **always**
need to go into :file:`typo3/sysext/core/Documentation/Changelog/master/`.

Choose one which fits your patch:

.. _documenting-changelog-breaking-changes:

Breaking Changes
~~~~~~~~~~~~~~~~

A patch moved or removed a specific part of core functionality
that may break extensions if they use this part.

**Mandatory sections:**

#. **Description** - why things had to break backwards compatibility.

#. **Impact** - how will the change affect your installation.

#. **Affected Installations** - describe scenarios under which circumstances
   a TYPO3 install will be affected by this change.

#. **Migration** - provide instructions what needs to be done to get things
   working again. Explicitly mention if no migration is possible.


.. _documenting-changelog-deprecations:

Deprecations
~~~~~~~~~~~~

A patch deprecates a certain core functionality
for a planned removal. See more information: :ref:`Deprecations <deprecations>`

**Mandatory sections:**

#. **Description** - why things had to be deprecated.

#. **Impact** - how will the change affect your installation.

#. **Affected Installations** - describe scenarios under which circumstances
   an TYPO3 install will be affected by this change.

#. **Migration** - provide instructions what needs to be done to get things
   working again. Explicitly mention if no migration is possible.


.. _documenting-changelog-features:

Features
~~~~~~~~

A patch adds new functionality.

**Mandatory sections:**

#. **Description** - what can the new feature do.

#. **Impact** - how users are affected by this new feature.


.. _documenting-changelog-important-information:

Important Information
~~~~~~~~~~~~~~~~~~~~~

Anything that does not fit the other categories but is
important enough to require a Changelog entry.

#. **Description** - describe what is so important it needed an rst snippet

.. _changelog-check-rst:

Check Your `rst` File
---------------------

When your change is finished, you can run the following script to check that
your rst file is ok. The script will check all files in
:file:`typo3/sysext/core/Documentation/Changelog`.

::

   Build/Scripts/validateRstFiles.php

This script will check if the .rst files contain all mandatory tags that
are required for the Changelog. It will **not** do a reST syntax check.

In order to make sure that your file contains no syntax errors and will
be rendered correctly, do one or more of the following:

* Check our :ref:`format-rest-cgl` and :ref:`rest-common-pitfalls`.
* Use an editor or IDE that properly supports reST and shows errors
* Render the Changelog locally with docker as explained in the next section


.. _render-the-changelog:

Render the Changelog
--------------------

If you wish to render the Changelog locally, you can use docker as described
in :ref:`h2document:rendering-docs-quickstart`.



.. code-block:: bash
   :linenos:

   cd typo3/sysext/core/
   source <(docker run --rm t3docs/render-documentation show-shell-commands)
   dockrun_t3rdf makehtml
   # on Mac
   open "Documentation-GENERATED-temp/Result/project/0.0.0/Index.html"
   # on Linux
   xdg-open "Documentation-GENERATED-temp/Result/project/0.0.0/Index.html"
   # On Windows
   start "Documentation-GENERATED-temp/Result/project/0.0.0/Index.html"
   cd -


#. First, change to the :file:`core` directory
#. This is a combined command that does docker pull, docker run, and makes some shell commands available in current terminal!
#. This runs the build command, it will create Documentation-GENERATED-temp in current directory
#. `open` will run a URL - this should work on MacOS
#. If you use Linux, use `xdg-open`, 
   if this does not work, just open the URL in quotes in your browser. 
#. cd - goes back to previous directory   

.. tip::

   The first time you run this, it will take long. :code:`docker pull` will download
   the Docker image. The next time, it will be faster, because the image does
   not have to be downloaded and `dockrun_t3rdf` will not build everything, it will only
   build changed files. 

.. important::

   If you switch branches, you should rebuild everything. Remove the Documentation-GENERATED-temp
   if in doubt or only generate documentation in master.

Make things easier for yourself by adding these commands as aliases or adding
them as commands in your IDE / editor. 

.. _documenting-system-extensions:

Document System Extensions
==========================

Documentation for system extensions is maintained within a :file:`Documentation`
directory in the respective system extension directory, e.g.
:file:`typo3/sysext/form/Documentation`.

Not all system extensions have their own documentation. Some documentation
(e.g. for the system extension *core*) is maintained within the :ref:`t3coreapi:start`.

If in doubt, ask in the **#typo3-cms-coredev** channel on Slack.

For starting a system extension from scratch, please see
:ref:`h2document:writing-doc-for-ext-from-scratch`.

For an overview of the rendered documentation for system extensions, see
`System Extensions <https://docs.typo3.org/typo3cms/SystemExtensions/Index.html>`__.

When you have made changes to the documentation, you can render
locally with docker to test your changes as described in
:ref:`render-the-changelog`.

More Information
================

* See `Documenting Changes <https://docs.typo3.org/typo3cms/extensions/core/latest/Changelog/Howto.html>`__ for more information on the Changelog
* See :ref:`extension-scanner` in TYPO3 Explained
