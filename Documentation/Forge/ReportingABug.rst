.. include:: ../Includes.txt

.. _bugreporting-index:

===============
Reporting a bug
===============


Searching for existing bugs
===========================

Before you want to report a bug, you may want to search through the existing issues, to see if any related issues
or even the exact same problem has already been reported.

In order to do this, you can use `Forger <https://forger.typo3.com>`__ to search and narrow down your search by using the filters on the left.

.. image:: _assets/forger-filter.png


Identify the issue
==================

Before you report a bug, make sure that your issue will be helpful by following these guidelines:

Be up to date
   First of all, you should make sure that the bug does exist in the latest master branch. Do a ``git pull`` on your
   development environment, flush all caches, do a ``composer install``, just to be sure.

Remove side effects
   Work on a TYPO3 instance which is as clean as possible so you can rule out extensions messing with the TYPO3 core. If you
   need to set up an extension to illustrate the problem, make sure it is as free of side effects as possible.

Narrow down the problem
   Try different browsers, this will help the team (and you) a lot to provide a proper description of the problem.

Check for already existing issues
   Search for already existing issues for this problem. You can use `Forger <https://forger.typo3.com>`__

Talk to the core team
   When in doubt, don't hesitate to talk to us on Slack in the
   `#typo3-cms-coredev <https://typo3.slack.com/messages/C03AM9R17/details/>`__ channel. (Remember to `register
   <https://forger.typo3.com/slack>`__ first.)


Create an issue
===============

Head over to Forge_ and log in (if you aren't already). You can find the TYPO3 core issue tracker here: https://forge.typo3.org/projects/typo3cms-core/.

If you click "New issue" you will see a form with a couple of fields that are important. Let's go over these really quick.

Tracker
   The tracker is just Redmines term for the type of issue. The trackers you will be using the most are **Feature** and **Bug**.
   The others are mostly for internal organization (like Stories and Epics) and things which aren't really a feature or
   a bug... they are just tasks somebody needs to take care of.

Subject
   Pick a meaningful subject. Something like "GIFBUILDER broken" is very generic and doesn't help describing the problem.
   Just imagine how you would like to get a report for yourself :)

Description
   As usual, provide steps how to reproduce the problem. See the next section for more information on formatting your
   text.

Category
   Choose a category that fits your issue.

TYPO3 version
   Choose the correct TYPO3 version.

PHP Version
   Choose the correct PHP version.


.. important::

   If you are not a member of the TYPO3 core team, you should not be filling out
   the following fields: Priority, Assignee, Target version, Start date, Due
   date, Estimated time, Done, Complexity, Is Regression and Sprint Focus. Do
   not set a Watcher, unless someone has requested that you do this.



Hints for Formatting in Redmine
===============================

Redmine offers quite a few text formatting options: use them to make your report readable. Remember, good formatting makes
reading the bug report easier and increases the probability that people will be able to reproduce the problem and help
with fixing, testing and merging patches. During the life cycle of a bug report and patch, several people will be reading
your report. High readability and clarity makes things easier for everyone and saves time.

Images
------

If you attach **images** (which makes sense, because a screenshot says more than 1000 words), consider
displaying it inline in your description using exclamation marks to wrap your filename in - this saves everybody a click
and makes it easier to understand which image goes where. Do not use fullscreen screenshots, provide a screenshot of the
relevant parts of the problem.

**Example:**

::

   !filename.png!

**See:**

* `Redmine Info <https://www.redmine.org/projects/redmine/wiki/RedmineTextFormattingTextile#Inline-images>`__

Code formatting
---------------

Do **not** add screenshots of code, use the ``<pre><code>`` tags in Redmine so we can search for the lines of code via
Forger.

External Links
---------------

Format your links correctly for better readability. You can insert the URL directly, but if the URL is long, it is
better to provide a descriptive anchor text.

**Syntax:**

::

   "Anchor text":url

**Example:**

::

   "Forger search example":https://forger.typo3.com/search?query=really+long+query+string+with+filters&filters%5Btypo3_version%5D%5B8%5D=true&filters%5Bcategory%5D%5BLink_Handling_%26_Routing%5D=true

**See:**

* `Redmine Info <https://www.redmine.org/projects/redmine/wiki/RedmineTextFormattingTextile#External-links>`__