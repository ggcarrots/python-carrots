#############
Tic Tac Toe
#############
In this chapter we will implement a game of tic-tac-toe and learn some very useful programming concepts along the way! :)

You might want to take some time to figure out how to approach this problem. Think about what you normally do when you play pen and paper version of the game.

We are going to start from the most basic version of this exercise so that we can later extend it to a more functional version. First thing we have to do is drawing the board.

.. code-block:: python

    print('_|_|_')
    print('_|_|_')
    print(' | | ')

.. testoutput::

    _|_|_
    _|_|_
     | |

It resembles the tic-tac-toe board, but is just a little bit too small. Let's try to add more `_` and `|` characters in order to make the board a bit bigger.

.. code-block:: python

    print('     |     |     ')
    print('     |     |     ')
    print('_____|_____|_____')
    print('     |     |     ')
    print('     |     |     ')
    print('_____|_____|_____')
    print('     |     |     ')
    print('     |     |     ')
    print('     |     |     ')

.. testoutput::

         |     |
         |     |
    _____|_____|_____
         |     |
         |     |
    _____|_____|_____
         |     |
         |     |
         |     |

It doesn’t look bad, but we have had to do a lot of typing. What if we would like to have a smaller board? Or a bigger one? Or maybe even do a board with more than 9 fields? We would have to do too much typing, even if we would do it by multiplying strings  (``"_____|" * 100``, and so on.).
This is a repetitive action, one that computers are great at, way better than humans. Let's use it!


The ``for`` loop
==========================

Loops will serve us to deal with repetitive actions. In this chapter you will find out how to facilitate our drawing of the board with their help.

Let's examine how we draw the board. We have two types of lines that we print:

.. code-block::python

  print('     |     |     ')

  print('_____|_____|_____')

.. testoutput::

         |     |
    _____|_____|_____

You might have noticed that what we're printing are just strings, consisting of "|", "_" and " " characters. Since they are strings, we can assign them to variables to make our lives easier!

.. code-block:: python

  line_middle = '     |     |     '

  line_bottom = '_____|_____|_____'

  print(line_middle)
  print(line_bottom)

.. testoutput::

         |     |
    _____|_____|_____

Well cool, the result is the same, but we did more writing than before. You might be wondering "what's the point of that?". Let's go back to drawing the entire board.

.. code-block:: python

  line_middle = '     |     |     '

  line_bottom = '_____|_____|_____'

  print(line_middle)
  print(line_middle)
  print(line_bottom)

  print(line_middle)
  print(line_middle)
  print(line_bottom)

  print(line_middle)
  print(line_middle)
  print(line_middle)

.. testoutput::

             |     |
             |     |
        _____|_____|_____
             |     |
             |     |
        _____|_____|_____
             |     |
             |     |
             |     |

When you read the code used for creating the board, you might notice that each of the rows (except for the last one, but we will ignore it for now) is buiilt by printing ``line_middle`` twice, followed by ``line_bottom``. That's the repetition we were talking about just before! Let's employ the ``for`` loop in order to save us some writing.

.. code-block:: python

  line_middle = '     |     |     '

  line_bottom = '_____|_____|_____'

  for row in [1, 2, 3]:
      print(line_middle)
      print(line_middle)
      print(line_bottom)
.. testoutput::


             |     |
             |     |
        _____|_____|_____
             |     |
             |     |
        _____|_____|_____
             |     |
             |     |
        _____|_____|_____


Most of the things should look familiar to you. We are creating the strings and storing our board's building blocks in them.

A new element is a ``for`` loop itself, which consists of:

* the word :keyword:`for`,
* names we want to give to the next elements,
* the word :keyword:`in`,
* the value of a list or the name that refers to it.
* the content indented of one level (the same way as in the case of :keyword:`if`).

You might notice that a horizontal line has appeared at the bottom of our board and it no longer looks as cool as it did when we were printing each line "by hand". Sometimes with loops we want almost all of the elements to behave one way, and one or two elements to behave differently (usually first, last, or both). In our case, we want to print ``line_middle`` instead of ``line_bottom`` for the last row. Before we do that, let's see another example of the ``for`` loop that will help us understand how to achieve that.

.. code-block:: python

  for row in [1, 2, 3]:
      print(f"We are printing row number {row}")

.. testoutput::

    We are printing row number 1
    We are printing row number 2
    We are printing row number 3


So you see that we go through our list in order, each element only once, and inside the loop we have an additional variable ``row`` (or another one if we gave it a different name) that stores the value of the element.


Well, unfortunately we still have to type the entire contents of the list. This problem can be solved by the function :func:`range`, that we already know as well.


.. code-block:: python

  for row in range(3):
      print(f"We are printing row number {row}")

.. testoutput::

    We are printing row number 0
    We are printing row number 1
    We are printing row number 2

.. note::

  Recall that everything in Python is numbered starting with zero. That's why ``range(3)`` produces numbers that are less than 3.

Task: getting rid of that horizontal line in the last row
`````````````````````````````````````````````````````````
    Description:
      Right now you have all the tools necessary for making our board as pretty as it was before but using the ``for`` loop.
      What you have to do is check ``if`` we're printing the last line right now, and if so - print ``line_middle`` instead of ``line_bottom``

.. code-block:: python

    line_middle = '     |     |     '
    line_bottom = '_____|_____|_____'

    for row in range(3):
        if row == 2:
            print(line_middle)
            print(line_middle)
            print(line_middle)
        else:
            print(line_middle)
            print(line_middle)
            print(line_bottom)


Nothing prevents us to put one loop inside another loop, so let's do it! Just remember to use appropriate indentations and use different names e.g. ``i`` and ``j`` (or more associated with the list content):

    >>> for i in range(1, 3):
    ...    for j in range(11, 14):
    ...        print(i, j)
    1 11
    1 12
    1 13
    2 11
    2 12
    2 13

Here we have inner loop that iterates from 11 to 13 (remember, 14 is not included when using ``range``) and outer loop that iterates from 1 to 2. As you can see, items from inner loop are printed twice, for each iteration of outer loop.


Defining a ``function``
=======================

We have already seen how functions solve many of our problems. However, they do not solve all our problems – or at least not exactly the way we would like functions to solve them.
Sometimes we must solve a problem on our own. If it occurs often in our program, it would be nice to have a function that solves it for us.

A problem we've encountered in the previous part was finding an easy way of drawing the tic-tac-toe board. What we have right now should look like this:

.. code-block:: python

  line_middle = '     |     |     '
  line_bottom = '_____|_____|_____'

  for row in range(3):
      if row == 2:
          print(line_middle)
          print(line_middle)
          print(line_middle)
      else:
          print(line_middle)
          print(line_middle)
          print(line_bottom)

The board consists of three rows, each of them drawn almost identically - only the last one differs, because it uses ``line_middle`` instead of ``line_bottom``.
For the code repetitions like this one, we normally use functions.

.. code-block:: python

    def draw_board_row(last_line):
        print(line_middle)
        print(line_middle)
        print(last_line)



    line_middle = '     |     |     '
    line_bottom = '_____|_____|_____'

    for row in range(3):
        if row == 2:
            draw_board_row(line_middle)
        else:
            draw_board_row(line_bottom)

Let's have a closer look at the function :func:`draw_board_row`.

The definition of a function always starts with the word :keyword:`def`. Next, we give the name to our
function. Between the parenthesizes, we indicate what names should be given to its arguments when the function is
called. In the following lines we provide instructions to be executed when we use the function. In our case we copied one of the ``for`` loops that we have been using before.

As shown in the example, the instructions in the function may include names that we have given as the
names of the arguments. The principle of operation is as follows - if you create a function with
three arguments:

    >>> def foo(a, b, c):
    ...     print("FOO", a, b, c)

When you call this new function, you need to
specify a value for each argument. This just like all the functions we called before:

    >>> foo(1, "Ala", 2 + 3 + 4)
    FOO 1 Ala 9
    >>> x = 42
    >>> foo(x, x + 1, x + 2)
    FOO 42 43 44

Note that the argument name is just a label. If we change the value attached to a label for another one, the other labels will not
change – the same happens with the arguments:

    >>> def plus_five(n):
    ...     n = n + 5
    ...     print(n)
    >>> x = 43
    >>> plus_five(x)
    48
    >>> x
    43

The variables inside the functions act similarly to the ones we've used before but with two small differences.

Firstly, argument names of a function are defined at each function call, and Python attaches the corresponding
argument value to to each of the argument names it just created.

Secondly, the argument names are not available outside the function as they are created when the function is called
and forgotten after the call. That is, if you try now to access
the argument name ``n`` we defined in our :func:`plus_five` function outside of the function's code,
Python tells you it is not defined:

    >>> n
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    NameError: name 'n' is not defined

That is, our prim and proper Python cleans up his room at the end of a function call :)

Going back to our game board, we face one last problem before we move to storing the moves that were already made. How should the players input their choices?

What we could do is give each field on the board a symbol describing it's location: ``A1`` could be the field in the upper-left corner, ``A3`` in the upper-right etc. When our player places her pawn on the board, we will add the field to the list. It would be quite difficult for the user to remember every field's symbol. The board should look like that:

  .. testoutput::

          1     2     3
             |     |
      A      |     |
        _____|_____|_____
             |     |
      B      |     |
        _____|_____|_____
             |     |
      C      |     |
             |     |

The first row is fairly easy: we just have to print numbers from 1 to 3 with an appropriate spacing between them. The tricky part are the letters on the left side of the board. We want our first row (or row 0 in Python index) to be 'A', our second (1), to be 'B' and third (2) to be 'C'. Looks like a job for a dictionary! Let's adapt our code a bit.


.. code-block:: python

    def draw_board_row(last_line, letter):
        print(f'  {line_middle}')
        print(f'{letter} {line_middle}')
        print(f'  {last_line}')


    line_middle = '     |     |     '
    line_bottom = '_____|_____|_____'
    letters = {0:'A', 1:'B', 2:'C'}


    for row in range(3):
        if row == 2:
            draw_board_row(line_middle, letters[row])
        else:
            draw_board_row(line_bottom, letters[row])

What changed? We've added the dictionary that translates our row numbers into letters as well as another parameter in our ``draw_board_row`` function, passing the letter that we want to be printed next to this row.

The last part that's missing is the top row, the one with column numbers. Let's add them now!

.. code-block:: python

    def draw_board_row(last_line, letter):
        print(f'  {line_middle}')
        print(f'{letter} {line_middle}')
        print(f'  {last_line}')


    line_middle = '     |     |     '
    line_bottom = '_____|_____|_____'
    letters = {0:'A', 1:'B', 2:'C'}

    print('    1     2     3  ')
    for row in range(3):
        if row == 2:
            draw_board_row(line_middle, letters[row])
        else:
            draw_board_row(line_bottom, letters[row])

Returning values
================

The functions which we have previously used had one important property that is missing in the
functions created by ourselves - they gave back the value they computed instead of printing it immediately. To achieve the same effect, you need to use the instruction :keyword:`return`. This is a special instruction that can be found only in functions.

In order to see an example of a function with the ``return`` statement, we will write another function that will help us draw our board.

Let's say that our players have already started the game. Nought has placed her pawn in the middle of the board, cross in the upper right corner. We need to store the list of moves somehow. One idea would be to make two lists: one for the pawns placed by each player. Then, when we will print our board, we can check our lists and print corresponding pawns to our board.

We will start with writing a function that will accept field's address as an argument and return 'X' if the field is on the ``crosses`` list, 'O' if it's on the ``noughts`` list, and ' ' if it's on neither of them.

.. code-block:: python

    def get_field_content(address):
        if address in noughts:
            return 'O'
        elif address in crosses:
            return 'X'
        else:
            return ' '

Now that we already have this function, let's test add it to the code that we've built before.

.. note::

    The key to understanding what's hapenning in the next code snippet is to remember that we can concatenate strings using the `+` sign. So, for example, `'A' + '1' = 'A1'`

.. code-block:: python

    def get_field_content(address):
        if address in noughts:
            return 'O'
        elif address in crosses:
            return 'X'
        else:
            return ' '

    def draw_board_row(last_line, letter):
        symbol1 = get_field_content(letter + '1')
        symbol2 = get_field_content(letter + '2')
        symbol3 = get_field_content(letter + '3')

        print(f'  {line_middle}')
        print(f'{letter}   {symbol1}  |  {symbol2}  |  {symbol3}  ')
        print(f'  {last_line}')


    line_middle = '     |     |     '
    line_bottom = '_____|_____|_____'
    letters = {0:'A', 1:'B', 2:'C'}
    noughts = ['B2']
    crosses = ['A3']

    print('    1     2     3  ')
    for row in range(3):
        if row == 2:
            draw_board_row(line_middle, letters[row])
        else:
            draw_board_row(line_bottom, letters[row])

In case you're wondering what happened to the `draw_board_row` function, in order to draw the entire row, we need to have all three of the symbols that appear in that row, so we start with fetching those. Then we have to edit the middle line of the field in order for the pawn to be displayed. We write the value gotten from the other function in the middle of the field.

Accepting user's input
======================

The finished tic-tac-toe game should do the actions below in a loop:
  * print our tic-tac-toe board
  * ask player for the next move
  * check if it's a valid move
  * add the move to the moves list
  * check if the player won

We have already finished the first point and it's high time to move to the next one. In order to accept the user's input (without validation) we have to just write:

.. code-block:: python

    user_move = input('Please input your next move')

    if current_move == 'O':
        noughts.append(user_move)
    else:
        crosses.append(user_move)

Let's add this move to our current version of the game. don't forget to empty the `noughts` and `crosses` lists and to add a new variable `current_move` that will store the info about which player moves next.

.. code-block:: python

    def get_field_content(address):
        if address in noughts:
            return 'O'
        elif address in crosses:
            return 'X'
        else:
            return ' '

    def draw_board_row(last_line, letter):
        symbol1 = get_field_content(letter + '1')
        symbol2 = get_field_content(letter + '2')
        symbol3 = get_field_content(letter + '3')

        print(f'  {line_middle}')
        print(f'{letter}   {symbol1}  |  {symbol2}  |  {symbol3}  ')
        print(f'  {last_line}')


    line_middle = '     |     |     '
    line_bottom = '_____|_____|_____'
    letters = {0:'A', 1:'B', 2:'C'}
    noughts = []
    crosses = []

    print('    1     2     3  ')
    for row in range(3):
        if row == 2:
            draw_board_row(line_middle, letters[row])
        else:
            draw_board_row(line_bottom, letters[row])

    user_move = input('Please input your next move: ')

    if current_move == 'O':
        noughts.append(user_move)
    else:
        crosses.append(user_move)

But wait! It only executes once. We want our game to have more than one round.

``while`` loop
==============

`while` is another example of a loop, after `for`. The difference is that when we want to use `for` we need to know how many times we want to execute the loop *before* we even start running it. `while` loop executes as long as a condition that we give it is fulfilled. It can run infinitely (`while True`) or never run (`while False`). We want our game to finish only if either of the players won or there are no more empty fields. Let's adapt our code.

.. code-block:: python

    def get_field_content(address):
        if address in noughts:
            return 'O'
        elif address in crosses:
            return 'X'
        else:
            return ' '

    def draw_board_row(last_line, letter):
        symbol1 = get_field_content(letter + '1')
        symbol2 = get_field_content(letter + '2')
        symbol3 = get_field_content(letter + '3')

        print(f'  {line_middle}')
        print(f'{letter}   {symbol1}  |  {symbol2}  |  {symbol3}  ')
        print(f'  {last_line}')


    line_middle = '     |     |     '
    line_bottom = '_____|_____|_____'
    letters = {0:'A', 1:'B', 2:'C'}
    noughts = []
    crosses = []
    current_move = 'O'

    while True:

        print('    1     2     3  ')
        for row in range(3):
            if row == 2:
                draw_board_row(line_middle, letters[row])
            else:
                draw_board_row(line_bottom, letters[row])

        user_move = input('Please input your next move: ')

        if current_move == 'O':
            noughts.append(user_move)
        else:
            crosses.append(user_move)

Whoops! We forgot one thing. Can you spot it?


.. code-block:: python

    def get_field_content(address):
        if address in noughts:
            return 'O'
        elif address in crosses:
            return 'X'
        else:
            return ' '

    def draw_board_row(last_line, letter):
        symbol1 = get_field_content(letter + '1')
        symbol2 = get_field_content(letter + '2')
        symbol3 = get_field_content(letter + '3')

        print(f'  {line_middle}')
        print(f'{letter}   {symbol1}  |  {symbol2}  |  {symbol3}  ')
        print(f'  {last_line}')


    line_middle = '     |     |     '
    line_bottom = '_____|_____|_____'
    letters = {0:'A', 1:'B', 2:'C'}
    noughts = []
    crosses = []
    current_move == 'O'

    while True:
        print('    1     2     3  ')
        for row in range(3):
            if row == 2:
                draw_board_row(line_middle, letters[row])
            else:
                draw_board_row(line_bottom, letters[row])

        user_move = input('Please input your next move: ')

        if current_move == 'O':
            noughts.append(user_move)
            current_move = 'X'
        else:
            crosses.append(user_move)
            current_move = 'O'

Before, we forgot to change the `current_move` variable, so every time it put a nought on the board. Now, we exchange the pawn after making a move. The game works!

It still doesn't validate whether the user has made a correct move nor does it proclaim a winner. We will take care of that in the next chapter.
