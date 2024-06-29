:navigation-title: Git
.. include:: /Includes.rst.txt

.. index::
   single: Git repository

.. _quickstart-git:

Quick Start: Set up Git repository
==================================

..  rst-class:: bignums-xxl

1.  Init directory and clone Repository

    ..  code:: bash

        mkdir -p ~/TYPO3-Contribute
        chdir ~/TYPO3-Contribute
        git clone https://github.com/typo3/typo3.git .

2.  Set up Git specifics

    ..  code:: bash

        # User meta data
        git config user.name "John Doe"
        git config user.email "john.doe@example.com"

        # Remote repository
        git config remote.origin.pushurl ssh://john-doe@review.typo3.org:29418/Packages/TYPO3.CMS.git
        git config remote.origin.push +refs/heads/main:refs/for/main

        # Git recommendation
        git config branch.autosetuprebase remote

        # Hooks and templates
        mkdir -p .git/hooks
        cp Build/git-hooks/commit-msg .git/hooks/commit-msg
        cp Build/git-hooks/unix+mac/pre-commit .git/hooks/
        chmod +x .git/hooks/commit-msg
        chmod +x .git/hooks/pre-commit

        echo "[BUGFIX|TASK|FEATURE|DOCS]" >> ~/.gitmessage-typo3.txt
        echo "" >> ~/.gitmessage-typo3.txt
        echo "Resolves: #" >> ~/.gitmessage-typo3.txt
        echo "Releases: main" >> ~/.gitmessage-typo3.txt
        git config commit.template ~/.gitmessage-typo3.txt