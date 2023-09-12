The Pool
===================

The basic idea here is pretty simple: the Pool provides you with permanent global disk space, accessible across all
of your tiles and notebooks.

.. warning::

    This is an advanced feature, currently only available to some users.

If you have access to the Pool, then it will appear in your sidebar, as shown in the image below.
Clicking on it brings up a tree-like image of your pool storage.

.. image:: images/pool_interface.png
   :scale: 40 %
   :align: center

You can use the menus to add a delete things from your storage, rename things, etc. I don't think I've implemented
download yet. That actually seems fairly important.

From notebooks and tiles, you can access pool files, using the standard python commands for opening and reading files,
with paths that all begin with "/mydisk" (as illustrated in the tree). You can also open a console in any tile or
notebook and use it to navigate your pool using standard linux commands.

There is also a new tile option called :ref:`pool_select. <pool-select>` which allows
the user to select a file or folder from their pool.
