.. include:: ../Includes.txt


.. _aliases:

=====================
Aliases & Git Aliases
=====================

.. important::

   The following should work on MacOS and Linux as well as on Windows with some bash
   compliant shell.
   It has been tested on Linux (Xubuntu). You can help to keep this page up-to-date
   by using "Edit me on GitHub" (see :ref:`h2document:docs-contribute` for more
   information).

For shell commands you often use, you can add them to your list of aliases.

You can use these lists to get started, adapt to your workflow as needed.

Once you have added the aliases, you can do the following (after opening a new shell / terminal):

* call `alias` to show all aliases or `t3a` to show all TYPO3 aliases
* type the beginning of an alias and then tab to show all, e.g. `t3doc` and then TAB.

Also, look at the tool `git-review <https://www.mediawiki.org/wiki/Gerrit/Tutorial#Installing_git-review>`__
which might further ease your workflow.

Aliases
=======

Where aliases are maintained, depends on your system, for example on Ubuntu
Linux, add them to the file `~/.bash_aliases`.

You may need to exchange the commands for **t3open**, if the check used here does not
work for you or the command does not open your browser. Additionally, you may
need to configure this for your system. This is required for opening the rendered
documentation in the browser.

For aliases to become active, you must open a new shell after adding them to
~/.bash_aliases.

Sample List of Aliases
----------------------

.. code-block:: bash

   # show t3 aliases
   alias t3a='alias | grep -E "^alias t3"'


   # open specified URL in browser
   # see https://superuser.com/a/38989
   case "$OSTYPE" in
      cygwin*)
         alias t3open="cmd /c start"
         ;;
      linux*)
         alias t3open="xdg-open"
         ;;
      darwin*)
         alias t3open="open"
         ;;
   esac

   # ---------------
   # --- testing ---
   # ---------------
   # Use t3test with same parameters as Build/Scripts/runTests.sh
   alias t3test='Build/Scripts/runTests.sh'

   # cgl check
   alias t3cglcheck='Build/Scripts/cglCheckMyCommit.sh'

   # validate Changelog files
   alias t3clcheck='Build/Scripts/validateRstFiles.php'

   # --------------------
   # render documentation
   # --------------------

   # --- lowlevel aliases ---

   # run docker container and source shell commands
   alias t3docrun='source <(docker run --rm t3docs/render-documentation show-shell-commands)'

   # build docs
   alias t3docmake='dockrun_t3rdf makehtml'

   # open generated docs in browser (uses t3open alias, see above)
   # - use xdg-open for Linux
   # - use open for Mac instead !!!
   alias t3docopen='t3open "file:///$(pwd)/Documentation-GENERATED-temp/Result/project/0.0.0/Index.html"'

   # remove generated docs
   alias t3docclean='rm -rf Documentation-GENERATED-temp/'

   # --- combined aliases ---

   # run docker, generate documenation and open result in browser
   alias t3doc='t3docrun && t3docmake && t3docopen'

   # check changelogs and render them, open result in browser
   alias t3doccl='t3clcheck && cd typo3/sysext/core && t3doc && cd -'

.. _git-aliases:

Git Aliases
===========

If you use `--global`, the alias will be added for the current user git configuration
(usually in ~/.gitconfig). This means, they will be active for all your git repositories.

Sample Git Aliases (Commands)
-----------------------------

These are typical git aliases you may already be using, not specific to TYPO3.

Run these commands in your terminal once, it will add the aliases to your global ~/.gitconfig.

.. code-block:: bash

   git config --global alias.co checkout
   git config --global alias.br branch
   git config --global alias.ci commit
   git config --global alias.st status

   # Create an alias 'alias' to list all git aliases (in global config)
   git config --global alias.alias "config --get-regexp ^alias\."

   git config --global alias.pullom 'pull origin master'
   git config --global alias.pushom 'push origin master'
   git config --global alias.resetom 'reset --hard origin/master'

These are aliases, that may be useful for TYPO3 core contribution workflow. We start all commands
with t3 to avoid conflicts with already existing aliases:

.. code-block:: bash

   git config --global alias.t3clone 'clone git://git.typo3.org/Packages/TYPO3.CMS.git .'
   git config --global alias.t3push 'push origin HEAD:refs/publish/master'
   git config --global alias.t3push8 'push origin HEAD:refs/publish/TYPO3_8-7'


You can then use these, for example:

.. code-block:: bash

   git alias

Sample Git Aliases (.gitconfig)
-------------------------------

Alternatively, manually add the aliases to your ~/.gitconfig:

.. code-block:: none

   [alias]
      co = checkout
      br = branch
      ci = commit
      st = status

      alias = config --get-regexp ^alias\\.

      pullom  = pull origin master
      pushom  = push origin master
      resetom = reset --hard origin/master

      t3clone = clone git://git.typo3.org/Packages/TYPO3.CMS.git .
      t3push  = push origin HEAD:refs/publish/master
      t3push8 = push origin HEAD:refs/publish/TYPO3_8-7

Additional Information
======================

General
-------

* `Git Aliases <https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases>`__
* `Superuser: Platform dependant open <https://superuser.com/a/38989>`__
* `StackOverflow: List Git aliases <https://stackoverflow.com/questions/7066325/list-git-aliases>`__

Linux
-----

* Linux: xdg-open: *"xdg-open opens a file or URL in the user's preferred
  application. If a URL is provided the URL will be opened in the user's
  preferred web browser. If a file is provided the file will be opened
  in the preferred application for files of that type."*
  (see `Linux man page xdg-open <https://linux.die.net/man/1/xdg-open>`__)
* `Unix Stackexchange: How does xdg-open work <https://unix.stackexchange.com/questions/144047/how-does-xdg-open-do-its-work>`__

MacOS
-----

* `Mac OS X man page for open <https://ss64.com/osx/open.html>`__
