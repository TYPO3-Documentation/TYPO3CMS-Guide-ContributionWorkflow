.. include:: ../Includes.txt

.. _lifeOfAPatch:
.. _improving-a-patch:

=======================================
Handling and improving a patch (Gerrit)
=======================================

This chapter focuses on handling an existing patch, by reviewing it, modifying
it, reverting it etc. If you want to create a new patch, look at :ref:`Fixing-a-bug-A-Z`.


.. note::

   This chapter assumes your environment is set up properly as described in
   :ref:`Contribution Walkthrough Environment Setup<setup>`


The code contribution workflow is based on patches and patchsets.
Each patch fixes one or more issues on Forge. A patch can be updated multiple times,
adding a new patchset on top.

For every change, a new patch is created and pushed to Gerrit. Every patch
contains a single commit. If changes are made to a patch, the already existing
commit is changed (:code:`git commit --amend`).

To make sure, every patch applied to the TYPO3 codebase meets highest standards,
every patch must be
reviewed. Only after at least 2 people have tested the patch and at least 2
people have verified it (one of them must be a member of the core team), can
the patch be merged (for more details on voting, see :ref:`gerrit-voting`.

Additionally, a suite of tests (unit, functional and acceptance) will
automatically run on every patch (set), the results being shown as a +1 or
-1 by typo3.com.


How this chapter is structured
==============================

First some basics are explained, such as :ref:`Working-with-Gerrit`.

Next, common steps that you will need for several operations are described:

* :ref:`Find-a-review`
* :ref:`cherry-pick-a-patch`

The rest of the chapter does not have to be read in the order listed, pick the
operation you will want to perform and jump directly to the pertinent section.


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
  <https://forger.typo3.com/gerrit/status>`__ to filter for rewiews
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

Reviewing a patch
=================

Reviewing consists of two parts:

A **code-review** (with optional comments) and **testing the change**. You can do both or just one or the other.


.. _lifeOfAPatch-review:

Code Review
-----------
A basic code review is possible by using the Gerrit web interface.
Simply navigate to the patch and use the diff-tool ("side-by-side" or "unified").

You can add comments to the code lines. More information on this can
be found in the section :ref:`Gerrit-Commenting-files`.

Using the **Reply button**, you can post your comments and add a note.
Of course you should also vote for the change (Be graceful with -1 votes though.).
More information on voting in general can be found in the section
:ref:`gerrit-voting`.

If you're able to improve the patch yourself, it is very much appreciated
if you also submit an improved version (see :ref:`lifeOfAPatch-improve-patch`
for more information on this).

.. _lifeOfAPatch-test:
.. _Gerrit-Testing-a-change:


Testing a patch
---------------

For testing the patch you need to import the change into your local repository.

Look at :ref:`cherry-pick-a-patch` for information on how to do this.

Test the patch in your local TYPO3 installation and verify the reported bug
is fixed and no other bugs are introduced with the change.

Depending on the outcome of your tests, place your positive/negative vote
in Gerrit, using the **Reply button**.

If you want to help the author and provide an improved patch, continue with the section
:ref:`lifeOfAPatch-improve-patch`.

Otherwise throw the changes away, to bring your repository back to a clean state:

.. code-block:: bash

   git reset --hard origin/master

.. _Gerrit-Commenting-files:

Commenting files
----------------

.. This section was moved from Gerrit/Index.rst

If you spotted a mistake in any file, you should provide the author with a useful clue where the mistake has been made.
One way would be to simply note the filename and line number in the central comment box. But this would be cumbersome and
annoying to handle (imagine a change with 150 files being modified). But Gerrit_ has a solution for that.

.. sidebar:: Diff View

   You can either use a **side-by-side** diff view or a classic **inline** diff depending on your settings in Gerrit_.

If you click on a file in the **changed files** section, you will see a diff of this file against the current codebase.

Simply point to the place you want to add a comment and hit the :kbd:`C` key on your keyboard. Leave your comment in the comment
box and hit ``Save``. Keep in mind that all comments will not be sent to the reviewers immediately - you will still need
to use the **Reply Button** to send them all (ideally with a vote indicating how severe your finding were).

.. figure:: _assets/gerrit-comment-box.png
    :class: with-shadow

.. _gerrit-voting:

Voting
------

In order to comment or vote on a change you can click on the **Reply button** and enter your comment. Here, you
can also apply your votes.

.. figure:: _assets/gerrit-vote.png
    :class: with-shadow

* +1 : you approve of the patch
* -1 : you do not approve, in this case give some reason as a comment

.. sidebar:: Votes

   The +2 and -2 votes only available for core developers. See the section `Policy for votes`_. for more details.

Click on ``Post`` and your comments will be saved. At the same time all other contributors who either watched this change
or have already voted on this change will get notified.



.. _Gerrit-Policy-for-votes:

Policy for votes
~~~~~~~~~~~~~~~~

.. This section was copied from Gerrit/Index.rst

**Code Review:** Needs +1 of two reviewers, one of them being a core developer.

**Verified:** Needs +1 of two reviewers, one of them being a core developer.

A core developer can give a +2 right away on these two checks if another +1 vote already exists.

Votes from the Bamboo build server (user *TYPO3com*) do not count. This means
that a patch which is fully reviewed usually has at least 3 **Verified** +1
votes, two from humans and one from Bamboo.

**Authors should not vote for their own patches**, unless the patch has been changed
substantially by other developers.

As soon as the patch has reached the approved status by getting a +2 on
**Code Review** and **Verified**, a core developer can decide to push the
"Submit" button, finally pushing it to the main repository.


.. _Gerrit-No-brainers:

No brainers
~~~~~~~~~~~

A core developer can give a +2 and submit right away in case of "no-brainers" (what used to be called "FYI").
A core developer can give a +2 and wait a bit before submitting (used to be FYI24, FYI48, ...).


.. _Gerrit-Practical-considerations:

Practical considerations
~~~~~~~~~~~~~~~~~~~~~~~~

The active core developer who gave an early +1 should try and go back to transform the +1 into a +2
after a second review came in, if applicable.

Each newly pushed patch requires a complete new round of voting before it can
be submitted. So everyone that reviewed once is invited to re-vote as soon as
a new patch is pushed. Using Gerrit's Patch History feature allows to quickly
see what has changed from the already reviewed patch to the new one.

Consider these rules when comparing patches:

* If the patch was re-pushed due to the comments, check the diff between the
  versions of the patch.
* If the patch needed to be rebased onto current master, the changeset might
  contain the changes due to rebasing. So better check the diff between base
  and most recent version in this case.


.. _lifeOfAPatch-improve-patch:

Improving a change and uploading a new Patch Set
================================================

To improve an existing patch set, make sure your local repository has the latest changes and
cherry-pick the latest patch set from Gerrit as described in :ref:`cherry-pick-a-patch`.

Edit the files to solve your concerns and test this new version carefully.

Update the change by **amending** the previous commit. This will overwrite the commit you fetched from Gerrit
with your changes:

.. code-block:: bash

   git commit --amend -a

.. warning::

   Make sure to not change or remove the Change-Id: line!

You can amend as often as you want. Once you are satisfied, push your improved Patch Set to Gerrit:

.. code-block:: bash

   git push origin HEAD:refs/publish/<release-branch>

where <release-branch> has to be replaced with the target branch as shown in Gerrit.
If you're currently working on the master-branch this must be ``refs/publish/master`` as well.



.. _lifeOfAPatch-backport:

Backporting a change to other branches
======================================

.. note::

   This is an informative section targeted towards members of the core team only.


First wait until the review process was successfully completed for the most recent affected branch.

Use Gerrit for the cherry-pick
------------------------------

First try to use the Gerrit cherry-pick feature for automatic backporting.

.. image:: _assets/gerrit_cherrypick_1.png
   :width: 400px

In the following modal, you can easily select the branch, you want to cherry pick to, by just typing partial information.

.. image:: _assets/gerrit_cherrypick_2.png
   :width: 400px

Remove from the commit message everything below the Change-ID because the information about former reviewers is not needed
for the cherry pick. Make sure that you **don't alter the Change-ID** but remove every line (also empty ones) below it. After doing so hit the "Cherry Pick Change" button.

.. image:: _assets/gerrit_cherrypick_3.png
   :width: 400px

Manual backport
---------------

If the automatic backporting fails, you need to manually cherry-pick the patch to the target branch. (e.g. cherry-pick the
master patch onto your local (up to date) TYPO3_6-2 branch) You will most likely need to adjust the code for the older branch.

Edit the commit message to comply to the guidelines again. (e.g. remove the Reviewed-* and Tested-* lines added by Gerrit)
**Keep the Change-Id though!**

Push the review back to Gerrit.

On Gerrit the original patch will show the cherry-pick as a related patch.

.. _lifeOfAPatch-Reverting-Patches:

Reverting patches
=================

.. note::

   This is an informative section targeted towards members of the core team only.

It is important to have traceable code. This means that any person inspecting the bug tracker, Gerrit changes or the
commit log shall be able to trace if a patch has been reverted. Therefore we must add this information to all affected
places.

If there's the need to revert a patch, please stick to the following rules:

#. Create a ticket on Forge for the revert, if there's not yet a bug report. (Maybe re-use the original ticket,
   if you re-push the patch again with the original ticket number.)

#. Visit the original ticket in Forge and

   #. link it to the revert ticket

   #. add a comment to the ticket with information that it is reverted

   #. set the Status from Resolved to Accepted

#. Use the Revert button in Gerrit

#. Modify the commit message of the newly created patch to contain

   #. the commit hash as generated by Gerrit

   #. a description why the revert is needed

   #. a Releases-line that contains all releases where the original patch was merged (check if the backports where
      really merged)

   #. a Resolves-line for the revert ticket as created above (you can skip this if you re-used the original ticket)

   #. a Reverts-line for the ticket of the original patch
