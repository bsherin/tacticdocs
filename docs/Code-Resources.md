# Code Resources

One of the main goals of Tactic is make it easier to reuse code snippets at different grain sizes.
Tile provide one method for code reuse. Code resources provide some additional methods.

A code resource looks just like raw python code. You can import a code resource into your tile
or notebook as if it was a module, using `tactic_import`. For example:

```python
tactic_import("flatten_snippet")
l = [[1, 2, 3], [4, 5, 6]]
new_l = flatten_snippet.flatten(l)
```

or you can write this this:

```python
tactic_import("flatten_snippet")
from flatten_snippet import flatten
l = [[1, 2, 3], [4, 5, 6]]
new_l = flatten(l)
```

You can also create functions and
classes inside of code resources that can be used independently,
without reference to the containing code resource.

A code resource can contain multiple functions and classes, if you like.

```python
@user_function
def test_function():
    return "hello2"

@user_class
class TestClass(object):
    def __init__(self):
        self.my_var = "some text"

    def return_it(self):
        return self.my_var
```

As shown above, you use the decorator `@user_function` to declare a
user function, and `@user_class` for classes.

The [tile commands](tile-commands.html) section of this documentation
explains how to access user functions and classes.

You can assign **tags** to code resources, just like with any other
resources in your library. This is important, because access to
functions will sometimes depend on these tags. But note that the tags
given to a code resource apply to all of the functions and classes in the
entire code resource.
