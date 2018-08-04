.. include:: ../../Includes.txt

.. _troubleshooting-for-windows:

============================
Troubleshooting for Windows
============================

.. important::
	Its strongly recommended to use the Git Bash on Windows as shown in previous chapters.
	We experienced issues with powershell etc. and some commands described in the documentation only work in Git Bash.

SSH
=========================

Permission denied (publickey)
-------------
If you try to push to gerrit and you keep getting the following error message:

.. shell::
	Permission denied (publickey).
	fatal: Could not read from remote repository.

Checklist:
	1. The public(!) SSH key is stored in your Gerrit Acccount
	2. Check if the SSH key is in the correct OpenSSH format
	3. In the Git Bash check if the ssh-agent is running or turn it on::

		ssh-agent -s

	4. Add your SSH key to the ssh-agent::

		ssh-add ~/.ssh/my_key

	the SSH key should have no file ending. In windows explorer you should find/place the SSH key to::

		C:\Users\<username>\.ssh\

Git
=========================

