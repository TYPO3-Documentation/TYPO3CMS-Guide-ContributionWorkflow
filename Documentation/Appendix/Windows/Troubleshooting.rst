.. include:: ../../Includes.txt

.. _troubleshooting-for-windows:

============================
Troubleshooting for Windows
============================

.. important::
   Its strongly recommended to use the Git Bash on Windows as shown in previous chapters.
   We experienced issues with powershell etc. and some commands described in the documentation only work in Git Bash.

SSH
===

Permission denied (publickey)
-----------------------------

If you try to push to gerrit and you keep getting the following error message

.. code-block:: none

   Permission denied (publickey).
   fatal: Could not read from remote repository.

Checklist for ssh problems
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. rst-class:: bignums-xxl

1. Make sure the **public** SSH key is stored in your Gerrit Acccount

   See :ref:`GerritAccount`

2. Check if your **private** SSH key is in the correct OpenSSH format. 

   You can export your SSH key to the correct OpenSSH format with the Putty Key 
   Generator with Conversions -> Export OpenSSH Key -> safe with a filename, 
   but without a file ending!

3. Check if the ssh-agent is running or turn it on

   .. code-block:: bash
  
      ssh-agent -s

4. Add your SSH key to the ssh-agent

   .. code-block:: bash

      ssh-add ~/.ssh/my_key

   The SSH key should have NO file ending (like .ppk). 
   In windows explorer you should find the SSH key in 
   the file:
   
   .. code-block:: bash
   
      C:\Users\<username>\.ssh\

