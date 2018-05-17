#############
Going Further
#############

This section shows some helpful tools that might aid you along your programming path. We briefly describe here how
to structure larger projects and work with multiple source files. We discuss python coding style guide (also known as PEP8).
and how pylint can help you to write and maintain readable and stylish code. At the end there is a list of resources you might find
helpful in your day-to-day python programming.


Managing larger projects
========================

Divide and conquer
--------------------

Up to this point, you might have put all of your source coed in one file. For small libraries and project this is fine, but when complexity
rises it is better to divide your code into smaller files, that is to create libraries or modules. It is not necessary, for example, to put
every class in a separate file, but having one file for classes that are logically connected is better for readability.
Going through a file that has thousands lines of code can be difficult.

As an example, let us consider a program for handling regular polygons. Every figure has its own, simplified class. You might want to
consider separating main functionality e. g. calculating perimeter, from definitions of those shapes [#fn1]_. That is, to put calculations of fields in one
file and definitions in another:

.. code-block:: python
    
    # File polygons.py
    class Circle:
        def __init__(self, radius):
            self.no_sides = 0
            self.radius = radius

    class Triangle:
        def __init__(self, side):
            self.no_sides = 3
            self.side = side

    class Square:
        def __init__(self, side):
            self.no_sides = 4
            self.side = side

.. code-block:: python

    # File shapefunctions.py
    PI = 3.141592 # or use math.PI
    def calc_perimeter(obj):
        if obj.no_sides > 0:
            perimeter = obj.no_sides * obj.side
        else:  
            perimeter = 2*PI*obj.radius
        return perimeter

Importing functionalities
-------------------------

To use definitions and perimeter function you must now import those functionalities. Code below asks user to specify which shape to
use and for the side length/radius, and calculates perimeter:

.. code-block:: python

    # Main file or command line
    import polygons
    import shapefunctions

    print("Choose a shape:")
    print("1. Circle")
    print("2. Triangle")
    print("3. Square")
    choice = int(input())
    print("Choose the side length")
    side = int(input())
    if choice == 1:
        shape = polygons.Circle(side)
    elif choice == 2:
        shape = polygons.Triangle(side)
    elif choice == 3:
        shape = polygons.Square(side)
    per = shapefunctions.perimeter(shape)
    print("The perimeter of your shape is %3.3f" % per)

The ``import polygons`` and ``import shapefunctions`` lines tell the program that we are going to use functionality defined in files ``polygons.py`` and ``shapefunctions.py``.
Note that these files must be in a place Python can find them, e.g. in the same directory you are running
python. Also, note that in the imports we are not using file type extensions, i.e. there is no ``.py`` in
``import`` statements.

There is also a possibility of using aliases for libraries:

.. code-block:: python
    
    # Main file or command line
    import polygons as plg
    triangle = plg.Triangle(10)

Here, whenever you need objects from ``polygons`` library, you can use ``plg`` alias instead of writing its full name.

Importing from
--------------

Sometimes you might want to explicitly state what you are importing. In that case use ``import from`` statement:

.. code-block:: python

    # Main file or command line
    from polygons import Circle, Triangle
    triangle = Triangle(10)
    circle   = Circle(20)

In this case, to create a shape you don't need to precede it's name with the name of the library. This approach, although more explicit,
and `Explicit is better than implicit <zen-of-python>`_,
has several major drawbacks. For one, if you need 100 functions from a large library it might be tedious to write every one of them. Secondly, you might
accidentally overwrite other functions. To ilustrate this, let's write a ``max`` function that sorts polygons by the number of sides:

.. code-block:: python

    # shapefunctions.py
    def max(obj1, obj2):
        if(obj1.no_sides > obj2.no_sides)
            return obj1
        else:
            return obj2

Importing this function explicitly, i.e. ``from shapefunctions import max``, will overwrite built in ``max`` function. That is, using ``max(1, 2)``
will cause an error. A better way to do this is, in this case, to use an alias:

.. code-block:: python

    # Main file or command line
    from shapefunctions import max as polygon_max
    from polygons import Triangle

    triangle1 = Triangle(10)
    triangle2 = Triangle(20)

    polygon_max(triangle1, triangle2) # returns triangle2
    max(1, 2) # Hey, it still works!

.. note::

    It is highly discouraged to name variables and functions using
    names of build-in functions (full list `here <https://docs.python.org/3/library/functions.html>`_).
    This might break your program and debugging those problems can be difficult. 

Get me ALL of them!
-------------------

You can also specify to import all of the functions and classes from a given library:

.. code-block:: python

    # Main function or command line
    from polygons import *
    triangle = Triangle(10)
    circle = Circle(29)
    square = Square(30)

This is usually highly discouraged, though, as it might overwrite existing functionality, just like in the previous case, but this time there is
no alias to help us.

You can manage which elements are imported by ``*`` using ``__all__`` variable:

.. code-block:: python

    # polygons.py
    # At the beginning of the file:
    __all__ = [ "Triangle", "Circle" ]
    # The rest of the library

.. code-block:: python

    # Main function or command line
    from polygons import *
    t = Triangle(10)
    c = Circle(10)
    # but no Square definition

Modules
--------

With even larger projects you might want to use directories to group files. For example, to extend shapes into a third dimension, you could create
a separate file with regular polyhedrons.

.. code-block:: python

    # polyhedrons.py
    class Sphere:
        def __init__(self, radius):
            self.no_faces = 0
            self.radius = radius

    class Tetrahedron:
        def __init__(self, side):
            self.no_faces = 4
            self.side = side
    
    class Cube:
        def __init__(self, side):
            self.no_faces = 6
            self.side = side

To keep all of shapes in one place, a good idea is to put all shape definitions into one folder - a module. This creates the following file structure:

.. code-block::

    + shapes
    |--- polygons.py
    |--- polyhedrons.py
    |--- __init__.py
    shapefunctions.py

The ``__init__.py`` file in the ``shapes`` folder is necessary to tell python that this is a module. :ref:`Using __init__.py <going-further-init>`_ section
has more information of usage of ``__init__.py`` file.

Importing from a module is quite similar to importing from regular files:

.. code-block:: python

    from shapes import polygons
    from shapes import polyhedrons as plh
    t = polygons.Triangle(10)
    c = plh.Cube(10)

To import explicit object, use this construction:

.. code-block:: python

    from shapes.polygons import Triangle
    t = Triangle(10)

Using ``__init__.py``
---------------------

.. _going-further-init: 

The ``__init__.py`` file can be used to simplify imports. For example, putting imports in this file allows to import from shapes explicitly:

.. code-block:: python

    # In __init__.py
    from shapes.polygons import Triangle

.. code-block:: python

    # Main file or command line
    from shapes import Triangle
    t = Triangle(10)

You can also specify the ``*`` behavior in the ``__init__.py`` by specifying ``__all__`` variable. This defines which
files or sub-modules to import:

.. code-block:: python

    # __init__.py
    __all__ = [ "polygons", "polyhedrons" ]

.. code-block:: python
    
    # Main file or command line
    from shapes import * 
    t = polygons.Triangle(10)
    # but no polyhedron definitions

Going even further!
-------------------

As the code base of your project grows, you will end up with a lot of modules and libraries. It is important to organize your work to increase
re-usability and readability. You can find more information on project handling in the `The Hitchhiker's Guide to Python <http://docs.python-guide.org/en/latest/writing/structure/>`_.

PEP8 and coding in style
========================

* `PEP8 can be found here <https://www.python.org/dev/peps/pep-0008/>`_.

A well formatted code improves readability. But what exactly does it mean for code to be well formatted? This definition might change from one developer
to another. Should you write ``x = max( 1, 2 )`` or ``x = max(1, 2)`` or ``x = max(1,2)``? 

Generally, there are two main coding guides for python developers. The first, most important, but also very broad, is the *Zen of Python*. You can see it
by typing ``import this`` in the interpreter:

.. _zen-of-python:

.. code-block:: python

    import this
    The Zen of Python, by Tim Peters

    Beautiful is better than ugly.
    Explicit is better than implicit.
    Simple is better than complex.
    Complex is better than complicated.
    Flat is better than nested.
    Sparse is better than dense.
    Readability counts.
    Special cases aren't special enough to break the rules.
    Although practicality beats purity.
    Errors should never pass silently.
    Unless explicitly silenced.
    In the face of ambiguity, refuse the temptation to guess.
    There should be one-- and preferably only one --obvious way to do it.
    Although that way may not be obvious at first unless you're Dutch.
    Now is better than never.
    Although never is often better than *right* now.
    If the implementation is hard to explain, it's a bad idea.
    If the implementation is easy to explain, it may be a good idea.
    Namespaces are one honking great idea -- let's do more of those!

We are going to leave the interpretation of this passage to the reader, although some of those rules might get clearer with gained programming experience.

A more detailed guidance can be found in PEP8. PEP stands for Python Enhancement Proposal, these are propositions published by core
developers that cover everything from release schedules, through peps about peps (like voting conventions - PEP10) to core language features
like Unicode integration (PEP100) or iterator implementations (PEP234) (two latter PEPs are examples of proposals already implemented). See
`pip index <https://www.python.org/dev/peps/>`_.

PEP8 gives a set of rules for code formatting. Below we show a few excerpts from this document, some of which you probably learned already during the workshops.
It is recommended, though, to read through the whole document (`pep8 <https://www.python.org/dev/peps/pep-0008/>`_).

.. note::

    Although important, style rules are just guidelines. They are not laws! Although is advised, especially for a beginner developer, to follow those
    rules, seasoned programmers tend to compromise between strict rule obedience and their work routine (consistency with surrounding code) or making the
    code less readable (*Beautiful is better than ugly* and *Readability counts*). Know when to break rules, or, in the words of PEP8 itself, *A Foolish Consistency is the Hobgoblin of Little Minds*.

* Use meaningful naming conventions. Don't use one or two letter variable names unless it's obvious or inline with other conventions
* Use 4 spaces per indentation level
* Be weary of long lines. PEP8 suggests the maximum of 72 characters, but in standard library it's 79. Break lines if you can.
* Use UTF-8 for file encoding
* Each import should be in a separate line, although this is fine: ``form shapes import Triangle, Circle, Square``
* Avoid extraneous spaces inside brackets or parentheses, i.e.

.. code-block:: python

    # YES
    spam = max(1, 2)
    spam = ham[10]
    spam = (0,)
    spam, ham = 1, 2
    def magic(real, imag=1):
        return complex(real=real, imag=imag)

    # NO
    spam = max( 1, 2 )
    spam = ham[ 10 ]
    spam = ( 0, )
    spam, ham = 1 , 2
    def magic(real, imag = 1):
        return complex(real = real, imag = imag)

* Comments are important, but you need to keep them up to date. Self documenting code is better (meaningful naming conventions, readable code, etc.)
* Modules should have all lowercase names (e.g. ``shapefunctions``), classes should use CamelCase convention (e.g. ``SmallShape``), functions should
  use snake_case (e.g. ``calc_perimeter``)


Using pylint
============

.. _going-further-pylint:

* `pylint webpage <https://www.pylint.org>`_
* `installation instructions <install-pylint>`_

Pylint is a tool that allows for an automatic check of coding style. It covers not only PEP8 guidelines, but also some issues that are common for
all programming languages. For example, it allows for checking the number of arguments function allows. Usually, a function with large
number of arguments is too complicated to be readable, and should be refactored. The full list of errors pylint can check
is found `here <http://pylint-messages.wikidot.com/all-codes>`_.

To lint code, use ``pylint`` command on a script/module you want to lint:

.. code-block:: sh

    (workshops) ~$ pylint shapes

    No config file found, using default configuration
    ************* Module shapes
    C:  1, 0: Missing module docstring (missing-docstring)
    ************* Module shapes.polygons
    C:  1, 0: Missing module docstring (missing-docstring)
    C:  1, 0: Missing class docstring (missing-docstring)
    R:  1, 0: Too few public methods (0/2) (too-few-public-methods)
    C:  6, 0: Missing class docstring (missing-docstring)
    R:  6, 0: Too few public methods (0/2) (too-few-public-methods)
    C: 11, 0: Missing class docstring (missing-docstring)
    R: 11, 0: Too few public methods (0/2) (too-few-public-methods)
    ************* Module shapes.polyhedrons
    C:  1, 0: Missing module docstring (missing-docstring)
    C:  1, 0: Missing class docstring (missing-docstring)
    R:  1, 0: Too few public methods (0/2) (too-few-public-methods)
    C:  6, 0: Missing class docstring (missing-docstring)
    R:  6, 0: Too few public methods (0/2) (too-few-public-methods)
    C: 11, 0: Missing class docstring (missing-docstring)
    R: 11, 0: Too few public methods (0/2) (too-few-public-methods)

    ------------------------------------------------------------------
    Your code has been rated at 4.23/10

This checks all files in the module and displays a report. Each file in the module gets its own report.
Letters at the beginning of each line correspond to a type of problem detected:

* [R]efactor for a "good practice" metric violation
* [C]onvention for coding standard violation
* [W]arning for stylistic problems, or minor programming issues
* [E]rror for important programming issues (i.e. most probably bug)
* [F]atal for errors which prevented further processing

In our case, "only" style problems were detected. Each reporting line consists also of the line and column number where the
problem that was spotted and a corresponing message. In the parenthesis is the name of the message, e.g. ``missing-docstring``.
If you are not sure what given message means, you can ask pylint to explain it. For example to show what
``too-few-public-methods`` mean use:

.. code-block:: sh

    (workshops) ~$ pylint --help-msg=too-few-public-methods
    No config file found, using default configuration
    :too-few-public-methods (R0903): *Too few public methods (%s/%s)*
    Used when class has too few public methods, so be sure it's really worth it.
    This message belongs to the design checker.

At the end of the report is the score. It tells you, in a more-less objective way, how good your code is when it comes to style.
In our case, the score of 4.23/10 is not a good one, but we are evaluating a simple example, not a real-life code. In your day-to-day
work, a good rule of thumb is to keep it above 7.

Configuring pylint
------------------

Pylint is fully configurable. You can suppress unwanted errors and format the report to your liking. You can do this using command
line options of ``pylint``, but a better way is to put those information in a configuration file attached to your project. By default,
``pylint`` will look for a file called ``.pylintrc``:

.. code-block:: sh

    # file .pylintrc
    [MESSAGES CONTROL]
    disable=too-few-public-methods,
            too-many-local-variables
    [REPORTS]        
    msg-template='{msg_id}:-:{line:3d}:-:{msg} found in {path}'
    
Here, we disable two checks and change how the messages are displayed. More on message formatting can be found in `pylint documentation <https://pylint.readthedocs.io/en/latest/user_guide/output.html>`_.
The result of running of pylint now looks like this:

.. code-block:: sh

    (workshops) ~$ pylint shapes
    Using config file .pylintrc
    ************* Module shapes
    C0111:-:  1:-:Missing module docstring found in shapes/__init__.py
    ************* Module shapes.polygons
    C0111:-:  1:-:Missing module docstring found in shapes/polygons.py
    C0111:-:  1:-:Missing class docstring found in shapes/polygons.py
    C0111:-:  6:-:Missing class docstring found in shapes/polygons.py
    C0111:-: 11:-:Missing class docstring found in shapes/polygons.py
    ************* Module shapes.polyhedrons
    C0111:-:  1:-:Missing module docstring found in shapes/polyhedrons.py
    C0111:-:  1:-:Missing class docstring found in shapes/polyhedrons.py
    C0111:-:  6:-:Missing class docstring found in shapes/polyhedrons.py
    C0111:-: 11:-:Missing class docstring found in shapes/polyhedrons.py

    ------------------------------------------------------------------
    Your code has been rated at 6.54/10 (previous run: 4.23/10, +2.31)

Note that linter does not check for ``too-few-public-methods``. As a result, the score of linting went up by 2.31 points. It is important to disable messages
carefully, and not just to increase your score.

It's dangerous to go alone. Take this!
======================================

Here are some resources to get you going on your further python development.

* `Python documentation <https://docs.python.org/3/>`_ - the most important source of Python knowledge.
* `Stack Overflow <https://stackoverflow.com/>`_ - there is a high chance that someone has asked about problem you are having, and got an answer.
* `The Hitchhikers Guide to Python <http://docs.python-guide.org/en/latest/>`_ - a living Python guide. Also, it has a fun name.
* `Dive Into Python 3 <http://www.diveintopython3.net/>`_ - A good introductory book to Python. And it's free!

.. _pep8: https://www.python.org/dev/peps/pep-0008/

.. rubric:: Footnotes

.. [#f1] This is just an example. In a day-to-day programming, writing such simple classes and not using inheritance is not a good idea.