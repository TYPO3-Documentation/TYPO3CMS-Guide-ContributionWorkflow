.. include:: ../../Includes.txt

.. _ssh-key-win:

====================================
Creating a SSH Public Key on Windows
====================================

In order to create a SSH key for windows you can follow these steps.


Generate your keys with Putty
=============================

.. image:: ../_assets/puttygen-generate.png
   :class: with-shadow float-left

* Download and run the PuTTY Windows Installer from the official `download page
  <https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html>`__ (chiark.greenend.org.uk)
* Start "PuTTYgen" from the start menu
* Select ``ED25519`` (1) in the groupbox ``Parameters`` on the bottom. Alternatively you can select ``RSA`` and
  increase the ``Number of bits in a generated key`` field to ``4096``
* Click the Generate (2) button and follow the screen instructions

.. rst-class::  clear-both

.. image:: ../_assets/puttygen-save.png
   :class: with-shadow float-left

* Fill the comment (1) to identify this key with your email for instance
* Add a passphrase for your pivate key (2, 3)
* Save you private key in a protected place on the local filesystem (4)
* Convert the key to the needed format (5) see note below
* Copy the displayed public key and add it to your Gerrit account (6)

.. note::

   Keep in mind that putty uses a proprietary format to store keys, which is incompatible with OpenSSH, when you use any
   of the save-buttons. If you need to store you private key in the OpenSSH format use the menu item Conversions->Export
   OpenSSH key.

.. rst-class::  clear-both


Use pageant to load your pivate key on startup
==============================================

Putty provides a key agent named "pageant", which can be added to your autostart folder.
This allows you to enter your passphrase only once at startup and any tools using putty (e.g. git-for-windows,
tortoisegit, etc.) can automatically use your private key.

In order to achieve this, create a new shortcut in the following folder:
:file:`C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\`.

The target of the shortcut must be:

.. code-block:: shell

   %ProgramFiles(x86)%\PuTTY\pageant.exe "<full path to your saved private key.ppk>"

pageant will run as background task and will place a nice little icon into your tray icons.
