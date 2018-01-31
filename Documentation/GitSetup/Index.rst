.. include:: ../Includes.txt

.. highlight:: bash

.. _git-setup:

===============================
Setting up your Git environment
===============================

.. toctree::
   :maxdepth: 1

   Prerequisites
   WorkflowExplained
   CommitMessageFormat

These steps will walk you through your basic Git setup when working with TYPO3.


.. tip::

   If you want to get an introduction to how our workflow works, :ref:`head over here<workflow-explained>`

.. note::

   We expect you have a fully-fledged web development setup at hand.

   If you are not sure, though, :ref:`take a look here <prerequisites>`.

Clone a fresh TYPO3 sourcecode
==============================

Switch into your **empty** htdocs directory of choice and clone a fresh master of TYPO3. Run ``composer install`` after that::

   git clone git://git.typo3.org/Packages/TYPO3.CMS.git .
   composer install

If you rather like to work with your favorite Git GUI, we compiled a list of the ones used throughout the core team
here.

* :ref:`SourceTree on Windows<windows-clonewithsourcetree>`
* SourceTree on OSX
* :ref:`Git Tower on OSX<gittower-osx>`

Add your TYPO3.org account to the git repository
================================================

You need to instruct git to work with your name and email address. Make sure the email address is the one you used when
:ref:`setting up your TYPO3 account<TYPO3Account>`.

::

   git config user.name "Your Name"
   git config user.email "your-email@example.com"

In order to avoid weird merges in your local repository when pulling in new commits from typo3.org, we encourage everybody
to set the autosetuprebase option, such that your local commits are always rebased on top of the official code::

   git config branch.autosetuprebase remote

.. _git-setup-precommithook:

Install your pre-commit hook
============================

::

   curl -o .git/hooks/commit-msg "https://typo3.org/fileadmin/resources/git/commit-msg.txt" && chmod +x .git/hooks/commit-msg

If you get a warning message from curl "*Failed to create the file .git/hooks/commit-msg: No such
file or directory.*" just create the directory .git/hooks: ``mkdir .git/hooks``

You can read about the why and where of the pre-commit hook :ref:`here<commit-hook>`.

Setting up your remote
======================

You can instruct Git to push to Gerrit_ instead of the original repository. It acts as a kind of facade in front of Git::

   git config url."ssh://<YOUR_TYPO3_USERNAME>@review.typo3.org:29418".pushInsteadOf git://git.typo3.org

If you get an error message after pushing to gerrit like below, you need to change manually the ``url`` parameter in ``.git/config``.
::
      fatal: unable to access 'https://git.typo3.org/Packages/TYPO3.CMS.git/': The requested URL returned error: 403
   
   


.. _git-setup-pushing:

Set a Commit Message
====================

See :ref:`how to compose a proper commit message <Commit-Message-Format>`.


.. _git-setup-pushing-your-changes:

Pushing your changes
====================

Once you are happy with your changes, you can push them via::

   git push origin HEAD:refs/publish/master

Where ``master`` is the target, so ``master`` is current development trunk. E.g. if you want to push
to 7.6 LTS instead, run ``git push origin HEAD:refs/publish/TYPO3_7-6``.

Pushing to the original repository is denied.

Other resources
===============

We have compiled a list of helpful examples for you in the :ref:`Appendix<appendix>` section.
