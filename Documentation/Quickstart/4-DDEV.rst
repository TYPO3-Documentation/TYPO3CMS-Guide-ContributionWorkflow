:navigation-title: DDEV
..  include:: /Includes.rst.txt

..  index::
    single: DDEV

..  _quickstart-ddev:

Quick Start: Set up DDEV
========================

..  rst-class:: bignums-xxl

1.  Set up DDEV with default convention

    ..  note::

        Ensure that your current working directory is the one
        used in previous steps, here :bash:`cd $HOME/work/TYPO3-Contribute`.

    ..  code:: bash
        :caption: **Create a suitable ddev configuration**

        ddev config \
            --project-name='t3c-main' \
            --project-type='typo3' \
            --docroot='.' \
            --database='mariadb:10.11' \
            --php-version='8.2' \
            --composer-version='stable' \
            --nodejs-version='22' \
            \
            --project-tld='ddev.site' \
            --router-http-port='80' \
            --router-https-port='443' \
            --webserver-type='apache-fpm' \
            --additional-hostnames='t3c-dev.ddev.site,t3c-prod.ddev.site' \
            \
            --timezone='Europe/Berlin' \
            --web-environment='TYPO3_CONTEXT=Development' \
            --webimage-extra-packages='build-essential,locales'

    ..  note::

        Recent DDEV versions (≥ 1.24) use Debian 12 (Bookworm) as base image.
        On Debian Bookworm, the package ``locales-all`` is no longer available
        and has been replaced by ``locales``.

        Older DDEV versions based on earlier Debian releases may still work
        with ``locales-all``.

        See:
        https://packages.debian.org/bookworm/locales

    Adapt parameters as wanted.

    ..  code::
        :caption: **The output should be similar to this:**

        Creating a new DDEV project config in the current directory (/.../TYPO3-Contribute)
        Once completed, your configuration will be written to /.../TYPO3-Contribute/.ddev/config.yaml.

        Configuring a 'typo3' named 't3c-main' project with docroot '.' at /.../TYPO3-Contribute
        TYPO3 does not seem to have been set up yet, missing settings.php (/.../TYPO3-Contribute/typo3conf/system/settings.php)
        Generating additional.php file for database connection.
        Configuration complete. You may now run 'ddev start'.

2.  Start DDEV instance

    ..  code:: bash
        :caption: **Start configured ddev project**

        ddev start

    ..  code::
        :caption: **The output should be similar to this:**

        Starting t3c-main...
        Building project images...
        .................Project images built in 17s.
        Network ddev-t3cmain_default  Created
        Container ddev-t3c-main-db  Created
        Container ddev-t3c-main-web  Created
        Container ddev-t3c-main-db  Started
        Container ddev-t3c-main-web  Started
        Waiting for containers to become ready: [web db]
        Starting ddev-router if necessary...
        Container ddev-router  Running
        Waiting for additional project containers to become ready...
        All project containers are now ready.
        Successfully started t3c-main
        Project can be reached at https://t3c-main.ddev.site https://t3c-dev.ddev.site.ddev.site https://t3c-prod.ddev.site.ddev.site https://127.0.0.1:32802
