.. include:: ../Includes.txt

.. _lifeOfAPatch-improve-patch:

=========================
Uploading a new Patch Set
=========================

To improve an existing patch set, make sure your local repository has the latest changes and
cherry-pick the latest patch set from Gerrit as described in :ref:`cherry-pick-a-patch`.

Edit the files to solve your concerns and test this new version carefully.

Update the change by **amending** the previous commit. This will overwrite the commit you fetched from Gerrit
with your changes:

.. code-block:: bash

   git commit --amend -a

.. warning::

   Make sure to not change or remove the Change-Id: line!

You can amend as often as you want. Once you are satisfied, push your improved Patch Set to Gerrit:

.. code-block:: bash

   git push origin HEAD:refs/publish/<release-branch>

where <release-branch> has to be replaced with the target branch as shown in Gerrit.
If you're currently working on the master-branch this must be ``refs/publish/master`` as well.