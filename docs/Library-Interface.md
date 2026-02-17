# Library Interface

This Library interface is what you see when you use to manage the resources in your library,
such as the data you upload, and the tiles you create or import. It is also from here that you can launch viewers
and editors of those resources. Here it is, with the {guilabel}`Tiles` area in the library selected.

:::{figure} images/library_interface.png
:::

Here's a little tour:

## The sidebar

The sidebar, on the left, includes a link to your library and to the pool, as well as to the panes with each of
your currently opened resources. The list of panes can be manually sorted. Panes can be closed or refreshed
from here.

## Filtering and Columns

Clicking on the filter icon about the resource list shows the filtering bar.

```{image} images/library_filters.png
:align: center
:scale: 75 %
```
The {guilabel}`Resources` dropdown lets you filter by resource type.

The switches behave as follows;

- {guilabel}`Search Metadata`. Include metadata in the search.
- {guilabel}`Search Inside`. Search inside the content of resources. This only works for some resource types.
- {guilabel}`Show Hidden`. Show resources that have the `hidden` tag.

The icon to the right of the filter icon brings up a dropdown that lets you select which columns are visible.

## The menubar

Across the top is a menubar with a number of menus. I think these will mostly be self-explanatory.
They do things such as let you view a resource, delete it, combine resources, etc.

## The tag tree

Just to the right of the sidebar is the tag tree. You can learn more about how this tree gets populated
{doc}`here. <Working-With-Tags>` Clicking on a tag in the tree filters the list of resources you see in the table.

Some tags are special. You can read about them {ref}`here. <special-tags>`

One thing that might not be obvious is that you can {kbd}`Right-Click` (or {kbd}`Control-Click`) on a tag to get
a context menu that will let you edit or delete a single tag.

## The central table

This is where you view your list of resources. You can select a resource here.

You can also select multiple rows. A subset of the toolbar functions can operate on multiple resources.
Also, you can supposedly edit the metatdata for multiple
resources in this way. This is useful, for example, to want to apply a tag to a bunch of resources.
I'm not sure it works now though.

You can also {kbd}`Right-Click` (or {kbd}`Control-Click`) on a row in the table to access a context menu. The available
functions replicate a subset of the functions available in the menubar.

## The metadata editor

Finally, on the ride side of the library interface is a panel where you can view and edit the metadata associated with
the selected resource.

## Keyboard shortcuts

Actually, I forgot something else. There are a few handy keyboard shortcuts in the Library:

{kbd}`Tab`

> Cycle forward through the sidebar panes.

{kbd}`Shift-Tab`

> Cycle backward through the sidebar panes.

{kbd}`Arrow-Up`, {kbd}`Arrow-Down`

> Move the selected row up or down.

{kbd}`space`, {kbd}`enter`

> View the selected resource.

{kbd}`Ctrl-Space`

> Show the omnibar.
