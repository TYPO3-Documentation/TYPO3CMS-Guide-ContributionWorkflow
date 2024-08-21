..  include:: /Includes.rst.txt

..  index::
    single: Documentation Contribution; Adding Documentation

..  _Bugfixing-Adding-documentation:
..  _Adding-documentation:

=================
Add Documentation
=================

**Quick links:**

*   :ref:`h2document:Formatting-with-reST`
*   :ref:`h2document:format-rest-cgl`
*   :ref:`h2document:rest-cheat-sheet`
*   :ref:`h2document:render-documentation-with-docker`


The documentation :doc:`TYPO3 Core Changelog <changelog:Index#typo3-core-changelog>`
and documentation for
:ref:`System Extensions <t3docs:System-Extensions>`
is maintained in the Core.

Quickstart to contribute documentation
======================================

To work on the Core documentation of TYPO3, you need to work with the main TYPO3
mono-repository. You can **not** contribute Documentation patches on single read-only
repositories like `https://github.com/typo3-cms/felogin`__ through the GitHub interface!

You can, however, use the GitHub interface and contribute to `https://github.com/TYPO3/typo3/tree/main/typo3/sysext/felogin`__.
Submitting a GitHub PR will result in a GitHub Action workflow that closes your
PR, transfers it to forge, transfers it to gerrit, and link them to each other. That workflow
can be prone to errors though, especially if a branch other than `main` is involved.

So, if possible you could better set follow the :ref:`Quickstart <quickstart>` guide to
set up a Core contribution installation. A lot can be left out,
as you do not necessarily even need a TYPO3 instance running when you only want to contribute
documentation.

The minimal steps to contribute documentation "the right way" (and to allow you to properly
participate in our review workflow) is this:

..  rst-class:: bignums-xxl

1.  Prerequisites

    From the :ref:`Quickstart Prerequisites <quickstart-prerequisites>` you need:

    1.  Operating System
    2.  GIT client
    3.  SSH client + keys
    4.  Optional Bonus: Docker (to render documentation), a suitable Text-Editor

2.  Set-up accounts

    You need all of the :ref:`Quickstart Accounts <quickstart-accounts>` (My TYPO3, GitHub, Gerrit, Forge)

3.  Set-up GIT

    Set up and clone the TYPO3 mono-repository as described in :ref:`Quickstart GIT <quickstart-git>`.

    Note: the steps :ref:`<quickstart-ddev>` and :ref:`<quickstart-typo3>` are not needed for Documentation-only use.

4.  Start documenting

    Now you can start editing files in, for example, :file:`typo3/sysext/felogin/Documentation/Index.rst` and
    when you are done, you can render the documentation (see :ref:`<render-extension>`) to verify
    the look of your changes.

5.  Create issue

    Once you feel comfortable and happy with your patch, you go to `create an issue on Forge
    <https://forge.typo3.org/projects/typo3cms-core/issues/new>`__. Choose the category `Documentation`
    and enter an appropriate description like:

        **Tracker**: Task

        **Subject**: Add example for EXT:felogin RedirectLoginHandler

        **Description**: (Describe what kind of documentation changes you made. Mention to which TYPO3 version it applies)

6.  Submit patch

    Now follow the steps outlined in :ref:`<quickstart-patch>`, and refer to the Documentation files
    you edited, instead of the PHP files given as examples there. This will then submit your patch
    to our Gerrit review instance.


..  index::
    single: Documentation Contribution Workflow; Add Changelog
    single: Changelog; Add Entries

..  _changelog:

Changelog
=========

Some patches require a :file:`.rst` (reStructuredText) Changelog file describing the change.
Not all patches
need an entry in the Changelog. Check the list below. Also see the current
:doc:`TYPO3 Core Changelog <changelog:Index#typo3-core-changelog>`
for some examples.

Every file may optionally contain tags, but it must contain at least a
`NotScanned`, `PartiallyScanned` or `FullyScanned` tag for the extension scanner.
See :ref:`t3coreapi:extension-scanner` in TYPO3 Explained for more
information.

..  _render-the-changelog:

Render the Changelog locally
----------------------------

If you have `Docker <https://www.docker.com>`__ or `Podman <https://podman.io/>`__
installed you can try out the rendering of the changelog locally:

..  tabs::

    ..  group-tab:: Docker

        ..  code-block:: bash

            cd typo3/sysext/core
            docker run --rm --pull always -v $(pwd):/project -it ghcr.io/typo3-documentation/render-guides:latest --config=Documentation
            xdg-open "Documentation-GENERATED-temp/Index.html"

    ..  group-tab:: Podman

        ..  code-block:: bash

            cd typo3/sysext/core
            docker run --rm --pull always -v $(pwd):/project -it ghcr.io/typo3-documentation/render-guides:latest --config=Documentation
            xdg-open "Documentation-GENERATED-temp/Index.html"

..  _render-extension:

Render any system documentation locally
---------------------------------------

As above, you can render any extension locally, too. You need to change the directory to the extension
directory you want to render. For `EXT:felogin` that would be:

..  tabs::

    ..  group-tab:: Docker

        ..  code-block:: bash

            cd typo3/sysext/felogin
            docker run --rm --pull always -v $(pwd):/project -it ghcr.io/typo3-documentation/render-guides:latest --config=Documentation
            xdg-open "Documentation-GENERATED-temp/Index.html"

    ..  group-tab:: Podman

        ..  code-block:: bash

            cd typo3/sysext/felogin
            docker run --rm --pull always -v $(pwd):/project -it ghcr.io/typo3-documentation/render-guides:latest --config=Documentation
            xdg-open "Documentation-GENERATED-temp/Index.html"

..  index::
    single: Tools; reST File Generator
    single: Changelog; Generate new Entries
    single: Documentation Contribution Workflow; Generating reST Files

..  _rest-file-generator:

Forger reST Helper
------------------

Use the `Forger reST Helper <https://forger.typo3.com/utilities/rst>`__ to
generate changelogs.

This is strongly recommended because the tool will generate correctly
formatted files. You can always add more to the .rst file directly later.

Select the type of rst snippet you want to create, enter your issue number
and click the search button. Select appropriate tags.

When you are done, copy the generated text and create a file with the same
name as suggested in the generator in
:file:`typo3/sysext/core/Documentation/Changelog/...`.


Types of Changes
----------------

There are four different types of changes
which have to follow a certain format and **always**
need to go into :file:`typo3/sysext/core/Documentation/Changelog/<release>/`.

Choose one which fits your patch:

..  index::
    single: Documentation Contribution Workflow; Breaking Changes

..  _documenting-changelog-breaking-changes:

Breaking Changes
~~~~~~~~~~~~~~~~

A patch moved or removed a specific part of core functionality
that may break extensions if they use this part.

**Mandatory sections:**

#.  **Description** - why things had to break backwards compatibility.

#.  **Impact** - how will the change affect your installation.

#.  **Affected Installations** - describe scenarios under which circumstances
    a TYPO3 install will be affected by this change.

#.  **Migration** - provide instructions what needs to be done to get things
    working again. Explicitly mention if no migration is possible.


..  index::
    single: Documentation Contribution Workflow; Deprecations

..  _documenting-changelog-deprecations:

Deprecations
~~~~~~~~~~~~

A patch deprecates a certain core functionality
for a planned removal. See more information: :ref:`Deprecations <deprecations>`

**Mandatory sections:**

#.  **Description** - why things had to be deprecated.

#.  **Impact** - how will the change affect your installation.

#.  **Affected Installations** - describe scenarios under which circumstances
    a TYPO3 install will be affected by this change.

#.  **Migration** - provide instructions what needs to be done to get things
    working again. Explicitly mention if no migration is possible.


..  index::
   single: Documentation Contribution Workflow; Features

..  _documenting-changelog-features:

Features
~~~~~~~~

A patch adds new functionality.

**Mandatory sections:**

#.  **Description** - what can the new feature do.

#.  **Impact** - how users are affected by this new feature.


..  index::
   single: Documentation Contribution Workflow; Important Information

..  _documenting-changelog-important-information:

Important Information
~~~~~~~~~~~~~~~~~~~~~

Anything that does not fit the other categories but is
important enough to require a Changelog entry.

#. **Description** - describe what is so important it needed an rst snippet

..  index::
    single: Documentation Contribution Workflow; Checking reST Files
    single: Tools; Checking reST Files
    single: Changelog; Checking

..  _changelog-check-rst:

Check Your `rst` File
---------------------

When your change is finished, you can run the following script to check that
your rst file is ok. The script will check all files in
:file:`typo3/sysext/core/Documentation/Changelog`:

..  code-block:: shell
    :caption: shell command

    Build/Scripts/validateRstFiles.php

This script will check if the .rst files contain all mandatory tags that
are required for the Changelog. It will **not** do a reST syntax check.

In order to make sure that your file contains no syntax errors and will
be rendered correctly, do one or more of the following:

*   Check out :ref:`h2document:format-rest-cgl`.
*   :ref:`Render the Changelog locally <render-the-changelog>` with Docker or
    Podman and resolve all warnings.

..  index::
    single: Documentation Contribution Workflow; Rendering Changelog
    single: Tools; Rendering Changelog
    single: Changelog; Rendering

..  _documentation-main:

Policy for Changing the Main Documentation
==========================================

Once a new TYPO3 release comes out, the main documentation (e.g. :ref:`t3coreapi:start`,
:ref:`t3tca:start` etc.) must be updated.

The procedure is documented in :ref:`h2document:update-docs`.

..  index::
    single: Documentation Contribution Workflow; Documenting System Extensions

..  _documenting-system-extensions:

Document System Extensions
==========================

Documentation for system extensions is maintained within a :file:`Documentation`
directory in the respective system extension directory, e.g.
:file:`typo3/sysext/form/Documentation`.

Not all system extensions have their own documentation. Some documentation
(e.g. for the system extension *core*) is maintained within the :ref:`t3coreapi:start`.

If in doubt, ask in the **#typo3-cms-coredev** channel on Slack.

For starting a system extension from scratch, please see
:ref:`h2document:how-to-start-docs-extension`.

For an overview of the rendered documentation for system extensions, see
`System Extensions <https://docs.typo3.org/typo3cms/SystemExtensions/Index.html>`__.

When you have made changes to the documentation, you can render
locally with docker to test your changes as described in
:ref:`render-the-changelog`.

More Information
================

*   See :doc:`Documenting Changes <changelog:Changelog/Howto#documenting-changes>`
    for more information on the Changelog
*   See :ref:`extension-scanner` in TYPO3 Explained
