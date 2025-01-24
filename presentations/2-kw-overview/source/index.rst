.. raw:: html

  <!-- Slide -->
  <section>
    <img width="800" height="327" src="_static/kw.png" style="background:none; border:none; box-shadow:none;">
    <br>
    <img width="120" height="41" src="_static/by.png" style="background:none; border:none; box-shadow:none;">
  </section>

==================
kworkflow Overview
==================

:Released: 2024-12-11

Preface
=======

Introduction
------------

Are you considering to write a new script for your workflow? Wait... you
already have a bunch of those scripts?

Introduction
------------

Just STOP for a moment and give a chance for kw...

.. container:: flex

  .. container:: half

    .. figure:: _static/stop.png
       :width: 50%

What is kw?
-----------

.. revealjs-fragments::

   * Everybody who works with Linux Kernel creates their scripts, which means
     we have a lot of duplicate effort. What if there is a centralized place to
     put all of these common tasks in a way that every kernel developer can
     benefit from?
   * Also, Linux kernel development has a steep learning curve. Would it be
     nice if we could have a way to reduce the learning curve?

What is kw?
-----------

It is a set of small software combined to reduce the environment and setup
overhead for developing Linux.

Part 1: Core features
=====================

Chapter 1: Install kw
=====================

Install
--------------

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

Chapter 2: kw init
==================

Configuration files
-------------------

* kw allows users to change its default behavior via configuration file
  (similar to how git works). There is two level of configuration files: global
  and local.

Global & Local config
---------------------

* All global configurations are available at `~/.config/kw/`.
* kw local configuration is stored in the `.kw` folder (similar to .git
  folder).
* Precedence: Local > Global

Create a local config folder (.kw)
----------------------------------

.. code-block:: shell

  cd linux # Your kernel tree with .config file

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/1-kw-init-template.png
       :width: 100%

Change configurations
---------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/2-kw-config-show-all.png
       :width: 50%

Example: Change build configuration
-----------------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/3-kw-config-show-build.png
       :width: 50%

Example: Change build configuration
-----------------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/4-kw-config-change-configuration.png
       :width: 100%

Example: Enable notifications
-----------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/4-kw-config-change-notification.png
       :width: 100%

Example: Enable notifications
-----------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/5-kw-config-change-notification-vs.png
       :width: 100%

Chapter 3: Target - Remote or Local
===================================

Setup kw for local deploy
-------------------------

* You will build and install your custom kernel on the same machine.

Setup kw for local deploy
-------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/remote/set-local.png
       :width: 50%

Setup kw for remote deploy
--------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/remote/set-remote.png
       :width: 50%

Setup Remote: Add new remote
----------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/remote/1-add-new-remote.png
       :width: 50%

Setup Remote: Set default remote and list
-----------------------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/remote/2-add-default-remote.png
       :width: 50%

Setup Remote: Remove remote
---------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/remote/3-remove-remote.png
       :width: 50%

Chapter 4: Managing .config files
=================================

Overview
--------

* The `.config` file holds all the information about what should be compiled or
  not during the build process.
* When you have a small config file that works in a target machine, the overall
  value of that config file skyrockets. 

Save .config file inside the kernel tree
----------------------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/kernel-config-manager/1-kernel-config-manager-save.png
       :width: 100%

List all of the saved config files
----------------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/kernel-config-manager/2-list-all.png
       :width: 100%

Get specific config file
------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/kernel-config-manager/3-get-specific-config.png
       :width: 100%

Get .config file from remote
----------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/kernel-config-manager/4-fetch-optmize.png
       :width: 100%

Chapter 5: Build!
=================

Just build it!
--------------

.. code-block:: shell

  kw build # or kw b

Get build info
--------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/build/1-build-info.png
       :width: 100%

Kernel Menu
-----------

Access the kernel configuration menu

.. code-block:: shell

  kw build --menu # or kw b -n

Build doc
---------

Generate the html doc

.. code-block:: shell

  kw build --doc # or kw b -d

Build with llvm
---------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/build/2-enable-llvm.png
       :width: 90%

Other build features
--------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/build/3-help.png
       :width: 100%


Deploy your custom kernel
=========================

Remote deploy: Recap
--------------------

Kw can help you to install your new kernel via the deploy feature. Keep in mind
that deploy works based on two different targets:

1. Remote: Your test machine.
2. Local: It is your host machine.

Deploy Limitations
------------------

* Setup ssh as a root (remote).
* Supported bootloader: Grub.

Distro support
--------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/deploy/families-min.png
       :width: 100%


Ok, ship it! Deploy!
--------------------

.. code-block:: shell

  kw deploy

Remote deploy: List
-------------------

You can list kernel installed via kw by using:

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/deploy/2-kw-deploy-list.png
       :width: 100%


Remote deploy: Remove
---------------------

You can uninstall kernels installed via kw deploy with:

.. code-block:: shell

  kw deploy --uninstall 6.8.0-ASDN-JUL-30+


Other deploy features
---------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/deploy/3-deploy-help.png
       :width: 100%

Part 3: kw env
==============

Create a new env
----------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/env/1-create-env.png
       :width: 100%

Use the new env
---------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/env/2-use-env-fail.png
       :width: 100%

Use the new env
---------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/env/3-use-env.png
       :width: 100%

Example of multiple envs
------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/env/4-envs-examples.png
       :width: 100%

Env destroy
-----------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/env/5-env-destroy.png
       :width: 100%


Part 4: Debug
=============

Debug with kw
=============

dmesg log
---------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/debug/1-dmesg-follow.png
       :width: 100%

List of ftrace and events
-------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/debug/2-debug-list.png
       :width: 100%

Enable ftrace and collect data
------------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/debug/3-ftrace-with-history.png
       :width: 100%

List specific event
-------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/debug/4-event-list.png
       :width: 100%

Follow specific event
---------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/debug/5-events.png
       :width: 100%

Other options
-------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/debug/6-help.png
       :width: 100%

Part 5: Development tools
=========================

send-patch: List configurations
-------------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/dev-tools/1-email-config.png
       :width: 100%

send-patch: setup from a template
---------------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/dev-tools/2-setup-from-template.png
       :width: 100%

send-patch: send patches
------------------------

Simulate before send:

.. code-block:: shell

  kw send-patch --send --simulate --to=some@email.com

Send patches:

.. code-block:: shell

  kw send-patch  -s <SHA1>..<SHA2>
  kw send-patch  -s -3

send-patch: send patches
------------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/dev-tools/3-send_patch_config.png
       :width: 100%

Maintainers
-----------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/dev-tools/4-maintainers.png
       :width: 100%

Codestyle
---------

.. code-block:: shell

  kw c /tmp/0001-drm-rockchip-vop2-Fix-the-mixer-alpha-setup-for-laye.patch
  kw codestyle drivers/gpu/drm/amd/display/amdgpu_dm/
  kw c drivers/gpu/drm/amd/amdgpu/sdma_v7_0.c 

Explore all files
-----------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/dev-tools/5-explore-generic.png
       :width: 100%

Explore with context
--------------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/dev-tools/6-explore-with-context.png
       :width: 100%

Explore headers
---------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/dev-tools/7-explore-headers-only.png
       :width: 100%

Explore git log
---------------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/dev-tools/8-explore-git-log.png
       :width: 100%

Conclusion
==========

Getting help: CLI
-----------------

Short help:

.. code-block:: shell

  kw <feature_name> -h # e.g., kw b -h

Full man page:

.. code-block:: shell

  kw <feature_name> --help # e.g., kw b --help


Getting help: Online doc
------------------------

Visit: https://kworkflow.org

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/conclusion/kw-site.png
       :width: 100%

Contribute
----------

.. container:: flex

  .. container:: half

    .. figure:: _static/steps-images/conclusion/github.png
       :width: 100%

Contribute
----------

If you want to contribute to kw, take a look at:

* https://kworkflow.org/content/howtocontribute.html
* https://kworkflow.org/content/developmentworkflow.html
* https://kworkflow.org/content/codingstyle.html

Thanks
------

