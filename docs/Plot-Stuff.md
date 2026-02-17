# Plot Stuff

There are a variety of ways you can create plots in tiles or notebooks. 
Any way you can convert a plot to html you can display it.

## Converting matplotlib plots to html

As described in [](#matplotlib-widgets) you can use a matplotlib widget.

```python
w = self.widget("matplotlib")
ax = w.fig.add_subplot(111)
ax.plot([1, 2, 3], [16, 25, 36])
w.set_html()
```

Then render the widget either with `return [w.render()]` in a tile or `w.show()` in a notebook.

Tactic also provides some tile commands that make it easy to convert
any matplotlib figure to html. You can use [create_figure_html](<./Tile-Commands.md#create_figure_html>) to 
convert a matplotlib figure to html.

```python
from matplotlib.figure import Figure
afig = Figure()
ax = afig.add_subplot(111)
ax.plot([1, 2, 3], [16, 25, 36])
self.create_figure_html(afig)
```

If you use matplotlib.pybplot to work in interactive mode, you can use
[create_pyplot_html](<./Tile-Commands.md#create_pyplot_html>) to convert your plot to html

```python
import matplotlib.pyplot as plt
plt.plot([1, 2, 3], [16, 25, 36])
self.create_pyplot_html()
```

## Matplotlib Tiles

If you create a tile with {menuselection}`New --> Matplotlib Tile`, you'll get a tile created with a template
that is set up to display a matplotlib plot. It has a method called draw_plot that handles all of the drawing
and returns the rendered widget. It also has a `handle_size_change` that `draw_plot` is called from, so that the 
plot will be redrawn when the tile is resized. This is generally a good pattern for creating plots in tiles.

## Dark Theme

Matplotlib tiles can look ugly if you're using the Tactic dark theme.
If, like me, you are bothered by such things, you can write your tile so
that it automagically uses different colors depending on the theme.
I've created a matplotlib style called "tactic_dark" that is specifically
designed for the Tactic dark theme.

```python
import matplotlib.pyplot as plt
use_dark = Settings["theme"] == "dark"
if use_dark:
    plt.style.use('tactic_dark')
else:
    plt.style.use('default')
```