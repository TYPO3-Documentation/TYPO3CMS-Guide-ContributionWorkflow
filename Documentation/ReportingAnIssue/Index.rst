.. include:: ../Includes.txt

.. _forge-index:
.. _bugreporting-index:

=======================
Report an issue (Forge)
=======================

.. _forge-introduction:


Introduction to Forge
=====================

The issue tracker Forge is currently based on Redmine. It is used to
report and handle open issues (including bugs and feature requests).
You need to set up an account first, see
:ref:`TYPO3-Guide-ContributionWorkflow-Account`.

When you want to report a bug or suggest a new feature, you need to go to the
`"Issues" section for the TYPO3 Core
<https://forge.typo3.org/projects/typo3cms-core/issues>`__.



Searching for existing issues
=============================

Before you go ahead and report a bug, it is recommended that you check
`Forger <https://forger.typo3.com>`__ to see if the same issue or
something similar has already been reported.

`Forger's <https://forger.typo3.com>`__ search functionality makes it
easy to find existing issues. Filters are located on the the left hand
side of the navigation menu. You can use this feature to help refine searches.

Identify the issue
==================

Before you report a bug or suggest a new feature, make sure that
the issue you report will be helpful
by following these guidelines:

Remove side effects
   Work on a TYPO3 instance which is as clean as possible so you can
   rule out extensions messing with the TYPO3 core. If you need to set
   up an extension to illustrate the problem, make sure it is as free
   of side effects as possible.

Narrow down the problem
   Try different browsers, this will help the team (and you) a lot to
   provide a proper description of the problem.

Be up to date
   First of all you should make sure that the bug does exist on the latest TYPO3
   version; we always recommend you to upgrade your TYPO3 environment to the latest
   release of the LTS version you use.
   See https://get.typo3.org/ to get the latest version of your LTS.

   Or even better: use the latest version from git.

Talk to the core team
   When in doubt, don't hesitate to talk to us on `Slack <https://typo3.slack.com>`__
   in the **#typo3-cms-coredev**
   channel. (Remember to `register <https://forger.typo3.com/slack>`__
   first.)


.. _create-an-issue:

Create an issue
===============

:ref:`Get your typo3.org account <TYPO3Account>`, head over to Forge_ and log in (if you aren't already). You can find the
TYPO3 core issue tracker here: https://forge.typo3.org/projects/typo3cms-core/.

If you click "New issue" you will see a form with a couple of fields
that are important. Let's go over these really quick.

.. important::

   If you are not a member of the TYPO3 core team, you should not be filling out
   the following fields: Priority, Assignee, Target version, Start date, Due
   date, Estimated time, Done, Complexity, Is Regression and Sprint Focus. Do
   not set a Watcher, unless someone has requested that you do this.

Tracker
-------

The tracker is just Redmines term for the type of issue. The trackers you will
be using the most are **Feature** and **Bug**.

The others are mostly for internal organization (like **Stories** and **Epics**)
and things which aren't really a feature or a bug... they are just **Tasks**
somebody needs to take care of.

Subject
-------

Pick a meaningful subject. Something like "GIFBUILDER broken" is very generic
and doesn't help describing the problem. Just imagine how you would like to get
a report for yourself :)

Bad example:
   GIFBUILDER broken

Good example:
   Text is not added to GIFBUILDER when using TEXT object

Description
-----------

Provide steps how to reproduce the problem; speaking in a general way, always
keep in mind these points when writing your issue report:

Be detailed in describing your problem
   The more detail you add, the higher are the chances that we understand your
   problem. Add screenshots or add a stacktrace can also be a great help.
Be concise and clear
   No one will judge you for your literary skills; we need to understand quickly
   where the problem lies.
Well format your issue
   Using formatted example code helps readability; also don't use very long
   sentences; instead use bullet points. See the section
   :ref:`hints-for-formatting-in-readmine` for more information on formatting your text.
Be polite.
   Always.

See :ref:`best-practices-bug-report` for additional hints on what should be in
the description of a bug report.

Category
--------

Choose a category that fits your issue.

TYPO3 version
-------------

Choose the TYPO3 version, where the error occurs.

PHP Version
-----------

Choose the PHP version, where the error occurs. If in doubt, leave this blank.



.. _best-practices-bug-report:

Best practices for writing a good bug report
============================================

A good bug report should contain all or at least most of these elements:

#. Prerequisites:

   Here you can add:

      + A brief description of your environment, including the operating system
        (Windows, Linux, macOS, ...), the full version of TYPO3, the webserver
        used, the database used (mySql, SQLServer, ...) and its version.
      + A description of the TYPO3 setup that you are using or that is necessary
        to trigger the bug. Your issue came out using TYPO3 with multiple
        languages? Or when you have more than two frontend groups? You have to
        tell us, otherwise we could not be capable of reproducing your issue.

   We don't need a full description of your environment, or the full TypoScript
   configuration, but just the parts that are relevant to trigger the bug.

#. Steps to reproduce the problem

   This is a short easy-to-follow guide that allows us to understand how to
   trigger the bug following it. Using a numerated list of steps is just fine
   here; you can also add screenshots.

#. Actual results

   This is the heart of your problem: what happened after you followed the
   steps? Please add also here if your problem is repeteable or comes out
   randomly.

#. Expected results

   What you expected to happen instead.

#. Additional notes

   Additional information like special conditions or other details not reported
   on the previous points.

Please consider that these guidelines are very generic; not always all these parts are
always necessary, but having as much information as possible really could help a
lot.


.. _hints-for-formatting-in-readmine:

Hints for formatting in Redmine
===============================

Redmine offers quite a few text formatting options: use them to make
your report readable. Remember, good formatting makes reading the
bug report easier and increases the probability that people will be
able to reproduce the problem and help with fixing, testing and
merging patches. During the life cycle of a bug report and patch,
several people will be reading your report. High readability and
clarity makes things easier for everyone and saves time.

Images
------

If you attach **images** (which makes sense, because a screenshot says
more than 1000 words), consider displaying it inline in your description
using exclamation marks to wrap your filename in - this saves everybody
a click and makes it easier to understand which image goes where. Do not
use fullscreen screenshots, provide a screenshot of the relevant parts
of the problem.

**Example:**

::

   !filename.png!

**See:**

* `Redmine Info <https://www.redmine.org/projects/redmine/wiki/RedmineTextFormattingTextile#Inline-images>`__

Code formatting
---------------

Do **not** add screenshots of code, use the ``<pre><code>`` tags in
Redmine so we can search for the lines of code via Forger.

External Links
---------------

Format your links correctly for better readability. You can insert the
URL directly, but if the URL is long, it is better to provide a
descriptive anchor text.

**Syntax:**

::

   "Anchor text":url

**Example:**

::

   "Forger search example":https://forger.typo3.com/search?query=really+long+query+string+with+filters&filters%5Btypo3_version%5D%5B8%5D=true&filters%5Bcategory%5D%5BLink_Handling_%26_Routing%5D=true

**See:**

* `Redmine Info <https://www.redmine.org/projects/redmine/wiki/RedmineTextFormattingTextile#External-links>`__
