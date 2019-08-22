.. include:: ../Includes.txt
.. highlight:: shell

.. _troubleshooting:

===============
Troubleshooting
===============

.. Some of this text was taken from the Wiki page: https://wiki.typo3.org/TroubleShooting_(Git)

.. _git-troubleshooting:

Git Troubleshooting
===================

Before you're able to push your commits you have to :ref:`set up your account <setting-up-your-account>`.
Make sure, you :ref:`setup Git <Setting-up-your-Git-environment>` correctly.

Also, you may want to :ref:`check your configuration <git-show-config>`

Permission Denied
-----------------

.. code-block:: bash

    $ git push origin HEAD:refs/for/master
    Permission denied (publickey).
    fatal: The remote end hung up unexpectedly

If this error happens, double check if you are

* Using the correct SSH user name (which is your :ref:`user name on typo3.org <TYPO3Account>`)
* If your username contains special characters (like @ or !), you must escape them using
  a backslash (or even better: use a username without special characters)
* You must use an SSH key :ref:`known to Gerrit <gerrit-ssh>`
* You must use the :ref:`correct URL <git-setup-remote>`

The following push command (with `-v`) shows you the push URL (which contain review.typo3.org)::

    $ git push origin HEAD:refs/for/master -v
    Pushing to ssh://<username>@review.typo3.org:29418/REPOSITORY_NAME.git
    Permission denied (publickey).
    fatal: The remote end hung up unexpectedly

Debugging the SSH Connection
----------------------------

Try connecting to the server with using an SSH client (OpenSSH, Putty, etc.)::

    ssh -p 29418 <username>@review.typo3.org

If the output looks like this, everything is fine::

    ****    Welcome to Gerrit Code Review    ****

    Hi <Name>, you have successfully connected over SSH.

    Unfortunately, interactive shells are disabled.
    To clone a hosted Git repository, use:

    git clone ssh://<username>@review.typo3.org:29418/REPOSITORY_NAME.git

    Connection to review.typo3.org closed.

Otherwise, your SSH client does not automatically choose the right private key file.
By default, ssh searches for the key in :file:`~/.ssh/id_rsa` and :file:`~/.ssh/id_dsa`.

You can manually specify it using the -i parameter::

    ssh -p 29418 -i <path-to-private-key> <username>@review.typo3.org

If this works, modify :file:`~/.ssh/config` to define the file name for
connections to review.typo3.org::

    Host review.typo3.org
       User <username>
       IdentityFile ~/.ssh/<keyfile>
       Port 29418

Now the connection should work without having to specify any parameters as described above.

Push: invalid committer
-----------------------

::

    $ git push -v origin HEAD:refs/for/master
    Pushing to ssh://<username>@review.typo3.org:29418/REPOSITORY_NAME.git
    remote: ERROR:  https://review.typo3.org/#/settings/contact
    remote:
    To ssh://<username>@review.typo3.org:29418/REPOSITORY_NAME.git
    ! [remote rejected] HEAD -> refs/for/master (invalid committer)
    error: failed to push some refs to 'ssh://<username>@review.typo3.org:29418/REPOSITORY_NAME.git'


This message simply means that your email address is not registered as an Web-Identity.
If this error happens, just go to the website that the error message suggests:
https://review.typo3.org/#/settings/contact Register the email address you
use to push (button "Register New Email") - even if it is already in the dropdownlist.
Click on the link you receive via email. Be sure your are already logged in on review.typo3.org.
Otherwise the link does register the email address. Check if your new identity is registered
(https://review.typo3.org/#/settings/web-identities). Pushing should work now.

You are not a committer
-----------------------

If you are trying to push changes and get this error message, then your
email address is probably not known to the system. Open Settings > Identities
in Gerrit and check the email address, which is connected to your account
(you can add more of them if needed). Additionally, check your setttings in
Git with the following command::

    git config user.email

If needed, change it with the following command::

    git config --global user.email your-email@example.com

You may change the user/author of your last commit with::

    git commit --amend

Missing Change-Id in commit message
-----------------------------------

::

    ! [remote rejected] HEAD -> refs/for/X/X (missing Change-Id in commit message)

If pushing a commit fails with this error message, you probably did not copy the :ref:`commit-hook <git-setup-commit-msg-hook>`.
Make sure that the file :file:`.git/hooks/commit-msg` exists and is executable.

Afterwards, you have to amend your commit to make it include the commit message::

    git commit --amend

Push: prohibited by gerrit
--------------------------

If Gerrit rejects your push with::

    [remote rejected] master -> master (prohibited by gerrit)

you are likely trying to do a simple `git push`. However, as Gerrit prohibits
directly pushing to the target branches, you have to use this lengthy command::

   git push origin HEAD:refs/for/<release-branch>


For example::

    git push origin HEAD:refs/for/master

Pushing old Patch Set again
---------------------------

You want to make an old patch set the current one. You cannot simply
checkout Patch Set 1 and push it again, as it is refused with a "no new changes" error message.

Amend the commit using::

    git commit --amend

Even without modifying the Commit Message, it gets a new SHA. This commit can be pushed again.