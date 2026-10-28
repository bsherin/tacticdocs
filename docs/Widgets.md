# Widgets

If you have read other parts of this document, you have learned that the display on the front of a tile
is determined by html returned by the `render_content` method. The same is true for the return value of cells
in a notebook.
This can html elements that are interactive, such as buttons and text boxes.
However, this makes it awkward to make tile displays that are truly interactive.

As an alternative, you can return _widgets_. Here's what that can look like in a tile:

```python
def render_content(self):
    my_text_widget = self.widget("text", {"value": "some text"})
    return [my_text_widget.render()]
```

The first line here creates a text widget. 

The second line renders the widget and returns it as an element in a list.
You can also return multiple widgets in a list, and they will be displayed one above the other.

The power comes from the fact that once a widget is created, you can easily change it's `value` property from code
in a way that will be reflected dynamically. For example:

```python
def render_content(self):
    my_text_widget = self.widget("text", {"value": "some text"})
    ds([my_text_widget.render()]) # immediately renders and displays the widget
    # do some stuff here
    my_text_widget.value = "some new text" # this will update the widget display to this new text
    # do some more stuff here
```

The general syntax for creating a widget is `self.widget(widget_kind, widget_data, **kwargs`).

The `widget_kind` is a string that specifies the type of widget you want to create. The `widget_data` is a
dictionary that contains parameters that define the widget. You can also specify parameters as keyword arguments. 
Under the hood, `widget_data` and `**kwargs` are merged together, so you can use either one to specify any parameters.

Actually, you can dynamically set properties other than `value` as well.
So for example, you could change the `options` property of a select widget to change the options that are displayed in the dropdown menu.
To do those other properties you have to do it using the more general set command, which takes a dict of properties to set. 
So for example, you could do `my_select_widget.set({"options": new_options_list})` to change the options of a select widget.

:::{note}
Where styles are specified, they can be in camel case or in kebab case. 
So for example, you could specify a background color like this: `{"background-color": "red"}` or 
like this: `{"backgroundColor": "red"}`. Both will work.
:::

(widgets-in-creator)=
## Creating widgets in the Tile Creator

If you define widgets in the Tile Creator, that creates a set of widget specs that are saved in your tile definition.
Then, when the tile is loaded, widgets are created for each of those specs and attached to the tile instance.
So if you define a widget in the Tile Creator with the name`my_widget`, you can access that in your code 
with `self.my_widget`. 

You can then render one of these widgets manually in your code as usual. Also, if you call `self.render_all_widgets()`
in your code, all of the widgets defined in the Tile Creator that have `to_render=True` will be rendered.

## Widget kinds

These are the currently available widgets, along with the parameters they accept. 
Note that the blueprintjs library is used to render the
widgets in the browser. So you might learn more in some cases by referring to the documentation for that 
library for the corresponding widget: <https://blueprintjs.com/docs/>.

All widgets also accept a `to_render` parameter that is a boolean that determines whether the widget will
be rendered when `self.render_all_widgets()` is called.

- **text**. Display a string of text.
  - _value_: The text to display.
  - _ellipsize_: Whether to truncate the text with an ellipsis if it gets too long.
  - _style_: A dictionary of styles to be applied.
- **table**. Display an interactive table of data
    - _value_: The table of data. This can be in the form of pandas Datframe, a list of dicts, a TacticDocument,
    an nltk FreqDist, a dict, a list, or a pandas Series.
    - _maxColumnWidth_ (default=None):
    - _expandRows_ (default=False): Whether rows begin expanded.
    - _maxRows_ (default=50):
    - _className_ (default=""):
    - _style_ (default={}): A dictionary of styles to be applied.
- **slider**. Displays an interactive slider.
  - _value_ The current value of the slider.
  - _on_change_ A function that will be called when the slider value changes. 
  This function should take a single argument, which will be the new value of the slider.
  - _min_ (default=0):
  - _max_ (default=10):
  - _stepSize_ (default=1): 
  - _labelStepSize_ (default=1)
  - _style_ (default={}): A dictionary of styles to be applied.
- **progressBar**. Display a progress bar.
    - _value_: The current value of the progress bar. This should be a number between 0 and 1.
    - _style_ (default={}): A dictionary of styles to be applied.
    - _helperText_ (default=None): A string of text that will be displayed under the widget.
    - _stripes_ (default=False): Whether the progress bar should have stripes.
    - _intent_ (default="primary"): The intent of the progress bar. This can be one of None, "primary", "success", "warning", or "danger".
    - _style_ (default={}): A dictionary of styles to be applied.
- **html**. Displays raw htmls.
  - _style_ (default={}): A dictionary of styles to be applied.
- **iframe**. Creates an iframe with data.
  - _value_: A inline string containing html that will be the srcDoc for the iframe.
  - _style_ (default={}): A dictionary of styles to be applied.
- **divider**. Creates a horizontal divider.
  _compact_: Passes the compact parameter to blueprintjs. But doesn't seem to do anything.
  - _style_ (default={}):
- **button**. Crates a button.
  - _value_: The value that will be provided when the button is pressed.
  - _text_ (default="Button"): The text to display on the button.
  - _on_click_: A function that will be called when the button is clicked. This function should take a single argument, which will be the value of the button.
  - _icon_ (default=None): The name of a blueprint icon to display on the button. For example, "add" or "delete".
  - _helperText_ (default=None): A string of text that will be displayed under the widget.
  - _fill_ (default=False): Whether the button should expand to fill its container.
  - _variant_ (default="solid"): The variant of the button. This can be one of "solid", "minimal", or "outlines".
  - _style_ (default={}): A dictionary of styles to be applied.
- **switch**. Displays a switch that can be toggled on and off.
  - _value_: The current value of the switch. This should be a boolean.
  - _on_change_: A function that will be called when the switch value changes. This function should take a single argument, which will be the new value of the switch.
  - _label_ (default="switch"): The label to display next to the switch.
  - _style_ (default={}): A dictionary of styles to be applied.
- **select**. Displays a dropdown select menu.
  - _value_: The current value of the select menu. This should be a string that matches one of the values in the options list.
  - _on_change_: A function that will be called when the select value changes. This function should take a single argument, which will be the new value of the select menu.
  - _options_: A list of options to display in the select menu. Each option can be a string or a dict with "label" and "value" keys.
  - _label_ (default="select"): The label to display next to the select menu.
  - _style_ (default={}): A dictionary of styles to be applied.
- **multi_select**. Displays a menu where users can select multiple options.
  - _value_: The list of select items.
  - _on_change_: A function that will be called when the select value changes. This function should take a single argument, which will be the new value of the select menu.
  - _options_: A list of options to display in the select menu. Each option can be a string or a dict with "label" and "value" keys.
  - _label_ (default="select"): The label to display next to the select menu.
  - _style_ (default={}): A dictionary of styles to be applied.
- **pool_select**. Displays an interface for selecting an item from the pool.
  - _value_: The path to the selected item..
  - _on_change_: A function that will be called when the select value changes. This function should take a single argument, which will be the new value of the select menu.
  - _select_type_: (default="both") This can be "both", "file", or "folder". It determines what types of items can be selected.
  - _label_ (default="pool select"): The label to display next to the select menu.
  - _style_ (default={}): A dictionary of styles to be applied.
- **input**. Displays an input box where users can type text.
  - _value_: The current value of the input box. This should be a string.
  - _fill_: (default=False): Whether the input box should expand to fill its container.
  - _inline_: (default=False): Whether the input box should be displayed inline with its label.
  - _on_change_: A function that will be called when the input value changes. This function should take a single argument, which will be the new value of the input box.
  - _helperText_ (default=None): A string of text that will be displayed under the widget.
  - _label_ (default="input"): The label to display next to the input box.
  - _style_ (default={}): A dictionary of styles to be applied.
- **integer**. Displays an input box where users can type an integer.
  - _value_: The current value of the input box. This will be an integer.
  - _fill_: (default=False): Whether the input box should expand to fill its container.
  - _inline_: (default=False): Whether the input box should be displayed inline with its label.
  - _helperText_ (default=None): A string of text that will be displayed under the widget.
  - _on_change_: A function that will be called when the input value changes. This function should take a single argument, which will be the new value of the input box.
  - _label_ (default="integer"): The label to display next to the input box.
  - _style_ (default={}): A dictionary of styles to be applied.
- **float**. Displays an input box where users can type a float.
  - _value_: The current value of the input box. This will be an float.
  - _fill_: (default=False): Whether the input box should expand to fill its container.
  - _helperText_ (default=None): A string of text that will be displayed under the widget.
  - _inline_: (default=False): Whether the input box should be displayed inline with its label.
  - _on_change_: A function that will be called when the input value changes. This function should take a single argument, which will be the new value of the input box.
  - _label_ (default="float"): The label to display next to the input box.
  - _style_ (default={}): A dictionary of styles to be applied.
- **box**. A widget that organizes other widgets. It takes a list of widgets and displays them in a div element to which th
the given style is applied.
  - _widgets_: A list of widgets to display.
  - _style_ (default={}): A dictionary of styles to be applied.
- **collapse**. A widget that organizes other widgets into a collapsible section.
  - _widgets_: A list of widgets to display.
  - _label_: The label that will appear on the button that expands the section.
  - _startOpen_ (default=True): Whether the section should be expanded by default.
  - _intent_ (default="primary"): The intent of the button that expands the section.
  - _style_ (default={}): A dictionary of styles to be applied.
- **matplotlib**. Displays a matplotlib figure. See below for a full discussion.
  - _style_ (default={}): A dictionary of styles to be applied.
  - _use_svg_ (default=False): Whether to render the figure as an svg.
  - _dpi_ (default=96): The dpi to use when rendering the figure, is use_svg is False.
- **javascript**. Displays a widget with executing javascript code. See below for a full discussion.
  - _value_: A value, typically a dict, that will be passed to the javascript code.
  - _function_name_: The name of a javascript function, defined in the Tile Creator. When set, the function code will be copied into the `code` parameter.
  - _code_: A string of javascript code to execute. This is just the body of the code.
  - _style_ (default={}): A dictionary of styles to be applied.

(matplotlib-widgets)=
## Matplotlib widgets

Using the matplotlib widget is just a little more complicated. First you create it. 
The created wdiget will have a matplotlib Figure object as its `fig` property. 
You can then use that figure object to create an axis and plot on it. Finally, 
before rendering the widget, you have to call the `set_html` method of the widget.

Here's how that looks:

```python
w = self.widget("matplotlib")
ax = w.fig.add_subplot(111)
ax.plot([1, 2, 3], [16, 25, 36])
w.set_html()
```
(javascript-widgets)=
## Javascript widgets

The javascript widget lets you create a widget that executes javascript code in the browser.

The function will ultimately have the signature `function myFunction(selector, w, h, value, setValue, resizing)`.
You pass the **body** of this function as a string in the `code` parameter. 
The `value` parameter this javascript function receives is the value of the `value` parameter of the widget.

Alternatively, if you define a javascript function in the Tile Creator, you can specify the name of that function in the `function_name` parameter. 
Then, when the Tile Creator builds the tile, the code for that function will be copied into the `code` parameter of the widget.

You can also set the `function_name` parameter at run time. If you do that, the code for that function will be copied into the `code` parameter of the widget.

The widget will re-render in the browser whenever its `code` changes, its `value` changes, or the tile resizes.

A javascript function might look like this:

```javascript
function showMessage(selector, w, h, value, setValue, resizing) {
    document.querySelector(selector).innerHTML = value;
}
```

## Widgets in the notebook

You can use widgets in a notebook pretty much just like in a tile. There is one critical
different however. Rather than returning `[my_widget.render()]` you instead execute
`my_widget.show()` from anywhere in a cell as it runs, and the widget will be displayed immediately.
