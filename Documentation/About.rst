.. include:: Includes.txt

.. _about:

================
About This Guide
================

This guide provides all necessary information to enable you to contribute to the TYPO3
source code.

The main focus is submitting patches (to fix bugs or add new features) to the TYPO3 source
code, but you will also find information for :ref:`writing bug reports <bugreporting-index>`,
:ref:`adding documentation <Adding-documentation>`, :ref:`running tests <testing>`,
:ref:`reviewing and testing patches <lifeOfAPatch>` etc.

How this guide is structured
============================

The guide is structured in a way to give you all necessary information **in the order
that you need it.** This means you can read it from the beginning and use it as a
hands on guide, performing the steps as you go along.

The further you go along, the more advanced the topics will become.

But, you can also use it as a reference guide and jump straight to a section you
are looking for. In this case, use the search box to search for what
you are looking for or browse through the menu.

For example:

*  :ref:`quickstart-create-a-patch` walks you through making a change in the TYPO3
   core (e.g. fix a bug or create a new feature).


The chapters are structured as follows:

*  The chapters in :guilabel:`INTRODUCTION` give you an introduction. They are not necessary
   for contribution but will give you some background information which may make
   some things easier.
*  The chapters in :guilabel:`SETUP` show how to setup a TYPO3 installation, Git and your
   accounts for contribution. This is a necessary prerequisite for most actions
   (e.g. creating a patch), but must be done only once. We recommend to start with
   this.
*  The chapters in :guilabel:`HOWTOS` walk you through one task. In most cases, it is assumed
   that you already setup your environment.
*  :guilabel:`ADDITIONAL INFORMATION` contains a cheat sheet
   :ref:`git cheat sheet <cheat-sheet-git>`, :guilabel:`Troubleshooting`
   and the :ref:`appendix` which is a reference of some topics in more depth than what
   was described in the main section. These pages near the end of the manual assume
   that you are already familiar with contributing and serve as reference pages.



Conventions used in this guide
==============================

*  When referring to elements in the gui, we use this formatting:
   :guilabel:`Add new SSH key`.
*  Keystrokes are referred to by :kbd:`CTRL + c`


.. _other-resources-for-contribution:

Other ways to contribute
========================

Besides developing for the TYPO3 core, there are many other ways to contribute and help the TYPO3 community.

You can find general information here:

*  General information about the various `Teams & Committes <https://typo3.org/teams-committees/>`__
*  General information on how you can `Participate <https://typo3.org/participate/>`__

.. _contribute:

Contribute to this Guide
========================

If you find a bug in this manual, please be so kind as to check the
online version on https://docs.typo3.org/typo3cms/ContributionWorkflowGuide/.
From there you can hit the "Edit me on GitHub" button in the top right corner
and submit a pull request via GitHub. Alternatively you can just report an `issue
on Github <https://github.com/TYPO3-Documentation/TYPO3CMS-Guide-ContributionWorkflow/issues>`__.

Maintaining high quality documentation requires time and effort
and the TYPO3 Documentation Team always appreciates support.
If you want to support us, please join the slack channel `#typo3-documentation
<https://typo3.slack.com/messages/C028JEPJL>`__.

Have a look at :ref:`h2document:docs-contribute` for more information
about how to contribute to the TYPO3 documentation.

And finally, as a last resort, you can get in touch with the
Documentation Team `by mail <documentation@typo3.org>`_.
