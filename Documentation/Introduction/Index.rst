.. include:: ../Includes.txt

.. _introduction:

============
Introduction
============


.. _overview:

Overview
========

This guide will walk you through everything necessary to become a TYPO3
contribution professional in no time.

Here is a video to get you started. Just make sure you come back here, 
to read the rest of the guide afterwards. 

.. youtube:: gN8BVSBlgfU

.. _intended-audience:

Intended audience
=================

This document is mostly intended to help developers who want to contribute to the TYPO3 CMS source code. It also
provides some sections which will be helpful for people reporting bugs. If you are not a developer,
you can still post a bug report and help in this area is appreciated very much.

.. _how-to-read-this-document:

How to read this document
=========================

If open-source development, git, composer, developing web applications, using Gerrit etc. is nothing new for you, you
may not have to read this entire document. Make sure that you **at least** look at the following sections, though,
because they are specific to TYPO3 development:

* :ref:`Contribution workflow <t3contrib:workflow-explained>`
* :ref:`Setting-up-your-Git-environment`

You must setup a specific git hook for the commit message, for example.

.. _recommended-reading:

Further recommended reading
===========================

In order to efficiently contribute to the TYPO3 core, you should familiarize yourself with its basic concepts. Helpful
reading for this is the following:

* :ref:`TYPO3 Core API <t3coreapi:start>`

You will need to format your Source Code according to the TYPO3 Coding Guidelines:

* :ref:`TYPO3 Coding Guidelines <t3coreapi:cgl>`


.. _slack-intro:

Slack
=====


If you wish to contribute, joining the `TYPO3 slack workspace <https://typo3.slack.com>`__ is strongly
recommended because it is the main communication medium currently used. In order to join the slack workspace, you
must `Register for TYPO3's Slack Platform <https://forger.typo3.com/slack>`__. On that page, you will also find
information about the most important channels.


The channel **#typo3-cms-coredev** is your channel of choice for core development. If you have some general TYPO3
support issues, please use **#typo3-cms** for that. If you are not sure which channel to use for your question
you can use **#random** where you get direct help or a hint for the right channel to ask your question.


.. hint::
   Do not ask if you can ask a question. Ask your question directly.


As always, regard the general `Code of conduct <https://typo3.org/community/code-of-conduct/>`__.


.. _botty:

Botty on Slack
~~~~~~~~~~~~~~

Also checkout the help page on `"Botty" <https://wiki.typo3.org/T3Bot>`__, the TYPO3 slack bot. We will show you
some of its commands later in this manual.


.. hint::

   You cannot use Botty in your private channel or in a direct messaging channel with someone else. Botty will
   only be available in a public channel, to which it has been invited (which is the case in #typo3-cms-coredev).


.. _other-resources-for-contribution:

Other ways to contribute
========================

Besides developing for the TYPO3 core, there are many other ways to contribute and help the TYPO3 community.

You can find general information here:

* General information about the various `Teams & Committes <https://typo3.org/teams-committees/>`__
* General information on how you can `Participate <https://typo3.org/participate/>`__

Some examples of areas where you can contribute are:

* `TYPO3 documentation <https://typo3.org/teams-committees/documentation/>`__:
  You can get in touch with the TYPO3 documentation team in the
  #typo3-documentation channel on :ref:`slack-intro` or just
  use the "Edit me on github" button which is located on the top right of every documentation page.
* `Translation <https://forge.typo3.org/projects/team-translation>`__
* A large number of extensions available for TYPO3 are hosted on github
  and "issues" and "pull requests" are welcome. If you are interested
  in helping with an extension, check out where the source is located
  by visiting the `TYPO3 Extension Repository <https://extensions.typo3.org/>`__
  (TER). In the detail view for each extension, you will usually find
  a "Take a look in the code" link, which will link directly to
  the source code repository.


   .. image:: _assets/ter_detail.png


.. _general-recommendations-contributions:

General recommendations for contribution
========================================

In general: If you wish to make a contribution, familiarize yourself with the basics and general conventions used. In
Open-source projects it is usually mandatory that your code must follow the general coding guidelines for the
project and that your commit messages either follow general recommendations for commit messages or use specific
constraints for the project.

Some github projects have a contribution guide available, the TYPO3 CMS project has this guide.

If in doubt, ask on slack. Most likely, someone will be happy to help you.


.. Credits
.. ==========
.. To be filled later or removed ...


.. What's new
.. ==========
.. To be filled later or removed ...


Feedback
========

If you find a bug in this manual, please be so kind as to check the
online version on https://docs.typo3.org/typo3cms/ContributionWorkflowGuide/.
From there you can hit the "Edit me on GitHub" button in the top right corner
and submit a pull request via GitHub. Alternatively you can just `file an issue
using the bug tracker <https://github.com/TYPO3-Documentation/TYPO3CMS-Guide-ContributionWorkflow/issues>`__.

Maintaining high quality documentation requires time and effort
and the TYPO3 Documentation Team always appreciates support.
If you want to support us, please join the slack channel `#typo3-documentation
<https://typo3.slack.com/messages/C028JEPJL>`__.

Visit https://forger.typo3.org/slack to gain access to Slack.

Have a look at the contribution page for more information about how to contribute to the TYPO3
documentation: https://docs.typo3.org/Contribute/Index.html

And finally, as a last resort, you can get in touch with the documentation team `by mail <documentation@typo3.org>`_.
