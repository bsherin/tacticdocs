Making Tiles
==================

Tile making basics
------------------

You can totally make your own tiles. Tactic tiles are represented as
Python classes. If you don't know what that means, it probably doesn't matter;
you should be able to do quite a lot understanding just a smattering of python.
(If you want the full story, you can look at the page on :doc:`Tile-Structure`.)

At it's very simplest, you can think of a tile as a some lines of Python ending ``return`` statement,
that returns some html. That's a tile's primary job: to
return some html to be displayed on the front of the tile. So this code

.. code-block:: python

    return "<b>Hello World</b>"

would display "Hello World" on the front of the tile in bold. More generally,
creating a tile requires defining the following elements, most of which are optional.

The ``render_content`` method
    Every tile must define include the code for the ``render_content`` method. This must end in a
    ``return`` statement, which returns a string containing html. This is the code that will be
    run when the user runs the tile.

Tile options
    These are the options that the user will see when they click on the gear symbol at top of a tile.

Exports
    These are tile attributes that are made available to other tiles via pipes, and to the exports viewer.
    So if you write ``self.my_attribute`` in your ``render_content`` code, and then list ``my_attribute`` as
    an export, then this value will be available via a pipe.

Additional methods
    As you'll see in the :doc:`Tile-Creator` documentation, you can define additional methods for your tile class.
    Partly, this is just a convenience; it's a way to keep your ``render_content`` code from becoming too cluttered.
    But this is also where you'll defined any special :doc:`Handler-Methods`.

Metadata
    Finally, you can attach metadata to your tile. This includes the same tags and notes you can attach
    to any resource. But it also includes a field that is specific to tiles called :guilabel:`Category`. This
    bit of metadata is what determines which tile menu your tile will appear on in the Main interface.

About the tile making tools
---------------------------

In the olden days, the only tool that we had available was the :doc:`Module-Viewer`.
It presents a tile, in its raw form, as a
python class. If you’re an accomplished python programmer, and
comfortable with python classes, then you might want to use this editor.
In addition, even if you aren’t comfortable with python classes, you
might have to use the Module Viewer to fix a tile that has somehow gotten into a bad
state, possibly because it has been garbled by the second editor,
which I will describe in the next paragraph.

Now, in our modern era, we have available to us the :doc:`Tile-Creator`. It’s
designed to provide much more scaffolding for the construction of tiles. At this point,
I pretty much only use the Tile Creator. So do not feel ashamed if you choose this path.

.. warning::
    If you do anything tricky in a tile created in the module
    viewer, there’s a chance it will be lost if you resave the tile from the
    Tile Creator.
