.. include:: ../Includes.txt

.. _gerrit-index:

===================
Working with Gerrit
===================

This document will explain the most important parts of the Gerrit_ UI to you and will provide with all the information
you need to have to work on TYPO3.

Overview of the UI
==================

This is a screenshot of an open review on Gerrit_. We will go through the parts of the UI next:

.. image:: _assets/gerrit-ui.png
   :alt: Screenshot of a code review on Gerrit

#. The **search box** lets you write complex search queries with little coding knowledge. For detailed information on how to
   use the search refer to the official documentation on https://review.typo3.org/Documentation/user-search.html.

#. The **commit message** formatted like we explained in :ref:`"The commit message"<commitmessage>`.

#. The **Reply Button** which you will use to vote on code quality and testing as well as to send comments. We will be
   covering this button in more detail later.

#. The **Download Button**. You will be using this control to cherry pick a change in order to test it later.

#. Other changes **related** to this change. This can be either due to a similar topic or because the commit summary is
   related to the change we are currently reviewing.

#. The **current review status**. Here you can see who has voted (and how they voted) on a change, yet. Notice that if a
   change gets refined over time with new patch sets your votes will be reset (simply because the review has changed.

#. All **changed files** in this current change. You can click every file to take a look at what exactly has changed. There
   is a select box on top of the file list that allows you to do a diff between patch sets to quickly see what has changed.

#. The **history** of this change. Here you can see comments, new patch sets, votes on a change etc.

Commenting and voting
=====================

In order to comment on a change you can click on the **Reply button** and enter your comment here. At the same place you
can apply your votes.

.. image:: _assets/gerrit-vote.png

Click on ``Post`` and your comments will be saved. At the same time all other contributors who either watched this change
or have already voted on this change will get notified. This is a good time to build a rule in your email client btw.

Commenting files
================

If you spotted a mistake in any file, you should provide the author with a useful clue where the mistake has been made.
One way would be to simply note the filename and line number in the central comment box. But this would be cumbersome and
annoying to handle (imagine a change with 150 files being modified). But Gerrit_ has a solution for that.

.. sidebar:: Diff View

   You can either use a **side-by-side** diff view or a classic **inline** diff depending on your settings in Gerrit_.

If you click on a file in the **changed files** section, you will see a diff of this file against the current codebase.

Simply point to the place you want to add a comment and hit the ``C`` key on your keyboard. Leave your comment in the comment
box and hit ``Save``. Keep in mind that all comments will not be sent to the reviewers immediately - you will still need
to use **Reply Button** to send them all (ideally with a vote indicating how severe your finding were.

.. image:: _assets/gerrit-comment-box.png

Testing a change
================

.. sidebar:: TYPO3 Review Box

   If you do not want to code anything but like to review changes, there is a dedicated, easy to use Review Box based
   on Vagrant available at https://github.com/Tuurlijk/TYPO3.Review.

If you want to test the changed code on your local machine you can use a technique called **cherry-picking** with Git.
In order to get the right command Gerrit_ offers a handy feature available under the **Download Button** in the top right
corner of the Gerrit_ UI.

If you click onto the command next to **Cherry Pick** Gerrit_ will automatically mark the entire line and you can copy it
into your clipboard via ``Ctrl-C`` or ``Cmd-C``, depending on your operating system.

Then run the command in your Terminal application of choice.

.. important::

   Make sure to always get the latest patch set of the current review. You can check this by looking at the **Patch Sets**
   menu left of the **Download Button**. The left and right numbers should always be the same, so you know you picked the
   latest patch set.

.. image:: _assets/gerrit-cherrypick.png

Resetting to a clean state
==========================

In order to reset your current master to a clean state again, you can use the following command in your TYPO3 root directory:

.. code-block:: bash

   git reset --hard origin/master
   git pull
