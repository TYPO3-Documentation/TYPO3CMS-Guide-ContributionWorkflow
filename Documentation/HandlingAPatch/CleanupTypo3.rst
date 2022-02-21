.. include:: ../Includes.txt

.. highlight:: bash

.. _cleanup-tasks:

=============
Cleanup tasks
=============

.. _Gerrit-Reset-to-a-clean-state:
.. _reset-to-a-clean-state:

Cleanup git repository
======================

Before :ref:`Cherry-picking a patch <cherry-pick-a-patch>` or starting a new patch::

   git reset --hard origin/main
   git pull


.. _cleanup-typo3:

Cleanup TYPO3 installation
==========================

After downloading a new patch or making changes to an existing patch, you may need to
cleanup your TYPO3 installation.

It depends on the files that have changed, what you need to execute. In
any case or if in doubt, you can safely perform all steps.

**Flush the cache**:

.. code-block:: shell
   
   bin/typo3 cache:flush
   
Or via the install tool

.. image:: /Images/ManualScreenshots/flush_cache.svg
   :class: with-shadow

**Changes in composer.json**::

   composer install

**Changes in .css / .js files**:

Delete browser cache or
`hard refresh <https://www.getfilecloud.com/blog/2015/03/tech-tip-how-to-do-hard-refresh-in-browsers/>`__
(e.g. CTRL + F5)

**Changes in DB schema (ext_tables.sql)**:

Maintenance: Analyze Database Structure, Apply selected changes.

.. image:: /Images/ManualScreenshots/analyze.svg
   :class: with-shadow
