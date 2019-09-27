.. include:: ../../Includes.txt

.. _ssh-key-win:

====================================
Creating a SSH Public Key on Windows
====================================

In order to create a SSH key for Windows you can follow these steps.


Generate Your Keys With Putty
=============================

.. image:: ../_assets/puttygen-generate.png
   :class: with-shadow

* Download and run the PuTTY Windows Installer from the `official download page
  <https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html>`__
  (chiark.greenend.org.uk)
* Start "PuTTYgen" from the start menu
* Select ``ED25519`` (1) in the groupbox ``Parameters`` on the bottom.
  Alternatively you can select ``RSA`` and increase the ``Number of bits in a
  generated key`` field to ``4096``
* Click the Generate (2) button and follow the screen instructions

.. image:: ../_assets/puttygen-save.png
   :class: with-shadow

* Fill the comment (1) to identify this key with your email for instance
* Add a passphrase for your pivate key (2, 3)
* Save you private key in a protected place on the local filesystem (4)
* Convert the key to the needed format (5) see note below
* Copy the displayed public key and add it to your Gerrit account (6)

.. note::

   Keep in mind that putty uses a proprietary format to store keys, which is
   incompatible with OpenSSH, when you use any of the save-buttons. If you need
   to store you private key in the OpenSSH format use the menu item 
   ``Conversions->Export OpenSSH key``.


Use Pageant to Load Your Pivate Key on Startup
==============================================

Putty provides a key agent named ``Pageant``, which can be added to your
autostart folder. This allows you to enter your passphrase only once at startup
and any tools using putty (e.g. git-for-windows, TortoiseGit, etc.) can
automatically use your private key.

In order to achieve this, create a new shortcut:

* Press :kbd:`Windows` + :kbd:`r`
* Copy and insert :file:`%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup`
* Right click into the folder and select ``New->Short Cut``
* Copy and insert %ProgramFiles%\PuTTY\pageant.exe "<full path to your saved
  private key.ppk>".
* Click ``Next``. If you get an error the program could not be found, delete
  the argument with your private key file and continue without an argument
* Name your new shortcut and click ``Finish``
* If you had to delete your private key file, check the properties of the newly
  created shortcut and add your private key again if it's not already there

Pageant will run as background task, place a nice little icon into your tray
icons and start automatically after your login.
