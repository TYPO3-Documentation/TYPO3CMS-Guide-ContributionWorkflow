.. include:: ../Includes.txt
.. highlight:: shell

.. _testing:

================
Testing the Core
================

For every patch that is uploaded to the Gerrit review server, a number
of tests are run automatically using Bamboo.

.. hint::
   For more in-depth information about how TYPO3 runs the automatic tests with Bamboo
   see the series "Testing TYPO3's Core" on the TYPO3 Blog. You can
   find the links in this article:
   `Serious software testing: TYPO3 runs its 20,000th build!
   <https://typo3.com/blog/serious-software-testing-typo3-runs-its-20000th-build>`__

You can run these tests locally with docker using the same setup Bamboo uses.


.. _testing-install-docker:

Install Docker
==============

All you need for this is `Docker installed locally.
<https://www.docker.com/get-docker>`__


Quickstart
==========

.. _testing-docker-pull:

docker pull
-----------

You have to pull the necessary docker image for PHP from `Bitbucket T3COM bamboo-
remote-agent <https://bitbucket.typo3.com/projects/T3COM/repos/bamboo-remote-agent/browse>`__.
There are various images for testing with different PHP versions and
different databases and the functional tests. As an example, if you want to run
the unit tests for current master you have to load the php72 container::

   docker pull typo3gmbh/php72:latest

.. _testing-docker-run:

docker run
----------

There are different ways to do this, you can start an interactive session
on your docker container or you can execute one of the commands for
running and executing the tests in one step.

Conventions
-----------

* You should be in your current core directory. 
* The directory inside the docker container will be :file:`/srv/tmp/cms`

.. _testing-docker-run-bash:


docker run - Interactive method
-------------------------------

docker run
~~~~~~~~~~

Start the container like this. It leaves the bash shell open::

   docker run -it --rm \
      --name=typo3_core_test \
      -v <absolute local path where your typo3 checkout is>:/srv/tmp/cms \
      -w /srv/tmp/cms \
      typo3gmbh/php72:latest \
      /sbin/my_init -- bash


Run all Tests in one directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To run only the tests in a specific directory (and its subdirectories)::

   bin/phpunit typo3/sysext/redirects/Tests/Unit/Service



Run all Unit Tests
------------------

*From inside the container*, to run all unit tests::


    export HOME=/root \
    bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/UnitTests.xml


Run all Functional Tests
------------------------

Running the functional tests is almost the same. It is just the phpunit command
that looks a bit different. For the MySQL setup use::

   export typo3DatabaseName="func" \
          typo3DatabaseUsername="funcu" \
          typo3DatabasePassword="funcp" \
          typo3DatabaseHost="localhost" \
          typo3InstallToolPassword="klaus" \
          && bin/phpunit -c vendor/typo3/testing-framework/Resources/Core/Build/FunctionalTests.xml

When you want to test against other databases like PostgreSQL or MSSQL you will
find the database credentials inside the :file:`Build` folder of the TYPO3
core in the file :file:`Build/bamboo/src/main/java/core/AbstractCoreSpec.java`.

Search for 'typo3DatabaseUsername' in this Java file to find the definitions of
the different database credentials.

.. hint::

   Be sure to have a cup of coffee, a good book or other things to be done to
   span the waiting time. Functional tests will take a lot more time than unit
   tests. Depending on the power of your local machine you can expect about 45
   minutes or more.

Alternative method: Run single command
======================================

You can also use docker in non-interactive mode. In that case, the docker
container is run with a specific command executed.

We'll show you some examples how you can do this but you may want to come up
with your own.

Run all unit tests
-------------------


::

   docker run --rm \
      --name=typo3_core_test \
      -v <absolute local path where your typo3 checkout is>:/srv/tmp/cms \
      -w /srv/tmp/cms \
      typo3gmbh/php72:latest \
      /sbin/my_init -- bin/phpunit \
      -c vendor/typo3/testing-framework/Resources/Core/Build/UnitTests.xml

If your system supports fetching the current directory with :code:`$(pwd)`
you might do something like this::

   docker run --rm \
      --name=typo3_core_test \
      -v $(pwd):/srv/tmp/cms \
      -w /srv/tmp/cms \
      typo3gmbh/php72:latest \
      /sbin/my_init -- bin/phpunit \
      -c vendor/typo3/testing-framework/Resources/Core/Build/UnitTests.xml


Run all functional test
-----------------------

.. hint::
   This section is still a work in progress because it is depending on
   changes in the core Build directory.

The functional tests require access to the database. For example, for
the MySQL database, use the following file for setting the environment
variables: :file:`Build/bamboo/docker/credentials-mysql`

As this file is still work in progress, you may have to create it yourself
with the following content::

   typo3DatabaseName="func"
   typo3DatabaseUsername="funcu"
   typo3DatabasePassword="funcp"
   typo3DatabaseHost="localhost"
   typo3InstallToolPassword="klaus"

You can use the paramter `--env-file` to specify a file with environment
variables for docker.


::

   docker run --rm \
   --name=typo3_core_test \
   -v <absolute local path where your typo3 checkout is>:/srv/tmp/cms \
   -w /srv/tmp/cms \
   --env-file Build/bamboo/docker/credentials-mysql \
   typo3gmbh/php72:latest \
   /sbin/my_init -- bin/phpunit \
   -c vendor/typo3/testing-framework/Resources/Core/Build/FunctionalTests.xml


