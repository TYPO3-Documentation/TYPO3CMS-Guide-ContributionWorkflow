.. include:: ../Includes.txt

.. _redmine-index:

===============
Ticket Workflow
===============

This document defines the workflow of handling tickets in TYPO3s Redmine available at Forge_.
There are edge cases to this which should be discussed on a per-case basis in order to refine the workflow more.

Target Versions
===============

Target versions are set by the core team only. Until we can enforce this technically, feel free to remove target versions set by issue reporters.

Candidate for patchlevel
------------------------

All issues that qualify for patchlevel versions should go into this pool.
Naturally, this can only be bug fixes or tasks.

A board does not make sense for this, since the issue status can only be New or Needs Feedback on these issues.
Find the pool `here <https://forge.typo3.org/projects/typo3cms-core/issues?set_filter=1&f%5B%5D=status_id&op%5Bstatus_id%5D=o&f%5B%5D=fixed_version_id&op%5Bfixed_version_id%5D=%3D&v%5Bfixed_version_id%5D%5B%5D=3285&f%5B%5D=subproject_id&op%5Bsubproject_id%5D=%21*&f%5B%5D=&c%5B%5D=tracker&c%5B%5D=status&c%5B%5D=priority&c%5B%5D=subject&c%5B%5D=assigned_to&c%5B%5D=category&c%5B%5D=fixed_version&group_by=>`__.

Dedicated Patchlevel Versions
-----------------------------

This is the “real” next patchlevel release that is planned.
Whenever a contributor takes up a task he/she will have to make sure the ticket is set from “Candidate for patchlevel” to this dedicated version.
Taking up such an issue comes with the commitment to get this issue done by the time of release. Other members of the core team should support this cause by reviewing as usual.

Candidate for Major Version
---------------------------

Features and tasks will go into this pool.
These can be worked on as usual.

Status
======

When an issue is reported, the status is set to "New".

Needs Feedback
--------------

This issue needs more information to get resolved. 

Under Review
------------

As soon as a patch is uploaded for the issue, the status will automatically
be set to "Under Review".

Resolved
--------

As soon as the patch is merged, the status will be set to "Resolved".