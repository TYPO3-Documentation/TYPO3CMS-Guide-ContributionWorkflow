.. include:: ../Includes.txt


.. _cgl-fix-my-commit:

==============
cglFixMyCommit
==============

If you don't make sure your source code is formatted correctly, the
automatic tests on the Gerrit review server will fail, after you upload
your patch.

If that happens to you, you can fix this by running the following
script. It will apply a fix to all php files in your last commit.

After that you will need to do the following:

`git commit -a --amend`


Linux and MacOS
===============

`Build/Scripts/cglFixMyCommit.sh -n`

This will show necessary modifications. To apply the modifications, run
it without the dryrun parameter:

`Build/Scripts/cglFixMyCommit.sh`


Windows
=======

`Build/Scripts/cglFixMyCommit.bat`



