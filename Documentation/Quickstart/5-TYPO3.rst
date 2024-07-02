:navigation-title: TYPO3
..  include:: /Includes.rst.txt

..  index::
    single: TYPO3

..  _quickstart-typo3:

Quick Start: Set up TYPO3
=========================

..  rst-class:: bignums-xxl

1.  Perform `composer` install

    Note that we encourage to use the TYPO3 Core `runTests.sh` runner,
    and thus do not use a local or DDEV `composer` command directly:

    ..  code:: bash

        chdir ~/TYPO3-Contribute
        ./Build/Scripts/runTests.sh -s composerInstall -p 8.3

    Bear in mind: Even though we use `composer` to install dependencies,
    the resulting TYPO3 installation will be in **Legacy** mode, not
    **Composer-Mode**. This is still how TYPO3 performs most of its core
    testing and development.

2.  Set up TYPO3 database

    Note that we perform the setup using the automatable TYPO3 Console,
    not the Web GUI. All command options use the DDEV configuration conventions,
    (`db:db@db`), you do not need to adapt this.

    ..  code:: bash

        ddev exec touch FIRST_INSTALL
        ddev typo3 setup \
            --driver=mysqli \
            --host=db \
            --port=3306 \
            --dbname=db \
            --username=db \
            --password=db \
            --admin-username=john-doe \
            --admin-user-password='John-Doe-1701D.' \
            --admin-email="john.doe@example.com" \
            --project-name='TYPO3 Contribution' \
            --no-interaction \
            --server-type=apache \
            --force

    This should result in a message:

    ..  code::

        ✓ Congratulations - TYPO3 Setup is done.

3.  Activate `EXT:styleguide`

    ..  code:: bash

        ddev typo3 extension:setup
        ddev typo3 extension:activate styleguide
        ddev typo3 setup:begroups:default --groups=Both
        ddev typo3 styleguide:generate --create -- all

    Which should give this output:

    ..  code::

        [OK] Extension(s) "core, filelist, frontend, impexp, lowlevel, form, extbase, fluid, fluid_styled_content, install,
            reports, redirects, setup, rte_ckeditor, adminpanel, backend, belog, beuser, dashboard, extensionmanager, felogin,
            info, seo, sys_note, tstemplate, viewpage" successfully set up.
        [OK] Activated extension styleguide successfully.
        [OK] Backend user group(s) created: Editor, Advanced Editor
        TCA page tree created!
        Frontend page tree created!

    Note there remain some extensions disabled (`filemetadata`, `indexed_search`,
    `linkvalidator`, `opendocs`, `reactions`, `recycler`, `scheduler`, `webhooks`,
    `workspaces`). If you plan to work on these, activate them similarly.

4.  Log in to TYPO3

    You should now be able to log in to the TYPO3 backend with the username and
    password as specified above (`john-doe : John-Doe-1701D.`) by calling:

    ..  code::

        ddev launch typo3

    ..  attention::

        **@TODO**: Frontend of `EXT:styleguide` does not seem to work for me,
        following the guide. Even after enabling the :guilabel:`styleguide frontend demo`
        page tree, this happens when opening `https://t3dev.ddev.site/styleguide-demo-187/`:

        ..  code:: text

            (1/1) #1607585445 TYPO3\CMS\Core\Error\Http\InternalServerErrorException
            No page configured for type=0.