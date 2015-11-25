.. include:: ../Includes.txt

.. _prerequisites:

==============================
Prerequisites and useful tools
==============================

Here's a list of the tools we use in the TYPO3 project.

If some of these are new for you, take a few minutes to read up about what they do for us, maybe they prove useful in
your everyday work as well.

You can find installation tutorials in the :ref:`Appendix<appendix>` section.

Composer
========

.. sidebar:: Composer

   You can learn a lot more about composer on their website https://getcomposer.org/.

Composer is a dependency manager for PHP.

So what is basically does is find packages you have defined to be part of your application (in our case TYPO3). But what
if these packages rely on other packages as well? This is where composer jumps in and takes care of keeping all these
packages in sync.

Since we use quite some packages (because why would we invent things oursevles that are already there?) composer is an
extremely useful tool for us.


node.js and NPM
===============

.. sidebar:: NodeJS and NPM

   You can learn more about node.js and NPM on their websites https://nodejs.org/ and https://www.npmjs.com/.

TYPO3 itself does not need node.js to run, but node.js is something similar to composer, but for the world outside of
PHP.

We will be mainly using NPM (NodeJS package manager) to get helpful tools like Grunt and Bower.

Bower
=====

.. sidebar:: Bower

   You can learn more about Bower on their website http://bower.io/.

Bower is - again - a dependency manager. But this time, we deal with frontend related things like Bootstrap, jQuery,
icon fonts and others.

Just like Grunt, we already included a turn-key setup so you just need to change things here if you want to add a new
dependency to the TYPO3 core.

Grunt
=====

.. sidebar:: Grunt

   You can learn more about Grunt on their website http://gruntjs.com/.

Grunt is a JavaScript-based task runner. While this does not sound very expressive at first this is basically, what grunt
does - it runs tasks for us.

In our case grunt compiles CSS from LESS, minifies and concatenates JavaScript files, runs syntax checks and a couple of
other useful things. The good news is that TYPO3 comes with a predefined set of tasks that grunt will run, so you don't
have to take care of all the busywork underneath.
