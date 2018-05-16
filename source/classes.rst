
Objects and classes
===================

Every value is an object
------------------------

Everything that we have called a variable until now can be called “an object” in the world of Python. We saw it in the
example of integers, when :func:`help` printed for us dozens of additional lines of information about
:func:`int`.

Every object has a class
------------------------

The class is the type of an object.
To know what is the class of an object, simply use the function :func:`type`:

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

When we use numbers in our program, we expect that it will behave like a number - we rely on our
intuition.

However, Python has to know exactly what it means to be a number, e.g., what should happen when we
sum up two numbers and what when we divide them. The class ``int`` provides all this information and
even more.

By using :func:`help` , check what the class ``str`` gives us. Here we give just a few interesting
features:

    >>> help(str.lower)
    Help on method_descriptor:
    <BLANKLINE>
    lower(...)
        S.lower() -> str
    <BLANKLINE>
        Return a copy of the string S converted to lowercase.
    <BLANKLINE>
    >>> help(str.upper)
    Help on method_descriptor:
    <BLANKLINE>
    upper(...)
        S.upper() -> str
    <BLANKLINE>
        Return a copy of S converted to uppercase.
    <BLANKLINE>
    >>> help(str.ljust)
    Help on method_descriptor:
    <BLANKLINE>
    ljust(...)
        S.ljust(width[, fillchar]) -> str
    <BLANKLINE>
        Return S left-justified in a Unicode string of length width. Padding is
        done using the specified fill character (default is a space).
    <BLANKLINE>
    >>> help(str.center)
    Help on method_descriptor:
    <BLANKLINE>
    center(...)
        S.center(width[, fillchar]) -> str
    <BLANKLINE>
        Return S centered in a string of length width. Padding is
        done using the specified fill character (default is a space)
    <BLANKLINE>

All these are operations that each string can do. We can get to them by using dots and calling the
function:

    >>> x = "Ala"
    >>> x.upper()
    'ALA'
    >>> x.lower()
    'ala'
    >>> x.center(9)
    '   Ala   '

And one more important function of a class - it can create a new object of the type it describes. This is called
called "an instance" of a class:

    >>> int()
    0
    >>> str()
    ''
    >>> list()
    []
    >>> tuple()
    ()

So an instance is a new, fresh value of the type described by the class.

In summary, we've looked at the classes :func:`int`, :func:`str`, :func:`tuple` and
:func:`list`. To find out from which class is the value (object), we use the function
:func:`type`. To create an instance of a class (a new object), we call the class like call
a function, by using parentheses ``()``. For instance:
``int()``.

Define classes
--------------

Classes like ``int`` or ``str`` are already known to Python, but we can create our own classes to
customize their behavior. This is called defining a class.

You can define your class as easy as you can define a function. In fact, a class is
basically nothing but a group of functions. Let's define a class named ``TicTacToeBoard``:

.. testcode:: simple-class

    class TicTacToeBoard(object):

        def plot(self):
            for row in range(3):
                print("   |   |   ")
    


Class definitions begin with the word :keyword:`class`, after which we give the name of the new class.
The ``(object)`` indicates that our new type ``TicTacToeBoard`` is a specific sub-type of ``object``.
That is, instances of our class, i.e. variables created from it, will be of the type ``TicTacToeBoard`` but
also of the more general type ``object``.

Actually this is what we said that every variable is an object.
Each class is a specialization of ``object`` in Python. Hence, every value always has ``object``
as most general type.
And so, because it is the default behaviour, we can actually ommit writing it:

.. code::

    class TicTacToeBoard:
        # ...

We can create an instance of a class ``TicTacToeBoard``; let's call it ``my_board``.
We can check it's type with ``type()`` function.
We can also ask if it's an instance of a type ``TicTacToeBoard``, ``list``, ``object`` or whatever we like
using function ``isinstance()``.

.. testcode:: simple-class

    my_board = TicTacToeBoard()
    type(my_board)
    isinstance(my_board, TicTacToeBoard)
    isinstance(my_board, list)
    isinstance(my_board, object)

.. testoutput::

    <class '__main__.TicTacToeBoard'>
    True
    False
    True

As you can see, you create an instance of a class just like you call a function:
by writing it's name and then ``()``.
(Spoiler: there can be some arguments in those brackets! But we will talk about it later.)
Every instance of ``TicTacToeBoard``, like ``my_board``, has all the methods that we defined for that class.
In that case that would be one method, called ``plot``.
You may have noticed that it has one weird argument ``self`` that we don't actually use in it.
It's important to remember that every function in the class must have at least one argument.
Its value is an object from which we have called this function -
that would be some instance of the class. This argument should be called ``self``
`by convention <https://www.python.org/dev/peps/pep-0008/#function-and-method-arguments>`_
(technically you could call it otherwise, but other programmers would be angry with you if you did).
Let's see how it works in practice:

.. testcode:: simple-class

    my_board = TicTacToeBoard()
    my_board.plot()

As you can see, you don't actually put any argument in the brackets while calling the function.
Rather it's the ``TicTacToeBoard`` instance before the dot;
we put it there, but ``plot`` function knows that ``my_board`` is now its ``self`` argument.
Recall that in the same way we called some methods on lists and other objects,
for example: ``my_list.append(4)``.


Attributes of objects
---------------------

Obviously, we don't want our board to stay empty all the time.
We want to be able to place crosses and noughts on the instances of our new class;
and we want these instances to remember where the crosses and noughts were placed,
and print itself accordingly.
This can be accomplished by giving our ``TicTacToeBoard`` instance some **attributes**.

.. testcode:: simple-class

    my_board = TicTacToeBoard()
    my_board.crosses = [(0, 1), (0, 0)]
    my_board.noughts = [(2, 2)]
    print(my_board.crosses)
    print(my_board.noughts)

.. testoutput:: simple-class

    [(0, 1), (0, 0)]
    [(2, 2)]

Now our instance ``my_board`` has attributes ``crosses`` and ``noughts``.
They both store list of tuples; every tuple is a pair of coordinates, where a nought or cross were placed.
As you can see we can get to them by writing the name of our instance, a dot and then the name of an attribute.
That way we can create  new attributes or get the values of the ones already created.

Values of the attributes are something specific to the instance of a class.
That means, if we create a new instance of the class ``TicTacToeBoard``, it won't have the defined attributes.
We can give them to it, of course, and they can be different than the attributes of ``my_board``,
and it won't affect the attributes of ``my_board``.
It's just like when we create different lists: we could put different values in every of them,
and they are totally independent,
though they all are instances of the class ``list``,
and have all the methods specific for the class ``list``.
Observe:

.. testcode:: class

    my_new_board = TicTacToeBoard()
    my_new_board.noughts

.. testoutput::

    ---------------------------------------------------------------------------
    AttributeError                            Traceback (most recent call last)
    <ipython-input-3-53eba1fc6abf> in <module>()
    ----> 1 my_new_board.noughts

    AttributeError: TicTacToeBoard instance has no attribute 'noughts'

.. testcode::

    my_new_board.noughts = [(1, 2), (2, 0)]
    print(my_board.noughts)
    print(my_new_board.noughts)

.. testoutput::

    [(2, 2)]
    [(1, 2), (2, 0)]

Now it would be nice if our boards could print the noughts and crosses that we put in them.
For that we need to modify the ``plot`` function:

.. testcode:: simple-class

    class TicTacToeBoard:

        def plot(self):
            for row in range(3):
                for column in range(3):
                    if (row, column) in self.crosses:
                        char_to_print = "x"
                    elif (row, column) in self.noughts:
                        char_to_print = "o"
                    else:
                        char_to_print = " "
                    print(char_to_print)

Notice that we didn't provide lists of positions of crosses or noughts as arguments.
We just told python to use attributes of the instance that called the function.
Recall that the instance is passed as ``self`` argument,
even though while calling the function we don't put the instance inside the brackets; we put it before the dot.
So now the ``plot`` function for every position will check
if this position is in the attribute ``crosses`` of the instance that it has been called from;
and the same with the attribute ``noughts``.
Let's see how it works:

.. testcode:: simple-class

    my_board = TicTacToeBoard()
    my_board.crosses = [(0, 0), (1, 1), (2, 2)]
    my_board.noughts = [(1, 2), (0, 2)]
    my_board.plot()

Great, now we have a way to plot crosses and noughts on our board!
But what if we forgot to define these attributes?
The ``plot()`` function wouldn't know what ``self.noughts`` or ``self.crosses`` are;
it won't even print an empty board, it will just return an error.
It would be better to assure that every instance of our class have these attributes.
Is there a way to do that? Yes!
We can define attributes of an object when it is created.
We need to tell python that we want some specific stuff to happen
(in this case, we want to create some attributes)
when we initialise an instance of a ``TicTacToeBoard``.
We do that by adding a method ``__init__`` to the definition of the class.
It's a function that is called when an object is created; that's why it's called a **constructor**.
Actually every class has this function defined, even if we don't do it ourselves.
So, when we typed ``my_board = TicTacToeBoard()`` python actually called a function ``__init__`` of a class ``TicTacToeBoard``.
We can define it ourselves and add what we need.

.. testcode:: simple-class

    class TicTacToeBoard:
        
        def __init__(self):
            self.crosses = []
            self.noughts = []
            

Now every time we create a new instance of the class TicTacToeBoard,
it already has the attributes ``crosses`` and ``noughts`` -
empty lists, ready to be filled.
Also, notice that the constructor also needs the ``self`` argument,
even if we don't provide it neither inside the brackets, nor before the dot. 

Now that our boards can store coordinates of noughts and crosses that was put,
let's add some methods to actually put them there.

.. testcode:: simple-class

    class TicTacToeBoard:
        
        def __init__(self):
            self.crosses = []
            self.noughts = []

        def add_cross(x, y):
            self.crosses.append((x, y))

        def add_nought(x, y):
            self.noughts.append((x, y))


Additional task: modify the method that adds a cross,
so that it will check whether it is a legal move:
that is, whether the coordinates are inside the board and whether the field is free.
Do the same for the ``add_nought()`` method.

Now we can finnally create a simple game using our class ``TicTacToeBoard``:

.. testcode:: simple-class  

    board = TicTacToeBoard()
    while True:
        answer = input("Player1, where do you place your 'o'?")
        x, y = answer.strip().split()
        board.add_nought(int(x), int(y))
        board.plot()
        answer = input("Player2, where do you place your 'x'?")
        x, y = answer.strip().split()
        board.add_cross(int(x), int(y))
        board.plot()

Of course now the game goes on forever.
Let's make ``board`` in charge of checking whether the game should end or not.

# kod z funkcja check

Notice that in the while loop we do almost the same thing two times.
When we added checking, we needed to remember to add it in two places.
Also if you added some checking if the move is legal,
you needed to put it in two different methods.
If we ever decide to do some small change, we need to do it in two places.
It seems like a lot of unnecessary work and also asking for mistakes.
Let's modify this code so that it will look more elegant:


.. code::

    class TicTacToeBoard:

        def __init__(self):
            self.pawns = {'o':[], 'x':[]}

        def add_pawn(pawn, x, y):
            self.pawns[pawn].append((x, y))

    board = TicTacToeBoard()
    while condition:
        for pawn in ('o', 'x'):
            answer = input("Player, where do you place your '" + pawn "'?")
            x, y = answer.strip().split()
            board.add_pawn(pawn, int(x), int(y))
            board.plot()
            condition = board.check()

Additional task:
modify the ``check`` method, so it will return who won the game.
Then at the end announce the winner.

Notice that we've cheated a little bit here -
to simplify constructing our prompt, we replaced customized phrase "Player 1" or "Player 2" with more general "Player".
We don't need to do that!
Furthermore, thanks to classes we can more easily store some informations about players, like their name,
and refer to them accordingly.
Let's create a class Player:

.. code::

    class Player:

        def __init__(self, name, char = 'o'):
            self.name = name
            self.char = char


Notice that we added some arguments to the ``__init__`` method;
we provide values for them while creating an instance of the ``Player`` class.
Now when we create ``Player`` object, we can provide his name and the character he uses,
and they will be stored in its attributes ``char`` and ``name``.
It's okay if we don't provide the character, because we defined some default value for it.
The ``__init__`` method called during the creation will assign the value of the argument ``char``
to attribute ``char`` of newly created object (and the same for ``name``).
These two names don't have to be the same;
the ``__init__`` method can get an argument called ``char``
and give it's value to some attribute called ``players_character``,
however when there is no need to call them differently, let's not do that;
after all, they mean the same thing.

Now we can make our game a little bit nicer for the players:

.. code::

    board = TicTacToeBoard()
    players = [Player('Loki', 'o'), Player('Thor', 'x')]
    while condition:
        for player in players:
            answer = input("Dear " + player.name + 
                ", where do you place your '" + player.char + "'?")
            x, y = answer.strip().split()
            board.add_pawn(player.char, int(x), int(y))
            board.plot()
            condition = board.check()

Now that we have a backbone of our game, we can develop it as we like:
we can store statistics of wins for every player,
ask for players' names at the beginning,
ask if they wish to play one more time,
allow them to choose their own pawns, different than 'x' and 'o',
add names of the rows and columns to the plotted board...
Sky is the limit!


Inheritance
-----------

Let's say we got bored with tic-tac-toe and want to write a new game - Connect Four.
It's different from tic-tac-toe, of course, but it has some simmilarities:
two players move in turns, by placing some pawns on the board;
the goal is to have some number of pawns in one line;
board can be printed in a simmilar manner, even though it has different size
(Connect Four is played on a board with 6 rows and 7 columns);
the whole game menu could be essentially the same.
What shall we do? Write it all from the scratch?
That would be a waste of time.
Maybe copy it all and just change the bits that we want to be different?
That would be a bad habit.
What if we want to change it later, for example - we have an idea how to improve printing of the board?
We would have to change it in both implemented games.
It would be nice if we can implement it once and just use it in two different games.
Can we do so? Of course! We can use class **inheritance**.

Let's make our TicTacToeBoard more general.

.. code::

    class Board:

        def __init__(self, nrow, ncol):
            self.nrow = nrow    # number of rows
            self.ncol = ncol    # number of columns
            self.pawns = {}

        def plot(self):
            for row in range(nrow):
                for column in range(ncol):
                    character_to_print = ' '
                    for pawn in self.pawns:
                        if (row, column) in self.pawns[pawn]:
                            character_to_print = pawn
                            break
                    print(character_to_print)

Now our board can have any size, and can have any pawns placed on it.
Next we will define two classes: TicTacToeBoard and ConnectFourBoard.
They will both be subtypes, or subclasses of Board.

.. code::

    class TicTacToeBoard(Board):

        def __init__(self):
            self.ncols = 3
            self.nrows = 3
            self.pawns = {'o':[], 'x':[]}

    class ConnectFourBoard(Board):

        def __init__(self):
            self.ncols = 7
            self.nrows = 6

Note the word ``Board`` in the brackets.
Now whenever we create an instance of class ``TicTacToeBoard`` it will be still an instance of ``TicTacToeBoard``, of course,
but it will be also an instance of a more general class ``Board``
(and of a class ``object``, as a matter of fact).
The same goes for ``ConnectFourBoard``.
We say that ``Board`` is a **parent** class of ``TicTacToeBoard`` and ``ConnectFourBoard``,
and ``TicTacToeBoard`` and ``ConnectFourBoard`` are **child** classes of ``Board``.
We can check it with ``isinstance`` function::

    board = ConnectFourBoard()
    isinstance(board, ConnectFourBoard)
    isinstance(board, TicTacToeBoard)
    isinstance(board, Board)

.. testoutput::

    True
    False
    True

Note that it's not anything new.
We already observed that everything in python is an instance of a class ``object``.
We can create a list and it will be an instance of a class ``list``, but also an instance of ``object``.
In other words, ``list`` is a subtype of ``object``.
Every type in python, including those that we define ourselves, like ``Board`` or ``Player``, are subtypes of ``object``.

Every instance of a class has all the methods defined in the definition of that class;
so far that meant for us that every ``TicTacToeBoard`` object has ``plot`` and ``add_pawn`` methods.
Now it means that every ``TicTacToeBoard`` object and every ``ConnectFourBoard`` object
has a ``plot()`` method, even though we don't define it in them anymore;
they just have all the methods defined in the ``Board`` class.
We say that classes ``TicTacToeBoard`` and ``ConnectFourBoard`` **inherited** the method ``plot``.

Let's see how it works in practice::

    tic_tac_toe = TicTacToeBoard()
    connect4 = ConnectFourBoard()
    some_small_board = Board(2, 2)
    print("Tic-tac-toe board:")
    tic_tac_toe.plot()
    print("Connect Four board:")
    connect4.plot()
    print("Some board:")
    some_small_board.print()


It works!
Now every ``TicTacToeBoard`` will be a ``Board``, and every ``ConnectFourBoard`` will be a ``Board``,
but not every ``Board`` will be a ``TicTacToeBoard`` or a ``ConnectFourBoard``.
Anything that we want to be shared by ``TicTacToeBoard`` and ``ConnectFourBoard``  we can store in ``Board``;
anything that should be specific to ``TicTacToeBoard`` or ``ConnectFourBoard``, we will store in ``TicTacToeBoard`` or ``ConnectFourBoard``.

Additional task: add a method ``add_pawn(pawn, x, y)`` to the ``Board`` class.

What about the function ``__init__``, that appears in all the classes?
More important for python is the more specific one;
that is,  if we create an object ``ConnectFourBoard``,
the one defined inside the ``ConnectFourBoard`` definition will be used.
The one inside the ``Board`` is more general,
and would be used only if we define a sub-class of ``Board`` without its own ``__init__`` function.
Observe: ::

    class Some_Random_Board(Board):
        pass
        
    really_big_board = Some_Random_Board(20, 30)
    print(really_big_board.nrow)

The type ``Some_Random_Board`` is a subtype of ``Board``, so any instance of class ``Some_Random_Board`` is also a ``Board``.
Figuratively speaking: when we created it, python tried to use ``__init__`` method defined in the most specific class, that is ``Some_Random_Board``,
but it didn't find it there;
so it moved to the declaration of more general class, that is ``Board``,
and used ``__init__`` method from there.
The ``Some_Random_Board`` class inherits the ``__init__`` function.
On the other hand, when we created ``TicTacToeBoard``, python used method from ``TicTacToeBoard`` -
as you can see, we didn't have to provide ``ncol`` and ``nrow`` arguments, and python knew they should be equal to 3.

This has some important consequence: not all child classes must have all the methods from parent class exactly the same.
We've already seen that child classes of ``Board`` had different ``__init__`` methods.
We can create some other class, for example ``Chessboard``, that will be a child of ``Board``,
but will have it's own unique ``plot`` method, that will allow it to print black and white fields.
In such cases we say that ``plot`` method is **overridden** in ``Chessboard``.

Additional task: Make the ``add_pawn`` method check whether the move is legal.
In the general class ``Board`` it means whether the move is inside the board, and that's all.
Implement more specific cases for the other boards:
for ``TicTacToeBoard``, it should also mean the field cannot be already taken
(it's not always the case, for example in chess, so we shoudn't put in in general class),
and for ``ConnectFourBoard`` it means we can't place pawns if there is nothing below them
(Connect Four is actually played in a standing board, not a lying one, and the pawns fall down).
Try not to copy your code - if something is shared (like the condition "don't put your pawn outside a board") put it in the ``Board`` class.

The inheritance chain can be much longer than the one we created here.
We can create a class ThreeDimensionChessboard, that would inherit from the class Chessboard, that would inherit from class SquaredBoard, that would inherit from class Board.
Furthermore, it's possible to inherit from more than one class;
so, ThreeDimensionChessboard could inherit from both MultidimensionalBoard and Chessboard.
Bear in mind, however, that too complicated schemes of inheritance can be hard to understand, and therefore also hard to use.

