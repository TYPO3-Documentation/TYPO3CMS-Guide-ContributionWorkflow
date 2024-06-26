.. include:: /Includes.rst.txt


.. highlight:: bash

.. index::
   single: Code Contribution Workflow; Uploading new Patch Set
   single: Git; Push
   single: Git; Upload new Patch Set

.. _lifeOfAPatch-improve-patch:

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

   Run the TYPO3 testsuite locally, as described under :ref:`testing`. Otherwise,
   don't worry, the automatic CI will do that for every committed patch set on the
   TYPO3 infrastructure.

5. Add files and amend to commit

   Update the change by **amending** the previous commit. This will overwrite
   the commit you fetched from Gerrit with your changes:

   .. code-block:: bash
      :caption: shell command

      git commit --amend -a

   .. warning::

      Make sure to not change or remove the Change-Id: line!

   You can amend as often as you want.

   Bear in mind that this kind of Git commit amending is a bit different than
   when you do it with GitHub (and using `force-push`). For Gerrit, every push
   will be a patch set. Previous patch sets can never be overwritten by amending,
   so do not worry.

.. _git-commit-with-message:
6. Push your change to Gerrit

   Once you are satisfied, push your improved Patch Set to Gerrit:

   .. code-block:: bash
      :caption: shell command

      git push origin HEAD:refs/for/main

   Each pushed set will iterate a new patch set, and all previous patch sets
   can always be compared and even checked out later on.

   If you want, you can even provide an individual commit message to your push,
   so that in gerrit your code change shows up with what usually a
   "commit message subject" could do:

   .. code-block:: bash
      :caption: shell command

      git push origin HEAD:refs/for/main%m="Some_String_Without_Whitespace"

   The underscore characters will be replaced by whitespace. You can also
   use the following bash script or shell alias to interactively do that:

   .. code-block:: bash
      :caption: push-with-message.sh

      #!/bin/bash

      read -p "Please enter pseudo-commit message: " answer
      answer=$(echo "$answer" | tr -c '[:alnum:]' '_')
      git push origin HEAD:refs/for/main%m=$answer
