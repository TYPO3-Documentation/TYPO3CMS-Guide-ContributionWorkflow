.. include:: ../Includes.txt

.. _prerequisites:

==============================
Prerequisites and useful tools
==============================

Here's a list of the tools we use in the TYPO3 project.
If some of these are new for you, take a few minutes to read up about what they
do for us. Maybe they prove useful in your everyday work as well.
You can find installation tutorials in the :ref:`Appendix <appendix>` section.

Composer
========

.. sidebar:: Composer

   You can learn a lot more about composer on their website https://getcomposer.org/.

Composer is a dependency manager for PHP.

So what it basically does is find packages you have defined to be part of your application (in our case TYPO3). But what
if these packages rely on other packages as well? This is where composer jumps in and takes care of keeping all these
packages in sync.

Since we use quite some packages (because why would we invent things ourselves that are already there?) composer is an
extremely useful tool for us.


Setting up your frontend build toolchain.
=========================================

Yarn
---------------

TYPO3 itself does not need yarn to run, but yarn is something similar to composer, but for the world outside of PHP.
We will be mainly using yarn to get helpful tools like Grunt and Bower.

Install on MacOS
~~~~~~~~~~~~~~~~

1. install the packagemanager homebrew => `$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
2. install yarn => `$ brew install yarn`


Installer for Windows and MacOS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Go to https://yarnpkg.com/lang/en/docs/install/#windows-tab
2. Download the package and install


Linux
~~~~~

1. Go to https://yarnpkg.com/lang/en/docs/install/#linux-tab
2. Download the package and install

Additional infos
https://yarnpkg.com


Install all required packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Go to the `Build` folder of your TYPO3 install root directory.
Install all dependencies with `yarn install`.
Wait for the the end of the install progress.
Type `yarn build` for the build process

Tasks
~~~~~

-   `yarn build` - Compile everything.
-   `yarn build-css` - Compile SCSS to CSS.
-   `yarn lint` -  Test your SCSS and ts files.
-   `yarn build-js` - Compile JavaScript.
-   `yarn format` - Resolve Style issues.
-   `yarn update` - Update dependencies (Use this if you are **really** sure what you're doing).

Grunt
=====

.. sidebar:: Grunt

   You can learn more about Grunt on their website http://gruntjs.com/.

Grunt is a JavaScript-based task runner. While this does not sound very expressive at first this is basically, what grunt
does - it runs tasks for us.

In our case grunt compiles CSS from LESS, minifies and concatenates JavaScript files, runs syntax checks and a couple of
other useful things. The good news is that TYPO3 comes with a predefined set of tasks that grunt will run, so you don't
have to take care of all the busywork underneath.


.. _cgl:

Coding Guidelines
===================

Make sure your IDE is setup properly to comply with the :ref:`Coding Guidelines for TYPO3 (CGL) <t3coreapi:cgl>`. For
example, (following PSR-2) space characters (not tabs) are used to indent source code. See
:ref:`Whitespace and indentation <t3coreapi:cgl-general-requirements-for-php-files>` for more information.

.. _cgl-fix-my-commit:

cglFixMyCommit
--------------

If you don't make sure your source code is formatted correctly, the automatic tests on the review server will fail,
after you upload your patch.

If that happens to you, you can fix this by running the following script. It will apply a fix to all php files
in your last commit.

After that you will need to do the following:

`git commit --amend`


Linux and MacOS
~~~~~~~~~~~~~~~

`Build/Scripts/cglFixMyCommit.sh dryrun`

This will show necessary modifications. To apply the modifications, run it without the dryrun parameter:

`Build/Scripts/cglFixMyCommit.sh`


Linux and MacOS
~~~~~~~~~~~~~~~

`Build/Scripts/cglFixMyCommit.bat`



