.. include:: ../Includes.txt

.. highlight:: bash

.. _composer:

========
Composer
========

About Composer
==============

Composer is a dependency manager for PHP.

So what it basically does is find packages you have defined to be part of your application (in our case TYPO3). But what
if these packages rely on other packages as well? This is where composer jumps in and takes care of keeping all these
packages in sync.

Since we use quite some packages (because why would we invent things ourselves that are already there?) composer is an
extremely useful tool for us.

.. _install-composer:

Install Composer
================

Follow the
installation instructions from https://getcomposer.org. Afterwards, you should
have a working executable `composer` available.

Verify composer is working::

   $ composer --version


.. _composer-commands:

Composer Commands
=================

Once you have installed Composer, this is the command you should run after you
clone the Git source and after every `git pull` request or switching branches::

   composer install

But, just follow the :ref:`setup instructions <setup>`, it will walk you through the commands
in the correct order!

.. _custom-composer-commands:

Custom TYPO3 Composer Commands
==============================

Some additional composer commands have been added for core development.

Just run::

   composer

to list them. You will see something like:

.. code-block:: none

   gerrit:setup                           Enable all the git hooks needed to make contribution easy
   gerrit:setup:commitMessageHook:enable  Enable the commit message hook needed for gerrit
   gerrit:setup:preCommitHook:disable     Disable pre commit hook to run some checks locally
   gerrit:setup:preCommitHook:enable      Enable pre commit hook to run some checks locally

