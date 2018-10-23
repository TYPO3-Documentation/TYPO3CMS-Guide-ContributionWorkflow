.. include:: ../Includes.txt

.. _issue-workflow:

======================
Issue Workflow (Forge)
======================

This chapter describes the workflow of handling issues in TYPO3s Redmine
available at Forge_. Once issues have been submitted, there may be information
missing or the status may changed. Additional information can be added. 

Everyone is welcome to help in improving issues.

There are edge cases to this which should be discussed on a per-case basis
in order to refine the workflow more.

If in doubt, ask on `Slack <https://typo3.slack.com>`__
in the **#typo3-cms-coredev** channel. (Remember to
`register <https://forger.typo3.com/slack>`__ first.)

Target Versions
===============

Target versions are set by the core team only. Until we can enforce this technically,
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

Status
======

When an issue is reported, the status is set to **New**. Here we list some
common status changes:

**Needs Feedback**

   This issue needs more information to get resolved. It is good practice to always
   combine this status change with a question to the issue reporter in order to
   make clear, what kind of information is missing.

**Under Review (Automatic)**

   As soon as a patch is uploaded for the issue, the status will automatically
   be set to "Under Review".

**Resolved (Automatic)**

   As soon as the patch is merged, the status will automatically be set to "Resolved".
