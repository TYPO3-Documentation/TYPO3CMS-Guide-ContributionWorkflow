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

Switch into your **empty** htdocs directory of choice and clone a fresh master of TYPO3. Run ```composer install``` after that.

.. code-block:: bash

   git clone https://git.typo3.org/Packages/TYPO3.CMS.git .
   composer install

If you rather like to work with your favourite GIT GUI, we compiled a list of the ones used throughout the core team
here.

* Sourcetree on Windows
* Sourcetree on OSX
* :ref:`GIT Tower on OSX<gittower-osx>`

Add your TYPO3.org account to the git repository
================================================

You need to instruct GIT to work with your name and email address. Make sure the e-mail address is the one you used when
:ref:`setting up your TYPO3 account<TYPO3Account>`.

.. code-block:: bash

   git config user.name "Your Name"
   git config user.email "your-email@example.com"

In order to avoid weird merges in your local repository when pulling in new commits from typo3.org, we encourage everybody
to set the autosetuprebase option, such that your local commits are always rebased on top of the official code.

.. code-block:: bash

   git config branch.autosetuprebase remote

.. _git-setup-precommithook:

Install your pre-commit hook
============================

.. code-block:: bash

   curl -o .git/hooks/commit-msg "https://typo3.org/fileadmin/resources/git/commit-msg.txt" && chmod +x .git/hooks/commit-msg

.. note::

   If you get a warning message from curl "Failed to create the file .git/hooks/commit-msg: No such file or directory." just create the directory .git/hooks .

.. note::

   You can read about the why and where of the pre-commit hook :ref:`here<commit-hook>`.

Setting up your remote
======================

You can instruct git to push to Gerrit_ instead of the original repository. It acts as a kind of fascade in front of GIT.

.. code-block:: bash

   git config url."ssh://<YOUR_TYPO3_USERNAME>@review.typo3.org:29418".pushInsteadOf git://git.typo3.org

.. note::

   If you want a little more verbosity or dislike the fascade of ``pushInsteadOf`` you can add Gerrit_ as a remote explicitely via

   .. code-block:: bash

      git remote add Gerrit ssh://<YOUR_TYPO3_USERNAME>@review.typo3.org:29418/Packages/TYPO3.CMS.git

.. _git-setup-pushing:

Pushing your changes
====================

Once you are happy with your changes, you can push them via

.. code-block:: bash

   git push origin HEAD:refs/publish/master

.. note::

   If you have set up your remote explicitly, you need to push to that remote name instead, of course.

   .. code-block:: bash

      git push Gerrit HEAD:refs/publish/master

Other resources
===============

We have compiled a list of helpful examples for you in the :ref:`Appendix<appendix>` section.
