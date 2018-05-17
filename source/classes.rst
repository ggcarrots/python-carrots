===================
Objects and classes
===================

Every value is an object
------------------------

Every value that we have seen in Python, can be called **an object**. Each object can be assigned to
a variable (even functions) and/or passed to a function as an argument (yes, even other functions).
Similar objects share their functionality - number ``1`` has the same functionality as number ``2``, ``3`` and so on.
We saw earlier, when :func:`help`, acting on any number, printed for us dozens of additional lines of information about
:func:`int`.

Every object has a class
------------------------

We say that similar objects have the same **type**. Number ``1`` is of type ``int``, same as ``2`` and ``42``.
The type of an object is defined by its **class**
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

.. code-block::

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

Define classes
--------------

Classes like ``int`` or ``str`` are already known to Python, but we can create our own types.
This is called defining a class.

You can define your class as easy as you can define a function. In fact, a class is
basically nothing but a group of functions. Let's define a class named ``TicTacToeBoard``:

.. testcode:: simple-class

    class TicTacToeBoard(object):

        def plot(self):
            for row in range(3):
                print("   |   |   ")
    


Class definitions begin with the word :keyword:`class`, after which we give the name of the new class.
The ``(object)`` indicates that our new type ``TicTacToeBoard`` is a specific sub-type of an ``object`` class.
That is, instances of our class, i.e. variables created from it, will be of the type ``TicTacToeBoard`` and
also of the more general type ``object``.

This is another way of looking at the phrase *Everything in Python is an object*.
Each class is a specialization of ``object`` in Python. Every value has ``object``
as the most general type. And so, because it is the default behaviour, we can actually ommit writing it:

.. code::

    class TicTacToeBoard:
        # ...

We can create an instance of a class ``TicTacToeBoard``. Let's call it ``my_board``.
We can check it's type with :func:`type` function.
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

As you can see, you create an instance of a class just like you call a function
by writing it's name and then ``()``.
(Spoiler: there can be some arguments in those brackets! But we will talk about it later.)
Every instance of ``TicTacToeBoard``, like ``my_board``, has all the methods that we defined in that class.
Here that would be one method, called ``plot``.
You may have noticed that it has one weird argument ``self`` that we don't actually use in it.
It's important to remember that every method in the class must have at least one argument.
Its value is an object from which we have called this method -
that would be some instance of the class. This argument should be called ``self``
`by convention <https://www.python.org/dev/peps/pep-0008/#function-and-method-arguments>`_
(technically you could call it otherwise, but other programmers would be angry with you if you did).
Let's see how it works in practice:

.. testcode:: simple-class

    my_board = TicTacToeBoard()
    my_board.plot()

As you can see, you don't actually put any argument in the brackets while calling the method.
Rather, :func:`plot` uses the ``TicTacToeBoard`` instance that is before the dot.
The method knows that ``my_board`` should be its ``self`` argument.
Recall that we called some methods of lists and other objects the same way,
for example: ``my_list.append(4)``.


Attributes of objects
---------------------

Obviously, we don't want our board to stay empty all the time.
We want to be able to place crosses and noughts on the instances of our new class.
We want our board to remember where the crosses and noughts were placed,
and print itself accordingly.
This can be accomplished by giving our ``TicTacToeBoard`` instance some **attributes**, values assigned
to this specific object.

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
They both store list of tuples. Every tuple is a pair of coordinates where a nought or cross were placed.
As you can see, we can get to them by writing the name of our instance, a dot, and the name of an attribute.

Values of the attributes are something specific to the instance of a class.
That means, if we create a new instance of the class ``TicTacToeBoard``, it won't have the defined attributes.
We can assign them to it, of course, and they can be different than attributes of ``my_board``,
This won't affect the attributes of ``my_board``.
It's just like when we create different lists. We can put different values into every object.
Although they all are instances of the class ``list``,
and have all the methods specific for the class ``list``, each one is independent of another.

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
For that we need to modify the ``plot`` method:

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
We just told python to use attributes of the instance that called the method.
Recall that the instance is passed as ``self`` argument,
even though while calling the method we don't put the instance inside the parentheses. We put it before the dot.
So now the ``plot`` method, for every position, will check
if this position is in the attribute ``crosses`` of the instance that it has been called from.
The same with the attribute ``noughts``.
Let's see how it works:

.. testcode:: simple-class

    my_board = TicTacToeBoard()
    my_board.crosses = [(0, 0), (1, 1), (2, 2)]
    my_board.noughts = [(1, 2), (0, 2)]
    my_board.plot()

Great, now we have a way to plot crosses and noughts on our board!
But what if we forgot to define these attributes?
The ``plot()`` method wouldn't know what ``self.noughts`` or ``self.crosses`` are.
It won't even print an empty board, just return an error.
It would be better to assure that every instance of our class has these attributes.
Is there a way to do that? Yes!
We can define attributes of an object when it is created.
We need to tell Python that we want some specific stuff to happen
(in this case, we want to create some attributes)
when we initialise an instance of a ``TicTacToeBoard``.
We do that by adding a method ``__init__`` to the definition of the class.
It's a method that is called when an object is created, that's why it's called a **constructor**.
Actually, every class has this method defined, even if we don't do it ourselves.
So, when we typed ``my_board = TicTacToeBoard()`` python actually called a method ``__init__`` of a class ``TicTacToeBoard``.
We can define it ourselves and add what we need.

.. testcode:: simple-class

    class TicTacToeBoard:
        
        def __init__(self):
            self.crosses = []
            self.noughts = []
            

Now every time we create a new instance of the class TicTacToeBoard,
it already has the attributes ``crosses`` and ``noughts`` -
empty lists, ready to be filled.
Note that the constructor also needs the ``self`` argument,
even if we don't provide it neither inside the brackets, nor before the dot. 

Now that our boards can store coordinates of noughts and crosses,
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
so that it will check whether it is a legal move.
That is, whether the coordinates are inside the board and whether the field is free.
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
Let's put ``board`` in charge of checking whether the game should end or not.

# kod z funkcja check

Notice that in the while loop we do similar thing two times.
When we added checking, we needed to remember to add it in two places.
Also, if you added some checking if the move is legal,
you needed to put it in two different methods.
If we ever decide to do some small change, we need to do it in several places.
It seems like a lot of unnecessary work and and is error-prone.
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
Then, at the end, announce the winner.

Notice that we've cheated a little bit here -
to simplify constructing our prompt, we replaced customized phrase "Player 1" or "Player 2" with more general "Player".
We don't need to do that!
Thanks to classes we can more easily store some informations about players, like their name,
and refer to them accordingly.
Let's create a ``Player`` class:

.. code::

    class Player:

        def __init__(self, name, char='o'):
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
however when there is no need to call them differently, let's not do that.
After all, they mean the same thing.

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
two players move in turns, by placing some pawns on the board.
The goal is to have some number of pawns in one line.
Board can be printed in a simmilar manner, even though it has different size
(Connect Four is played on a board with 6 rows and 7 columns).
The whole game menu could be essentially the same.
What shall we do? Write it all from the scratch?
That would be a waste of time.
Maybe copy it all and just change the bits that we want to be different?
That would be a bad habit.
What if we want to change it later, for example - we have an idea how to improve printing of the board?
We would have to change it in both game implementations.
It would be nice if we could implement it once and then just use it in two different games.
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

Every instance of a class has all the methods defined in the definition of that class.
So far that meant that every ``TicTacToeBoard`` object has ``plot`` and ``add_pawn`` methods.
Now, after adding inheritance, every ``TicTacToeBoard`` object and every ``ConnectFourBoard`` object
has a ``plot()`` method, even though we don't define it in them anymore.
They have all the methods defined in the ``Board`` class.
We say that classes ``TicTacToeBoard`` and ``ConnectFourBoard`` **inherit** the method ``plot``.

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
Anything that we want to be shared by ``TicTacToeBoard`` and ``ConnectFourBoard``  we store in ``Board``.
Anything that should be specific to ``TicTacToeBoard`` or ``ConnectFourBoard``, we store in ``TicTacToeBoard`` or ``ConnectFourBoard``.

Additional task: add a method ``add_pawn(pawn, x, y)`` to the ``Board`` class.

What about the method ``__init__``, that appears in all the classes? Which one will be used during construction of an object?
Well, wehen we create an object ``ConnectFourBoard``, its constructor will be evoked, not its parent's.
The one inside the ``Board`` is more general, and would be used only if we define a sub-class of ``Board`` without its own ``__init__`` method.
Observe: ::

    class Some_Random_Board(Board):
        pass
        
    really_big_board = Some_Random_Board(20, 30)
    print(really_big_board.nrow)

The type ``Some_Random_Board`` is a subtype of ``Board``, so any instance of class ``Some_Random_Board`` is also a ``Board``.
When we created it, Python tried to use ``__init__`` method defined in ``Some_Random_Board``,
but it didn't find it there.
It moved then to the declaration of more general class, that is ``Board``, and used its ``__init__`` method.
We say that ``Some_Random_Board`` class inherits the ``__init__`` method.
On the other hand, when we created ``TicTacToeBoard``, python used constructor from ``TicTacToeBoard``.
We didn't have to provide ``ncol`` and ``nrow`` arguments, and python knew they should be equal to 3.

This has some important consequence: not all child classes must have all the methods from parent class exactly the same.
We've already seen that child classes of ``Board`` had different ``__init__`` methods.
We can create some other class, for example ``Chessboard``, that will be a child of ``Board``,
but will have it's own, unique ``plot`` method, that will allow it to print black and white fields.
In such cases we say that ``plot`` method gets **overridden** in ``Chessboard``.

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
Furthermore, it's possible to inherit from more than one class.
The ThreeDimensionChessboard could inherit from both MultidimensionalBoard and Chessboard.
Bear in mind, however, that too complicated schemes of inheritance can be hard to understand, and therefore also hard to use.

