.. include:: ../Includes.txt

.. _git-setup:

===============================
Setting up your GIT environment
===============================

.. toctree::
   :maxdepth: 1

   Prerequisites
   WorkflowExplained

These steps will walk you through your basic GIT setup when working with TYPO3.


.. tip::

   If you want to get an introduction to how our workflow works, :ref:`head over here<workflow-explained>`

.. note::

   We expect you have a fully fledged web development setup at hand.

   If you are not sure, though, :ref:`take a look here <prerequisites>`.

Clone a fresh TYPO3 sourcecode
==============================

Switch into your htdocs directory of choice and clone a fresh master of TYPO3. Run ```composer install``` after that.

.. code-block:: bash

   git clone https://git.typo3.org/Packages/TYPO3.CMS.git .
   composer install

If you rather like to clone using your favourite GIT GUI, we compiled a list of the ones used throughout the core team
here.

* Cloning with Sourcetree on Windows
* Cloning with Sourcetree on OSX
* Cloning with GIT Tower on OSX

Add your TYPO3.org account to the git repository
================================================

.. _git-setup-precommithook:

Install your pre-commit hook
============================

.. note::

   You can read about the why and where of the pre-commit hook here

Setting up your remote
======================

.. note::

   If you want a little more verbosity or dislike magic you can add Gerrit_ as a remote explicitely via

   .. code-block:: bash

      git remote add blabla

Pushing your changes
====================
