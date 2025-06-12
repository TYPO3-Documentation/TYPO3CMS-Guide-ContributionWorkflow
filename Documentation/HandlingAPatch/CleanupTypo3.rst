..  include:: /Includes.rst.txt

..  highlight:: bash

..  _cleanup-tasks:

=============
Cleanup tasks
=============

..  _Gerrit-Reset-to-a-clean-state:
..  _reset-to-a-clean-state:

Cleanup git repository
======================

Before :ref:`Cherry-picking a patch <cherry-pick-a-patch>` or starting a new patch:

..  code-block:: bash
    :caption: **Reset local repository**

    Build/Scripts/runTests.sh -s clean && \
        git fetch --all && \
        git reset --hard origin/main && \
        git pull --rebase


..  _cleanup-typo3:

Cleanup TYPO3 installation
==========================

After downloading a new patch or making changes to an existing patch, you may need to
cleanup your TYPO3 installation.

It depends on the files that have changed, what you need to execute. In
any case or if in doubt, you can safely perform all steps.

..  code-block:: bash
    :caption: **Flush the cache**:

    ddev typo3 cache:flush && \
        ddev typo3 cache:warmup

..  code-block:: bash
    :caption: **Changes in composer.json**:

    Build/Scripts/runTests.sh -s composerInstall

**Changes in .css / .js files**:

Delete browser cache or
`hard refresh <https://www.filecloud.com/blog/2015/03/tech-tip-how-to-do-hard-refresh-in-browsers/>`__
(e.g. CTRL + F5)

Also you may need to create the JS/CSS assets:

..  code-block:: bash

    ./Build/Scripts/runTests.sh -s build

**Changes in DB schema (ext_tables.sql)**:

..  code:: bash
    :caption: Create missing tables and fields

    ddev typo3 extension:setup

:guilabel:`Maintenance: Analyze Database Structure, Apply selected changes.`

..  image:: /Images/ManualScreenshots/analyze.svg
    :class: with-shadow

**Update core-testing docker images**

..  code:: bash
    :caption:  **Pull latest core-testing images versions**

    ./Build/Scripts/runTests.sh -u


..  _cleanup-typo3-one-liner:

One-liner command
~~~~~~~~~~~~~~~~~

If you want to reset your local installation in one go, you could use the following
one-liner command, combining the mentioned parts from above:

..  code:: bash
    :caption: **Reset local repository to upstream state**

    ./Build/Scripts/runTests.sh -u && \
        Build/Scripts/runTests.sh -s clean && \
        git fetch --all && \
        git reset --hard origin/main && \
        git pull --rebase && \
        ./Build/Scripts/runTests.sh -s composerInstall && \
        ddev typo3 cache:flush && \
        ddev typo3 cache:warmup && \
        ddev typo3 extension:setup

..  note::

    You may still check the `Database Analyzer` in the backend for changes or
    removed columns and tables to ensure a clean state.
