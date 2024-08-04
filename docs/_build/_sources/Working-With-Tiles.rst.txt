Working with tile instances
===========================

If you've just added a tile to a project, it will look something like this:

.. figure:: images/unconfigured_tile.png
    :scale: 40 %

At this point, the tile has not been configured or run. To configure the tile, you should click on the gear
symbol at the top left of its header. Then you'll see something that looks like this:

.. figure:: images/tile_options.png
    :scale: 40 %

Here you make choices that provide the parameters required by the tile. Then click submit and the tile will
close the options and execute tile (i.e., run the tile's ``render_content`` method).

.. figure:: images/tile_after_run.png
    :scale: 40 %

Now, if you click on the three dots at the top right of the tile's header, you'll get a very important menu,
as in the image below.

.. figure:: images/tile_with_menu.png
    :scale: 40 %

These menu items need some explanation.

* :guilabel:`Run me`. Reruns the tiles ``render_content`` method without changing options (or other elements of the
  internal state that might be lurking).

* :guilabel:`Stop me`. Attempts to stop a tile that is currently running its ``render_content`` method.

* :guilabel:`Kill and reload`. Thorough clears out a tile container. It reboots the container, loads the current
  current version of the tile's source from the library, and then displays the the tile's options.

* :guilabel:`Kill, reload, and resbumit`. Same as the above, except that the tile is immediately rerun
  with the previously used options.

* :guilabel:`Toggle console`. Shows and hides the tile's console. This is where the tile prints messages
  reporting on various aspects of its inner workings. You might never need to look here. But note that if you
  have a ``print`` statement in the code for your tile this is where the output will appear. This is handy for
  debugging.

* :guilabel:`Log me`. Copies the current visual contents displayed on the tile into the Log at the bottom of the
  Main Interface.

* :guilabel:`Log parameters`. Creates a table of the current option selections that copies it into the Log.

* :guilabel:`Edit my source`. Opens a new tactic pane in which you can edit the source code for the tile.

* :guilabel:`Delete me`. Deletes the tile instance from the project.

One last thing you might not guess: You can reposition tiles by clicking and dragging on the rows of vertical dots
to the left of the tile's name.