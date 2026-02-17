# The Log and Notebook

As mentioned in the section on the {doc}`Main-interface`,
there is a component at the bottom of the screen called the Log. Tiles
can send information to the Log. The Log is also designed to be used more like a full-fledged
python notebook.

Furthermore, you can create projects that consist of nothing more
than a Notebook of this sort. There are two ways to create one of these
Notebook projects. First, from within the Main Interface, you can go to
the Project menu and select {guilabel}`open-console-as-notebook`. This will
start a Notebook project using the current contents of the Log.

The second way to create a Notebook project is from the Library
manager with {menuselection}`New --> New Notebook`.

Logs and Notebooks pretty much work the same way. Below, I'm going to use the word "Notebook," but all of this will
apply in both cases.

## Under the hood

In some important ways, the Log and Notebook *are* tiles. There is a (pretty much) standard tile container associated
with a Notebook. Most of the code that you can write in a tile can also be run in a notebook, including most of
the commands in the API, both object-oriented and standard.

## Notebook menus

There are a bunch of menus at the top of a Notebook. I think they are mostly self-explanatory, but I'll mention a few
points that might not be obvious. First, the edit menu has items that allow you to copy and paste cells within and
across projects. They act on any currently selected cells. (You can select multiple cells using {kbd}`shift-click`.

## Text cells

You create a text cell using the {guilabel}`insert` menu or the associated keyboard shortcut. As shown in the figure
above, each text cell has some buttons associated with it. These buttons become visible when hovering over the cell.

You can enter text as Markdown and Latex (see below). If you do,
clicking the convert button converts between raw and converted text.

Currently, the library that is used to do the conversion of the markdown to
html is [markdown-it](https://github.com/markdown-it/markdown-it).

The library used to convert Latex is
[markdown-it-latex](https://github.com/tylingsoft/markdown-it-latex).
Refer to the docs for these libraries for syntax specifics.

## Code cells

You create a text cell using the {guilabel}`insert` menu or the associated keyboard shortcut.

As mentioned above, code fields in Logs and Notebooks function like a tile.
You can write any code that you can write in a tile, which means you can
test code here, and that you have access to the whole tile API.
(However, some of these commands won’t make sense in Notebooks.)

Any local variables you introduce within a code field are added to a
global namespace. This means that these variables are shared across the code
fields in your Log/Notebook.

Like a tile, output here is treated as html. So you might need to add
html tags to get the output that you want. For example, you might want
to wrap your output in `<pre>..</pre>` tags.

You can also make plots and use widgets in code cells. More on this in {docs}`Widgets.md` and {docs}`Plot-Stuff.md`.

## Keyboard shortcuts

The normal [keyboard shortcuts](Module-Viewer-Keyboard-Shortcuts.html) work inside of code items.
In addition, {kbd}`Ctrl-Enter` and {kbd}`Cmd-Enter` will execute a cell. Those same two shortcuts,
executed inside of a text cell, will display the formatted text.

## The exports viewer

As discussed {ref}`here, <exports-viewer>` the exports viewer is always available on the right hand side of the
log and notebook. In addition to displaying any tile exports, the exports viewer displays any variables or
objects defined within a Notebook.
