.. include:: /Includes.rst.txt

.. highlight:: bash

.. _use-styleguide:
.. _after-setup-typo3:

==================
Use EXT:styleguide
==================

It is recommended to use the styleguide extension to auto generate several
example pages which can be used for testing the frontend and backend of TYPO3.

The typo3/cms-styleguide extension is part of the TYPO3 core repository.
It used mostly to showcase TCA / FormEngine features but has since evolved
to provide additional features.

The styleguide extension can create pages within the TYPO3 site, specifically:

*  The "Styleguide TCA demo" will create several pages showcasing TCA features,
   including examples for common column types.
*  The "Styleguide Frontend" uses a custom TypoScript template provided by
   the styleguide extension and creates pages which can be viewed
   in the frontend.

Setup
=====

.. tip::

   Once the styleguide extension is activated, it is possible to create
   (or delete) the pages via command line::

      # show help
      bin/typo3 styleguide:generate -h

      # create pages
      bin/typo3 styleguide:generate -c

      # or (with DDEV)
      ddev exec bin/typo3 styleguide:generate -c

.. rst-class:: bignums-xxl

1. Activate the styleguide extension in the extension manager
2. Click on :guilabel:`?` in the top bar
3. Click on the :guilabel:`Styleguide` menu item

   The Styleguide overview appears.

4. Click on :guilabel:`TCA / Records / Frontend`
5. Create pages

   Click the buttons:

   *  :guilabel:`Create styleguide page tree with data`
   *  :guilabel:`Create styleguide frontend`

The pages will now be created. Wait a moment until a flash message appears.
