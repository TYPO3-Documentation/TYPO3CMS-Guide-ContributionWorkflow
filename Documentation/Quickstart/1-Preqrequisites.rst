:navigation-title: Prerequisites
..  include:: /Includes.rst.txt

..  index::
    single: Prerequisites

..  _quickstart-prerequisites:

Quick Start: Prerequisites
==========================

We will not explain you how to set up the following prerequisites.
There are several tutorials for this on the web, and if you follow
the Quick Start guide, you should know how to do this.

..  rst-class:: bignums-xxl

1.  Operating System

    A computer running Windows with WSL2, macOS or Linux - connected to
    the Internet.

2.  Docker

    Either the "original" `Docker Desktop <https://www.docker.com/products/docker-desktop/>`__
    or an alternative like `OrbStack <https://orbstack.dev/>`__, `Podman <https://podman.io/>`__,
    `Colima <https://github.com/abiosoft/colima>`__ or others.

3.  DDEV

    `DDEV <https://ddev.com>`__ is a layer on top of Docker. How to utilize it is
    covered in this guide.

4.  Terminal (Bash)

    Your operating system needs to provide a Bash terminal, many steps of this guide
    will be executed on the shell.

5.  Git client

    This guide expects you can execute `git` terminal commands.

    This guide uses the *https* method to connect to GitHub, so you do not
    need to have a GitHub account.

6.  SSH client plus SSH key(s) and an email account

    This guide expects you can execute `ssh` terminal commands and connect to
    foreign hosts. You will need a private SSH key pair and know how to authenticate
    with it. You need an email account to setup accounts.

7.  PHP IDE / Editor

    It is recommended to use a good PHP IDE. As part of the target audience of this guide
    you should already use something like PhpStorm, Visual Studio Code, vi(m)...

8.  Assumed path structure and name usage

    We will use:

    * **~/TYPO3-Contribute/** as your working directory (created in the guide).
    * **John Doe** to be your name.
    * **john.doe@example.com** to be your email address that you used for all accounts.
    * **john-doe** to be your TYPO3.org username.
    * A TYPO3 **legacy mode** installation (Non-Composer) with MariaDB 10.11 and PHP 8.3.

    Adjust any occurences of this to match your environment.
