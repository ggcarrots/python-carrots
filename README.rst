========================
Code Carrots tutorials
========================

Python tutorials for newbies in programming.
Written for workshops orginised by Geek Girls Carrots.

Loose outline

#. Installing Python and setting up development environment
#. Python basics
#. Data structures, loops, functions
#. Creating classes
#. Going further...


Build instructions
==================

Just run::

    $ pip install -r requirements.txt
    $ make html

Documentation should be created in ``build/html`` directory.

Print version
-------------

For print version you will need XeTeX engine (because PDFLatex doesn't support
Unicode, go figure)::

    $ make latex
    $ cd build\latex

    # Open workshops.tex and remove '\DeclareCharacter' directive
    $ xelatex workshops.tex


Why Python 3?
=============

Because it's the future. Also, Python 3 makes it possible to skip the
whole section of the tutorial describing Unicode and character
encodings in general. There is no use in scaring newbies from the
start.


Contributing
============

Please do!

Code Carrots guides and related software are free works: you can
redistribute them and/or modify them under the terms of the GNU
General Public License as published by the Free Software Foundation
version 3 with the additional attribution requirements. See
``LICENSE`` file at the root of the source directory for details.
