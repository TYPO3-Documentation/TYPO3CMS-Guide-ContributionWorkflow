.. include:: ../Includes.txt


.. highlight:: bash

.. _lifeOfAPatch-improve-patch:

.. index::
   single: Code Contribution Workflow; Uploading new Patch Set
   single: Git; Push
   single: Git; Upload new Patch Set

======================
Upload a new Patch Set
======================

This chapter handles improving an existing patch. For creating a new patch, see :ref:`Fixing-a-bug-A-Z`.


.. rst-class:: bignums-xxl

1. Get the latest patchset of the patch

   The latest version of the patch is still in your local git repository. If not,
   you must cherry-pick the latest patch set from Gerrit as described in
   :ref:`cherry-pick-a-patch`.

2. Edit files to improve the patch

3. Add tests (recommended)

   If you add functionality, it is a good idea to add tests.

   See :ref:`t3coreapi:testing-writing-unit` in TYPO3 Explained for more information
   about writing Unit Tests.

4. Test your changes (optional)

   Run the TYPO3 testsuite locally, as described under :ref:`testing`.

5. Add files and amend to commit

   Update the change by **amending** the previous commit. This will overwrite
   the commit you fetched from Gerrit with your changes::

      git commit --amend -a

   .. warning::

      Make sure to not change or remove the Change-Id: line!

   You can amend as often as you want.

6. Push your change to Gerrit

   Once you are satisfied, push your improved Patch Set to Gerrit::


      git push origin HEAD:refs/for/master
