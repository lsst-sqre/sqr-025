..
  Technote content.

  See https://developer.lsst.io/docs/rst_styleguide.html
  for a guide to reStructuredText writing.

  Do not put the title, authors or other metadata in this document;
  those are automatically added.

  Use the following syntax for sections:

  Sections
  ========

  and

  Subsections
  -----------

  and

  Subsubsections
  ^^^^^^^^^^^^^^

  To add images, add the image file (png, svg or jpeg preferred) to the
  _static/ directory. The reST syntax for adding the image is

  .. figure:: /_static/filename.ext
     :name: fig-label

     Caption text.

   Run: ``make html`` and ``open _build/html/index.html`` to preview your work.
   See the README at https://github.com/lsst-sqre/lsst-technote-bootstrap or
   this repo's README for more info.

   Feel free to delete this instructional comment.

:tocdepth: 1

.. Please do not modify tocdepth; will be fixed when a new Sphinx theme is shipped.

.. sectnum::

.. TODO: Delete the note below before merging new content to the master branch.

.. note::

   **This technote is not yet published.**

   This is a short technote to describe the various features of the notebook aspect (hereafter JupyterLab).

.. Add content here.
Introduction
============

This note is intended to help people just coming to the JupyterLab environment for the first time.
I will cover data access, user environments, authentication, and brief discussion on getting started in notebooks.

For those too impatient to read to the end, the JupyterLab environment can be accessed `here 1<https://lsst-lspdev.ncsa.illinois.edu>`_.

Authentication
==============

Currently access is restricted to those IPs on the allowed list.
At the moment, this is only addresses in the Tucson/AURA network.
However, others may gain access via the NCSA hosted VPN. Follow instructions in the "Loging into the NCSA VPN" section of `this <https://confluence.lsstcorp.org/display/DM/PDAC+networking+and+user+accounts+for+developers>1`_ page.

Whether logging in via direct connection or through the VPN, you will need to provide your NCSA Kerberose credentials (the username/password you use to log on to `lsst-dev`).

Quick Start
===========

After authentication, you will see a page that allows you to choose the type of container to spawn.
You can choose one of the last three dailies, two of the last weeklies, or the most recent release.
You can also choose any tagged version, but note these won't, in general, be pre-staged to the node, so will take more time to spawn.
You can also choose the size of the backing virtual machine.
Please be judicious and choose the smallest container that will serve your needs.

Once logged in, you will see a file browser on the left and a launcher in the main pane.
Select "LSST_Stack (Python 3)" to get a blank notebook with the LSST stack set up.
You can always get to the launcher by navigating the menu File --> New Launcher.

In the bottom row, there is a Terminal tool.
This will open up a shell session in your LupyterLab environment.
It should behave like any normal `bash` shell.

In the file browser, there is a directory called `notebook-demo`.
Double clicking this will open up the directory to reveal several demo notebooks.
These should all be runnable out of the box.

File Systems
============

All the shared filesystems you would expect are exposed with the same permissions in the JupyterLab environment.
These include:

- `/datasets` -- This is for shared, curated data.  This filesystem is read only.
- `/project` -- This is for shared, uncurate, persisted data. There is no disaster recovery, but there is also no enforced quota or purge policy.
- `/scratch` -- This is for completely transient data. There is no disaster recovery or quota, but there is a purge cycle, so data in this filesystem should not be expected to persist.
- `/software` -- This is where the shared stack available on other LDF resouces resides. Users should not place files in this filesystem.

The `home` environment on other LDF resources is not exposed here for security reasons.  However, the JupyterLab `home` is available outside of the JupyterLab environment at `/lsst/jhome/$USER`.

User Environment
================

Because the environment is just a Linux shell, you can do all the same configuration you do on any other Linux system.

We also provide a mechanism for cusomizing the notebook environment.
The process is to add shell commands in a special file called `$HOME/notebooks/.user_setups`.
This file is sourced immediately after calling `setup lsst_distrib`.
This is where you can override the installed stack versions.

Because you have complete control of your user environment, this means you can also install any arbitrary package via the `pip install --user package_name` mechanism, for example.
But, of course, with great responsibility...
The container does provide versions of some libraries: e.g. bokeh, holoviews, etc.
Care should be taken since it is possible to shadow versions which can cause issues.
If you are having problems, you could try moving `$HOME/.local` to a temporary name to see if it is a version collision problem.
Also, if you are installing modules to use with the stack, make sure you have set up the stack in the shell
before installing libraries `source /opt/lsst/software/stack/loadLSST.bash`.

.. Do not include the document title (it's automatically added from metadata.yaml).

.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :encoding: latex+latin
..    :style: lsst_aa
