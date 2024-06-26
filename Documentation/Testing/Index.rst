.. include:: /Includes.rst.txt
.. highlight:: shell



.. index::
   single: Code Contribution Workflow; Running Tests Locally
   single: Testing; Running Tests Locally
   single: Code Contribution Workflow; runTests.sh
   single: runTests.sh

.. _testing:
.. _runTests_sh:

=================
Using runTests.sh
=================

What is runTests.sh?
====================

This is a shell script which is included in the TYPO3 Core git repository. It
used to supply commands for running tests, but has since evolved to include
other commands as well for checking, fixing, building etc. It will be used for a
number of tasks during the core contribution workflow.

The script uses Docker and several Docker images to run the
tasks - using the correct versions (of PHP etc.) for the current
branch of your TYPO3 repository.

Show help
=========

It is recommended to use the `-h` option (help) to show the help output and
especially look at the beginning of the output for a description and the listing
of dependencies. The listing in section `-s` shows available commands, and the bottom
lists several examples you can copy+paste to try.

Show help:

.. code-block:: bash
   :caption: shell command

   Build/Scripts/runTests.sh -h


.. _runTests.sh-prerequisites:

Prerequisites
=============

See the listed options/commands in the help output.

Options
=======

-h
   show help
-s
   choose the command to run (if omitted, unit tests are run)
-p
   PHP version (if omitted, the default version is used)

For more options, see the help (`-h`).

We will quickly go over each type of command next.

Output example:

.. code-block:: text

   Options:
    -s <...>
        Specifies which test suite to run
            - acceptance: main application acceptance tests
            - acceptanceInstall: installation acceptance tests, only with -d mariadb|postgres|sqlite
            - buildCss: execute scss to css builder
            - buildJavascript: execute typescript to javascript builder
            - cgl: test and fix all core php files
   ...

Commands
========

We categorize the commands and show some examples here. It is recommended to
use `-h` as described previously to view the help output and examples. The
trailing `*` is used as wildcard to indicate that there are further commands
which start with the same string.

Commands for building:

*  -s composerInstall (composerInstall*)
*  -s buildCss: build CSS assets
*  -s buildJavascript
* ...

Checks and fixes, run static analyzer, lint etc:

*  -s cglGit : check (and fix!) the CGL issues in the files which are in the most
   recent git commit
*  -s lintPhp
*  -s lintScss
*  -s phpstan
*  -s checkComposer (check*)
* ...

Commands for running tests:

*  -s unit (unit*)
*  -s functional (functional*)
*  -s acceptance (acceptance*)
* ...

Cleanup, clear cache:

*  -s clean (clean*)
* ...

Additional setup
================

Be sure to exclude the :file:`typo3temp` directory from indexing in your IDE
(e.g. PhpStorm) before starting the acceptance tests.

Examples
========

All examples expect to be executed from a git cloned working directory
of TYPO3 CMS **main** branch (as described in :ref:`setup`).

.. note::

   Running the script or a specific command line argument combination for the first
   time will take some time, because all necessary prerequisites for the docker images
   need to be fetched. The next runs should be faster.

composer install
----------------

Run composer install:

.. code-block:: bash
   :caption: shell command

   Build/Scripts/runTests.sh -s composerInstall

.. _runTestsShCgl:
.. _cgl-fix-my-commit:

CGL check and fix
-----------------

Do Coding Guidelines checks and fix them.

Check and fix. This applies the command only to the files in the latest commit:

.. code-block:: bash
   :caption: shell command

   Build/Scripts/runTests.sh -s cglGit

Check and do NOT fix. This applies the command only to the files in the latest
commit:

.. code-block:: bash
   :caption: shell command

   Build/Scripts/runTests.sh -s cglGit -n


Run all unit tests
------------------

.. code-block:: bash
   :caption: shell command

   Build/Scripts/runTests.sh

Run unit tests with xdebug (uses default port 9000)
---------------------------------------------------

.. code-block:: bash
   :caption: shell command

   ./Build/Scripts/runTests.sh -x

Run specific unit tests with xdebug
-----------------------------------

.. code-block:: bash
   :caption: shell command

   Build/Scripts/runTests.sh -x <directory or file>

Example::

   Build/Scripts/runTests.sh -x typo3/sysext/core/Tests/Unit/LinkHandling/

Run functional tests
--------------------

.. code-block:: bash
   :caption: shell command

   ./Build/Scripts/runTests.sh -s functional

Run functional tests with PostgreSQL
------------------------------------

.. code-block:: bash
   :caption: shell command

   ./Build/Scripts/runTests.sh -s functional -d postgres

Run acceptance tests
--------------------

.. code-block:: bash
   :caption: shell command

   ./Build/Scripts/runTests.sh -s acceptance

Depending on the power of your local machine you can expect about 30 minutes
or more for the acceptance tests.

Troubleshooting
===============

If something does not work as expected, it might help to run the script
with the additional `-v` (for verbose output) option.

Before diagnosing problems in the script, make sure to check if
Docker is running smoothly on your system.

A quick test is to run the docker hello-world image:

.. code-block:: bash
   :caption: shell command

   docker run hello-world

You should see something like this message:

.. code-block:: text
   :caption: result

   Hello from Docker!
   This message shows that your installation appears to be working correctly.

See `Get Started, Part 1: Orientation and setup <https://docs.docker.com/get-started/#test-docker-version>`__

Also, see docker troubleshooting pages for more in-depth information,
such as `Docker for Mac: Logs and troubleshooting
<https://docs.docker.com/docker-for-mac/troubleshoot/>`__

Results
=======

All results will be displayed on the screen. The script should exit with
standard exit codes:

*  0 means all is ok
*  != 0 means error

Reports of the acceptance tests will be stored in
:file:`typo3temp/var/tests/AcceptanceReports` with screenshots from the browser.



.. index::
   single: Code Contribution Workflow; Running Tests Locally without Docker
   single: Testing; Running Tests Locally without Docker

.. _run-tests-directly-without-docker:

Direct commands without Docker
==============================

If you have problems with docker, you can run some of the lowlevel scripts and
commands directly. However it does depend on your system, whether they run
successfully. The docker / :file:`runTests.sh` method gives us the possibility to have
a controlled environment where the tests run in. That also means, the databases
that the functional tests require are already created automatically. That is not
the case, if you run the tests locally on your current system.

That being said, running the tests directly is not being officially supported,
but you can try this out yourself.

You can look in the source of :file:`Build/Scripts/runTests.sh` or rather in
:file:`Build/testing-docker/local/docker-compose.yml` to see which commands the :file:`runTests.sh`
script calls and run these directly. Not everything will work, because there may
be dependencies, that are only available in the docker container.

Also, you can run some of the scripts in :file:`Build/Scripts` directly.

Examples:

Run all unit tests
------------------

.. code-block:: bash
   :caption: shell command

   bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/UnitTests.xml

Run specific unit tests
-----------------------

.. code-block:: bash
   :caption: shell command

   bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/UnitTests.xml <directory or file>

Example::

   bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/UnitTests.xml typo3/sysext/core/Tests/Unit/LinkHandling/


Run all functional tests
------------------------

.. code-block:: bash
   :caption: shell command

   bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/FunctionalTests.xml



.. index::
   single: Code Contribution Workflow; Checking for Coding Guidelines
   single: Tools; Checking for Coding Guidelines

.. _check-for-coding-guidelines:

Check for Coding Guidelines
---------------------------

The cgl checking commands / scripts not only check, they repair as well!

Mac / Linux:

.. code-block:: bash
   :caption: shell command

   Build/Scripts/cglFixMyCommit.sh

Windows:

.. code-block:: bash
   :caption: shell command

   Build/Scripts/cglFixMyCommit.bat


.. important::

   Remember, cglFixMyCommit only checks files in latest commit, so you must have
   committed already. Commit again with --amend after you checked things and repaired
   the file, or call cglFixMyCommit.sh -h for alternatives.

More information
================

*  More details about the test system, test strategies, execution and set up can
   be found in :ref:`TYPO3 explained <t3coreapi:testing>`.

..  toctree::
    :glob:

    *
