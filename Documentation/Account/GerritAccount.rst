.. include:: ../Includes.txt

.. _GerritAccount:

Setting up your Gerrit account
------------------------------

Head over to Gerrit_, scroll to the end of the page and switch to the new UI.

.. note::
    If you still want to use the old UI, please follow the version 1.0 of this guide.

.. image:: _assets/gerrit_newui.png
   :width: 400px

Now you can click the **Sign In** button in the top right corner.

.. image:: _assets/gerrit_signin.png
   :width: 400px

You will be prompted with a regular **Basic Authentication** window, simply enter your TYPO3.org username and password you
had :ref:`set up earlier <TYPO3Account>`.

.. note::

   Once you are logged into Gerrit_, you can start to make yourself familiar with the interface. Don't worry if it looks
   intimidating at first, you'll be a **Pro** with it in no time.

Adding your SSH key
~~~~~~~~~~~~~~~~~~~

All communication with Gerrit_ works via SSH, so you will need to set up your public key to work.
Click on your profile in the top right corner and click **Settings**.

.. image:: _assets/gerrit_settings.png
   :width: 400px

On the left hand side, click **SSH Public Keys** to set up your key.

.. note::

   If you work with different computers, for example with a notebook at work and another computer at home you can either
   copy your private key or create a separate key for the other computer. Luckily Gerrit_ can handle multiple keys.

.. image:: _assets/gerrit_ssh_keys.png
   :width: 400px

.. important::

   Keep your keys private. Never give them away. No member of the TYPO3 project will ever ask you for your keys.

Click **Add Key** to add your new key and paste your key into the textbox below.

If you don't know how to create your SSH Public Key, we have compiled a list of links for you:

* :ref:`OS X <ssh-key-osx>`
* :ref:`Microsoft Windows <ssh-key-win>`
* :ref:`Linux/Unix <ssh-key-unix>`
