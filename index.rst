Introduction
============

This note is intended to help people just coming to the JupyterLab environment for the first time.
I will cover data access, user environments, authentication, and brief discussion on getting started in notebooks.

For those too impatient to read to the end, the JupyterLab environment can be accessed at https://lsst-lspdev.ncsa.illinois.edu/nb.

Authentication
==============

Currently access is restricted to those IPs on the allowed list.
At the moment, this is only addresses in the Tucson/AURA network.
However, others may gain access via the NCSA hosted VPN. Follow instructions in the "Logging into the NCSA VPN" section of `the PDAC wiki <https://confluence.lsstcorp.org/display/DM/PDAC+networking+and+user+accounts+for+developers>`_.

Whether logging in via direct connection or through the VPN, you will need to provide your NCSA Kerberos credentials (the username/password you use to log on to lsst-dev).

Quick Start
===========

After authentication, you will see a page that allows you to choose the type of container to spawn.
You can choose one of the last three dailies, two of the last weeklies, or the most recent release.
You can also choose any tagged version, but note these won't, in general, be pre-staged to the node, so will take more time to spawn.
You can also choose the size of the backing virtual machine.
Please be judicious and choose the smallest container that will serve your needs.

Once logged in, you will see a file browser on the left and a launcher in the main pane.
Select "LSST_Stack (Python 3)" to get a blank notebook with the LSST stack set up.
You can always get to the launcher by navigating the menu File → New Launcher.

In the bottom row, there is a Terminal tool.
This will open up a shell session in your JupyterLab environment.
It should behave like any normal ``bash`` shell.

In the file browser, there is a directory called :file:`notebook-demo`.
Double clicking this will open up the directory to reveal several demo notebooks.
These should all be runnable out of the box.

File Systems
============

All the shared filesystems you would expect are exposed with the same permissions in the JupyterLab environment.
These include:

- :file:`/datasets` -- This is for shared, curated data.  This filesystem is read only.
- :file:`/project` -- This is for shared, uncurated, persistent data. There is no disaster recovery, but there is also no enforced quota or purge policy.
- :file:`/scratch` -- This is for completely transient data. There is no disaster recovery or quota, but there is a purge cycle, so data in this filesystem should not be expected to persist.
- :file:`/software` -- This is where the shared stack available on other LDF resouces resides. Users should not place files in this filesystem.

The ``home`` environment on other LDF resources is not exposed here for security reasons.  However, the JupyterLab ``home`` is available outside of the JupyterLab environment at :file:`/home/$USER/jhome` (a symbolic link to :file:`/lsst/jhome/$USER`).

User Environment
================

Because the environment is just a Linux shell, you can do all the same configuration you do on any other Linux system.

We also provide a mechanism for customizing the notebook environment.
The process is to add shell commands in a special file called :file:`$HOME/notebooks/.user_setups`.
This file is sourced immediately after calling ``setup lsst_distrib``.
This is where you can override the installed stack versions.

Because you have complete control of your user environment, this means you can also install any arbitrary package via the ``pip install --user package_name`` mechanism, for example.
But, of course, with great power...
The container does provide versions of some libraries: e.g. bokeh, holoviews, etc.
Care should be taken since it is possible to shadow versions which can cause issues.
If you are having problems, you could try moving :file:`$HOME/.local` to a temporary name to see if it is a version collision problem.
Also, if you are installing modules to use with the stack, make sure you have set up the stack in the shell
before installing libraries ``source /opt/lsst/software/stack/loadLSST.bash``.

.. Do not include the document title (it's automatically added from metadata.yaml).

.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :encoding: latex+latin
..    :style: lsst_aa
