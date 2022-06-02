.. include:: /Includes.rst.txt

.. highlight:: bash

.. _setup-typo3:
.. _setup-typo3-installation:

============================
Setup the TYPO3 installation
============================

.. important::

   If you are setting TYPO3 up with DDEV, you can skip this page and jump straight to

   .. rst-class:: horizbuttons-primary-m

   - :ref:`DDEV <settting-up-typo3-with-ddev>`

You will now need to setup a working installation
of TYPO3. There are different ways how you can do this. We
provide a few examples in the Appendix:

* :ref:`DDEV <settting-up-typo3-with-ddev>`
* :ref:`setting-up-typo3-manually`

In any case, use the cloned Git repository as basis (see :ref:`git-clone`).

.. index::
   single: Code Contribution Workflow; composer install

.. _composer-install:

composer install
================

Run composer install in the same directory you cloned the TYPO3 CMS core
repository.

It is recommended to use runTests.sh for this. The "direct command" is an
alternative. You only need to run one of these!


.. note::

   This is **no longer necessary for the current main branch**, but may be necessary
   for older version (if working in other branches) (see related
   `issue <https://github.com/TYPO3-Documentation/TYPO3CMS-Guide-ContributionWorkflow/issues/254>`__).
   Composer could not detect the TYPO3 version of your cloned project because there was none. Before you run
   `composer install` may need to export the `COMPOSER_ROOT_VERSION environment variable <https://getcomposer.org/doc/03-cli.md#composer-root-version>`__.
   Here you need to set a full version string matching the TYPO3 version of your clone.

   Example:

   .. code-block:: bash

      # cd <cloned project>
      export COMPOSER_ROOT_VERSION=12.0.0


.. tabs::

   .. group-tab:: runTests.sh

      .. code-block:: bash

         Build/Scripts/runTests.sh -s composerInstall

   .. group-tab:: direct command

      .. code-block:: bash

         composer install
