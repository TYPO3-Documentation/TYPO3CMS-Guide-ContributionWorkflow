..  include:: /Includes.rst.txt

..  highlight:: bash

..  _prerequisites:

==============================
Prerequisites and Useful Tools
==============================

Required:

*   Git
*   Once you have setup the Git repository, it is advised to look at the listed
    dependencies (basically: Docker) for  :file:`runTests.sh` (see :ref:`runTests_sh`).

Recommended:

*   IDE with TYPO3 plugins, such as PhpStorm or Visual Studio Code. While you
    can also use a simple editor, a properly setup IDE will help with
    code-completion, marking errors and applying coding guidelines.
*   `DDEV <https://ddev.com>`__ for setting up the PHP/Database web environment as a base for the TYPO3
    installation. Alternative methods
    are possible (XAMPP, LAMP, MAMP, WAMP, custom docker-compose) or even using a custom
    locally installed web server and database. DDEV
    provides custom configurations for TYPO3 which can be used for core
    development as well, and is an easy-to-use layer on top of docker-compose.

Information on using these tools is covered in detail later on this chapter.
