.. include:: ../../Includes.txt

.. _osx-bower:

====================
BOWER install on OSX
====================

First off, make sure you installed **npm** like described :ref:`here<osx-npm>`.

In your Terminal app navigate to the folder that you cloned the TYPO3 source into. Switch into the ``Build`` folder and run

.. code-block:: bash

   npm install bower

This will install Bower and all its dependencies.
To make sure Bower works, run

.. code-block:: bash

   bower -v

If you get a version number back, everything went fine and you can run

.. code-block:: bash

   bower update

to load all frontend dependencies for the TYPO3 core.
