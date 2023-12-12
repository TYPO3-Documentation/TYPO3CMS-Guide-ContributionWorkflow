.. include:: /Includes.rst.txt

.. index::
   single: Troubleshooting

.. _troubleshooting:

===============
Troubleshooting
===============


.. index::
   single: Git; Troubleshooting
   single: Troubleshooting; Git

.. _git-troubleshooting:

Git Troubleshooting
===================

Before you're able to push your commits you have to :ref:`set up your account <setting-up-your-account>`.
Make sure, you :ref:`setup Git <Setting-up-your-Git-environment>` correctly.

Also, you may want to :ref:`check your configuration <git-show-config>`

Permission Denied
-----------------

.. code-block:: bash
   :caption: shell command

   git push origin HEAD:refs/for/main

.. code-block:: none
   :caption: result

   Permission denied (publickey).
   fatal: The remote end hung up unexpectedly

If this error happens, double check if you are

* Using the correct SSH user name (which is your :ref:`user name on typo3.org <TYPO3Account>`)
* If your username contains special characters (like @ or !), you must escape them using
  a backslash (or even better: use a username without special characters)
* You must use an SSH key :ref:`known to Gerrit <gerrit-ssh>`
* You must use the :ref:`correct URL <git-setup-remote>`

The following push command (with `-v`) shows you the push URL (which contain review.typo3.org):

.. code-block:: bash
   :caption: shell command

   git push origin HEAD:refs/for/main -v

.. code-block:: none
   :caption: result

   Pushing to ssh://<username>@review.typo3.org:29418/REPOSITORY_NAME.git
   Permission denied (publickey).
   fatal: The remote end hung up unexpectedly

Debugging the SSH Connection
----------------------------

Try connecting to the server with using an SSH client (OpenSSH, Putty, etc.):

.. code-block:: bash
   :caption: shell command

   ssh -p 29418 <username>@review.typo3.org

If the output looks like this, everything is fine:

.. code-block:: none
   :caption: result

   ****    Welcome to Gerrit Code Review    ****

   Hi <Name>, you have successfully connected over SSH.

   Unfortunately, interactive shells are disabled.
   To clone a hosted Git repository, use:

   git clone ssh://<username>@review.typo3.org:29418/REPOSITORY_NAME.git

   Connection to review.typo3.org closed.

Otherwise, your SSH client does not automatically choose the right private key file.
By default, ssh searches for the key in :file:`~/.ssh/id_rsa` and :file:`~/.ssh/id_dsa`.

You can manually specify it using the -i parameter:

.. code-block:: bash
   :caption: shell command

   ssh -p 29418 -i <path-to-private-key> <username>@review.typo3.org

If this works, modify :file:`~/.ssh/config` to define the file name for
connections to review.typo3.org:

.. code-block:: text
   :caption: ~/.ssh/config

   Host review.typo3.org
      User <username>
      IdentityFile ~/.ssh/<keyfile>
      Port 29418

Now the connection should work without having to specify any parameters as described above.

If this does not work another issue might be that your SSH version is too new and does not
accept the signature algorithm . You can test this by executing:

.. code-block:: bash
   :caption: shell command

   ssh -v -p 29418 -i <path-to-private-key> <username>@review.typo3.org 2>&1 | grep "no mutual signature algorithm"

If you see the following:

.. code-block:: none
   :caption: result

   debug1: send_pubkey_test: no mutual signature algorithm

you need to allow the rsa Algorithm in your SSH config:

.. code-block:: text
   :caption: ~/.ssh/config

   Host review.typo3.org
      ...
      PubkeyAcceptedKeyTypes +ssh-rsa

Push: invalid committer
-----------------------

.. code-block:: bash
   :caption: shell command

   git push -v origin HEAD:refs/for/main

.. code-block:: none
   :caption: result

   Pushing to ssh://<username>@review.typo3.org:29418/REPOSITORY_NAME.git
   remote: ERROR:  https://review.typo3.org/#/settings/contact
   remote:
   To ssh://<username>@review.typo3.org:29418/REPOSITORY_NAME.git
   ! [remote rejected] HEAD -> refs/for/main (invalid committer)
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
Git with the following command:

.. code-block:: bash
   :caption: shell command

   git config user.email

If needed, change it with the following command:

.. code-block:: bash
   :caption: shell command

   git config --global user.email your-email@example.org

You may change the user/author of your last commit with:

.. code-block:: bash
   :caption: shell command

   git commit --amend

Missing Change-Id in commit message
-----------------------------------

.. code-block:: none
   :caption: result

    ! [remote rejected] HEAD -> refs/for/X/X (missing Change-Id in commit message)

If pushing a commit fails with this error message, you probably did not copy the :ref:`commit-hook <git-setup-commit-msg-hook>`.
Make sure that the file :file:`.git/hooks/commit-msg` exists and is executable.

Afterwards, you have to amend your commit to make it include the Change-Id:

.. code-block:: bash
   :caption: shell command

    git commit --amend

Push: prohibited by gerrit
--------------------------

If Gerrit rejects your push with:

.. code-block:: none
   :caption: result

    [remote rejected] main -> main (prohibited by gerrit)

you are likely trying to do a simple `git push`. However, as Gerrit prohibits
directly pushing to the target branches, you have to use this lengthy command:

.. code-block:: bash
   :caption: shell command

   git push origin HEAD:refs/for/<release-branch>


For example:

.. code-block:: bash
   :caption: shell command

    git push origin HEAD:refs/for/main


Push: Invalid Key Format
------------------------

You get an error about an invalid key format. This might happen if you didn't save your key in the OpenSSH format but in a proprietary format like i.e. offered by PuTTY.

Review the sections about creating a valid public/private key pair on your operating system: :ref:`gerrit-ssh`

A valid private key in OpenSSH format starts with the following lines:

.. code-block:: none

   -----BEGIN RSA PRIVATE KEY-----
   Proc-Type: 4,ENCRYPTED
   DEK-Info: DES-EDE3-CBC,0314A92F87D7FEDF

followed by about 25 lines of seemingly random signs.

Pushing old Patch Set again
---------------------------

You want to make an old patch set the current one. You cannot simply
checkout Patch Set 1 and push it again, as it is refused with a "no new changes" error message.

Amend the commit using:

.. code-block:: bash

    git commit --amend

Even without modifying the Commit Message, it gets a new SHA. This commit can be pushed again.

Resolving Merge Conflicts in generated asset files
--------------------------------------------------

If you cherry pick a patch for review; you might encounter a mergeconflict with a generated asset file:

.. code-block:: none
   :caption: result

   Mergeconflict in typo3/sysext/backend/Resources/Public/Css/backend.css

To resolve the conflict, use the following workflow:

.. code-block:: bash
   :caption: shell command

   cd Build
   npm run build
   git add
   git add typo3/sysext/backend/Resources/Public/Css/backend.css
   git cherry-pick --continue

You will see the Commit Message again and you can now save it.
When you push this change, it will create a new Patchset - this is expected behavior.
