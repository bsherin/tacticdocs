The Tile Creator
================

Welcome to the future of tile creation.
The Tile Creator is the editor that provides a more scaffolded
environment for creating and editing tiles.

Creating the new tile
---------------------

With that said, here’s how to create a new tile with the creator:

Go to the :guilabel:`tile` tab of your resource library and click :menuselection:`+creator --> StandardTile`.

.. figure:: images/bpcreate_in_creator.png

When prompted give your tile some sort of useful name. Then you should
see something that looks like this:

.. figure:: images/bpstarting_creator_view.png

Writing the tile body
---------------------

The large box on the left-hand side is where you write the code that
will be the ``render_content`` method in your new tile. In short, what
you need to understand is that this bit of python code must return the
html that will be displayed in your tile. Thus, the last line in the box
should be a ``return`` statement.

So, for example, if you change the content of the box to be:

.. code:: python

    new_html = "hello world"
    return new_html

Then you will have a tile that simply prints “hello world” on its face.

Remember that the text you display can be any valid html and will be
displayed as such. So, for example, if you instead write this:

.. code:: python

    new_html = "<b>hello world</b>"
    return new_html

Then you’ll instead have a tile that display “hello world” in bold text.

For its styling, Tactic uses the awesome `blueprint <https://blueprintjs.com/docs/>`__ project.
That means you can use blueprint's special CSS styles in the html that your tiles produce. For example,
if there is a button on the front of your tile, giving that button the class "bp3-button" will cause
the button to be styled in the manner of blueprint.

In writing your tile, you have access to a number of tactic-specific
commands that, for example, give you access to your data. These are
described in some detail here: `Tile Commands <Tile-Commands.html>`__.

You can use these `Keyboard Shortcuts <Module-Viewer-Keyboard-Shortcuts.html>`__ within the box
containing your code.

Finally, typing :kbd:`ctrl-space` while in the code area brings up the
autocomplete widget. This will prompt you with various useful
possibilities, including the Tile Commands

You can also import and make use of a number of `scientific libraries <Tile-commands.html#scientific-libraries>`__.

Go to the relevant web sites for documentation on these libraries.

Specifying tile resources
-------------------------

The area on the right-hand side of the interface allows you to create
and edit various resources and metadata for your tile.

.. figure:: images/bpmetadata_pane.png

metadata
~~~~~~~~

The :guilabel:`metadata` is where you specify a bit of metadata for your tile.
The “Category” field determines the menu under which your tile will
appear in the main project environment.

options
~~~~~~~

The :guilabel:`options` tab is where you specify `Tile
Options <Tile-Structure.html#options>`__ that will appear on back of your
tile. Here I have clicked on the options tab and then used the form at
the bottom to create an option called ``some_user_text``.

.. figure:: images/bpcreator_options.png

These option can now be referred to in the tile code as
``self.some_user_text``. So if you then change your code to be:

.. code:: python

    new_html = "<b>" + self.some_user_text + "</b>"
    return new_html

You can reorder the options in the table that appears in the options pane
by clicking and dragging the number at the start of the row that you want to move.

The button that looks like a trash can deletes the selected option. The button
that looks like a bulleted list converts the list of options to some markdown
that will display nicely, and copies it to the :guilabel:`notes` field in the metadata pane.

There are many different types of options as described here: `Tile
Options <Tile-Structure.html#options>`__. there’s an extra step required in
making use of some of these options (``list_select``, ``pipe_select``,
``function_select``, ``class_select``). In these options, the variable
you get contains only the name of the selected resource. To extract the
value you have to use one of the tile commands described
`here <Tile-Commands.html#other>`__. For example
``self.get_user_list(list_name)`` returns the actual list referred to.

exports
~~~~~~~

You can also specifythe name of parameters that will be :guilabel:`exports` for
your tile. (Exported parameters are available as pipes within other tiles.
Note that these must be instance variables assigned values in your code
in this manner ``self.variable_name =  ...``. ) Also, note that the tile creator
adds exported variables to the list of parameters that are saved when a project is saved.

The interface for this is pretty much the same as for the :guilabel:`options` pane.

methods
~~~~~~~

The :guilabel:`methods` tab displays additional methods defined within a tile
class. This is for advanced users. But if you use the tile creator to
look at existing tiles they will often have methods that are visible
here. You can define new methods that will be accessible in your tile.
For example, you could define a method ``my_method`` like so:

.. code:: python

    def my_method(self, avar):
        return myvar + 2

All methods that you define need to have ``self`` as the first argument.

Creating Matplotlib Tiles
-------------------------

You can use the Tile Creator to make tiles that display matplotlib
figures. If you open an existing matplotlib figure or create a new one
from your resource manager, then the Tile Creator opens with a slightly
different interface. Rather than having one large box for code on the
left, there are two. The bottom one holds the code for the
``render_content`` method. The other holds the code for the
``draw_plot`` method, which all matplotlib tiles must have.

This is explained a bit `here <Matplotlib-Tiles.html>`__.

Creating D3 Tiles
-----------------

You can also use the Tile Creator to make tiles that display interactive
D3 figures. If you open an existing D3 figure or create a new one from
your resource manager, then the Tile Creator opens with a slightly
different interface. Rather than having one large box for code on the
left, there are two. The bottom one holds the ``render_content`` method.
The top one must hold the body of a function that will be passed the
arguments `selector`, `w`, `h`, and `arg_dict`.

Also, ``render_content`` must return a dictionary of arguments that will
be passed to the javascript function in ``arg_dict``.

This is explained a bit `here <D3-Tiles.html>`__.

