:navigation-title: Git
..  include:: /Includes.rst.txt

..  index::
    single: Git repository

..  _quickstart-git:

Quick Start: Set up Git repository
==================================

..  tip::

    Some commands needs replacing values with your information. Copy them by using
    the copy icon in the code block and paste them in a raw text file or editor,
    adjust the values, copy it again and paste it into your terminal to make handling
    these commands easier.

..  rst-class:: bignums-xxl

1.  Init directory and clone Repository

    ..  code:: bash
        :caption: **Head over to your working folder**

        cd /path/to/your/working/folder

        # or create one
        mkdir -p $HOME/working-folder && \
            cd $HOME/working-folder

    ..  code:: bash
        :caption: **Create contribution folder and clone TYPO3 into a it**

            mkdir -p ./TYPO3-Contribute && \
                cd ./TYPO3-Contribute && \
                git clone https://github.com/typo3/typo3.git .

2.  Set up Git specifics

    ..  note::

        Replace `user.name` and `user.email` values in the next commands with
        your name and email address to be used for git commit message author
        information.

    ..  code:: bash
        :caption: **Set User meta data to git (author information)**

        git config user.name "John Doe" ; \
            git config user.email "john.doe@example.com"

    ..  note::

        Replace `john-doe` in next command with your Gerrit (TYPO3) user name.

    ..  code:: bash
        :caption: **Set push remote repository to the TYPO3 Gerrit instance**

        git config remote.origin.pushurl ssh://john-doe@review.typo3.org:29418/Packages/TYPO3.CMS.git ; \
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
          } > ~/.gitmessage-typo3.txt && \
          git config commit.template ~/.gitmessage-typo3.txt

    ..  code:: bash
        :caption: **Display repository git config ...**

        cat .git/config

    ..  code::
        :caption: **... and verify that following options are contained with your settings**

        [core]
            repositoryformatversion = 0
            filemode = true
            bare = false
            logallrefupdates = true
        [remote "origin"]
            url = https://github.com/typo3/typo3.git
            fetch = +refs/heads/*:refs/remotes/origin/*
            pushurl = ssh://john-doe@review.typo3.org:29418/Packages/TYPO3.CMS.git
            push = +refs/heads/main:refs/for/main
        [branch "main"]
            remote = origin
            merge = refs/heads/main
        [user]
            name = John Doe
            email = john.doe@example.com
        [branch]
            autosetuprebase = remote
        [commit]
            template = /home/sbuerk/.gitmessage-typo3.txt

