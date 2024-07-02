:navigation-title: Quick Start: 15 Mins to contribute!

..  include:: /Includes.rst.txt

..  index::
    single: Quickstart, Kickstart

..  _quickstart:

============================================================
Quick Start: Get ready to contribute to TYPO3 in 15 Minutes!
============================================================

This `Tutorial` / `How To` will show you the easiest and
*quickest way to become a contributor* to TYPO3.

It is aimed at developers who have a *good general knowledge*,
but need to know the *specifics and rules* of TYPO3 contributions.

We will use *very brief wording* and only few "read further" hints to
*streamline the process* with conventions. Please check out the
structure of this whole guide for more information.

These are the sections:

.. container:: row m-0 p-0

   .. container:: col-md-6 pl-0 pr-3 py-3 m-0

      .. container:: card px-0 h-100

         .. rst-class:: card-header h3

            .. rubric:: :ref:`1. Prerequisites <quickstart-prerequisites>`

         .. container:: card-body

            *  OS: Windows WSL2, macOS, Linux

            *  **Docker environment** (Podman, OrbStack, Colima works too)

            *  **DDEV**

            *  **Terminal** (Bash)

            *  **Git** client

            *  **SSH** client plus SSH key(s) and an email account

            *  A **PHP IDE** of your choice (PhpStorm, Visual Studio Code, vi(m), ...)
               core concepts.

   .. container:: col-md-6 pl-0 pr-3 py-3 m-0

      .. container:: card px-0 h-100

         .. rst-class:: card-header h3

            .. rubric:: :ref:`2. Accounts <quickstart-accounts>`

         .. container:: card-body

            *  **my.TYPO3.org**, using SSO for:

               *  Gerrit (**Review System**)

               *  Forge (Redmine **Issue Tracker**)

            *  (recommended) Slack (**Chat**)

   .. container:: col-md-6 pl-0 pr-3 py-3 m-0

      .. container:: card px-0 h-100

         .. rst-class:: card-header h3

            .. rubric:: :ref:`3. Set up Git <quickstart-git>`

         .. container:: card-body

               *  **Clone repository**

               *  Set up **SSH key**, **Git hooks** and **push URL**

   .. container:: col-md-6 pl-0 pr-3 py-3 m-0

      .. container:: card px-0 h-100

         .. rst-class:: card-header h3

            .. rubric:: :ref:`4. Set up DDEV <quickstart-ddev>`

         .. container:: card-body

               *  **Configure DDEV**

               *  **Start Docker containers**

   .. container:: col-md-6 pl-0 pr-3 py-3 m-0

      .. container:: card px-0 h-100

         .. rst-class:: card-header h3

            .. rubric:: :ref:`5. Set up TYPO3 <quickstart-typo3>`

         .. container:: card-body

               *  **Install TYPO3**

               *  Enable **EXT:styleguide**

               *  Launch **TYPO3 Backend**

   .. container:: col-md-6 pl-0 pr-3 py-3 m-0

      .. container:: card px-0 h-100

         .. rst-class:: card-header h3

            .. rubric:: :ref:`6. Create a patch <quickstart-patch>`

         .. container:: card-body

               *  **Develop**

               *  **Set up Forge issue**

               *  **Commit** and **push to Gerrit**

               *  **Work in Gerrit**

               *  **Announce** your contribution

               *  Implement **Feedback**

               *  **Merge**/abandon a patch

   .. container:: col-md-6 pl-0 pr-3 py-3 m-0

      .. container:: card px-0 h-100

         .. rst-class:: card-header h3

            .. rubric:: :ref:`7. Contribute more! <quickstart-contribute>`

         .. container:: card-body

               *  **Coordinate** with the team

               *  **Cherry-picks** and **resetting**

               *  **Reviewing** other patches

..  toctree::
    :hidden:
    :glob:

    *
