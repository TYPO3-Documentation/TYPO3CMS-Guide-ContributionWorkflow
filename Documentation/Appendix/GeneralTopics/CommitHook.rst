.. include:: ../../Includes.txt

.. _commit-hook:

======================
Why a pre-commit hook?
======================

First of all, this hook will be executed whenever you do a commit on your local machine.

The most important task of the hook is to generate an unique `Change-Id` for your commit. This Change-Id is **mandatory** for
Gerrit_ to identify your change. There is no way around this and it is not up for discussion :)
This Change-Id will only be generated if it is not yet present in your commit message - please do not try to come up with
a Change-Id on your own, the result will be chaos.

Apart from that the hook will check your commit message for logical errors like missing keywords, Resolves lines etc.
For detailed information on the format of a commit message, :ref:`click here<commitmessage>`.

.. important::

   The hook will **not** prevent you from comitting. It will complain about a messed up commit message, though. In case
   you forgot to write a correct commit message, you can always ``amend`` your last commit message to correct it.
