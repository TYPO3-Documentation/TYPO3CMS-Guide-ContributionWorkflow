:navigation-title: Git
..  include:: /Includes.rst.txt

..  index::
    single: Git repository

..  _quickstart-git:

Quick Start: Set up Git repository
==================================

..  tip::

    You may want to adapt some commands that are shown here.
    Copy them by using the copy icon in the code block, paste them
    in a raw text file or editor, adjust the values. Then copy it
    from there to paste it into your terminal again.

..  rst-class:: bignums-xxl

1.  Init directory and clone Repository

    ..  code:: bash
        :caption: **Create contribution folder and clone TYPO3 into a it**

            mkdir -p $HOME/work/TYPO3-Contribute && \
                cd $HOME/work/TYPO3-Contribute && \
                git clone https://github.com/typo3/typo3.git .

2.  Set up Git specifics

    ..  note::

        Remember that we use some convetions for username and email, see
        :ref:`prerequisite assumptions <quickstart-assumptions>.

    ..  code:: bash
        :caption: **Set up git user meta data and repository**

        git config user.name "John Doe" && \
            git config user.email "john.doe@example.com" && \
            git config remote.origin.pushurl \
                ssh://john-doe@review.typo3.org:29418/Packages/TYPO3.CMS.git && \
            git config remote.origin.push +refs/heads/main:refs/for/main

    ..  code:: bash
        :caption: **Configure recommended git options only for the repository**

        git config branch.autosetuprebase remote

    ..  code:: bash
        :caption: **Install hooks and git commit template**

        mkdir -p .git/hooks && \
          cp Build/git-hooks/commit-msg .git/hooks/commit-msg && \
          cp Build/git-hooks/unix+mac/pre-commit .git/hooks/ && \
          chmod +x .git/hooks/commit-msg && \
          chmod +x .git/hooks/pre-commit && \
          {
            echo '[BUGFIX|TASK|FEATURE|DOCS]'
            echo ''
            echo 'Resolves: #'
            echo 'Releases: main'
          } > $HOME/.gitmessage-typo3.txt && \
          git config commit.template $HOME/.gitmessage-typo3.txt
