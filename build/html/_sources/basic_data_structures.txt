######################
Basic Data Structures
######################

Data structures are Python objects (no surprise here). They help us organize and store data on our computer. Just as the name suggests, they provide structure to our data, not only keeping the values, but also the relationships between them and even defining operations that can be applied to them.

In this chapter you will learn about Python's most popular data structures, starting with a list.

Lists
=====

In real life we can have shopping lists, or "todo" lists. They are very similar to their Python counterparts. In Python, we use them in order to store some values, where the order might be important.

Lists are associated with the square brackets, so in order to create a new :func:`list`, you need to define it:

.. code-block:: python

    >>> L = []
    >>> L
    []

At any time we can check how many items we have saved on our list by using the function :func:`len`.

    >>> len(L)
    0

Let's make another list (which can have the same name or a different one):

    >>> L = ["Jack", "Jill", "John"]
    >>> len(L)
    3

To preview a particular position of an element on the list (remember that we count the positions from 0):

    >>> L[0]
    'Jack'
    >>> L[1]
    'Jill'
    >>> L[2]
    'John'
    >>> L[3]
    Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
    IndexError: list index out of range

Python's lists are flexible enough to let us store any type of value we want - `int`, `float`, `str` - you name it. Not only on different lists, but we can also store all of them on one list:

.. code-block:: python

  L = [1, "Some string", 2.0]
  print(L)
  [1, "Some string", 2.0]


There are also some helpful methods defined on the ``list`` objects.

.. code-block:: python

  L = []
  L.append(1)
  print(L)
  [1]
  # append to the end of the list
  L.append(2)
  print(L)
  [1, 2]
  # insert at a given position; here at 0
  L.insert(0, 3)
  print(L)
  [3, 1, 2]
  # remove first occurence from the list
  L.remove(2)
  print(L)
  [3, 1]
  # yo dawg! I've heard you like lists, so I put a list in your list
  L.append(['a', 2])
  print(L)
  [3, 1, ['a', 2]]

Generators
==========

Imagine that you need a list of a length 100 consisting of numbers 0-99 (or 1-100). Thus far you know no smart way of doing that. We have to type the entire contents of the list. This problem can be solved by the function :func:`range`. Check ``help(range)`` for the full story, or check these quick examples:

.. code-block:: python

    >>> list(range(5))
    [0, 1, 2, 3, 4]
    >>> list(range(1, 5))
    [1, 2, 3, 4]
    >>> list(range(1, 11, 2))
    [1, 3, 5, 7, 9]
    >>> list(range(1, 11))
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    >>> list(range(1, 2))
    [1]
    >>> list(range(2))
    [0, 1]

The :func:`range` function does not directly create a list, but it returns a generator.

You wouldn't see much of a difference for our examples, but if you start playing with really big numbers, it will become apparent.
When you create a list, each element needs to be evaluated and saved to memory before we even begin our operations on it. So if we try to create a list of a bilion elements, it might take up some of our memory and slow our computers down.
On the other hand, generator only works at one element at the time. It fetches the element, does the operations that needed to be done and generates the next element only after the first one was completely processed.

In order to obtain a list of the sequence, we use the function :func:`list`. If we skip :func:`list` call,
the result will look like this:


    >>> range(1, 4)
    range(1, 4)


The :func:`range` function has three forms. The most basic and most used one creates a sequence from 0 to the
given number minus one. The other forms allow you to specify the start of the range and a step. The created
sequence never includes the end of the specified range.

Tuples
======

Tuples are very similar to lists, with one *crucial* difference - they are immutable. It means, that once we define our tuple, we won't be able to add nor delete objects from it. They are really useful, for example if you don't want people to mess up your data by accident.

`list` was associated with the square brackets, `tuple` is associated with the round ones (although the parentheses are optional):

.. code-block:: python

    tuple1 = (1, 2, 3)
    tuple2 = 4, 5, 6
    not_a_tuple=(2)

The last example is not a tuple. Since the parentheses are optional, Python will treat ``(2)`` as a normal `2`, not a tuple. In order for it to be treated as a tuple, we need to add a coma afterwards:

.. code-block:: python

    tuple3=(2, )

Sets
====

Sets are once again structures that differ slightly from lists. Two of the biggest differences are that:
  * sets are not ordered (each time you ask Python to print it, it can give you a different ordering)
  * every value in the set is unique

.. code-block:: python

  L = [1, 2, 3, 1, 2, 3]
  print(L)
  [1, 2, 3, 1, 2, 3]

  S = set(L)
  print(S)
  {2, 3, 1}

There is one very cool property of sets: you can subtract two sets from each other:

.. code-block:: python

  S1 = {1, 2, 3}
  S2 = {1, 2}
  print(S2 - S1)
  {3}

Dictionaries
============

Introduction
------------

Dictionary is the last data structure you will get to know. It is a bit more complex than the previous ones. Dictionaries are used to store data as a key and value (just like in encyclopedia - you have entry and a description attached to it). Imagine you want to store information about library users. For every reader you have: name, surname, birthdate, birthplace, id number.
In python such a structure would look like this:

.. code-block:: python

  reader = {
    'name': 'Kasia',
    'surname': 'Kowalska',
    'date_of_birth': '19-01-1985',
    'place_of_birth': 'Wrocław',
    'readers_nr': 'ASDF1234',
  }

In this example ``name`` is a key (dictionary entry), witch assigned value ``Kasia`` (entry description).
Try to create your own user entry.

Nowoczesna Biblioteka Raczyńskich in Poznan wants to send its users birthday wishes. For the library worker to know when you were born it only takes to check:

  >>> print reader['date_of_birth']
  '19-01-1985'

The clerk recalled: to send you birthday wishes he needs your address as well. You can add them to your reader's data in such manner:

.. code-block:: python

  reader['address'] = 'ul. Marszałkowska 1, 01-234 Warszawa'

You can easily change the value in dictionary, if you make any mistake- it only takes to rewrite existing value:

.. code-block:: python

  reader['place_of_birth'] = 'Łódź'

Task 1
------

Description: Library system contains author data assigned to every book. Library clerk checks book author while putting books on shelf in alphabetic order.
Try to write down pairs: book --> author for every record in dictionary, used to store library information.

EXAMPLE (one line output):

.. code-block:: python

  'Introduction to Algorithms' --> 'Thomas H. Cormen'

.. code-block:: python

  title_to_author = {
    'Structure and Interpretation of Computer Programs' : 'Harold Abelson',
    'Introduction to Algorithms' : 'Thomas H. Cormen',
    'The C Programming Language' : 'Brian W. Kernighan',
    'The Pragmatic Programmer: From Journeyman to Master' : 'Andrew Hunt',
    'Art of Computer Programming' : 'Donald Ervin Knuth',
    'Design Patterns: Elements of Reusable Object-Oriented Software' : 'Erich Gamma',
    'Artificial Intelligence: A Modern Approach' : 'Stuart Russell',
    'Introduction to the Theory of Computation' : 'Michael Sipser',
    'Code Complete' : 'Steve McConnell',
    'The Mythical Man-Month: Essays on Software Engineering' : 'Frederick P. Brooks Jr.'}


Task 2
------

You can help the clerk to find out on which shelf given book should be putted. In this very moment the library store data about its books in two dictionaries:: ``title_to_author`` and ``title_to_shelf_number``. We need to join them.
After join there will be one dictionary, containing information about shelf and author of a book.
These information will be stored in tuplets of such elements (shelf number, author's full name)

Merge two dictionaries ``title_to_author`` and ``title_to_shelf_number`` in one, stored in variable ``title_to_book_record``:

* The key in dictionary ``title_to_author`` is "book's title", and value is "main author's name"
* The key in dictionary ``title_to_shelf_number`` is "book's title", and value is "shelf number"
* The key in output dictionary ``title_to_book_record`` should be "book's title", and value should contain 2 elements tuple
  ("main author's name", "shelf number")

EXAMPLE:

For key ``The C Programming Language`` dictionary ``title_to_book_record`` should return a tuplet:
``('Brian W. Kernighan', 23)``. In Python interpreter:

  >>> title_to_book_record['The C Programming Language']
  ('Brian W. Kernighan', 23)

.. code-block:: python

  title_to_author = {
    'Structure and Interpretation of Computer Programs' : 'Harold Abelson',
    'Introduction to Algorithms' : 'Thomas H. Cormen',
    'The C Programming Language' : 'Brian W. Kernighan',
    'The Pragmatic Programmer: From Journeyman to Master' : 'Andrew Hunt',
    'Art of Computer Programming' : 'Donald Ervin Knuth',
    'Design Patterns: Elements of Reusable Object-Oriented Software' : 'Erich Gamma',
    'Artificial Intelligence: A Modern Approach' : 'Stuart Russell',
    'Introduction to the Theory of Computation' : 'Michael Sipser',
    'Code Complete' : 'Steve McConnell',
    'The Mythical Man-Month: Essays on Software Engineering' : 'Frederick P. Brooks Jr.'}

.. code-block:: python

  title_to_shelf_number = {
    'Structure and Interpretation of Computer Programs' : 1,
    'Introduction to Algorithms' : 34,
    'The C Programming Language' : 23,
    'The Pragmatic Programmer: From Journeyman to Master' : 12,
    'Art of Computer Programming' : 4,
    'Design Patterns: Elements of Reusable Object-Oriented Software' : 586,
    'Artificial Intelligence: A Modern Approach' : 32,
    'Introduction to the Theory of Computation' : 98,
    'Code Complete' : 77,
    'The Mythical Man-Month: Essays on Software Engineering' : 3}


Task 3
------

If you would like to find books particular edition by ISBN, you can use dictionary as below.

Print out dictionary's content in such manner::

    'TITLE' by 'AUTOR' is on shelf 'NUMBER_OF_SHELF' (ISBN: 'NUMBER_OF_ISBN')

The key in dictionary ``books`` is integer "ISBN" , and value is THREE ELEMENTS TUPLE ("book's title", "main author's name", "shelf number")

EXAMPLE (one line output)::

    Introduction to Algorithms by Thomas H. Cormen is on shelf 34 (ISBN: 0262032937)

.. code-block:: python

  books = {
    '0262510871' : ('Structure and Interpretation of Computer Programs', 'Harold Abelson', 1),
    '0262032937' : ('Introduction to Algorithms', 'Thomas H. Cormen', 34),
    '0131103628' : ('The C Programming Language', 'Brian W. Kernighan', 23),
    '020161622X' : ('The Pragmatic Programmer: From Journeyman to Master', 'Andrew Hunt', 12),
    '0201485419' : ('Art of Computer Programming', 'Donald Ervin Knuth', 4),
    '0201633612' : (
      'Design Patterns: Elements of Reusable Object-Oriented Software', 'Erich Gamma', 586),
    '0130803022' : ('Artificial Intelligence: A Modern Approach', 'Stuart Russell', 32),
    '0534950973' : ('Introduction to the Theory of Computation', 'Michael Sipser', 98),
    '0735619670' : ('Code Complete', 'Steve McConnell', 77),
    '0201835959' : (
      'The Mythical Man-Month: Essays on Software Engineering', 'Frederick P. Brooks Jr.', 3
    )
  }


Additional task
---------------

Fill the body of method ``find_by_isbn_part``, so it would return all books' titles matching part of given ISBN.
The key in dictionary ``books`` is ``ISBN``, and value is THREE ELEMENTS TUPLE::

    ("book's title", "main author's name", "shelf number")

Running this script will execute test function, that will verify if the method works properly and output the result to the terminal.

.. code-block:: python

  books = {
    '0262510871' : ('Structure and Interpretation of Computer Programs', 'Harold Abelson', 1),
    '0262032937' : ('Introduction to Algorithms', 'Thomas H. Cormen', 34),
    '0131103628' : ('The C Programming Language', 'Brian W. Kernighan', 23),
    '020161622X' : ('The Pragmatic Programmer: From Journeyman to Master', 'Andrew Hunt', 12),
    '0201485419' : ('Art of Computer Programming', 'Donald Ervin Knuth', 4),
    '0201633612' : (
      'Design Patterns: Elements of Reusable Object-Oriented Software', 'Erich Gamma', 586),
    '0130803022' : ('Artificial Intelligence: A Modern Approach', 'Stuart Russell', 32),
    '0534950973' : ('Introduction to the Theory of Computation', 'Michael Sipser', 98),
    '0735619670' : ('Code Complete', 'Steve McConnell', 77),
    '0201835959' : (
      'The Mythical Man-Month: Essays on Software Engineering', 'Frederick P. Brooks Jr.', 3
    )
  }

CORRECT THE FUNCTION ``find_by_isbn_part``:

.. code-block:: python

    def find_by_isbn_part(books, isbn_part):
        result = []

        # HINTS:
        #  - user for loop
        #  - isbn_part in isbn is a condition that verifies if isbn contains isbn_part
        #  - adding elements to list, where x is a list and e is an element to add: x.append(e)
        return result

    # DO NOT ALTER
    def test(books):
        single_test(books, '020', ['The Pragmatic Programmer: From Journeyman to Master',
                                 'Art of Computer Programming',
                                 'Design Patterns: Elements of Reusable Object-Oriented Software',
                                 'The Mythical Man-Month: Essays on Software Engineering'])
        single_test(books, '18', ['The Mythical Man-Month: Essays on Software Engineering'])
        single_test(books, '22', ['The Pragmatic Programmer: From Journeyman to Master',
                                'Artificial Intelligence: A Modern Approach'])
        single_test(books, '0735619670', ['Code Complete'])

    def single_test(books, input, expected_output):
        output = find_by_isbn_part(books, input)
        if set(output) != set(expected_output) or len(output) != len(expected_output):
            print(
              "WRONG! FOR '" + input +
              "' RESULT IS: '" + str(output) +
              "', EXPECTED: '" + str(expected_output) + "'")
        else:
            print("OK! FOR '" + input + "'")

    test(books)
