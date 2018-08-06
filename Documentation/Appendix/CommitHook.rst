.. include:: ../Includes.txt

.. _appendix-commit-hook:
.. _commit-hook:

============
Commit hooks
============

.. _why-a-commit-msg-hook:
.. _why-pre-commit-hook:

Why a commit-msg hook?
======================

First of all, this hook will be executed whenever you do a commit on your local machine.

The most important task of the hook is to generate a unique `Change-Id` for your commit. This Change-Id is **mandatory** for
Gerrit_ to identify your change. There is no way around this and it is not up for discussion :)
This Change-Id will only be generated if it is not yet present in your commit message - please do not try to come up with
a Change-Id on your own, the result will be chaos.

Apart from that the hook will check your commit message for logical errors like missing keywords, Resolves lines etc.
For detailed information on the format of a commit message, :ref:`click here<commitmessage>`.


.. _post-checkout-for-composer-update:

Post-checkout hook for composer update
======================================

If you want to run `composer update` for each checkout (e.g. when switching branches, tags, etc), then you can use the `post-checkout` commit hook.

Create a file named `.git/hooks/post-checkout` with the following contents:

.. code::

   #!/usr/bin/env python3
   #-*- coding: utf-8 -*-

   """A post-checkout git hook to execute `composer install`

   :Author: Philipp Gampe
   """

   import subprocess
   import string
   import os
   import sys

   PATH_TO_COMPOSER = '/home/phil/bin/composer.phar'
   HOOK_DIR = os.path.dirname(os.path.realpath(__file__))
   GIT_ROOT_DIR = os.path.dirname(os.path.dirname(HOOK_DIR))

   def main():
       if sys.argv[3] == '1':
           os.chdir(GIT_ROOT_DIR)
           return subprocess.run([PATH_TO_COMPOSER, 'install'], timeout=30)

   if __name__ == '__main__':
       result = main()
       if result:
           exit(result.returncode)
       else:
           exit(0)

.. important::

   You need to adjust the `PATH_TO_COMPOSER` variable, that is defiened after the import statements.
   Additionally the `python3` executable needs to be available in your `PATH`.
