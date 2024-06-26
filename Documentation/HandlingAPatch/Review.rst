.. include:: /Includes.rst.txt

.. _reviewPatch:

==============
Review a patch
==============

Reviewing a patch consists of two steps:

#. :ref:`Code-review <lifeOfAPatch-review>`
#. :ref:`Testing the change <lifeOfAPatch-test>`

You have the option to contribute to both stages or just a single stage in the review process.

Both steps are free for everyone in the OpenSource community, you are not required to be
a Core merger or Team member.

If you're able to improve the patch yourself, your contribution would be very much appreciated.
Visit :ref:`lifeOfAPatch-improve-patch` to find out more about how you can help improve patches.

.. seealso::

   *  :ref:`Find the patch <Find-a-review>`
   *  :ref:`Introduction to Gerrit <Working-with-Gerrit>`


.. index::
   single: Review; Code Review
   single: Code Review
   single: Gerrit; Review

.. _lifeOfAPatch-review:
.. _Gerrit-Commenting-files:

Code Review
===========

A basic code review is possible by using the Gerrit web interface.

For some tips on what to review, check our :ref:`common-review-checks`.

.. rst-class:: bignums-xxl

#. Select the latest patchset

   This should already be selected by default, but if you changed the patchset, you should
   select :guilabel:`Go to the latest patch set` (above the list of changed files).

#. To leave a comment, click on one of the files

   .. image:: /Images/External/Gerrit/HandlingAPatch/gerrit_review_click_on_file.png

   Commenting in the files directly is optional, but strongly recommended. If you just want to leave a general
   comment which needs no context, you can skip to step 8 (:guilabel:`Reply`).

#. Optionally change the view

   You will see a diff of this file against the current codebase.

   You can change the view in the top right (:guilabel:`Diff view`) e.g. :guilabel:`side-by-side` or
   :guilabel:`unified` (or change this in your settings).

#. Leave one or more comments

   Click on the line number in the file and a comment box will open.

   .. image:: /Images/External/Gerrit/HandlingAPatch/gerrit_review_comment_click.png

   .. image:: /Images/External/Gerrit/HandlingAPatch/gerrit_review_comment_file.png

#. Click :guilabel:`Save`.

   .. important::

      You comment(s) will not yet be visible for others until you go back and click :guilabel:`Reply`.

#. Go back

   .. image:: /Images/External/Gerrit/HandlingAPatch/gerrit_review_go_back.png

#. (Optional) Add comments to more files.

#. Now press :guilabel:`Reply`.

   Using the :guilabel:`Reply` button, you can post your comments
   (and optionally add an additional note).

   .. figure:: /Images/External/Gerrit/CoreMergers/VoteUser.png
      :class: with-shadow

      Vote by clicking the :guilabel:`Reply` button

   Of course you should also :ref:`vote <gerrit-voting>` for the change
   (Be graceful with -1 votes though).

.. _lifeOfAPatch-test:
.. _Gerrit-Testing-a-change:

Test a patch
============

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

   git reset --hard origin/main

.. index::
   single: Review; Vote
   single: Gerrit; Vote
   single: Vote

.. _gerrit-voting:

Vote
====

In order to comment or vote on a change you can click on the :guilabel:`Reply`
and enter your comment. Here, you can also apply your votes.

Remember, everyone with just a TYPO3 user account is able to vote, you do not
need to be a team member or Core merger.

.. figure:: /Images/External/Gerrit/CoreMergers/VoteUser.png
   :class: with-shadow

   Chose your vote, say something nice and click :guilabel:`SEND`

*  :guilabel:`+1` : you approve of the patch
*  :guilabel:`-1` : you do not approve, in this case give your reason as a comment

.. sidebar:: Votes

   The :guilabel:`+2` and :guilabel:`-2` votes are only available for Core Mergers.
   See the section :ref:`Review a patch as a Core Merger <coreMergers-review>`.
   for more details.

Click on :guilabel:`Send` and your comments will be saved. At the same time
all other contributors who either watched this change
or have already voted on this change will get notified.



.. _Gerrit-Policy-for-votes:

Policy for votes
----------------

.. This section was copied from Gerrit/Index.rst

**Code Review:** Needs :guilabel:`+1` of two reviewers, one of them being a Core Merger.

**Verified:** Needs :guilabel:`+1` of two reviewers, one of them being a Core Merger.

Votes from the CI GitLab Pipeline Server (user "Core CI") do not count. This means
that a patch which is fully reviewed usually has at least 3 **Verified** :guilabel:`+1`
votes, two from humans and one from "Core CI" ("Core CI is happy" for Verified+1, "Core CI is not happy"
for Verified-1). Each comment by Core CI is linked to the log of the performed job,
so that you can inspect the output.

**Authors should not vote for their own patches**, unless the patch has been changed
substantially by other developers.

As soon as the patch has reached the approved status by getting a :guilabel:`+2` on
**Code Review** and **Verified**, a Core Merger can decide to push the
:guilabel:`Submit` button, finally pushing it to the main repository.


Hints on voting -1
------------------

See also :ref:`reviewPatch` about the policies on voting and how to vote.

In general, :guilabel:`-1` on reading and/or testing of a patch is a mechanism used to
improve a patch. Still, -1 still takes a risk to kill someone elses patch
and it usually actively prevents a merge. There are ways to override a -1, but
those are not pushed through in real live Gerrit habits. In general, if voting
-1, you take some responsibility for this patch by saying "This one shouldn't
be solved until this or that is fixed". Some hints on using -1 in reviews:

*  Think about your vote and always give a logical explanation. "-1 looks ugly" is
   not enough.
*  If a patch is broken, does not fix the issue, is bogus, architecturally wrong
   or collides with other goals, a -1 is clearly ok.
*  -1 can also be used if you are actively working on a patch and want to prevent
   a quick merge: "-1, working on it now, will push soonish".
*  -1 may be ok if you have general doubts but you can not pinpoint it and need
   a second opinion: "Hey, this solution looks somehow weird and I doubt this is
   what we should do here. I think we should ask person x or person y, who has
   a deeper knowledge of this subsystem, to take a look at it. I do not want
   this patch to be merged until this is sorted out and will vote -1 for now
   for this reason."
*  If you are on the "receiving end" of a "-1" or even a "-2" vote, please do not
   be afraid or feel bad. This is done as part of the process to make TYPO3
   evolve as best as it can. Try to work out problems or negative feedback,
   be kind to each other and remember you are contributing to OpenSource because
   the experience of improving things together, and learning from each other
   is what drives us.

Vote resets ("Revote")
----------------------

Whenever a new patch is submitted, all votes are reset. So if previously
a patch was voted to be merged, but then a last-minute issue is getting
addressed, after the commit every vote will be back to zero.

Contributors to a patch review will receive notifications about this and
are encouraged to review the patch and re-apply their vote if they
still feel confident.

It is ok if the patch owner pings previous votes to please consider
adding a revote, so that a patch can be pushed forwards.

How to handle [WIP] patches
===========================

It is possible to push patches as "WIP" (:ref:`work in progress <git-work-in-progress>`)
patches. This is a
way to show people a quick-shot version of something that is not finished yet,
but goes into the right direction. Usually, WIP patches are not actively
reviewed by others and the original author should take responsibility to finish
this patch later.

As a contributor, you usually can not expect someone else to pick up your WIP
patch and finish it, except you stated that goal clearly: "Hey, I've done a
quick shot with this patch to show a possible solution for this issue, but the patch
is not finished yet. Foo and bar is missing and we still need a concept for foobar.
I'll probably not work actively work on it anytime soon, but maybe the current
state is helpful already".

Better: "Hey, I worked in this area and came up with this WIP patch for now. I
wanted to show into which direction this patch is leading, but we currently have
some open questions. However, it would be great if you can give me feedback to
the general approach at this early state already to decide if it is worth
following this solution to its end."

Having too many WIP patches in the review queue is not really helpful. Consider
to fork the project in GitHub or somewhere else and push to gerrit again if
your patches evolved.

Stale reviews / Cleaning up
===========================

Since TYPO3 iterates on many, many patches and issues each day, the list
of Gerrit reviews (as well as Forge issues) may feel intimidating.

Due to this it is vital to "clean up" patches from time to time:

*  If you are no longer planning to work on a patch, maybe better anbandon
   it, or ask other involved people to carry on.
*  If your patch is not getting feedback for a long time, ask in the
   #typo3-cms-coredev channel of the `TYPO3 slack workspace <https://typo3.slack.com>`__
   if people may want to review or give feedback on. Or try to find people
   working in a similar area of your patch and see if you can join forces.
*  From time to time, check on patches you have voted on, to see if you can
   push things forward to either get merged or abandoned.
*  Sometimes just check all your own open patches and see if you might catch
   interest in picking it up again.
*  Please either update older patches in "Merge conflict" mode or state your
   intent to abandon the patch.