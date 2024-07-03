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

        Ensure to be in the TYPO3 monorepo checkout `TYPO3-Contribute` created
        in the previous step, for example :bash:`cd ~/TYPO3-Contribute`.

    ..  code:: bash
        :caption: **Create a suitable ddev configuration**

        ddev config \
            --project-name 't3c-main' \
            --project-type 'typo3' \
            --docroot '.' \
            --database 'mariadb:10.11' \
            --php-version '8.2' \
            --composer-version 'stable' \
            --nodejs-version '20' \
            \
            --project-tld 'ddev.site' \
            --router-http-port '80' \
            --router-https-port '443' \
            --webserver-type 'apache-fpm' \
            --additional-hostnames 't3dev-staging.ddev.site,t3dev-production.ddev.site' \
            \
            --timezone 'Europe/Berlin' \
            --web-environment='TYPO3_CONTEXT=Development' \
            --webimage-extra-packages='build-essential'

    Adapt parameters as wanted.

    ..  code::
        :caption: **The output should be similar to this:**

        Creating a new DDEV project config in the current directory (/.../TYPO3-Contribute)
        Once completed, your configuration will be written to ~/TYPO3-Contribute/.ddev/config.yaml

        Configuring a 'typo3' project with docroot '.' at /.../TYPO3-Contribute
        TYPO3 does not seem to have been set up yet, missing LocalConfiguration.php (/.../TYPO3-Contribute/typo3conf/LocalConfiguration.php)
        Generating AdditionalConfiguration.php file for database connection.
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
        Successfully started t3dev
        Project can be reached at https://t3c-main.ddev.site https://t3dev-production.ddev.site.ddev.site https://t3dev-staging.ddev.site.ddev.site https://127.0.0.1:32802
