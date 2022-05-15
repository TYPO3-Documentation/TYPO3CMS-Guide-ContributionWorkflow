.. include:: /Includes.rst.txt

.. highlight:: bash

.. _use-styleguide:

==================
Use EXT:styleguide
==================

It is recommended to use the styleguide extension to autogenerate several
example pages which can be used for testing frontend and backend of TYPO3.

The typo3/cms-styleguide extension is part of the TYPO3 core repository.
It used to mostly showcase TCA / FormEngine features but has since evolved
to provide further features.

The styleguide extension can create pages within the TYPO3 site, specifically:

*  The "Styleguide TCA demo" will create several pages showcasing TCA features,
   e.g. there are examples for the common column types.
*  The "Styleguide Frontend" uses a custom TypoScript template provided by
   the styleguide extension and creates pages which can be viewed
   in the frontend.

Setup
=====

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

The pages will now be created. Wait a bit for flash messages to appear.
