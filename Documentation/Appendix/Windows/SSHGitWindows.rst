.. include:: /Includes.rst.txt

.. index::
   single: Windows; SSH Key; Git
   single: Git; SSH Key; Windows

============================
SSH and Git tools on Windows
============================

.. note::

   This guide refers to Windows 10 1803 and similarly featured Windows Server products.

On Windows you have two different ways to use Git:

  * WSL2 - The Windows Subsystem for Linux (2nd edition) is a native Linux environment that runs alongside Windows
  * Git for Windows - The native Git version for Linux

As Git requires SSH tools in order to talk to repositories via SSH you have two options:

  * WSL2 - SSH is available within the WSL distributions by default
  * Git for Windows - You may either use the Windows native tools (see below) or use those shipped with Git for Windows.

Installing native SSH tools
===========================

Using the native tools has the benefit of having an `ssh-agent` as a Windows service.

OpenSSH Client tools is an optional Windows feature and can be installed via the Windows settings.
Search for "Manage Optional Features". Check for "OpenSSH Client" and install via "Add a feature" button if not already present.

.. _git-for-windows:

Installing Git For Windows
==========================


Download Git For Windows from  https://git-scm.com/download/win.

Run the installer ``Git-x.y.z-nn-bit.exe``.

The following steps outline some of the dialogs shown in the process to help you making the right decisions.

.. image:: /Images/External/GitSetup/git-setup-1.jpg

Accept the GPL2 license.

.. image:: /Images/External/GitSetup/git-setup-2.jpg

Windows Explorer integration is very handy, especially the "Git Bash here" option.

.. image:: /Images/External/GitSetup/git-setup-3.jpg

Choose your editor.

.. image:: /Images/External/GitSetup/git-setup-4.jpg

Adjust the default Git branch naming to your likings.

.. image:: /Images/External/GitSetup/git-setup-5.jpg

Follow the recommendation. This is especially necessary for some IDEs.

.. image:: /Images/External/GitSetup/git-setup-6.jpg

Decide whether you want to go with the bundled OpenSSH binaries or use "external" ones, for instance those shipped with Windows.
For users of PuTTY the second option might be feasible too, but this usually involves more setup with IDEs and other tools than going with OpenSSH binaries.

.. image:: /Images/External/GitSetup/git-setup-7.jpg

Select what best fits your needs.

.. image:: /Images/External/GitSetup/git-setup-8.jpg

Select the option "Checkout as-is, commit commit as-is". This ensures Git does not mangle your files magically.
Better make sure your editor is set to use LF while contributing to TYPO3.
(While the other options seem convenient, keep in mind that maybe you have to use CRLF for some reason at some point. This will need extra work to achieve.)

.. image:: /Images/External/GitSetup/git-setup-9.jpg

Select the terminal of your choice. MinTTY is a good choice, because it's mostly what you would expect from a terminal.

.. image:: /Images/External/GitSetup/git-setup-10.jpg

Choosing "Rebase" is a safe default setting to start with. It makes sure that your commits are placed on top of whatever you pull in from the remote.
If conflicts occur you have to solve them in your commit, contrary to a merge commit.
This is a good option for TYPO3 development, but you may want to adjust this for other projects. It can be configured per repository, this is just the global default.

.. image:: /Images/External/GitSetup/git-setup-11.jpg

Check if GCM is helpful for you. With TYPO3 repositories you always use SSH to push things, so this won't matter.

.. image:: /Images/External/GitSetup/git-setup-12.jpg

Try those features. The caching is indeed neat.

.. image:: /Images/External/GitSetup/git-setup-13.jpg

Pseudo console support eases use of `docker exec` commands from within Git Bash. The "file system monitor" is up to you.

Done! You are good to go.

Continue with :ref:`the general Git setup instructions <Setting-up-your-Git-environment>`.


.. _ssh-key-win:

Creating an SSH Public Key on Windows
=====================================

Microsoft has decent documentation on this:

https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement#user-key-generation

