..  include:: /Includes.rst.txt

..  highlight:: bash

..  _use-styleguide:
..  _after-setup-typo3:

==================
Use EXT:styleguide
==================

It is recommended to use the `styleguide` extension to auto generate several
example pages which can be used for testing the frontend and backend of TYPO3.

The :t3src:`styleguide` extension is part of the TYPO3 Core repository.
It is mostly used to showcase TCA / FormEngine features, but it has since evolved
to provide additional features.

The styleguide extension can create pages within the TYPO3 site, specifically:

*   The "Styleguide TCA demo" will create several pages showcasing TCA features,
    including examples for common column types.
*   The "Styleguide Frontend" uses a custom TypoScript template provided by
    the styleguide extension and creates pages which can be viewed
    in the frontend.

Also, the styleguide presents you with examples of several backend UI elements
like notifications, tabs, accordions and more.

The extension is very helpful for Core contributors and reviewers, because it
allows to test many TCA related configurations easily, without the need to
create custom extensions to reproduce problems.

`EXT:styleguide` has been integrated to the TYPO3 Core monorepository with
version 13. On former TYPO3 versions you need to install this package either in the Extension Manager or by Composer.

Go explore!

Setup
=====

..  rst-class:: bignums-xxl

1.  Activate the styleguide extension in the Extension Manager
    ..  tip::

        Once the styleguide extension is activated, it is possible to create
        (or delete) the pages via command line:

        ..  code-block:: bash
            :caption: shell command

            # create pages
            bin/typo3 styleguide:generate -c
            # or (with DDEV)
            ddev typo3 styleguide:generate -c

            # show help
            bin/typo3 styleguide:generate -h

2.  In the Modules bar click on :guilabel:`System > Styleguide`
3.  Click on the :guilabel:`Styleguide` menu item (former TYPO3 versions
    present a custom module menu item)

    The :guilabel:`Styleguide` overview appears.

4.  Click on :guilabel:`TCA / Records / Frontend`
5.  Create pages

    Click the buttons:

    *   :guilabel:`Create styleguide page tree with data`
    *   :guilabel:`Create styleguide frontend`

The pages will now be created. Wait a moment until a flash message appears.
