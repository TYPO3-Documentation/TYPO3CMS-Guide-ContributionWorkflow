.. include:: ../Includes.txt

=============
Gerrit Basics
=============


.. _Working-with-Gerrit:

Introduction to Gerrit
======================

.. This text has been moved from Gerrit/Index.rst

Gerrit is a web based code review and project management tool for Git based projects.

TYPO3's Gerrit interface is located at https://review.typo3.org.

Gerrit handles the review process and is a gatekeeper in front of the official TYPO3 Git repository on git.typo3.org. Pushing to git.typo3.org repository is not allowed for anybody, instead every change has to pass a review process in Gerrit, which later pushes the change to the repository.

.. _Gerrit-Overview-of-the-UI:

Overview of the UI
------------------

This chapter will explain the most important parts of the Gerrit_ UI to you.

.. note::
   We will focus on the new UI in this chapter. Currently, when you first open Gerrit, you might see an older
   version of the UI. If so, please scroll down and click on the link "New UI" on the right side of the footer.

This is a screenshot of an open review on Gerrit_. We will go through the parts of the UI next:

.. image:: _assets/gerrit-ui.png
   :alt: Screenshot of a code review on Gerrit
   :class: with-shadow

#. The **search box** lets you write complex search queries with little coding knowledge. For detailed information on how to
   use the search, refer to the official documentation on https://review.typo3.org/Documentation/user-search.html.
   Most people use `Forger <https://forger.typo3.org>`__, because it provides more sophisticated ways to
   find a review. Look at :ref:`Find-a-review` for more information.

#. The **commit message** formatted like we explained in :ref:`"The commit message"<commitmessage>`.

#. The **Reply Button** which you will use to vote on code quality and testing as well as to send comments. We will be
   covering this button in more detail later.

#. The **Download Button**. You will be using this control to cherry pick a change in order to test it later.

#. Other changes **related** to this change. This can be either due to a similar topic or because the commit summary is
   related to the change we are currently reviewing.

#. The **current review status**. Here you can see who has voted (and how they voted) on a change. Note that if a
   change gets refined over time with new patch sets, your votes will be reset (simply because the review has changed).

#. All **changed files** in this current change. You can click every file to take a look at what exactly has changed. There
   is a select box on top of the file list that allows you to do a diff between patch sets to quickly see what has changed.

#. The **history** of this change. Here you can see comments, new patch sets, votes on a change etc.


.. _Find-a-review:

Finding a review on Gerrit
==========================

For finding an existing review (patch), there are several possibilities:

* If you are in any way involved in the review (e.g. you are author,
  reviewer or you made changes), you will get a notification about
  it to your email adress. The notification contains a link
* Once a patch has been pushed for an issue, the corresponding issue
  on `Forge <https://forge.typo3.org>`__ will contain comments with the
  topic "Updated by Gerrit Code Review ..."
  and a link to the review on Gerrit.
* In any case, you can use `Forger <https://forger.typo3.org>`__ to
  search for the review, for example use the `Forger Gerrit Overview
  <https://forger.typo3.com/gerrit/status>`__ to filter for reviews
  or the `Review board bugfixes
  <https://forger.typo3.com/sprint/reviews?&boardId=bugfix>`__ to get
  an overview of all open patches for bugs.
* Or use the search box on `Gerrit <https://review.typo3.org>`__

.. _cherry-pick-a-patch:
.. _Gerrit-Reset-to-a-clean-state:

Cherry-Pick a patch
===================

In order to test a patch or make additional changes on it, you will need
to cherry-pick it from the review-system into your local git repository.


.. rst-class:: bignums

1. Find the review on Gerrit, see :ref:`Find-a-review`

2. Select the latest patchset and click download

   .. image:: _assets/gerrit-go-to-latest-patchset.png
      :class: with-shadow

   .. image:: _assets/gerrit-download.png
      :class: with-shadow

3. Click on copy next to the line for "Cherry pick"

   This copies the command to the clipboard.

   .. image:: _assets/gerrit-cherry-pick.png
      :class: with-shadow

4. Clean up your local repository

   .. code-block:: bash

      git reset --hard origin/master
      git pull

5. Execute the command (git cherry-pick)

   In your shell, paste the copied command and execute it.

.. important::

   Make sure to always get the latest patch set of the current review. You can check this by looking at the **Patch Sets**
   menu left of the **Download Button**. The left and right numbers should always be the same, so you know you picked the
   latest patch set. You can also click on **Go to latest patch set**.
