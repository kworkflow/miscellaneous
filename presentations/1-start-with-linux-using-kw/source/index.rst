.. raw:: html

  <!-- Slide -->
  <section>
    <img width="800" height="327" src="_static/kw.png" style="background:none; border:none; box-shadow:none;">
    <br>
    <img width="120" height="41" src="_static/by.png" style="background:none; border:none; box-shadow:none;">
  </section>

======================================================
Introduction: Linux Kernel development using kworkflow
======================================================

:Released: 2021-10-03

Overview
========

Linux kernel is a huge puzzle
-----------------------------

.. revealjs-section::
    :data-background-image: _static/linux-puzzle.jpg
    :data-background-size: contain

Linux Kernel as a project
-------------------------

* Linux kernel is a giant puzzle where each piece is a subsystem.
* All subsystems have their repository and their way to work.
* To put things in perspective, some numbers from the
  `kernel 5.6 release <https://lwn.net/Articles/816162/>`_:

 * 12,665 non-merge
 * 1,712 developers
 * More than 207 companies

About kw
========

What is kw?
-----------

It is a set of small software combined to reduce the environment and setup
overhead for developing for GNU/Linux.

Why you should use kw?
----------------------

* Everybody who works with Linux Kernel creates their scripts, which means we
  have a lot of duplicate effort. Kw intends to centralize many repeatable
  tasks in a single project, and it tries to be adaptable for different
  scenarios.

* Developing for Linux Kernel has a steep learning curve, and kw intends to
  reduce this learning curve.

kw: Basic concepts
==================


kw config file
--------------

.. container:: flex

  .. container:: half

    .. figure:: _static/kw-config.png
       :width: 30%

kw config file
--------------

kw uses a series of configuration files to determine non-default behavior that
you may want.

- kw’s configuration files are plain-text, so you can set these values by
  manually editing the file and inserting the correct syntax.

Global config
-------------

kw looks for the `~/.config/kw/kworkflow.config` file, which is specific to
each user.

Local config
------------

Finally, kw looks for configuration values in the configuration file in the kw
directory (`$PWD/.kw/kworkflow.config`) of whatever repository you're currently
using.

Example: Alerts
---------------

kw allows you to set a visual and sonorous alerts for some of its tasks:

.. code-block:: shell

  vim ./kw/kworkflow.config

Add:

.. code-block:: shell

    [..]
    alert=vs
    [..]

Targets
-------

.. container:: flex

  .. container:: half

    .. figure:: _static/kw-targets.png
       :width: 50%


Preparation
===========

QEMU VM
-------

For the sake of simplicity, in this presentation, we will use a QEMU Virtual
machine. If you want to know how to set it up in a convenient way for Linux
development, take a look at:

`Setup QEMU VM <https://flusp.ime.usp.br/others/use-qemu-to-play-with-linux/>`_

QEMU VM
-------

**IMPORTANT:**

For this presentation, we will suppose:

* You already have ssh set up in your development system.
* Add your public ssh key for the `root` user in the VM.
* Install rsync and screen in the VM.

kw setup
--------

1. Clone kworkflow

.. code-block:: shell

  git clone https://github.com/kworkflow/kworkflow.git

2. Install

.. code-block:: shell

  cd kworkflow
  ./setup -i

3. Open a new terminal and check it

.. code-block:: shell

  kw version

Clone Linus Torvalds Repository
-------------------------------

Let's use the Linus Torvalds repository:

.. code-block:: shell

  git clone git://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git

Create a local config
---------------------

In your Linux kernel project:

.. code-block:: shell

  kw init

For this presentation:

.. code-block:: shell

  kw init --target "remote" --remote "root@localhost:2222"

Kernel config file
==================

Overview
--------

The `.config` file holds all the information about what should be compiled or
not during the build process. The .config file has three possible answers per
target: (1) m, (2) y, and (3) n.

Overview
--------

Every Linux Distribution (e.g., Arch, Debian, and Fedora) usually maintain and
distribute their own `.config` file. The distributions `.config` usually
enables most of the available options (especially the device drivers) because
they have to run in a large variety of hardware.

kw config manager: fetch a config file
--------------------------------------

Kw provides a feature to extract the config file from a target machine:

.. code-block:: shell

  kw configm --fetch # or kw g --fetch

You can use the optimize option:

.. code-block:: shell

  kw configm --fetch --optimize

kw config manager: Save your config file
----------------------------------------

kw can be used to save your config file:

.. code-block:: shell

  kw configm --save MY_FIRST_CONFIG --description "Kw presentation"

kw config manager: List your config file
----------------------------------------

.. code-block:: shell

  kw configm --list
  Name                       | Description
  MY_FIRST_CONFIG            | Kw presentation

kw config manager: Get your config file
----------------------------------------

You can retrieve a config file under kw management by using:

.. code-block:: shell

  kw configm --get MY_FIRST_CONFIG

Kernel Compilation
==================

Overview
--------

kw can help you with basic tasks related to building the kernel, such as:

- Cross-compilation
- Kernel menu
- Build

Kernel Menu
-----------

Access the kernel configuration menu

.. code-block:: shell

  kw build --menu # or kw b -n

Kernel Menu
-----------

.. revealjs-section::
    :data-background-image: _static/nconfig.png
    :data-background-size: contain

Kernel Menu
-----------

.. revealjs-section::
    :data-background-image: _static/change_name.png
    :data-background-size: contain

Compiling your kernel
---------------------

Now that you have your kernel config file, let's compile the kernel:

.. code-block:: shell

  kw build # or kw b

Deploy your custom kernel
=========================

Remote deploy: Recap
--------------------

Kw can help you to install your new kernel via the deploy feature. Keep in mind
that deploy works based on three different targets:

1. Remote: Your test machine. For this presentation, it is your QEMU VM.
2. Local: It is your host machine; only use it if you really know what you are
   doing.
3. VM: If you don't want to use the remote deploy for your VM, you can use the
   VM option.

Remote deploy: Recap
--------------------

Make sure that you setup your `kworkflow.config` file correctly:

.. code-block:: shell

  vim .kw/kworkflow.confg
  [..]
  ssh_ip=localhost
  ssh_port=2222
  ssh_user=root
  [..]

Remote deploy: Test
-------------------

.. code-block:: shell

  kw ssh

Remote deploy: Deploy!
----------------------

* If you have already compiled your kernel:

.. code-block:: shell

  kw deploy

* If you did not compile your kernel yet:

.. code-block:: shell

  kw bd

Remote deploy: List
-------------------

You can list kernel installed via kw by using:

.. code-block:: shell

  kw deploy --list # Or kw d -l

You can list kernel installed in your system by using:

.. code-block:: shell

  kw deploy --uninstall "5.13.0-VM-TORVALDS"


Summary
=======

Setup
-----

.. code-block:: shell

  git clone https://github.com/kworkflow/kworkflow.git
  cd kworkflow
  ./setup -i
  cd ..
  git clone git://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git
  kw init --target "remote" --remote "root@localhost:2222"
  kw build --menu

Build & Deploy
--------------

.. code-block:: shell

  kw bd

Next Steps
==========

Getting help with kw
--------------------

kw quick help:

.. code-block:: shell

  kw -h
  kw b -h
  kw d -h

kw detailed help:

.. code-block:: shell

  kw b --help
  kw man build
  kw man <feature>

Getting help with kw
--------------------

* Try: `kworkflow.org <https://kworkflow.org>`_:

Ask questions at:

* `Github discussion: <https://github.com/kworkflow/kworkflow/discussions>`_
* IRC: kw-devel@oftc (kw-devel-br@oftc - Brazillian community)

Contribute to kw
----------------

If you want to contribute to kw, take a look at:

* https://kworkflow.org/content/howtocontribute.html
* https://kworkflow.org/content/developmentworkflow.html
* https://kworkflow.org/content/codingstyle.html

Thanks
------

