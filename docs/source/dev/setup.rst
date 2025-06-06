Setting up a development environment
====================================

When you want to develop LiberTEM itself, or run the latest git version, the installation works a
bit differently as opposed to installing from PyPI.
As a first step, please follow the instructions for creating a Python virtual environment from
the :ref:`installation` section. Then, instead of installing from PyPI, follow the instructions below.

Prerequisites
~~~~~~~~~~~~~

In addition to a Python installation, there are a few system dependencies needed when contributing:

* `pandoc <https://pandoc.org/installing.html>`_ and `graphviz <https://graphviz.org/download/>`_
  are needed to build and test the documentation.
* Node.js is needed for rebuilding the LiberTEM GUI. On Linux, we recommend
  to `install via package manager
  <https://nodejs.org/en/download/package-manager/>`_, on Windows `the installer
  <https://nodejs.org/en/download/>`_ should be fine. Choose the current LTS
  version.

.. _`installing from a git clone`:

Installing from a git clone
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
    Distinguish between installing a released version and installing the latest
    development version. Both :ref:`installing from PyPI <installation>` and :ref:`installing from a git
    clone` use pip, but they do fundamentally different things. :code:`python -m pip
    install libertem` downloads the latest release from PyPI.

    Changing directory to a git clone and running :code:`python -m pip install -e .`
    installs from the local directory in editable mode. "Editable mode" means
    that the source directory is "linked" into the current Python environment
    rather than copied. That means changes in the source directory are
    immediately active in the Python environment.

    Installing from a git clone in editable mode is the correct setup for
    development work and using :ref:`the latest features in the development
    branch <continuous>`. Installing from PyPI is easier and preferred for
    production use and for new users.

If you want to follow the latest development, you should install LiberTEM from
a git clone. As a prerequisite, you need to have git installed on your system. On Linux,
we suggest using the git package that comes with your package manager. On Windows, you can use one
of the many available clients, like  `git for windows <https://gitforwindows.org/>`_, 
`GitHub Desktop <https://github.com/apps/desktop>`_, `TortoiseGit <https://tortoisegit.org/>`_,
or the git integration of your development environment.

.. code-block:: shell

    $ git clone https://github.com/LiberTEM/LiberTEM

Or, if you wish to contribute to LiberTEM, create a fork of the LiberTEM repository
by following these steps:

#. Log into your `GitHub <https://github.com/>`_ account.

#. Go to the `LiberTEM GitHub <https://github.com/liberteM/LiberTEM/>`_ home page.

#. Click on the *fork* button:

    ..  figure:: ../images/forking_button.png

#. Clone your fork of LiberTEM from GitHub to your computer

.. code-block:: shell

    $ git clone https://github.com/your-user-name/LiberTEM

More information about `forking a repository
<https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo>`_.
For a beginner-friendly introduction to git and GitHub, consider going through
the following resources:

* This `free course <https://www.udacity.com/course/version-control-with-git--ud123>`_
  covers the essentials of using Git.
* Practice `pull request <https://github.com/firstcontributions/first-contributions>`_
  in a safe sandbox environment.
* Detailed `documentation for contributing to astropy <https://docs.astropy.org/en/latest/index_dev.html>`_.

Activate the Python environment (conda or virtualenv) and change to the newly
created directory with the clone of the LiberTEM repository. Now you can start
the LiberTEM installation. Please note the dot at the end, which indicates the
current directory!

.. code-block:: shell

    (libertem) $ python -m pip install -e .

This should download the dependencies and install LiberTEM in the environment.
Please continue by reading the :ref:`usage documentation`.

Installing extra dependencies works just like when installing LiberTEM from PyPI:

.. code-block:: shell

    (libertem) $ python -m pip install -e .[torch,cupy]

Updating
~~~~~~~~

If you have installed from a git clone, you can easily update it to the current
status. Open a command line in the base directory of the LiberTEM clone and
update the source code with this command:

.. code-block:: shell

    $ git pull

The installation with :code:`python -m pip install -e` has installed LiberTEM in `"editable"
mode <https://pip.pypa.io/en/stable/cli/pip_install/#editable-installs>`_.
That means the changes pulled from git are active immediately. Only if the
requirements for installed third-party packages have changed, you should re-run
:code:`python -m pip install -e .` in order to install any missing packages.

Setting up tox on Windows
~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
  This doesn't seem to work on the newest tox major release 4.x anymore.
  We are still figuring out how to make it work. Help is appreciated!

We are using tox to run our tests.
On Windows with Anaconda, you have to create named aliases for the Python
interpreter before you can run :literal:`tox` so that tox finds the python
interpreter where it is expected. Assuming that you run LiberTEM with Python
3.9, place the following file as :literal:`python3.9.bat` in your LiberTEM conda
environment base folder, typically
:literal:`%LOCALAPPDATA%\\conda\\conda\\envs\\libertem\\`, where the
:literal:`python.exe` of that environment is located.

.. code-block:: bat

    @echo off
    REM @echo off is vital so that the file doesn't clutter the output
    REM execute python.exe with the same command line
    @python.exe %*

To execute tests with Python 3.12, you create a new environment with Python 3.12:

.. code-block:: shell

    > conda create -n libertem-3.12 python=3.12

Now you can create :literal:`python3.12.bat` in your normal LiberTEM environment
alongside :literal:`python3.9.bat` and make it execute the Python interpreter of
your new libertem-3.12 environment:

.. code-block:: bat

    @echo off
    REM @echo off is vital so that the file doesn't clutter the output
    REM execute python.exe in a different environment
    REM with the same command line
    @%LOCALAPPDATA%\conda\conda\envs\libertem-3.12\python.exe %*

See also:
https://tox.wiki/en/3.0.0/developers.html#id2
