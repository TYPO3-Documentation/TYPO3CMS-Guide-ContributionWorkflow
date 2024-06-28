.. include:: /Includes.rst.txt

.. highlight:: bash

.. _cleanup-tasks:

=============
Cleanup tasks
=============

.. _Gerrit-Reset-to-a-clean-state:
.. _reset-to-a-clean-state:

Cleanup git repository
======================

Before :ref:`Cherry-picking a patch <cherry-pick-a-patch>` or starting a new patch:

.. code-block:: bash
   :caption: shell command

   git fetch --all
   git reset --hard origin/main
   git pull --rebase


.. _cleanup-typo3:

Cleanup TYPO3 installation
==========================

After downloading a new patch or making changes to an existing patch, you may need to
cleanup your TYPO3 installation.

It depends on the files that have changed, what you need to execute. In
any case or if in doubt, you can safely perform all steps.

**Flush the cache**:

.. code-block:: bash
   :caption: shell command

   Build/Scripts/runTests.sh -s clean
   # For DDEV environments, prefix with `ddev ...`
   bin/typo3 cache:flush
   bin/typo3 cache:warmup

**Changes in composer.json**:

.. tabs::

   .. group-tab:: runTests.sh

      .. code-block:: bash

         Build/Scripts/runTests.sh -s composerInstall

   .. group-tab:: direct command

      .. code-block:: bash

         composer install

**Changes in .css / .js files**:

Delete browser cache or
`hard refresh <https://www.filecloud.com/blog/2015/03/tech-tip-how-to-do-hard-refresh-in-browsers/>`__
(e.g. CTRL + F5)

Also you may need to create the JS/CSS assets:

   .. code-block:: bash

      ./Build/Scripts/runTests.sh -s buildCss
      ./Build/Scripts/runTests.sh -s buildJavascript

**Changes in DB schema (ext_tables.sql)**:

:guilabel:`Maintenance: Analyze Database Structure, Apply selected changes.`

.. image:: /Images/ManualScreenshots/analyze.svg
   :class: with-shadow
