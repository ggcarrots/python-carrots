=======================
Everything is an object
=======================

    
Every value that we have seen in Python, can be called **an object**. Each object can be assigned to
a variable (even functions) and/or passed to a function as an argument (yes, even other functions).
Similar objects share their functionality - number ``1`` has the same functionality as number ``2``, ``3`` and so on.
We saw earlier, when :func:`help`, acting on any number, printed for us dozens of additional lines of information about
:func:`int`.

Every object has a class
------------------------

We say that similar objects have the same **type**. Number ``1`` is of type ``int``, same as ``2`` and ``42``.
The type of an object is defined by its **class**.
To know what is the class of an object, what is its type, simply use the function :func:`type`:

.. code-block:: python

    >>> type(2)
    <class 'int'>
    >>> type(2.0)
    <class 'float'>
    >>> type("spam eggs")
    <class 'str'>
    >>> x = 1, 2
    >>> type(x)
    <class 'tuple'>
    >>> type([])
    <class 'list'>

We have talked about classes you can see here earlier: ``int``, ``float``, ``str``, ``tuple``.

When we use a ``int`` or a ``float`` in our program, we expect it to behave like a number. We rely on our
intuition.
However, Python has to know exactly what it means to be a number, e.g., what should happen when we
add two numbers or divide them. The class ``int`` provides all this information and
even more.

Using :func:`help` , check what functionality class ``str`` provides us. Here we give just a few interesting
features:

.. code-block:: python

    >>> help(str.lower)
    Help on method_descriptor:

    lower(...)
        S.lower() -> str
    
        Return a copy of the string S converted to lowercase.
    
    >>> help(str.upper)
    Help on method_descriptor:

    upper(...)
        S.upper() -> str
    
        Return a copy of S converted to uppercase.

    >>> help(str.ljust)
    Help on method_descriptor:

    ljust(...)
        S.ljust(width[, fillchar]) -> str

        Return S left-justified in a Unicode string of length width. Padding is
        done using the specified fill character (default is a space).

    >>> help(str.center)
    Help on method_descriptor:

    center(...)
        S.center(width[, fillchar]) -> str

        Return S centered in a string of length width. Padding is
        done using the specified fill character (default is a space)

All these are operations that each string can do. We can get to them by using dots and calling the
function:

.. code-block:: python

    >>> x = "Ala"
    >>> x.upper()
    'ALA'
    >>> x.lower()
    'ala'
    >>> x.center(9)
    '   Ala   '

Functions of classes are called **methods**. This is opposed to **free functions** that do not require 
objects to be evoked.

Creating an object of a given type, also called **an instance** of a class, is done by using its class name:

.. code-block:: python

    >>> int()
    0
    >>> str()
    ''
    >>> list()
    []
    >>> tuple()
    ()

An instance is a new, fresh value of the type described by the class.

In summary, we've looked at the classes :func:`int`, :func:`str`, :func:`tuple` and
:func:`list`. To find the type of an object, its class, we use the function
:func:`type`. To create an instance of a class, we call the class like we would call
a function, by using parentheses ``()``, e. g. ``int()``.

In the next chapters you will not only learn how to use classes and methods,
but also how to create your own.
