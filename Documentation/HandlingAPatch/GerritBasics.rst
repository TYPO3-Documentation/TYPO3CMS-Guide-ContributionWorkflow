.. include:: ../Includes.txt


.. _Working-with-Gerrit:

======================
Introduction to Gerrit
======================


.. This text has been moved from Gerrit/Index.rst

Gerrit is a web based code review and project management tool for Git based projects.

TYPO3's Gerrit interface is located at https://review.typo3.org.

Gerrit handles the review process and is a gatekeeper in front of the official TYPO3 Git repository on git.typo3.org. Pushing to git.typo3.org repository is not allowed for anybody, instead every change has to pass a review process in Gerrit, which later pushes the change to the repository.

.. _Gerrit-Overview-of-the-UI:

Overview of the UI
==================

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

#. The **Download Button**. You will be using this control to :ref:`cherry pick a change <cherry-pick-a-patch>`.

#. Other changes **related** to this change. This can be either due to a similar topic or because the commit summary is
   related to the change we are currently reviewing.

#. The **current review status**. Here you can see who has voted (and how they voted) on a change. The votes only apply
   to one given patchset. If a new patchset is uploaded, it must be revoted. Note the +1 by TYPO3com, which means that
   the automatic testsuite ran successfully. 

#. All **changed files** in this current change. You can click every file to take a look at what exactly has changed. There
   is a select box on top of the file list that allows you to do a diff between patch sets to quickly see what has changed.

#. The **history** of this change. Here you can see comments, new patch sets, votes on a change etc.




