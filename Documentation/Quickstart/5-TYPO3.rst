:navigation-title: TYPO3
..  include:: /Includes.rst.txt

..  index::
    single: TYPO3

..  _quickstart-typo3:

Quick Start: Set up TYPO3
=========================

..  note::

    Ensure that your current working directory is the one
    used in previous steps, here :bash:`cd $HOME/work/TYPO3-Contribute`.

..  rst-class:: bignums-xxl

1.  Perform `composer` install

    Note that we encourage to use the TYPO3 Core `runTests.sh` runner,
    and thus do not use a local or DDEV `composer` command directly:

    ..  code:: bash
        :caption: **Install composer dependencies using default php version**

        ./Build/Scripts/runTests.sh -s composerInstall

    Bear in mind: Even though we use `composer` to install dependencies,
    the resulting TYPO3 installation will be in **Legacy** mode, not
    **Composer-Mode**. This is still how TYPO3 performs most of its core
    testing and development.

2.  Set up TYPO3 database

    Note that we perform the setup using the automatable TYPO3 Console,
    not the Web GUI. All command options use the DDEV configuration conventions,
    (`db:db@db`), you do not need to adapt this.

    ..  code:: bash
        :caption: **Setup the instance using the TYPO3 setup command**

        ddev exec touch FIRST_INSTALL && \
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

    ..  code::
        :caption: **This should result in a message:**

        ✓ Congratulations - TYPO3 Setup is done.

3.  Activate `EXT:styleguide`

    ..  code:: bash
        :caption: **Ensure extension setup and activate required extensions (EXT:styleguide, EXT:indexed_search)**

        ddev typo3 extension:setup && \
            ddev typo3 extension:activate indexed_search && \
            ddev typo3 extension:activate styleguide

    ..  code:: bash
        :caption: **Setup all default backend user groups**

        ddev typo3 setup:begroups:default --groups=Both

    ..  code:: bash
        :caption: **Create styleguide TCA and FRONTEND page tree**

        ddev typo3 styleguide:generate --create -- tca && \
            ddev typo3 styleguide:generate --create -- frontend-systemplate

    ..  code::
        :caption: **Which should give this output:**

        [OK] Extension(s) "core, filelist, frontend, impexp, lowlevel, form, extbase, fluid, fluid_styled_content, install,
            reports, redirects, setup, rte_ckeditor, adminpanel, backend, belog, beuser, dashboard, extensionmanager, felogin,
            info, seo, sys_note, tstemplate, viewpage" successfully set up.
        [OK] Activated extension styleguide successfully.
        [OK] Backend user group(s) created: Editor, Advanced Editor
        TCA page tree created!
        Frontend page tree created!

    Note there remain some extensions disabled (`filemetadata`, `indexed_search`,
    `linkvalidator`, `opendocs`, `reactions`, `recycler`, `scheduler`, `webhooks`,
    `workspaces`). If you plan to work on these, activate them similarly, or use
    the :guilabel:`Extension Manager` in the TYPO3 Backend.

    ..  attention::

        **HINT**: Frontend of `EXT:styleguide` does not seem to work right now
        using the new Site Sets feature. Thus the `EXT:styleguide` frontend page
        tree is installed using the `TypoScript Template Records` variant. Bear
        that in mind if you want to work on the `Site Sets Feature`.

4.  Log in to TYPO3

    You should now be able to log in to the TYPO3 backend with the username and
    password as specified above (`john-doe : John-Doe-1701D.`) by calling:

    ..  code::
        :caption: **Open up the TYPO3 Backend for the ddev instance**

        ddev launch typo3

