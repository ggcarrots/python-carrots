############
Installation
############

Before we start, we need to prepare our environment. Below are some instructions on installing the latest version of Python. Here we install version 3.6.5.

Windows
=======

You can download Python for Windows directly from `python.org`_. Look for version 3 and above.
After downloading the file  ``*.msi``, open it and follow the instructions.
It is important to remember the path of installation, i.e. the directory, as we will need this information during the :ref:`installation of tools <tools>`.

.. note::
    Remember to check "Add Python 3.6 to PATH" when running the installer . This way you will be able to run Python form
    console by just writing ``python``.


Linux (Ubuntu, Fedora, etc.) or Mac
===================================

In order to check our version of Python, enter the following in the command line:

.. code-block:: sh

    $ python --version
    Python 3.6.5

If the ``python`` command is not available or the wrong version appears try using ``python3`` command:

Ubuntu
------

In the command line enter::

    sudo apt-get install python3.6

Fedora
------

In the command line enter::

    sudo yum install python3.6

OS X
----

In the command line enter::

    brew install python3

Other
-----

Use the system of packages adequate for your distribution. If there is no adequate system
or you cannot find python, you can install it using the sources on the `python.org`_. website.
A compiler and readline library will be required.



.. _tools:

Tools
=====

Windows command line
--------------------

We will do most of our work on the command line. To activate the command line in Windows,
press ``Win+R``. In the open window, type ``cmd`` and click ``OK``.
A new window will appear with white text on a black background:

.. code-block:: bat

    Microsoft Windows [Version 6.1.7601]
    Copyright (c) 2009 Microsoft Corporation. All rights reserved.


    C:\Users\Name>

Text may be different depending on the version of Windows you use.

``C:\Users\Name>``  is a prompt. It informs us of the directory (or folder) in which we currently are and waits for a command.
Later during the workshop ``C:\Users\Name>`` we will refer to it with ``~$``, independently of your
operating system (Windows, Linux, MacOS).

Using the command line, you can move around the contents of the disc (in the same way as in
``My Computer``).  You can do that by entering commands and pressing ``Enter``.
Use the following commands:

``dir``
    Displays the contents of the current directory. For example, if the ``prompt``
    shows  ``C:\Users\Name``, the ``dir`` command displays the contents of our home directory.

``cd directory``
    Changes the current directory. For example, if you are in ``C:\Users\Name``,
    you can access the directory with your documents by entering ``cd Documents``. If you execute the
    ``dir`` command, you will see something familiar.
    The command  ``cd..`` will move you one level up in the directory tree, that is,
    to the directory that contains your current directory.

``mkdir directory``
    Creates a new directory.


Virtual environment
-------------------

A virtual environment is a tool that allows us to
isolate our work from other parts of the system. This ensures that any
new and experimental library you use will be confined to this sandbox and won't contaminate
your system.

To create a venv you need to choose a place where it will be created. For example, you can choose your home
directory. If you select a different place, just remember where venv is created as we will use it often.

In Windows, the path to your home directory, for the user  ``Ala``, will look like this:
``C:\Users\Ala\``. In Linux, writing ``cd`` in the command line will get you to your $HOME directory.

In Windows, to create virtual environment, write:

.. code-block:: bat

    C:\Users\Ala> python -m venv workshops

This assumes that during installation python was added to your:w
 PATAH.

For Linux or Mac user:

.. code-block:: sh

    ~$ python3.6 -m venv workshops

This creates a directory ``workshops``. This is your virtual environment. Right now it's still incative.

To activate it on Windows write:

.. code-block:: bat

    C:\Users\Ala> workshops\Scripts\activate

For Linux or Mac users:

.. code-block:: sh

    ~$ source workshops/bin/activate

The ``python`` command will run the correct version of Python, so we will not have to enter the full
path at the beginning nor the version at the end. Note ``(workshop)`` at the beginning of your new prompt.

.. code-block:: bat

    (workshops) C:\Users\Ala>where python
    C:\Users\Ala\workshops\Scripts\python.exe
    ...

    (workshops) C:\Users\Ala>where pip
    C:\Users\Ala\workshops\Scripts\pip.exe
    ...

    (workshops) C:\Users\Ala>python --version
    3.6.5

.. code-block:: sh

    # Linux or Mac
    (workshops) ~$ which python
    /home/Ala/workshops/bin/python
    (workshops) ~$ which pip
    /home/Ala/workshops/bin/pip
    ...

    (workshops) ~$ python --version
    3.6.0



.. note::
    You may already have the ``pip`` command available on your system. Always check which pip you are using with command: ``pip --version``.
    You can do this by running one of these commands:

    .. code-block:: sh

        ~$ pip --version
        ~$ pip3 --version
        ~$ pip3.6 --version

    It will give you the version of pip and a path to your virtual environment directory.

    If you can't find your ``pip`` or there is a problem after typing ``which pip`` (``where pip`` on windows), you may need to reinstall pip:

    .. code-block:: sh

        ~$ python -m pip uninstall pip
        ~$ python -m ensurepip


Summary
-------

New virtual environment installation:

.. code-block:: bat

    :: Windows
    C:\Users\Ala> C:\Python36\python -m venv workshops

.. code-block:: sh

    # Linux or Mac
    ~$ python3.6 -m venv workshops

Virtual environment activation:

.. code-block:: bat

    :: Windows
    C:\Users\Ala> workshops\Scripts\activate

.. code-block:: sh

    # Linux or Mac
    ~$ source workshops/bin/activate

Just make sure that you use the proper Python version:

.. code-block:: sh

    (workshops) ~$ python --version
    3.6.0

pip
---

Over the years, people have been creating new tools using python. Usually they are distributed in a form of packages. In most cases, those tools can be installed
using python's installation manager ``pip``. By default it downloads packages from PyPI ( `pypi.org`_ ), python package index, a free software depository
used by open source python developers to distribute their work. After downloading the package, ``pip`` will install it, all done automatically.


Below, we use ``pip`` to install some helpful tools, ``IPython`` and ``pylint``. Besides installing, ``pip`` allows for searching of specific packages and
updating packages if newer version is available in PyPI.

To look for a specific package use ``pip`` with ``search`` option:

.. code-block:: sh

    (workshops) ~$ pip search ipython

This prints a list of packages containing ``ipython`` in their names with a short description and a version available. If a package is already
installed, ``pip search`` will display ``INSTALLED`` and ``LATEST`` versions so you know whether library is up to date:

.. code-block:: sh

    (workshop) ~$ pip search ipython
    ipython (6.4.0)                              - IPython: Productive Interactive
                                                    Computing
    INSTALLED: 4.1.2
    LATEST:    6.4.0

To update a package, use ``pip install --upgrade``.

To list all installed packages us ``pip list``.

To see all options and flags that can be used with ``pip`` write ``pip --help`` and ``pip <option> --help``, where option is i.e. ``install``.

IPython
-------

IPython is a better shell for python. It enables code completion and enhances editing capabilities. We strongly suggest to use
it instead of the `stock` version (i.e. ``python`` command).
To install ``IPython`` in your virtual environment, write:
from the console.

``IPython`` installation:

.. code-block:: sh

    (workshops) ~$ pip install ipython

Pylint
------

Pylint is a tool that helps keeping your code clean. It will check your source files for errors, but alse for common style problems
like non-descriptive variable names, lack of documentation. In the result, it will display a grade of your code, from -10 to 10, higher
means better code. A good rule of thumb, especially for beginners, is to keep your code above 7.

To install it, type:

.. code-block:: sh

    (workshops) ~$ pip isntall pylint

More on ``pylint`` can be found in :ref:`Going further <going-further-pylint>` section.


.. _python.org: https://www.python.org/downloads/release/python-365/
.. _pypi.org: https://www.pypi.org
