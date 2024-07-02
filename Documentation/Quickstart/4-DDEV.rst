:navigation-title: DDEV
..  include:: /Includes.rst.txt

..  index::
    single: DDEV

..  _quickstart-ddev:

Quick Start: Set up DDEV
========================

..  rst-class:: bignums-xxl

1.  Set up DDEV with default convention

    ..  code:: bash

        cd ~/TYPO3-Contribute
        ddev config \
            --project-name 't3dev' \
            --project-type 'typo3' \
            --docroot '.' \
            --database 'mariadb:10.11' \
            --php-version '8.3' \
            --composer-version 'stable' \
            --nodejs-version '20' \
            \
            --project-tld 'ddev.site' \
            --router-http-port '80' \
            --router-https-port '443' \
            --additional-hostnames 't3dev-staging.ddev.site,t3dev-production.ddev.site' \
            --webserver-type 'apache-fpm' \
            \
            --timezone 'Europe/Berlin' \
            --web-environment='TYPO3_CONTEXT=Development' \
            --webimage-extra-packages='build-essential'

    Adapt parameters as wanted.

    The output should be similar to this:

    ..  code::

        Creating a new DDEV project config in the current directory (~/TYPO3-Contribute)
        Once completed, your configuration will be written to ~/TYPO3-Contribute/.ddev/config.yaml

        Configuring a 'typo3' project named 't3dev' with docroot '.' at '~/TYPO3-Contribute/'.
        For full details use 'ddev describe'.
        Configuration complete. You may now run 'ddev start'.

2.  Start DDEV instance

    ..  code:: bash

        ddev start

    The output should be similar to this:

    ..  code::

        Starting t3dev...
        Building project images...
        .................Project images built in 17s.
        Network ddev-t3dev_default  Created
        Container ddev-t3dev-db  Created
        Container ddev-t3dev-web  Created
        Container ddev-t3dev-db  Started
        Container ddev-t3dev-web  Started
        Waiting for containers to become ready: [web db]
        Starting ddev-router if necessary...
        Container ddev-router  Running
        Waiting for additional project containers to become ready...
        All project containers are now ready.
        Successfully started t3dev
        Project can be reached at https://t3dev.ddev.site https://t3dev-production.ddev.site.ddev.site https://t3dev-staging.ddev.site.ddev.site https://127.0.0.1:32802
