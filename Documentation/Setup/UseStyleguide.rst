.. include:: /Includes.rst.txt

.. highlight:: bash

.. _use-styleguide:
.. _after-setup-typo3:

==================
Use EXT:styleguide
==================

It is recommended to use the `styleguide` extension to auto generate several
example pages which can be used for testing the frontend and backend of TYPO3.

The :t3src:`styleguide` extension is part of the TYPO3 Core repository.
It used to mostly to showcase TCA / FormEngine features but has since evolved
to provide additional features.

The styleguide extension can create pages within the TYPO3 site, specifically:

*  The "Styleguide TCA demo" will create several pages showcasing TCA features,
   including examples for common column types.
*  The "Styleguide Frontend" uses a custom TypoScript template provided by
   the styleguide extension and creates pages which can be viewed
   in the frontend.

Also, the styleguide presents you with examples of several backend UI elements
like notifications, tabs, accordions and more.

The extension is very helpful for Core contributors and reviewers, because it
allows to test many TCA related configurations easily, without the need to
create custom extensions to reproduce problems.

`EXT:styleguide` has been integrated to the TYPO3 Core monorepository with
version 13. On older TYPO3 versions you need to install the package for example
via TER or Packagist (using Composer).

Go explore!

Setup
=====

1. Activate the styleguide extension in the extension manager
.. tip::

   Once the styleguide extension is activated, it is possible to create
   (or delete) the pages via command line:

   .. code-block:: bash
      :caption: shell command

      # show help
      bin/typo3 styleguide:generate -h

      # create pages
      bin/typo3 styleguide:generate -c

      # or (with DDEV)
      ddev exec bin/typo3 styleguide:generate -c

.. rst-class:: bignums-xxl


2. Click on :guilabel:`?` in the top bar
3. Click on the :guilabel:`Styleguide` menu item (older TYPO3 versions
   present a custom module menu item)

   The Styleguide overview appears.

4. Click on :guilabel:`TCA / Records / Frontend`
5. Create pages

   Click the buttons:

   *  :guilabel:`Create styleguide page tree with data`
   *  :guilabel:`Create styleguide frontend`

The pages will now be created. Wait a moment until a flash message appears.
