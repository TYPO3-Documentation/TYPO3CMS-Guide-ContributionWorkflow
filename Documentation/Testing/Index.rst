.. include:: ../Includes.txt
.. highlight:: shell

.. _testing:

=========
Run Tests
=========

For every patch that is uploaded to the Gerrit review server, a number
of tests are run automatically using Bamboo.

.. hint::
   For more in-depth information about how TYPO3 runs the automatic tests with Bamboo
   see the series "Testing TYPO3's Core" on the TYPO3 Blog. You can
   find the links in this article:
   `Serious software testing: TYPO3 runs its 20,000th build!
   <https://typo3.com/blog/serious-software-testing-typo3-runs-its-20000th-build>`__

You can run these tests locally with docker using a similar setup.

Practical Considerations
========================

Running *all* tests takes a considerable amount of time on a standard development
machine, so it is not recommended to run all tests on your local
platform for every patch you wish to submit. That's what Bamboo is for.

You might however want to run specific tests, for example for the following
use cases:

* You wrote new tests or changed functionality that might break tests. You want to
  run specific tests and possibly debug them.
* You want to run some quick specific tests, for example to test for cgl
  (coding guideline) problems or syntax errors in PHP (lint) *before* you
  upload your patch.

How to Run the Tests
====================

Tests can be run using the script `Build/Scripts/runTests.sh`. This
script provides a number of command line options for executing various tests
in different environments (PHP version, database engine, ...). The script
automatically runs docker using an image which corresponds to the environment
you provide with the command line arguments.


Run Tests with runTests.sh using docker
=======================================

.. _testing-install-docker:

Prerequisites
-------------

You might want to run the script with the -h option to get up-to-date
information about system requirements::

   Build/Scripts/runTests.sh -h

We cannot test the script with all current environments, so get the latest
`docker <https://www.docker.com/get-docker>`__
and `docker-compose <https://docs.docker.com/compose/>`__
for your system and ask for help in Slack if something does
not work as expected.

Examples
--------

All examples expect to be executed from a git cloned working directory
of master (as described in :ref:`setup`).

.. _hint::

   Running the script or a specific command line argument combination for the first
   time will take some time, because all necessary prerequisites for the docker images
   need to be fetched. The next runs should be faster.

Show help
~~~~~~~~~

.. code-block::

   ./Build/Scripts/runTests.sh -h

Run all unit tests
~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   Build/Scripts/runTests.sh

Run unit tests with xdebug (uses default port 9000)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   ./Build/Scripts/runTests.sh -x
   
Run specific unit tests with xdebug
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   Build/Scripts/runTests.sh -x <directory or file>

Example::

   Build/Scripts/runTests.sh -x typo3/sysext/core/Tests/Unit/LinkHandling/   

Run functional tests
~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   ./Build/Scripts/runTests.sh -s functional

Run functional tests with PostgreSQL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   ./Build/Scripts/runTests.sh -s functional -d postgres

Run acceptance tests
~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   ./Build/Scripts/runTests.sh -s acceptance

Depending on the power of your local machine you can expect about 30 minutes
or more for the acceptance tests.


Additional hints
----------------

Be sure to exclude the `typo3temp` directory from indexing in your IDE (e.g. PhpStorm)
before starting the acceptance tests.


Troubleshooting
---------------

If something does not work as expected, it might help to run the script
with the additional `-v` (for verbose output) option.

Before diagnosing problems in the script, make sure to check if
docker is running smoothly on your system.

A quick test is to run the docker hello-world image::

   docker run hello-world

You should see something like this message:

.. code-block:: none

   Hello from Docker!
   This message shows that your installation appears to be working correctly.

See `Get Started, Part 1: Orientation and setup <https://docs.docker.com/get-started/#test-docker-version>`__

Also, see docker troubleshooting pages for more in-depth information,
such as `Docker for Mac: Logs and troublehooting
<https://docs.docker.com/docker-for-mac/troubleshoot/>`__

Results
-------

All results will be displayed on the screen. The script should exit with
standard exit codes:

* 0 means all is ok
* != 0 means error

Reports of the acceptance tests will be stored in
:file:`typo3temp/var/tests/AcceptanceReports` with screenshots from the browser.

Run tests directly without docker
=================================

If you have problems with docker, you can run some of the lowlevel scripts and
commands directly. However it does depend on your system, whether they run
successfully. The docker / runTests.sh method gives us the possibility to have
a controlled environment where the tests run in. That also means, the databases
that the functional tests require are already created automatically. That is not
the case, if you run the tests locally on your current system.

That being said, running the tests directly is not being officially supported,
but you can try this out yourself.

You can look in the source of Build/Scripts/runTests.sh or rather in
Build/testing-docker/local/docker-compose.yml to see which commands the runTests.sh
script calls and run these directly. Not everything will work, because there may
be dependencies, that are only available in the docker container.

Also, you can run some of the scripts in Build/Scripts directly.

Examples:

Run all unit tests
------------------

.. code-block:: bash

   bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/UnitTests.xml

Run specific unit tests
-----------------------

.. code-block:: bash

   bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/UnitTests.xml <directory or file>

Example::

   bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/UnitTests.xml typo3/sysext/core/Tests/Unit/LinkHandling/


Run all functional tests
------------------------

.. code-block:: bash

  bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/FunctionalTests.xml

Check for Coding Guidelines
---------------------------

The cgl checking commands / scripts not only check, they repair as well!

You can use the already mentioned script cglFixMyCommit::

Mac / Linus::

   Build/Scripts/cglFixMyCommit.sh

Windows::

   Build/Scripts/cglFixMyCommit.sh


.. important::

   Remember, cglFixMyCommit only checks files in latest commit, so you must have
   committed already. Commit again with --amend after you checked things and repaired
   the file, or call cglFixMyCommit.sh -h for alternatives.

More information
================

* More details about the test system, test strategies, execution and set up can
  be found in :ref:`TYPO3 explained <t3coreapi:testing>`.
* :ref:`t3coreapi:testing-writing-unit` in TYPO3 explained
* external: `Serious software testing: TYPO3 runs its 20,000th build!
  <https://typo3.com/blog/serious-software-testing-typo3-runs-its-20000th-build>`__ for more information
  on how the automatic tests are run with Bamboo for every patchset that is uploaded for the core
