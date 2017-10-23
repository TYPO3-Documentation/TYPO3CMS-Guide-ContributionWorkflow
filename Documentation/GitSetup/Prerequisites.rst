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

node.js and NPM
---------------

TYPO3 itself does not need node.js to run, but node.js is something similar to composer, but for the world outside of PHP.
We will be mainly using NPM (NodeJS package manager) to get helpful tools like Grunt and Bower.

Install on MacOS
~~~~~~~~~~~~~~~~

1. install the packagemanager homebrew => `$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
2. install nodejs => `$ brew install nodejs`
3. install latest npm => `$ npm install -g npm@latest`


Installer for Windows and MacOS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Go to https://nodejs.org/en/
2. Download the package and install
3. after this get the newest npm with `$ npm install -g npm@latest`


Linux
~~~~~

1. Download Installer => `$ curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -`
2. install nodejs => `$ sudo apt-get install -y nodejs`
3. install latest npm => `$ sudo npm install -g npm@latest`

Additional infos
https://nodejs.org/en/download/package-manager/


Install all required packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Go to the `Build` folder.
Install all dependencies with `npm install`.
Wait for the the end of the install progress.
Type `npm run` to see availablel tasks.
Type `npm run build` for the build process

Tasks
~~~~~

-   `npm run build` - Compile all.
-   `npm run build-css` - Compile SCSS to CSS.
-   `npm run lint` -  Test your SCSS and ts files.
-   `npm run build-js` - Compile JavaScript.
-   `npm run format` - Resolve Style issues.
-   `npm run update` - Update dependencies.

Grunt
=====

.. sidebar:: Grunt

   You can learn more about Grunt on their website http://gruntjs.com/.

Grunt is a JavaScript-based task runner. While this does not sound very expressive at first this is basically, what grunt
does - it runs tasks for us.

In our case grunt compiles CSS from LESS, minifies and concatenates JavaScript files, runs syntax checks and a couple of
other useful things. The good news is that TYPO3 comes with a predefined set of tasks that grunt will run, so you don't
have to take care of all the busywork underneath.
