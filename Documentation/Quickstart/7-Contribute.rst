:navigation-title: Reviewing & more
..  include:: /Includes.rst.txt

..  index::
    single: Reviewing and more contribution

..  _quickstart-contribute:

Quick Start: Reviewing and contributing more
============================================

Now that you followed this guide, you have a
setup to continuously work with. It has hopefully
not taken up much of your time.

With your environment, you can:

..  note::

    Ensure that your current working directory is the one
    used in previous steps, here :bash:`cd $HOME/work/TYPO3-Contribute`.

..  rst-class:: bignums-xxl

..  _quickstart-reset:
1.  Keep up to date with development

    By executing this in your working environment,
    you can always catch up to the latest `main`
    TYPO3 version:

    ..  code:: bash
        :caption: **Stash away things you may be working on**

        git stash

    ..  code:: bash
        :caption: **Reset to current upstream state**

        Build/Scripts/runTests.sh -s clean && \
            git fetch --all && \
            git reset --hard origin/main && \
            git pull --rebase && \
            ./Build/Scripts/runTests.sh -u && \
            ./Build/Scripts/runTests.sh composerInstall && \
            ddev typo3 cache:flush && \
            ddev typo3 cache:warmup && \
            ddev typo3 extension:setup

    This resets your local state to the the current upstream state, including
    recently merged changes. This may involve changes in Composer
    dependencies, database changes or changes in the Dependency Injection container
    configuration. The steps above are a fail-safe way to ensure a working environment:

    ..  code:: bash
        :caption: **Check status of the repository**

        git status

    ..  code::
        :caption: **... which should output something similar to following:**

        On branch main
        Your branch is up-to-date with 'origin/main'.

        nothing to commit, working tree clean

    ..  hint::

        You may want to create a Bash alias for this, if you
        do it more often.
        Also see :ref:`cleanup-typo3` for details.

    After that, you should also log into the TYPO3 backend
    and ensure via the :guilabel:`Database Analyzer` that your
    database is up to date.

2.  Coordinate with the team

    You can review and vote on other people's patches, gather knowledge
    and enjoy improving TYPO3 as a whole.

    You can check out any Patch on gerrit on your updated instance:

    ..  code:: bash
        :caption: **Check out the patch and changeset by using the corresponding download link in Gerrit**

        git fetch https://review.typo3.org/Packages/TYPO3.CMS refs/changes/25/85025/1 \
            && git cherry-pick FETCH_HEAD

    ..  code:: bash
        :caption: **Ensure working state for checkout change**

        ./Build/Scripts/runTests.sh composerInstall && \
            ddev typo3 cache:flush && \
            ddev typo3 cache:warmup && \
            ddev typo3 extension:setup

    Also maybe execute 'Database Analyzer' and clear browser cache

    After that you can :bash:`git commit --amend && git push` and publish
    new patch sets.

    You can even commit and contribute on other people's patches -
    always make sure to ask first, before you do that.

3.  Read on

    Further information on reviewing and contributing:

    *  :ref:`core-contrib-quickstart`
    *  :ref:`lifeOfAPatch`
    *  :ref:`reviewPatch`
