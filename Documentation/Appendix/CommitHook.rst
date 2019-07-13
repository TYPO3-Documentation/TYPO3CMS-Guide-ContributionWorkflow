.. include:: ../Includes.txt

.. _appendix-commit-hook:
.. _commit-hook:

============
Commit Hooks
============

.. _why-a-commit-msg-hook:
.. _commit-msg-hook:

`commit-msg` Hook
=================

* File: :file:`.git/hooks/commit-msg`
* Source file: :file:`Build/git-hooks/commit-msg`
This hook is mandatory. It **must** be used for core contribution!

First of all, this hook will be executed whenever you do a commit on your local machine.

The most important task of the hook is to generate a unique `Change-Id` for your commit. This Change-Id is **mandatory** for
Gerrit_ to identify your change. There is no way around this and it is not up for discussion :)
This Change-Id will only be generated if it is not yet present in your commit message - please do not try to come up with
a Change-Id on your own, the result will be chaos.

Apart from that the hook will check your commit message for logical errors like missing keywords, Resolves lines etc.
For detailed information on the format of a commit message, :ref:`click here<commitmessage>`.

If the commit-msg hook finds errors in your commit-msg, you can try again, by ammending to the commit::

   git commit --amend

.. _why-pre-commit-hook:
.. _pre-commit-hook:

`pre-commit` Hook
=================

* File: :file:`.git/hooks/pre-commit`
* Source file: :file:`Build/git-hooks/unix+mac/pre-commit`
* This hook is optional. **This hook is not available for Windows.**

The :file:`pre-commit` hook checks all added PHP files staged for the commit for Coding
Guideline issues and will report any problems it finds.

To fix the issues, see :ref:`cgl-fix-my-commit`.

After fixing the files you must amend your
commit::

   git commit -a --amend



.. _post-checkout-for-composer-update:

Post-checkout hook for composer install
======================================

If you want to run `composer install` for each checkout (e.g. when switching branches, tags, etc), then you can use the `post-checkout` commit hook.

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

   You need to adjust the `PATH_TO_COMPOSER` variable, that is defined after the import statements.
   Additionally the `python3` executable needs to be available in your `PATH`.
