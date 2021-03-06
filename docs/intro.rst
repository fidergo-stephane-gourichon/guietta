
Introduction
============

The problem with GUIs
---------------------

If you have worked with any GUI framework, like the excellent QT library,
you will have noticed a very common problem: in order to make
difficult things possible, simple things become difficult.

Guietta makes simple GUIs *simple*. For example, suppose that you want to
make a GUI where the user enters two numbers, and when a button is
clicked some complicated operation is performed, say, the numbers
are added up, and the result displayed back to the user.
With plain QT, you have two choices:

1. Start Qt Designer up and build your GUI using drag and drop. Designer saves
   an .ui file, which can be converted using pyuic to a python module,
   which can be imported into your program....
2. Skip Designer and do things
   programmatically: create a layout, then create your three or four widgets,
   then add them to the layout. Ah wait, should we build a row with
   HBoxLayout and join several of them into a VBoxLayout, or is it the
   other way around? How things are going to line up?
 
It's not over. In both cases, now define a function that does
the calculation, connect the right signal to the right slot (what was the
signal name again?), etc etc....

I've given up already.

Using Guietta's compact syntax, here is how the layout looks like::

    from guietta import _, Gui, Quit
    
    gui = Gui(
        
      [  'Enter numbers:', '__a__'  , '+' , '__b__',  ['Calculate'] ],
      [  'Result:  -->'  , 'result' ,  _  ,    _   ,       _        ],
      [  _               ,    _     ,  _  ,    _   ,      Quit      ] )
    
   
can you *see* the GUI? Right in the code? We can add then the behaviour
with a few more lines::

    with gui.Calculate:
       gui.result = float(gui.a) + float(gui.b)
        
    gui.run()


That's enough to get it working! That was 11 lines in total, including
a few blank ones for clarity.

And here is the result on my computer:

.. image:: example.png

It's *that* simple.

.. note:: for IPython users: if you type the previous example on the command
          prompt, it may or may not work (it appears to work on recent
          ipython versions). IPython does strange things
          with the command history. If it does not work, put the example
          into a file and run it.

What Guietta is
---------------

Guietta is actually a thin wrapper over QT. It allows one to quickly
create QT widgets, assemble them into a layout, and make it responsive
to user input. All standard QT features are available, including
signals/slots and the event loop, so if you know enough QT,
you can do some pretty amazing things.

And if you have a big graphical program with multiple windows and pop-ups,
you can use a subset of Guietta to simplify the window creation where
it makes sense.

It also works in the other direction: if you have a big complicated custom
QT widget, and you need to insert it into a dialog together with some
more buttons, Guietta can do that too.

What Guietta is not
-------------------

Guietta is a tool for making *simple* GUIs. You will not able to use it
to make the next version of Photoshop, not even the next version of
MS Paint. It does not do super-fancy layouts, or cinema-like animations.

Aren't you just copying from PySimpleGUI?
-----------------------------------------

PySimpleGUI is a much bigger project with a bigger goal: produce a
GUI framework that can work with multiple interfaces (QT, TKinter, even
web-based) and is easy to use for the beginner. PySimpleGUI's simplified
syntax was a great idea and it was the inspiration for Guietta,
but it stopped to soon. Guietta goes much further in simplifying things,
and as a result it has less features than PySimpleGUI.

The layout doesn't respect PEP8!
--------------------------------

Alas, no. Laying out GUIs with code was not foreseen when PEP8 was written.

Next topic: the `tutorial <tutorial.html>`_.


