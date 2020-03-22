.. include:: ../Includes.txt


.. index::
   single: Tools; Gerrit
   single: Account; Gerrit

.. _GerritAccount:
.. _gerrit-ssh:

=======================
Setting up Gerrit (ssh)
=======================

.. rst-class:: bignums-xxl

1. Click the :guilabel:`Sign In` button in the top right corner of the page
   `review.typo3.org <https://review.typo3.org>`__.

   .. image:: _assets/gerrit_signin2.png
      :class: with-shadow

   You will be prompted with a regular :guilabel:`Basic Authentication`
   window, simply enter your TYPO3.org username and password you had
   :ref:`set up earlier <TYPO3Account>`.


2. Create your ssh key

   If you don't know how to create your SSH Public/Private Key,
   we have compiled a list of links for you:

   * :ref:`OS X <ssh-key-osx>`
   * :ref:`Microsoft Windows <ssh-key-win>`
   * :ref:`Linux/Unix <ssh-key-unix>`


3. Add your public SSH key to Gerrit

   .. image:: _assets/gerrit-add-ssh-key2.png
      :class: with-shadow

   * Click on your profile in the top right corner and click :guilabel:`Settings`.

   * On the left hand side, click :guilabel:`SSH Keys`.

   * Copy-paste the contents of your public ssh key file (e.g.
     :file:`~/.ssh/id_rsa.pub`) into the text field next to
     :guilabel:`New SSH key` and
     then click on :guilabel:`Add new SSH key`.

If you work with different computers, for example with a notebook
at work and another computer at home you can either copy your
private key or create a separate key for the other computer. Luckily
Gerrit can handle multiple keys.

.. important::

   Always keep your keys private. Never give them away. No member of the
   TYPO3 project will ever ask you for your keys.
