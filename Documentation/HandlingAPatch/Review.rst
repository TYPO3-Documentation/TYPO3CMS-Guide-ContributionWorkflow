.. include:: ../Includes.txt

.. _reviewPatch:

==============
Review a patch
==============

Reviewing a patch consists of two steps:

#. :ref:`Code-review <lifeOfAPatch-review>`
#. :ref:`Testing the change <lifeOfAPatch-test>`

You have the option to contribute to both stages or just a single stage in the review process.

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

.. rst-class:: bignums-xxl

#. Select the latest patchset

   This should already be selected by default, but if you changed the patchset, you should
   select :guilabel:`Go to the latest patch set` (above the list of changed files).

#. To leave a comment, click on one of the files

   .. image:: _assets/gerrit_review_click_on_file.png

   Commenting in the files directly is optional, but strongly recommended. If you just want to leave a general
   comment which needs no context, you can skip to step 8 (:guilabel:`Reply`).

#. Optionally change the view

   You will see a diff of this file against the current codebase.

   You can change the view in the top right (:guilabel:`Diff view`) e.g. :guilabel:`side-by-side` or
   :guilabel:`unified` (or change this in your settings).

#. Leave one or more comments

   Click on the line number in the file and a comment box will open.

   .. image:: _assets/gerrit_review_comment_click.png

   .. image:: _assets/gerrit_review_comment_file.png

#. Click :guilabel:`Save`.

   .. important::

      You comment(s) will not yet be visible for others until you go back and click :guilabel:`Reply`.

#. Go back

   .. image:: _assets/gerrit_review_go_back.png

#. (Optional) Add comments to more files.

#. Now press :guilabel:`Reply`.

   .. image:: _assets/gerrit_reply.png

   Using the :guilabel:`Reply` button, you can post your comments (and optionally add an additional note).

   .. image:: _assets/gerrit_comment.png

   Of course you should also :ref:`vote <gerrit-voting>` for the change (Be graceful with -1 votes though.).

   .. image:: _assets/gerrit_vote.png

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

   git reset --hard origin/master



.. index::
   single: Review; Vote
   single: Gerrit; Vote
   single: Vote

.. _gerrit-voting:

Vote
====

In order to comment or vote on a change you can click on the **Reply button** and enter your comment. Here, you
can also apply your votes.

.. figure:: _assets/gerrit-vote.png
   :class: with-shadow

* +1 : you approve of the patch
* -1 : you do not approve, in this case give some reason as a comment

.. sidebar:: Votes

   The +2 and -2 votes only available for core developers. See the section `Policy for votes`_. for more details.

Click on ``Send`` and your comments will be saved. At the same time all other contributors who either watched this change
or have already voted on this change will get notified.



.. _Gerrit-Policy-for-votes:

Policy for votes
----------------

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


Hints on voting -1
------------------

See also :ref:`reviewPatch` about the policies on voting and how to vote.

In general, -1 on reading and/or testing of a patch is a mechanism used to
improve a patch. Still, -1 still takes a risk to kill someone elses patch
and it usually actively prevents a merge. There are ways to override a -1, but
those are not pushed through in real live gerrit habits. In general, if voting
-1, you take some responsibility for this patch by saying "This one shouldn't
be solved until this or that is fixed". Some hints on using -1 in reviews:

* Think about your vote and always give a sane explanation. "-1 looks ugly" is
  not enough.
* If a patch is broken, does not fix the issue, is bogus, architecturally wrong
  or collides with other goals, a -1 is clearly ok.
* -1 can also be used if you are actively working on a patch and want to prevent
  a quick merge: "-1, working on it now, will push soonish".
* -1 may be ok if you have general doubts but you can not pin point it and need
  a second opinion: "Hey, this solution looks somehow weird and I doubt this is
  what we should do here. I think we should have a statement by x or y who have
  a deeper knowledge of this subsystem to have an eye on that. I do not want
  this patch to be merged until this was sorted out and will vote -1 for now
  for this reason."

Hints on voting -2
------------------

A -2 vote by an active contributor blocks a patch from merging. In contrast to
-1, a -2 is a "veto". Use with care. With a -2, you
are taking responsibility of this patch and basically state that it will not
be done until you actively removed your vote again.

In the past, we usually had no real problem with someone giving -2 and then
not acting responsible. It would be great if it stays this way.


.. _Gerrit-No-brainers:
.. _Gerrit-Low-brainers:

Low brainers
-----------

A core developer can give a +2 and submit right away in case of "low-brainers" (what used to be called "FYI").
A core developer can give a +2 and wait a bit before submitting (used to be FYI24, FYI48, ...).


.. _Gerrit-Practical-considerations:

Practical considerations
------------------------

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
