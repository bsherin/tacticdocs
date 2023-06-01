Library Interface
===================

This Library interface is what you see when you use to manage the resources in your library,
such as the data you upload, and the tiles you create or import. It is also from here that you can launch viewers
and editors of those resources. Here it is, with the :guilabel:`Tiles` area in the library selected.

.. figure:: images/bplibrary_interface4.png

Here's a little tour:

The sidebar
-------------

.. image:: images/sidebar2.png
   :scale: 40 %
   :align: center

The sidebar, on the left, includes a link to your library, as well as to the panes with each of
your currently opened resource.

In the image above, there are currently two resources open, a project named "spam_project"
and a tile named "HelloWorld." You can click on one of these to go to the associated pane. You can also close or
reload one of these resources using the little icons next to each name.

Filtering
-------------

.. image:: images/library_filters.png
   :scale: 40 %
   :align: center

You can filter the resources visible in a variety of ways. Clicking on one of the colored icons
will filter by resources type. These are, from left to right:

1. All. This shows all resource types.
2. Data Collections. This is your raw data.
3. Projects. This is where you access your in-progress projects. You can also create new notebooks here.
4. Tiles. Your tile modules.
5. Lists. Your lists, obviously.
6. Code resources. These are explained a bit :doc:`here. <Working-With-Code-Resources>`

The switches behave as follows;

* :guilabel:`metadata`. Include metadata in the search

* :guilabel:`inside`. Search inside the content of resources. This only works for some resource types.

* :guilabel:`show hidden`. Show resources that have the ``hidden`` tag.

The menubar
-------------

Across the top is a menubar with a number of menus. I think these will mostly be self-explanatory.
They do things such as let you view a resource, delete it, combine resources, etc.

The tag tree
--------------

Just to the right of the sidebar is the tag tree. You can learn more about how this tree gets populated
:doc:`here. <Working-With-Tags>` Clicking on a tag in the tree filters the list of resources you see in the table.

Some tags are special. You can read about them :ref:`here. <special-tags>`

One thing that might not be obvious is that you can :kbd:`Right-Click` (or :kbd:`Control-Click`) on a tag to get
a context menu that will let you edit or delete a single tag.

The central table
---------------------

This is where you view your list of resources. You can select a resource here.

You can also select multiple rows. A subset of the toolbar functions can operate on multiple resources.
Also, you can edit the metatdata for multiple
resources in this way. This is useful, for example, to want to apply a tag to a bunch of resources.

You can type in the search field above the table to filter the list of resources. Also, for some resource types,
there are switches that allow you to search :guilabel:`inside` a resource or search the :guilabel:`metadata`
associated with a resource.

You can also :kbd:`Right-Click` (or :kbd:`Control-Click`) on a row in the table to access a context menu. The available
functions replicate a subset of the functions available in the menubar.

The omnibar
-------------

Typing :kbd:`Ctrl-Space` brings up the omnibar. Start typing to select from a list of resources in the current tab.
Then press enter to select and view a resource. All hail the awesome `omnibar. <https://blueprintjs.com/docs/#select/omnibar>`__

.. warning::
    The omnibar has not been updated for a while, and it doesn't yet behave naturally within the single-window interface.

The metadata editor
---------------------

Finally, on the ride side of the library interface is a panel where you can view and edit the metadata associated with
the selected resource.

Keyboard shortcuts
---------------------

Actually, I forgot something else. There are a few handy keyboard shortcuts in the Library:

:kbd:`Tab`

    Cycle forward through the sidebar panes. (For these purposes, the Libray is treated as a single pane.)

:kbd:`Shift-Tab`

    Cycle backward through the sidebar panes.

:kbd:`Arrow-Up`, :kbd:`Arrow-Down`

    Move the selected row up or down.

:kbd:`space`, :kbd:`enter`

    View the selected resource.

:kbd:`Ctrl-Space`

    Show the omnibar.
