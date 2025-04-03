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
number of tasks and will be a vital part during your Core contribution workflow.

The script uses Docker (also supporting podman) and several Docker images to run the
tasks - using the correct versions (of PHP, Node/NPM etc.) for the current
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
-b
   choose podman (default) or docker for image execution
-d
   Database type (sqlite, mariadb, mysql, postgres)
-i
   Database version in conjunction with `-d`, for example `-d mariadb -i 11.4` for MariaDB 11.4
-x
   Enable xdebug usage
-u
   Update docker image versions

For more options, see the help (`-h`).

We will quickly go over each type of command next.

Output example:

.. code-block:: text

   Options:
    -s <...>
        Specifies which test suite to run
            - acceptance: main application acceptance tests
            - acceptanceInstall: installation acceptance tests, only with -d mariadb|postgres|sqlite
            - build: execute frontend build (TypeScript, Sass, Contrib, Assets)
            - cgl: test and fix all core php files
   ...

Commands
========

We categorize the commands and show some examples here. It is recommended to
use `-h` as described previously to view the help output and examples. The
trailing `*` is used as wildcard to indicate that there are further commands
which start with the same string.

Commands for building:

*  `-s composerInstall`: install composer dependencies from `composer.lock`
*  -s build: build CSS+JS assets
* ...

Checks and fixes, run static analyzer, lint etc:

*  -s cglGit : check (and fix!) the CGL issues in the files which are in the most
   recent git commit
*  -s cgl (cgl*)
*  -s lintPhp
*  -s lintScss (lint*)
*  -s phpstan (phpstan*)
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

Dispatchers:

*  -s npm -- `[npm command]`
*  -s composer -- `[composer command]`

Additional setup
================

Be sure to exclude the :file:`typo3temp` and :file:`.cache` directory from indexing in your IDE
(e.g. PhpStorm) before starting the acceptance tests.

Also, if you are using `DDEV` for example with `Mutagen` performing filesystem
synchronization, it is vital that you configure the `typo3temp` and `.cache` directory
to be excluded in your file :file:`.ddev/mutagen/mutagen.yml` like this:

..  code-block:: yaml

    sync:
      defaults:
        mode: "two-way-resolved"
        stageMode: "neighboring"
        ignore:
          paths:
            # ...
            - "typo3temp/"
            - "public/typo3temp"
            - ".cache"
            # ...

Due to the testing framework and involved components like PHPstan,
PHPUnit and Composer writing many, many small files this can make
your tests several HUNDREDS percent slower, especially on macOS.

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

Perform checks on Coding Guidelines and fix them.

This applies the command only to the files in the latest commit:

.. code-block:: bash
   :caption: shell command

   Build/Scripts/runTests.sh -s cglGit

If you only want to see possible fixes being applied, you can
execute the command in "dry-run" mode:

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

There is no built-in debugging to the `runTests.sh` script. It can happen
that (docker or other) command execution needs to be debugged.

For this you need to get your hands dirty and inspect the file. Most commands
are performed like this:

.. code-block:: bash
   :caption: runTests.sh (excerpt)

    lintScss)
        COMMAND="cd Build; npm ci || exit 1; node_modules/grunt/bin/grunt stylelint"
        ${CONTAINER_BIN} run ${CONTAINER_COMMON_PARAMS} --name lint-css-${SUFFIX} -e HOME=${CORE_ROOT}/.cache ${IMAGE_NODEJS} /bin/sh -c "${COMMAND}"
        SUITE_EXIT_CODE=$?
        ;;

to debug this, you can add an "echo" statement to reveal `$COMMAND` and also put
an `echo` before the `${CONTAINER_BIN}` statement, like this:

.. code-block:: bash
   :caption: runTests.sh (excerpt)

    lintScss)
        COMMAND="cd Build; npm ci || exit 1; node_modules/grunt/bin/grunt stylelint"
        CONTAINER_COMMAND="${CONTAINER_BIN} run ${CONTAINER_COMMON_PARAMS} --name lint-css-${SUFFIX} -e HOME=${CORE_ROOT}/.cache ${IMAGE_NODEJS} /bin/sh -c ${COMMAND}"
        echo "EXECUTE:"
        echo $COMMAND
        echo $CONTAINER_COMMAND
        SUITE_EXIT_CODE=$?
        ;;

Then when you execute the script, instead of the command being executed, you can see what is used.
Copy+paste that execution to your local shell and see if you can spot specific errors.
You may want to add options like `-v` to the `$COMMAND` to see, why that command may fail.

Results
=======

All results will be displayed on the screen. The script should exit with
standard exit codes:

*  0 means all is ok
*  != 0 means error

Reports of the acceptance tests will be stored in
:file:`typo3temp/var/tests/AcceptanceReports` with screenshots from the remotely controlled browser.



.. index::
   single: Code Contribution Workflow; Running Tests Locally without Docker
   single: Testing; Running Tests Locally without Docker

.. _run-tests-directly-without-docker:

Direct commands without Docker
==============================

If you have problems with docker, you can run some of the lowlevel scripts and
commands directly. However it does depend on your system, whether they run
successfully (due to PHP, composer and other dependencies).
The docker / :file:`runTests.sh` method gives us the possibility to have
a controlled environment where the tests run in. That also means, the databases
that the functional tests require are already created automatically. That is not
the case, if you run the tests locally on your current system.

That being said, running the tests directly is not being officially supported,
but you can try this out yourself.

You can look in the source of :file:`Build/Scripts/runTests.sh` to see which
commands the :file:`runTests.sh` script calls and run these directly
(also see the "Troubleshooting" section above). Not everything will work, because there may
be dependencies, that are only available in the docker container.

Also, you can run some of the scripts in :file:`Build/Scripts` directly,
which are otherwise just dispatched from within a docker container.

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
They can also be utilized from GIT hooks.

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
   committed already. Commit again with `git commit --amend` after you checked things and repaired
   the file, or call `cglFixMyCommit.sh -h` for alternatives.

More information
================

*  More details about the test system, test strategies, execution and set up can
   be found in :ref:`TYPO3 explained <t3coreapi:testing>`.

..  toctree::
    :glob:

    *
