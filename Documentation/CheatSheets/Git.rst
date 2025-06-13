..  include:: /Includes.rst.txt

...  highlight:: bash

..  index::
    single: Git; Git Cheat Sheet
    single: Cheat Sheets; Git Cheat Sheet

..  _cheat-sheet-git:

===============
Git Cheat Sheet
===============

This is a short list of commands. If you are not familiar with the
workflow yet, make sure you follow the link at the beginning of
each section and read the detailed description.

The following commands assume you are in the working directory of the TYPO3 core repository.

..  _cheat-sheet-git-clone:

git clone
=========

Clone TYPO3 CMS Git repository into current directory:

..  code-block:: bash
    :caption: shell command

    git clone git@github.com:typo3/typo3 .

..  _cheat-sheet-git-setup:

Setup
=====

For detailed setup instructions, please see: :ref:`Setting-up-your-Git-environment`

Migrations
==========

..  _migrate-master-main:

Migrate master => main
----------------------

If you are using an older installation with the master branch you can switch
like this from master to main:

..  code-block:: bash
    :caption: shell command

    # Make sure that git pull loads from the "main" branch
    git branch --set-upstream-to origin/main

    # Rename your current "master" branch locally to "main" to match TYPO3's naming scheme
    git branch -m master main

Please also adapt your :ref:`commit message template <committemplate>` (if
configured) to use "main" instead of "master".

*   `TYPO3 Core Development to Change Branch Name <https://typo3.org/article/typo3-core-development-to-change-branch-name>`__ (November 28, 2021)

..  _migrateToGithub:

Migrate to GitHub
-----------------

If you are working with an older t3coredev installation and are not using the
GitHub URL yet, you can switch like this:

..  code-block:: bash
    :caption: shell command

    # set remote url for "origin"
    git remote set-url origin https://github.com/typo3/typo3.git
    # set push URL to gerrit (this has not changed)
    git config remote.origin.pushurl "ssh://<your-username>@review.typo3.org:29418/Packages/TYPO3.CMS.git"

*   `Renaming the TYPO3 GitHub Repository <https://typo3.org/article/renaming-the-typo3-github-repository>`__. (July 6, 2021)

Workflow - common commands
==========================

For details see :ref:`Fixing-a-bug-A-Z`

Reset repo to last remote commit in (remote) main branch:

..  code-block:: bash
    :caption: shell command

    git reset --hard origin/main && git pull origin main

Stage and commit all changes:

..  code-block:: bash
    :caption: shell command

    git commit -a

Is the same as:

..  code-block:: bash
    :caption: shell command

    git add .
    git commit

Stage and commit all changes to already existing commit:

..  code-block:: bash
    :caption: shell command

    git commit -a --amend

Push changes to remote main branch on gerrit (default method):

..  code-block:: bash
    :caption: shell command

    git push

This assumes, you have correctly configured your remote as described in
:ref:`git-setup-remote`. If not, you must explicitly push using the
`refs/for namespace <https://gerrit-review.googlesource.com/Documentation/concept-refs-for-namespace.html>`__:

..  code-block:: bash
    :caption: shell command

    git push origin HEAD:refs/for/main

..  note::
    Pushing to `refs/publish` is deprecated, we now push to `refs/for`.
    Check out :ref:`git-commit-with-message` on how to specify a distinct
    small message alongsite your patch set.

..  _git-work-in-progress:

Workflow - work in progress
===========================

In case you want to push a "Work in progress", use the following instead:

..  code-block:: bash
    :caption: shell command

    git push origin HEAD:refs/for/main%wip

You can also configure Gerrit to always mark your pushes as WIP. In order to do this
head over to https://review.typo3.org/settings/ and configure "Set new
changes" to "work in progress" by default".

See: https://gerrit-review.googlesource.com/Documentation/user-upload.html#wip

..  _cheat-sheet-git-other-branches:

Workflow -other branches
========================

Show all branches:

..  code-block:: bash
    :caption: shell command

    git branch -a

Checkout 13.4 branch:

..  code-block:: bash
    :caption: shell command

    git checkout 13.4

Checkout 12.4 branch:

..  code-block:: bash
    :caption: shell command

    git checkout 12.4


..  important::
    Pushing to a branch other than main only makes sense if the bug only
    exists on that branch and does not exist on main. Backporting of a
    fix to a branch is done by the core team member who merges the original
    fix to the main branch.


Long story short: In most cases, **push to main**. The rest is being taken
care of by core team members!

Push 13.4 branch:

..  code-block:: bash
    :caption: shell command

    git push origin HEAD:refs/for/13.4

Push 12.4 branch:

..  code-block:: bash
    :caption: shell command

    git push origin HEAD:refs/for/12.4

Workflow - commit msg
=====================

Details: :ref:`commitmessage`

Example commit message for a bugfix:

..  code-block:: text
    :caption: commit message

    [BUGFIX] Subject line

    Description

    Resolves: #12345
    Releases: main, 10.4

Other keywords:

..  code-block:: text

    [BUGFIX]
    [FEATURE]
    [DOCS]
    [TASK]
    [!!!][FEATURE]
    [WIP][TASK]

*   subject < 52 chars (if possible, otherwise <= 72)
*   other lines <= 72 chars
*   hyperlinks with > 72 chars are allowed when required (:ref:`<commitmessage-links>`)

..  _cheatsheet-git-push-with-message:

Workflow - push with Gerrit message
===================================

Due to the nature of the commit workflow with gerrit, and a commit
always getting amended, you have no individual commit messages for one
Gerrit patch set.

To workaround that, you can add small comments to individual patch sets
pushed to Gerrit like this:

..  code-block:: bash

    git push origin HEAD:refs/for/main%m=Fixed_issue_in_JavaScript

Since that notation is a bit bland (no spaces, no linebreaks, no special
characters, it can be helpful to utilize a small Bash script:

..  code-block:: bash
    :caption: push_with_message.sh

    #!/bin/bash
    read -p "Please enter pseudo-commit message: " answer

    answer=$(echo "$answer" | tr -c '[:alnum:]' '_')
    git push origin HEAD:refs/for/main%m=$answer

Replace "main" with possibly other branches (`13.4`, `12.4`, ...) that
you may want to push to.

Workflow - Undoing / fixing things
==================================

Throw away all changes since last commit:

..  code-block:: bash
    :caption: shell command

    git reset HEAD --hard

Unstage a file (remove file from index, but keep in working dir):

..  code-block:: bash
    :caption: shell command

    git reset <path>

Change author for last commit:

..  code-block:: bash
    :caption: shell command

    git commit --amend --author "Some Name <some@email>"


Squash last 2 commits:

..  code-block:: bash
    :caption: shell command

    git rebase -i HEAD~2

In the editor, replace 'pick' with 'squash' in the line describing the latest commit

This is very handy, in case you accidentally created a new commit
instead of adding to an existing commit (with `git commit --amend`). This way,
you can merge the last 2 commits and the commit messages.

..  _cheatsheet-git-included-in:

Information: Where was a patch included?
========================================

Sometimes you see an old gerrit issue that was committed and pushed against
`main`, but wonder in which TYPO3 version it was included. Often, you can
already deduce from a `Releases: main, 12.4` line that it was committed when
`13.4` was `main`. But if you only see `Releases: main` you might begin to look
up the date of a patch and relate it to release dates, or begin to inspect the
git repository manually.

But: Hold on! Just check out the Gerrit interface and on the top right you see
the menu, from where you also cherry-pick a patch or download a patch. There's
a menu entry :guilabel:`Included in` which will reveal all TYPO3 releases (via
GIT tags), a patch was included in.

References
==========

See also these not TYPO3 specific cheat sheets for git if you are not very familiar with git:

*   `cheat sheet for git
    <https://training.github.com/>`__
    (in several languages)
*   `"git - the simple guide" by Roger Dudler <http://rogerdudler.github.io/git-guide/>`__
*   `"Oh, shit, git!" by Katie Sylor-Miller <https://ohshitgit.com/>`__ is basically a cheat sheet for Git, but
    focuses mostly on fixing things that went wrong.

To learn more about the internal working of Git, check out these resources:

*   `Git Internals in the Pro Git book <https://git-scm.com/book/en/v1/Git-Internals>`__
