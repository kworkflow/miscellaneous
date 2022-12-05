.. raw:: html

  <!-- Slide -->
  <section>
    <img width="800" height="327" src="_static/kw.png" style="background:none; border:none; box-shadow:none;">
    <br>
    <img width="120" height="41" src="_static/by.png" style="background:none; border:none; box-shadow:none;">
    <img width="111" height="111" src="_static/qrcode.png" style="background:none; border:none; box-shadow:none;">
  </section>

======================================================
Introduction: Linux Kernel development using kworkflow
======================================================

Released: 2021-10-03, Updated: 2022-12-03

About kw
========

What is kw?
-----------

It is a set of small software combined to simplify the work with Linux. It is a
tool that can be used to make kernel development easier.

Why you should use kw?
----------------------

* Everybody who works with Linux Kernel creates their scripts, which means we
  have a lot of duplicate effort. Kw intends to centralize many repeatable
  tasks in a single project and tries to be adaptable to different scenarios.
* Developing for Linux Kernel has a steep learning curve, and kw intends to
  reduce this learning curve.

Presentation assumptions
========================

Assumptions
-----------

For this presentation, we will suppose:

* You already have ssh set up in your development system.
* Add your public ssh key for the `root` user in the test machine.

kw setup
========

Clone kworkflow
---------------

.. code-block:: shell

  $ git clone https://github.com/kworkflow/kworkflow.git
  $ cd kworkflow

Optional: If you want the cutting-edge version of kw, switch to the `unstable`
branch.

.. code-block:: shell

  $ git checkout unstable

Install
-------

.. code-block:: shell

  $ ./setup -i

Open a new terminal and check your installation:

.. code-block:: shell

  $ kw version
  alpha
  Branch: unstable
  Commit: 0dd80c0

Clone Linux Repository
----------------------

Let's use AMDGPU repository as a reference:

.. code-block:: shell

  git clone https://gitlab.freedesktop.org/agd5f/linux.git

Example full installation:
--------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/full-kw-install.gif
       :width: 70%

Example after:
--------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-install-example.gif
       :width: 80%



Create a local kw config
------------------------

In your Linux kernel project:

.. code-block:: shell

  kw init

For this presentation:

.. code-block:: shell

  kw init --template=x86-64

Example:
--------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-init.gif
       :width: 100%


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

- kw uses configuration files to determine non-default behavior or a specific
  configuration per repository.

Global config
-------------

kw looks for the `~/.config/kw/` folder, which is specific to each user.

Local config
------------

After reading the global configuration, kw attempts to find the local
configuration values in the directory: $PWD/.kw/. If it finds it, it replaces
the global config with the local one.

Example: Change configurations
------------------------------

kw allows you to set a visual and sonorous alerts for some of its tasks:

.. code-block:: shell

  kw config [config file name].[option] [value]

Example:

.. code-block:: shell

  kw config notification.alert vs

Example:
--------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-config-change-notificaton.gif
       :width: 100%


Kernel config file
==================

Overview
--------

The kernel .config file holds all the information about what should be compiled
or not during the build process.

Every Linux Distribution (e.g., Arch, Debian, and Fedora) usually maintain and
distribute its .config file. The distributions .config usually enable most of
the available options (especially the device drivers) because they have to run
on a large variety of hardware.

kw config manager: Save your config file
----------------------------------------

kw can be used to save your config file:

.. code-block:: shell

  kw kernel-config-manager --save MY_FIRST_CONFIG \
  --description "Kw presentation"

kw config manager: List your config file
----------------------------------------

.. code-block:: shell

  kw kernel-config-manager --list
  Name                       | Description
  MY_FIRST_CONFIG            | Kw presentation

Example:
--------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-kernel-config-add-entry.gif
       :width: 100%

kw config manager: Get your config file
----------------------------------------

You can retrieve a config file under kw management by using:

.. code-block:: shell

  kw kernel-config-manager --get MY_FIRST_CONFIG

kw config manager: fetch a config file
--------------------------------------

Kw provides a feature to extract the config file from a target machine:

.. code-block:: shell

  kw kernel-config-manager --fetch # or kw k --fetch

You can use the optimize option:

.. code-block:: shell

  kw kernel-config-manager --fetch --optimize


Kernel Compilation
==================

Overview
--------

kw can help you with basic tasks related to the kernel compilation, such as:

- Cross-compilation
- Kernel menu
- Build
- Separate build in a different folder

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

Example:
--------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-build-menu.gif
       :width: 100%


Compiling your kernel
---------------------

Now that you have your kernel config file, let's compile the kernel:

.. code-block:: shell

  kw build # or kw b

Example:
--------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-build.gif
       :width: 100%

Check kernel info
-----------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-build-info.gif
       :width: 100%


Deploy your custom kernel
=========================

Overview
--------

Kw can help you to install your new kernel via the deploy feature. Keep in mind
that deploy works based on three different targets:

1. Remote: Your test machine is connected via a network.
2. Local: It is your host machine; only use it if you really know what you are
   doing.

Supported OSes
--------------

.. container:: flex

  .. container:: half

    .. figure:: _static/supported_distros.png
       :width: 100%


Remote deploy
-------------

Make sure that you setup your `remote` configuration correctly:

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-set-remote.gif
       :width: 100%

Remote deploy: Test
-------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-ssh.gif
       :width: 100%

Remote deploy: Deploy!
----------------------

* If you have already compiled your kernel:

.. code-block:: shell

  kw deploy

* If you did not compile your kernel yet:

.. code-block:: shell

  kw bd

Example:
--------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-deploy.gif
       :width: 100%


Remote deploy: List
-------------------

You can list kernel installed via kw by using:

.. code-block:: shell

  kw deploy --list # Or kw d -l

You can list kernel installed in your system by using:

.. code-block:: shell

  kw deploy --uninstall "5.13.0-VM-TORVALDS"


Example: List
-------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-deploy-list.gif
       :width: 100%

Example: Remove
---------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-remove-kernel.gif
       :width: 100%

Example: Create kw package
--------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-create-package.gif
       :width: 100%

Others
======

Example: Turn GUI off/on
------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-drm-gui.gif
       :width: 100%

Example: Modes and Connectors
-----------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-drm-modes.gif
       :width: 60%

Example: Maintainers
--------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-maintainers.gif
       :width: 100%

Example: Codestyle
------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-codestyle.gif
       :width: 100%

Example: Explore
----------------

.. container:: flex

  .. container:: half

    .. figure:: _static/gifs/kw-explore.gif
       :width: 100%



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
  kw init --template=x86-64
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

Coming Soon
===========

* ChromeOS support
* Lore interface

Thanks
======

