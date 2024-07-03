:navigation-title: Create patch
..  include:: /Includes.rst.txt

..  index::
    single: Patch

..  _quickstart-patch:
Quick Start: Create a patch
===========================

Please read :ref:`quickstart-intent` for a longer text about an example
which kind of patch you could contribute.

Now with this example in mind, we have two modified files that we want to commit:

*  :file:`typo3/sysext/backend/Classes/Form/Element/JsonElement.php`
*  :file:`typo3/sysext/backend/Tests/Unit/Form/Element/JsonElementTest.php`

..  note::

    Ensure to be in the TYPO3 monorepo checkout `TYPO3-Contribute` created
    in the previous step, for example :bash:`cd ~/TYPO3-Contribute`.

..  rst-class:: bignums-xxl

1.  Create a matching Forge Ticket

    Every patch needs to have a reason to be introduced. For this,
    you need to `create an issue on Forge
    <https://forge.typo3.org/projects/typo3cms-core/issues/new>`__,
    see :ref:`forge-introduction`. With our example you could create
    an issue like:

        **Tracker**: Task

        **Subject**: The TCA Json FormEngine input needs a HTML5 attribute "input-type='json'"

        **Description**: (Describe why the attribute would be needed. Conclude with "I will create a patch for this" to let other know you'll be working on it)

    Now note down the number of your issue which you can see next to the
    title after creation, or in the URL (for example: `12345`).

2.  Ensure proper Git state

    Make sure you are in the right directory and following the previous
    steps, you should not have any other modified files:

    ..  code:: bash
        :caption: **Check git status of the repository**

        git status

    The output should be:

    ..  code:: text

        On branch main
        Your branch is up to date with 'origin/main'.

        Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git restore <file>..." to discard changes in working directory)
            modified:   typo3/sysext/backend/Classes/Form/Element/JsonElement.php
            modified:   typo3/sysext/backend/Tests/Unit/Form/Element/JsonElementTest.php

        no changes added to commit (use "git add" and/or "git commit -a")

3.  Add changed files to git stage:

    ..  code:: bash
        :caption: **Add single files to git stage to be pre-selected for a commit**

        git add typo3/sysext/backend/Classes/Form/Element/JsonElement.php && \
            git add typo3/sysext/backend/Tests/Unit/Form/Element/JsonElementTest.php

    ..  note::

        Please ensure to only add files related to your change to the stage,
        and discard unrelated files if reasonable.

4.  Commit the files

    ..  code:: bash
        :caption: **Create a git commit for files in the git stash**

        git commit

    Now your default terminal editor should open (usually `vi` or `nano`)
    and show this:

    ..  code:: text
        :caption: **The commit message template is loaded to help with commit message structure**

        [BUGFIX|TASK|FEATURE|DOCS]

        Resolves: #
        Releases: main

        # Please enter the commit message for your changes. Lines starting
        # with '#' will be ignored, and an empty message aborts the commit.
        #
        # On branch main
        # Your branch is up to date with 'origin/main'.
        #
        # Changes to be committed:
        #       modified:   typo3/sysext/backend/Classes/Form/Element/JsonElement.php
        #       modified:   typo3/sysext/backend/Tests/Unit/Form/Element/JsonElementTest.php
        #

    ..  code:: text
        :caption: **Replace that to read:**

        [TASK] Add HTML5 spec "input-type='json'" to TCA type=json

        Resolves: #12345
        Releases: main

    Close your editor with saving the commit message.

5.  Push to Git repository

    ..  code:: bash
        :caption: **Push the commit to configured remote push url (Gerrit)**

        git push

    ..  code:: text
        :caption: **Output:**

        Enumerating objects: 11859, done.
        Counting objects: 100% (11859/11859), done.
        Delta compression using up to 10 threads
        Compressing objects: 100% (3900/3900), done.
        Writing objects: 100% (9919/9919), 3.06 MiB | 9.53 MiB/s, done.
        Total 9919 (delta 6847), reused 8104 (delta 5373), pack-reused 0 (from 0)
        remote: Resolving deltas: 100% (6847/6847)
        remote: Processing changes: refs: 1, new: 1, done
        remote:
        remote: SUCCESS
        remote:
        remote:   https://review.typo3.org/c/Packages/TYPO3.CMS/+/85025 [TASK] Add HTML5 spec "input-type='json'" to TCA type=json [NEW]
        remote:
        To ssh://review.typo3.org:29418/Packages/TYPO3.CMS.git
        * [new reference]         main -> refs/for/main

6.  Open review URL

    Open the given URL `https://review.typo3.org/c/Packages/TYPO3.CMS/+/85025`
    in your browser. You should now see your contributed patch!

    Also, automatically the Pipeline will now run server-side tests on
    your patch. Coding Guidelines will be addressed. This may lead to further
    patch modification.

7.  Announce your patch, gather feedback, improve

    Sometimes, feedback will come naturally to your patch, by people seeing
    it in the Gerrit patch pipeline.

    You are welcome to join the Slack channel `#typo3-cms-coredev` and
    :ref:`advertise your contribution for feedback <announce-slack>`.

    You might want to check :ref:`common-review-checks` for things that
    people will review in your patch, hopefully leading to be merged.

    Depending on the feedback you may need to further refine your patch.

    You can do this by locally editing your files. Then it is **vital**
    that you do not perform a new git commit, but always only **amend your commit**:

    ..  code:: bash

        // ... edit files
        git commit . --amend
        git push

    See :ref:`lifeOfAPatch-improve-patch` for details.

8.  Cleaning up

    It's important to cleanup your local checkout after working on a change or
    reviewing it to avoid stacking multiple changes into a **not intented**
    relation chain and stack to the simple one commit workflow.

    At least resetting the repository and removing your created commit is the
    bare minimum you need to do:

    ..  code:: bash
        :caption: **Reset repository**

        git reset --hard origin/main

    Usually you want to reset to the current upstream state, including recently
    merged changes. Due to the nature that this could involve changes in composer
    dependencies, database changes or changes in the Dependency Injection container
    configuration, following chained commands are a fail-safe variant - which you
    may add as an alias to your shell:

    ..  code:: bash
        :caption: **Reset repository to current upstream and ensure working state**

        git fetch --all && \
            git reset --hard origin/main && \
            Build/Scripts/runTests.sh -s composerInstall && \
            ddev typo3 cache:flush && \
            ddev typo3 cache:warmup

    ..  code:: bash
        :caption: **Check status of the repository**

        git status

    ..  code::
        :caption: **... which should output something similar to following:**

        On branch main
        Your branch is up-to-date with 'origin/main'.

        nothing to commit, working tree clean



9.  Special notes

    In some cases you may need to alter assets of the TYPO3 Core, like
    `TypeScript` or `SCSS`. See :ref:`building-assets` for how to build
    and then commit these files to your patch.

10. Thank you!

    The TYPO3 community is thankful for you following this guide, and we
    hope once you have set up your development environment for it
    you can enjoy being an active contributor!

