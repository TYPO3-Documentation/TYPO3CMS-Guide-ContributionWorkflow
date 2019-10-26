.. include:: ../Includes.txt

.. _GerritAccount:
.. _gerrit-ssh:

.. index::
   single: Tools; Gerrit
   single: Account; Gerrit

=======================
Setting up Gerrit (ssh)
=======================

.. rst-class:: bignums-xxl

1. Switch to new UI in Gerrit

   .. image:: _assets/gerrit-new-ui2.png
      :class: with-shadow

   Head over to `Gerrit <https://review.typo3.org>`__, scroll to the bottom
   of the page and click the link "New UI". You can also work with the old
   UI, but then some things will look a little different.


2. Click the **Sign In** button in the top right corner.

   .. image:: _assets/gerrit_signin2.png
      :class: with-shadow

   You will be prompted with a regular **Basic Authentication** window,
   simply enter your TYPO3.org username and password you had
   :ref:`set up earlier <TYPO3Account>`.


3. Create your ssh key

   If you don't know how to create your SSH Public/Private Key,
   we have compiled a list of links for you:

   * :ref:`OS X <ssh-key-osx>`
   * :ref:`Microsoft Windows <ssh-key-win>`
   * :ref:`Linux/Unix <ssh-key-unix>`


4. Add your public SSH key to Gerrit

   .. image:: _assets/gerrit-add-ssh-key2.png
      :class: with-shadow

   * Click on your profile in the top right corner and click **Settings**.

   * On the left hand side, click **SSH Keys**.

   * Copy-paste the contents of your public ssh key file (e.g.
     :file:`~/.ssh/id_rsa.pub`) into the text field next to **New SSH key** and
     then click on **Add new SSH key**.

If you work with different computers, for example with a notebook
at work and another computer at home you can either copy your
private key or create a separate key for the other computer. Luckily
Gerrit can handle multiple keys.

.. important::

   Always keep your keys private. Never give them away. No member of the
   TYPO3 project will ever ask you for your keys.
