.. include:: /Includes.rst.txt



.. index::
   single: Forge; Issue Workflow
   single: Issue Workflow

.. _issue-workflow:

======================
Issue Workflow (Forge)
======================

So, you've filed an issue following the steps above, and submitted it.

What now?

First and foremost: Thank you for doing this. You are now a part of the OpenSource
ecosystem. It lives and thrives with its users, and is constantly evolving.

The TYPO3 community is proud to be active and diverse, and boast a long-standing
track record of fostering this system that we all love with continuous development
effort.

Most of the TYPO3 Contributors perform their work in their spare time, and we all
spend our time differently. Some people work on big tasks and have an agenda of
years ahead, and maybe are even paid to work on TYPO3 (through either Partners, Agencies,
TYPO3 GmbH or other means). Other people work on this system instead of watching a
movie in the evening.

So the bottom line is: In OpenSource development, you do not really know who and when
somebody will take care of your issue. It can catch someones instant attention,
but it may also lay unchecked for days, or weeks... or longer. Impactful bugs are
easily addressed because the more people report an issue, the more likely it is to
get awareness and interest.

A few volunteers in the TYPO3 community try to regularly catch up with issues,
so no report is likely to be lost like tears in the rain. Your input is valuable,
and valued by our team - but please bear with us.

If your issue does not get addressed immediately, try to get involved in the Community.
Check out `https://typo3.org/help`__ for platforms to discuss about the issue you found.

Or, maybe you can find time and capacity to work on an issue yourself, with the help of this
Contributor's Guide!

Once an issue has been triaged by our support volunteers, this will usually happen:

.. index::
   single: Issue Workflow; Status

Status
======

#. New

   This is the initial state of an issue. It may get reverted to this status,
   when possible feedback loops are done, but the issue itself could not yet
   be "Accepted" due to missing strategic or capacity decisions.

#. No status change, but "things happen"

   Your issue may remain in status "New" or "Accepted", but further feedback
   might be added, or relations to other issues could be added, or
   other metadata (like tags) get adjusted. If you see this happening,
   some of our support staff has "seen" your issue. If your issue is
   older, and you see this happening, this might be a good time to get
   involved again and see if your issue still applies.

#. Needs Feedback:

   Your issue has been set from Status "New" to "Needs Feedback".

   This means, we have further questions to process or discuss your issue.
   Once you provide the feedback, the person involved with it will usually
   get back to you again.

#. Accepted

   Your issue has been "accepted" to be reproducible and understandable,
   and will hopefully find a volunteer to fix it.

   Please bear in mind that this status does not mean someone immediately
   begins to work on it. It is just a status that developers can use to
   search for accepted issues to work on. And it is a good pool of issues
   to address for example in remote or on-site Code sprints (see
   `https://typo3.org/community/meet/regular-open-sprints`__).

#. In Progress

   Someone has actively taken on your issue to work on.

#. Under Review

   This is the status you are looking for.

   This means a Patch has been made that should address your problem.
   The link to such a Patch in our review system will be attached to the
   comment.

   Now it is very important for that patch to:

   * actually fix your issue
   * be accepted by Core mergers to be part of the TYPO3 code

   Anyone can create/contribute a patch to any issue, one does not need
   to be assigned to it. One is also free to contribute to existing
   Patches of an issue.

   And most importantly: You are VERY welcome to review the patch
   yourself. If you can comment on the patch tracking system that
   a patch solves your problem, and even vote for it, this will
   highly increase the chances of your patch getting merged.

   Sometimes discussion about solving an issue is then carried on to the
   Gerrit review system, which is linked in the issue comment. You may want
   to regularly check on that patch state and maybe give feedback there.

   Please note that the patch system is meant for highly technical feedback.
   If your feedback is more general, please provide that only in the issue tracker.

   An issue that is "Under Review" may get merged very quickly, but it may
   also even take very long to get merged, or even rejected/abandoned.

#. Resolved

   Making a note here: Huge success! Your issue report lead to an actual
   code improvement of TYPO3, and the patch resulting from your issue
   has been merged. Thank you!

   Sometimes it might not be what you expected at first, because requirements
   and needs may change, and need to be adapted for the broad community.

   It can also occur that the issue you reported for a specific TYPO3
   version is only fixed for a more recent version, and not the one you
   reported with. Sadly we cannot backport every single bugfix, and need
   to make internal decissions about which changes get put into older
   versions. Patches never get merged to versions below the LTS (Long-term support)
   threshold.

   The upside: The patch that has been made may apply to your own instance.
   You can always download patches and apply them locally, see
   :ref:`Applying Core patches <t3upgrade:applying-core-patches>` for details.

#. Closed

   This may be a frustrating status for your issue to be put in. We need to
   close issues that:

   *  are no longer reproducible
   *  are outdated
   *  are not fixable/adressable within reasonable resource limits
   *  do not align with the TYPO3 project goal
   *  receive no feedback for a longer time
   *  relate to abandoned patches

   If your issue has been closed but you believe this is a mistake, our support
   staff are just humans after all, please bear with us. You can still give feedback
   to closed issues, you can reach out through other community means, or you can
   also create follow-up issues.

#. Outside help / Volunteering opportunity

   The more watchers an issue has, the more likely it is regarded as being of importance.

   It can help if you regularly search the issue tracker yourself for similar problems
   than yours, and maybe set relations to new issues, or comment in issues that you
   haven't submitted yourself, but where you can contribute.

   The task of maintaining the issue tracker is a large one; several dozen issues
   are worked on each day. If you can help to add relations to related tickets,
   or provide feedback or additional information in "foreign" tickets, this can help us out.

   The ideal help of course is if you are able to solve issues by providing solutions
   or patches to issues.




.. index::
   single: Issue Workflow; Target Versions

Target Versions
===============

Target versions are set by the Core team only. Until we can enforce this technically,
feel free to remove target versions set by issue reporters.

**Candidate for patchlevel:**

All issues that qualify for patchlevel versions should go into this pool.
Naturally, this can only be bug fixes or tasks.

A board does not make sense for this, since the issue status can only be New or Needs Feedback on these issues.
Find the pool `here <https://forge.typo3.org/projects/typo3cms-core/issues?set_filter=1&f%5B%5D=status_id&op%5Bstatus_id%5D=o&f%5B%5D=fixed_version_id&op%5Bfixed_version_id%5D=%3D&v%5Bfixed_version_id%5D%5B%5D=3285&f%5B%5D=subproject_id&op%5Bsubproject_id%5D=%21*&f%5B%5D=&c%5B%5D=tracker&c%5B%5D=status&c%5B%5D=priority&c%5B%5D=subject&c%5B%5D=assigned_to&c%5B%5D=category&c%5B%5D=fixed_version&group_by=>`__.

**Dedicated Patchlevel Versions:**

This is the “real” next patchlevel release that is planned.

Whenever a contributor takes up a task he/she will have to make sure the ticket is set
from “Candidate for patchlevel” to this dedicated version.

Taking up such an issue comes with the commitment to get this issue done by the
time of release. Other members of the core team should support this cause by reviewing as usual.

**Candidate for Major Version**

Features and tasks will go into this pool.
These can be worked on as usual.
