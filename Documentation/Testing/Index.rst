.. include:: ../Includes.txt
.. highlight:: shell

.. _testing:

=========
Run tests
=========

For every patch that is uploaded to the Gerrit review server, a number
of tests are run automatically using Bamboo.

.. hint::
   For more in-depth information about how TYPO3 runs the automatic tests with Bamboo
   see the series "Testing TYPO3's Core" on the TYPO3 Blog. You can
   find the links in this article:
   `Serious software testing: TYPO3 runs its 20,000th build!
   <https://typo3.com/blog/serious-software-testing-typo3-runs-its-20000th-build>`__

You can run these tests locally with docker using the same setup Bamboo uses.

Practical considerations
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

How to run the tests
====================

Tests can be run using the script `Build/Scripts/runTests.sh`. This
script provides a number of command line options for executing various tests
in different environments (PHP version, database engine, ...). The script
automatically runs docker using an image which corresponds to the environment
you provide with the command line arguments.

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

**Show help**::

   ./Build/Scripts/runTests.sh -h

**Run all unit tests**::

   ./Build/Scripts/runTests.sh

**Run unit tests with xdebug (uses default port 9000)**::

   ./Build/Scripts/runTests.sh -x

**Run functional tests**::

   ./Build/Scripts/runTests.sh -s functional

**Run functional tests with PostgreSQL**::

   ./Build/Scripts/runTests.sh -s functional -d postgres

**Run acceptance tests**::

   ./Build/Scripts/runTests.sh -s acceptance

Depending on the power of your local machine you can expect about 30 minutes
or more for the acceptance tests.

**See help for more options**::

   ./Build/Scripts/runTests.sh -h

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
