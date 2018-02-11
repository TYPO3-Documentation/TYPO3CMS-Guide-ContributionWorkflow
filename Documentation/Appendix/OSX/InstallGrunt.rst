.. include:: ../../Includes.txt

.. _osx-grunt:

====================
GRUNT install on OSX
====================

First off, make sure you installed **yarn** like described :ref:`here<osx-npm>`.

In your Terminal app navigate to the folder that you cloned the TYPO3 source into. Switch into the ``Build`` folder and run

.. code-block:: bash

   yarn install

This will install Grunt as well a s couple of Task plugins we use in the TYPO3 core.
To make sure grunt is running, run

.. code-block:: bash

   grunt css

This will run all registered tasks defined in the TYPO3 core.
