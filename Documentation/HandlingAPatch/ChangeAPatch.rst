.. include:: ../Includes.txt


.. highlight:: bash

.. _lifeOfAPatch-improve-patch:

======================
Upload a new Patch Set
======================

This chapter handles improving an existing patch.


.. rst-class:: bignums-xxl

1. Get the latest patchset of the patch

   The latest version of the patch is still in your local git repository. If not,
   you must cherry-pick the latest patch set from Gerrit as described in
   :ref:`cherry-pick-a-patch`.

2. Edit files to improve the patch

3. Test your changes

   Run the TYPO3 testsuite locally, as described under :ref:`testing`.

4. Add files and amend to commit

   Update the change by **amending** the previous commit. This will overwrite
   the commit you fetched from Gerrit with your changes::

      git commit --amend -a

   .. warning::

      Make sure to not change or remove the Change-Id: line!

   You can amend as often as you want.

5. Push your change to Gerrit

   Once you are satisfied, push your improved Patch Set to Gerrit::
     

      git push origin HEAD:refs/publish/master
