======================
Introduction to Python
======================

Let’s start with running the Python interpreter we installed in the previous chapter. Please run:

.. code-block:: sh

    (workshops) ~$ python
    Python 3.4.0 (...)
    Type "copyright", "credits" or "license" for more information.

    >>>

Earlier we were working in the operating system's command line and we could give commands.
The prompt was ``~$``. After running the ``python`` command, the prompt changed to
``>>>``.  For us, that means that for now we may only use commands from the Python language. Recent commands (
such as: ``cd``, ``mkdir``) will not work. This is the moment when we start to learn a new language!

We don't type the prompt ``>>>`` (the same as with ``~$``) - the interpreter will do that for us.

Now we can count something, for example: ``2 + 2``:

    >>> 2 + 2
    4

Python is excellent as a calculator:

    >>> 6 * 7
    42
    >>> 1252 - 38 * 6
    1024
    >>> (3 - 5) * 7
    -14
    >>> 21 / 7
    3.0
    >>> 3**2
    9
    >>> 5 / 2
    2.5

Please pay special attention when writing decimals: use a period, not a comma. Commas will be used to
define some data structures like lists or tuples (but more on that later).


Introduce yourself
==================

Strings
-------

Numbers, however, are not enough to communicate effectively. So we need to learn how to use ``strings``.
Here are some examples:

    >>> "Hello World"
    'Hello World'
    >>> 'Foo Bar'
    'Foo Bar'
    >>> "Rock 'n' Roll"
    "Rock 'n' Roll"
    >>> 'My name is "James"'
    'My name is "James"'

You can also add strings as follows:

    >>> 'My name is ' + '"James"'
    'My name is "James"'

or they can be multiplied by whole numbers:

    >>> 'Hastur' * 3
    'HasturHasturHastur'

The string must always begin and end with the same character. This may be a single quote (``'``) or
double quotes (``"``). It has no effect on the value of the string, i.e, typing ``"Batman"`` creates
a string ``Batman`` - quotes are not a part of it, they only indicate that it is a string (
unfortunately, Python is not so clever as to guess it by itself).


Printing the strings
--------------------

How do we present values in a readable form? We can do it by using the :func:`print` command:

    >>> print("Hello World")
    Hello World

In a similar way, we can write several strings in a single line without adding them to each other.
They will be separated by spaces:

    >>> print("Hi, my name is", "Łukasz")
    Hi, my name is Łukasz

:func:`print` command has many more applications as it can write almost everything.
For now, the only other kind of values we know are numbers:

    >>> print(1)
    1
    >>> print(1, 2, 3)
    1 2 3
    >>> print("2 + 2 =", 2 + 2)
    2 + 2 = 4

We are done with the interactive console for now. To exit it enter `quit()`::

    >>> quit()

Or hold ``Ctrl+D`` (for Linux or OSX) or ``Ctrl+Z`` (for Windows).

Source files
============

So far, our code was executed in an interactive mode where we give commands
separately and immediately get an answer. It’s a great way to experiment and learn
new language elements, which is why we will get back to it eventually.
However now we will try to write our own, separate program.

Our first program will look like this::

    print("Hi, my name is Bond")

In order to write and save code in a file we need to use a text editor.
Find a text editor that works on your OS (see `list of text editors on Wikipedia <http://en.wikipedia.org/wiki/List_of_text_editors>`_ for examples).
Type the above Python code and save it in a new file called ``visitingcard.py``.
Then run your first Python program, from the command line, using the following.

.. code-block:: sh

    (workshops) ~$ python visitingcard.py
    Hi, my name is Bond
    (workshops) ~$

A single program can contain more than one command. Each should be on a separate line. For example::

    print("Hi,")
    print()

    print("my name is Bond.")

    print()
    print("James Bond.")

We can insert blank lines wherever we want in ``visitingcard.py`` file to increase its readability.
Here, we split the message header from the content and the end.


BMI calculator
==============

Now we are going to write a simple program to calculate `BMI` (`Body Mass Index`_).
The formula for its calculation is as follows::

    BMI = (mass (kg)) / (height (m)) squared

We already know how to divide, exponentiate, and print out numbers. Let's create a new file called ``bmi.py``
and write a program that calculates our BMI:

.. code:: python

    print("Your BMI is:", 65.5 / (1.75 ** 2))

Run our new program with::

    $ python bmi.py

We get the following result:

.. testoutput::

    Your BMI is: 21.387755102040817

As you can see, our program still needs some improvements:

1. If someone else would like to use this program, we must change the contents of the ``bmi.py`` file.

2. To someone who does has not memorized the BMI table, the value 21.387755102 won’t mean
   anything.

3. Printing so many decimal places is unnecessary. BMI is measured with an accuracy of two decimal
   places.

Programming is the art of solving problems, so… let's get to work! It will give us an
opportunity to learn about some new features of Python.

.. _`Body Mass Index`: http://pl.wikipedia.org/wiki/Body_Mass_Index


Variables
=========

Let's try to solve the first problem. We would like to make our program more
readable, i.e. so that for the person reading the results, it would be obvious which value is the
weight and which is the height.

That's why we give names to these values:

.. testcode::

    weight = 65.5
    height = 1.75

    bmi = weight / height**2
    print("Your BMI is:", bmi)


That way we created **variables** ``weight`` and ``height``.
The result has not changed:

.. testoutput::

    Your BMI is: 21.387755102040817


In order to better understand how variables work, let’s go back to the interactive mode
for a while and give names to some values;
that is, store some values on variables:

    >>> x = 42
    >>> PI = 3.1415
    >>> name = "Amelia"
    >>> print("Things:", x, PI, name)
    Things: 42 3.1415 Amelia

We can change the value assigned to the variable. The new value does not need to be of the same type as the old one:

    >>> x = 13
    >>> print(x)
    13
    >>> x = "Scarab"
    >>> print(x)
    Scarab

The variables are independent of each other. We have just assigned a new value
to ``x``, but the value assigned to ``y`` remains unchanged:

    >>> print(y)
    42

As we have seen in our program, we can also give names to the results of calculations and use variables in
calculations:

    >>> w = 65.5
    >>> h = 175.0 / 100.0
    >>> bmi = w / h**2
    >>> print(w, h, bmi)
    65.5 1.75 21.387755102040817

Once a value is calculated, it is not modified:

    >>> w = 64
    >>> print(w, h, bmi)
    64 1.75 21.387755102040817

Until we give the Python the command to repeat the calculation again:

    >>> bmi = w / h**2
    >>> print(w, h, bmi)
    64 1.75 20.897959183673468

Now is time to add some comments to our program so that the user (and us too!)
remembers that the weight has to be given in kilograms.

Comments allow us to put arbitrary text in our python program. Comments will be ignored by the interpreter.

A comment in Python is everything after the character ``#`` until the end of the line:

.. code:: python

    # Weight in kilograms
    weight = 65.5

    # Height in meters
    height = 1.75

    bmi = weight / height**2 # Count BMI
    print("Your BMI is:", bmi)

Calling a function
==================

Our program looks good, but if a user wants to calculate his/her BMI, they still have to change the
content of the program. It would be more convenient to enter the required values in the console after
opening the program and get the BMI result.

To write such a program, we need to learn how to use ``functions``. The first function we are
going to learn is :func:`help`:

    >>> help
    Type help() for interactive help, or help(object) for help about object.

The :func:`help` function is very friendly and tells us how we should use it. It can also tell you how to
use other functions:

    >>> help(input)
    Help on function input in module builtins:
    <BLANKLINE>
    input(...)
        input([prompt]) -> string
    <BLANKLINE>
        Read a string from standard input.  The trailing newline is stripped.
        If the user hits EOF (Unix: Ctl-D, Windows: Ctl-Z+Return), raise EOFError.
        On Unix, GNU readline is used if enabled.  The prompt string, if given,
        is printed without a trailing newline before reading.
    <BLANKLINE>

We will use :func:`input` to load data from the user. As we read in the description, :func:`input` reads the
string:

.. code:: python

    >>> input()
    Ala has a cat
    'Ala has a cat'


Now you will learn what "calling a function" means. You can call a function using ``()``, which is
an information for the interpreter to call a function. Calling a function will run a function. If you
forget  to type ``()`` after the function name, the function is not called. In this situation,
you will not get any informations about errors, because the command you typed is still correct.

Generally, function calls **return** some values. The :func:`input` function returns a string, that’s why
we can use it the same way that we used strings before.

For example, we can use ``input()`` to save a given string as a name:

.. testsetup::

    input.queue.append("Joanna")

.. doctest::

    >>> print("Hello, stranger. What's your name?")
    >>> name = input()
    Joanna
    >>> name
    'Joanna'
    >>> print("Very nice to meet you,", name)
    Very nice to meet you, Joanna

We can simplify it a little bit,
by telling :func:`input` function what should it ask:

.. code:: python

    >>> name = input("Hello, stranger. What's your name?")
    Joanna
    >>> name
    'Joanna'
    >>> print("Very nice to meet you,", name)
    Very nice to meet you, Joanna


Is that enough to improve our program?

.. testsetup::

    input.queue.append("60.5")

.. doctest::

    >>> w = input()
    60.5
    >>> w
    '60.5'
    >>> print(w + 3)
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: Can't convert 'int' object to str implicitly

As you can see, Python doesn’t know what result we expect. Both strings (``str``), and
numbers (``int``) can't be added together. Python does not know if we are referring to the number ``60.5``
or to the string ``"60.5"``. Only we know that, so we have to include this information in the program.


Let’s introduce two more functions:

    >>> help(int)  # doctest: +NORMALIZE_WHITESPACE
    Help on class int in module builtins:
    <BLANKLINE>
    class int(object)
     |  int(x=0) -> integer
     |  int(x, base=10) -> integer
     |
     |  Convert a number or string to an integer, or return 0 if no arguments
     |  are given.  If x is a number, return x.__int__().  For floating point
     |  numbers, this truncates towards zero.
     |
     |  ...

and

    >>> help(float)  # doctest: +NORMALIZE_WHITESPACE
    Help on class float in module builtins:
    <BLANKLINE>
    class float(object)
     |  float(x) -> floating point number
     |
     |  Convert a string or number to a floating point number, if possible.
     |
     |  ...

The :func:`help` function does not hesitate to inform us that, in fact,
:func:`int` and :func:`float` are not functions but classes (we will talk about those later), hence the information about all the other things that you can use them for. For now, we
are only interested in the basic functionality of converting strings into numbers of a
determined type.


Let’s test :func:`int` and :func:`float`:

    >>> int("0")
    0
    >>> int(" 63 ")
    63
    >>> int("60.5")
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ValueError: invalid literal for int() with base 10: '60.5'
    >>> float("0")
    0.0
    >>> float(" 63 ")
    63.0
    >>> float("60.5")
    60.5


Before we use the newly learnt functions in our program, let’s make a plan of how it should work:

1. Ask the user to enter the height.
2. Load the string from the user and save it under the name ``height``.
3. Change the string with the number to a number with a fraction.
4. Ask the user to enter the weight.
5. Load the string from the user and save it under the name of ``weight``.
6. Change the string with the number to a number with a fraction.
7. Using the remembered values calculate BMI and save as ``bmi``.
8. Print the calculated BMI.


It should not surprise us that these eight points can be directly translated into eight lines of our
program (not counting spaces):

.. testsetup::

    input.queue.append("1.75")
    input.queue.append("65.5")

.. testcode::

    print("Enter the height in meters:")
    height = input()
    height = float(height)

    print("Enter the weight in kilograms:")
    weight = input()
    weight = float(weight)

    bmi = weight / height**2 # calculate BMI
    print("Your BMI is:", bmi)

You can save this program to ``bmi.py`` and run ``python bmi.py``. The result should look like this:

.. testoutput::

    Enter the height in meters:
    1.75
    Enter the weight in kilograms:
    65.5
    Your BMI is: 21.387755102040817

In conclusion, to call a function we need to know its name (until now we learnt a bunch of functions: :func:`print`, :func:`help`, :func:`input`, :func:`int`, :func:`float` and :func:`quit`),
and what data it expects from us.
The data we provide in the brackets is called the list of **arguments**.

Entering just the name does not activate the function. It will tell us only that it is a function:

    >>> input  # doctest: +SKIP
    <built-in function input>

.. We skip the test above because we can't mock input.__repr__ :(

In order to call the function, we must put parentheses after its name:

    >>> input()  # doctest: +SKIP

Now Python will execute the function.

All arguments are given in parentheses. To specify more than one, separate them with a comma:

    >>> print("a", "b", "c", sep = ", ")
    a, b, c


Checking conditions
===================

Let’s go to our next problem. We want our program to print the appropriate
classification for the calculated BMI by using the table below:


=====================   ==================
   BMI                    Classification
=====================   ==================
 < 18,5                    underweight
 18,5 – 24,99            normal weight
 ≥ 25,0                     overweight
=====================   ==================

We need to use the **conditional statement** :keyword:`if`. It will execute the rest of the program
depending on a given condition:


.. testsetup::

    input.queue.append("1.75")
    input.queue.append("65.5")

.. testcode::

    print("Enter your height in meters:")
    height = input()
    height = float(height)

    print("Enter your weight in kilograms:")
    weight = input()
    weight = float(weight)

    bmi = weight / height**2  # Calculate BMI

    if bmi < 18.5:
        print("underweight")
    elif bmi < 25.0:
        print("normal weight")
    else:
        print("overweight")

.. testoutput::

    Enter your height in meters:
    1.75
    Enter your weight in kilograms:
    65.5
    normal weight

Comparisons:  true or false?
----------------------------

Let us now talk about comparisons. Let's look at how they behave in a short math lesson:

    >>> 2 > 1
    True
    >>> 1 == 2
    False
    >>> 1 == 1.0
    True
    >>> 10 >= 10
    True
    >>> 13 <= 1 + 3
    False
    >>> -1 != 0
    True

The result of a comparison is always ``True`` or ``False``.
Comparisons can be combined into more complex conditions by using the words :keyword:`and` and
:keyword:`or`:

    >>> x = 5
    >>> x < 10
    True
    >>> 2*x > x
    True
    >>> (x < 10) and (2*x > x)
    True
    >>> (x != 5) and (x != 4)
    False
    >>> (x != 5) and (x != 4) or (x == 5)
    True


Indentations
------------

Another thing you should pay attention to is the indentation in the code. Open the interactive mode
and enter a simple condition such as::

    >>> if 2 > 1:
    ...

So far nothing has happened, as evidenced by dots ``...`` instead of a prompt ``>>>``, which we
have seen so far. Python expects us to give further instructions that are supposed to be executed if the
condition ``2 > 1``  turns out to be true. Let’s try to make Python print "OK"::

    >>> if 2 > 1:
    ... print("OK")
      File "<stdin>", line 2
        print("OK")
            ^
    IndentationError: expected an indented block

Unfortunately, we did not succeed. Python needs to know whether the instruction we have written is a
continuation of :keyword:`if` or it is the next instruction not covered by the condition. For this
purpose, we need to indent our code:

    >>> if 2 > 1:
    ...  print("OK")
    ...
    OK

All you need is one space or ``TAB``. However, all the lines that are supposed to be executed one
after another should be indented the same way::

    >>> if -1 < 0:
    ...  print("A")
    ...   print("B")
      File "<stdin>", line 3
        print("B")
        ^
    IndentationError: unexpected indent

    >>> if -1 < 0:
    ...     print("A")
    ...   print("B")
      File "<stdin>", line 3
        print("B")
                ^
    IndentationError: unindent does not match any outer indentation level

    >>> if -1 < 0:
    ...   print("A")
    ...   print("B")
    ...
    A
    B


To avoid chaos, most Python programmers use four spaces for each level of indentation. We will
do the same:

    >>> if 2 > 1:
    ...     if 3 > 2:
    ...         print("OK")
    ...     else:
    ...         print("FAIL")
    ...     print("DONE")
    OK
    DONE


What if not?
------------

Actually, we could write our program just by using :keyword:`if` ::

    if bmi < 18.5:
        print("underweight")
    if bmi >= 18.5:
        if bmi < 25.0:
            print("normal weight")
    if bmi >= 25.0:
        print("overweight")

We can also use :keyword:`else` and :keyword:`elif` to avoid repeating similar conditions and increase readability. In more complex programs it may not be obvious from
the beginning that a certain condition is the opposite of the previous one.


Using :keyword:`else` , we have the guarantee that the given instructions will be executed only if the instructions printed under :keyword:`if` haven’t been executed::

    if bmi < 18.5:
        print("underweight")
    else:
        # If your program executes this instruction,
        # for sure bmi >= 18.5 !
        if bmi < 25.0:
            print("normal weight")
        else:
            # now for sure bmi >= 25.0, we don’t have to
            # check it
            print("overweight")

Pay particular attention to the indentations. Every use of :keyword:`else`,
will cause an increased indentation of our code. It is very annoying when you have to check a few or a
dozen or so conditions which exclude one another. Therefore the authors of Python added a little
'improvement' in the form of :keyword:`elif`: instruction, which allows you to check another condition
immediately::


    if n < 1:
        print("one")
    elif n < 2:
        # if it wasn’t n < 1, and now it is n < 2
        print("two")
    elif n < 3:
        # ,if none of the previous condition was true.
        # n >= 1 i n>= 2, but n < 3
        print("three")
    else:
        # trolls can count only to three
        print("more")


Strings formatting
==================

The last issue which we have mentioned above was the problem with too many digits in a printed BMI.
Out of the three problems we had, this one is the easiest to solve.

That’s why we left it for the end of our adventure with the BMI calculator. We already know
that we can add strings to each other and multiply them by integers. You will see that we can also
format them. 

Currently the result is reduced to a single line. Now we want to write the
BMI as a number and the interval in which it is located, that is to say::

    Your BMI is equal: 21.39 (normal weight)

Modify the current program so that the calculated BMI would be available under the name of ``bmi``,and
the name of the interval under the name of ``category``. Then we can use :func:`print` and obtain the
required result:

.. testsetup::

    bmi = 21.387755102040817
    category = "normal weight"

.. testcode::

    print("Your BMI is equal:", bmi, "(" + category + ")")

.. testoutput::
    :hide:

    Your BMI is equal: 21.387755102040817 (normal weight)

Well, almost…. We still have too many digits. We would also have a problem if we wanted to generate
such a string and save with a name, because we use :func:`print` to separate the elements.
Fortunately, there is a better way:

    >>> bmi = 21.387755102040817
    >>> category = "normal weight"
    >>> result = "Your BMI: %f (%s)" % (bmi, category)
    >>> result
    'Your BMI: 21.387755 (normal weight)'
    >>> print(result)
    Your BMI: 21.387755 (normal weight)

We have here a string and a couple of variables in brackets, joined by ``%``. The string is a template which will be completed
with values present after ``%``. The spaces to be filled are also labeled with the percentage (``%``). .
The letter that follows defines the type of a value we want to insert. The integers are represented
by  ``i`` as **integer** (we can also use ``d`` as **decimal**),  strings are represented by ``s`` as
**string**, and floating-point numbers are represented by ``f`` for **float**:

    >>> "String: %s, Numbers: %d %f" % ("Ala", 10, 3.1415)
    'String: Ala, Numbers: 10 3.141500'

Now instead of nine decimal places we always get six, but the formatting has the advantage that it
allows us to have more control by putting between ``%`` and ``f`` additional information, e.g. if you
want to display only two places after the decimal point:


    >>> "%.2f" % 3.1415
    '3.14'
    >>> "%.2f" % 21.387755102040817
    '21.39'

There are plenty options of formatting, so we will not show them all here. One of the most useful is
the option of aligning to a specific number of characters:

.. testcode::

    WIDTH = 28

    print("-" * WIDTH)
    print("| Name and last name |  Weight  |")
    print("-" * WIDTH)
    print("| %15s | %6.2f |" % ("Łukasz", 67.5))
    print("| %15s | %6.2f |" % ("Pudzian", 123))
    print("-" * WIDTH)

.. testoutput::

    --------------------------------
    | Name and last name  |  Weight|
    --------------------------------
    |              Łukasz |  67.50 |
    |             Pudzian | 123.00 |
    --------------------------------

We can also align the string to the left by putting ``-`` before the number of characters:

.. testcode::

    WIDTH = 28

    print("-" * WIDTH)
    print("| Name and last name |  Weight |")
    print("-" * WIDTH)
    print("| %-15s | %6.2f |" % ("Łukasz", 67.5))
    print("| %-15s | %6.2f |" % ("Pudzian", 123))
    print("-" * WIDTH)

.. testoutput::

    -------------------------------
    | Name and last name|  Weight |
    -------------------------------
    | Łukasz            |  67.50  |
    | Pudzian           | 123.00  |
    -------------------------------

Aligning towards the centre is an additional excercise for you :).


Task: Game ‘rock-paper-scissors’
``````````````````````````````````

Description:

We will implement a simple game called rock-paper-scissors. Let's define goals of the game:

1. Show game manual
2. Get users choice as an input
3. Compare user's choice with predefined computer's choice
4. Print the outcome

Initial code:

.. code-block:: python

    print("Welcome")
    computer_choice = 'rock'

    # Print game manual, possible chocies, author itp.

    # Get user input

    # Compare user's and computer's choices

    # Print the outcome

Explore:

    * Print game manual in stylish frame
    * Print game manual on call (for instance, when user's choice was help)


Summary
=======

In this chapter we learned basics of Python syntax. We discovered how to print integers,
floating-point numbers and strings.

We learnt the function :func:`print`, that prints information for the user and the function
:func:`input`, which reads it.

We also know now that indentations can be important, especially when we want to use
the instruction :keyword:`if` (also in connection with :keyword:`else` and :keyword:`elif`).

We successfully created a program stored in a file and ran it. Our program asks the user to answer
a few simple questions, performs calculations and presents results in the form which is useful for the
user.

This is quite a lot like for a first program. We still have a lot of work, anyhow you can be proud of
what we have done so far!
