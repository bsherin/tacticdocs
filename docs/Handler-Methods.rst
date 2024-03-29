Handler Methods
===============

Various events lead to the calling of handler methods in a tile.
For example, if a user changes the size of a tile, a ``TileSizeChange`` event is generated, which
in turn leads to the calling of the handler ``handle_size_change()``. The ``TileBase`` class
has default handlers for all of these events, but some of them don't do anything.

Your tile can choose to include its methods to handle these events.
For example, you might do something like this.

.. code-block:: python

    def handle_size_change(self):
        new_html = self.draw_plot()
        self.display_status(new_html)
        return

In the case of the ``handle_size_handler``, no additional arguments are passed. But as noted below,
some handlers are passed arguments.

.. category_start

Clicks on Tile Front
--------------------

    Many of the handler calls are generated when the user interacts with the front of a tile.
    This can happen if, for example, you have displayed a button on the front of the tile.

    In addition to passing information specific to the event, many of these handlers
    are also passed the name of the currently visible document as well as the currently selected
    row in that document.

    .. py:method:: handle_button_click(self, value, doc_name, active_row_index)

        A call to this handler is generated when the the user clicks a button within the body
        of a tile. ``value`` is the button value. The default handler has no effect.

        For example, your ``render_content`` method could add a button to the html it displays
        like this:

        .. code-block:: python

            the_html += "<button value='{0}'>{1}</button>".format (val, txt)

    .. py:method:: handle_select_change(self, value, doc_name, active_row_index, select_name)

        This handler is called when the user changes the value of a select element
        in the body of the tile. ``value`` is the value selected. `select_name` is the value
        of the ``name`` property assigned in the html for your select component. The default
        handler does nothing.

    .. py:method:: handle_tile_row_click(self, clicked_row, doc_name, active_row_id=None)

        This handler is called when the user clicks on a row in a table that is displayed
        on the tile. Note that the row must have the class ``row-clickable``. This can be
        accomplished by calling :py:meth:`html_table` with ``click_type=row-clickable``.
        ``clicked_row`` contains a list of the values in the cells in the row. The default handler does nothing.

    .. py:method:: handle_tile_word_click(self, clicked_word, doc_name, active_row_id=None)

        This handler is called when the user clicks on a word on the front of the tile.
        Note that the word must be within an element with the class ``word-clickable``.
        The default handler selects all appearances of the clicked word in the main data table.

    .. py:method:: handle_form_submit(self, form_data, doc_name, active_row_index)

        Called when the user clicks submit in a form within the body of a tile.
        ``form_data`` is a dictionary in which the keys are the names of
        elements in the form, and the values are their current values. Note
        that one of these entries will correspond to the submit button
        itself. The default handler does nothing.

    .. py:method:: handle_textarea_change(self, value)

        Called when the user the user changes the contents of a textarea DOM
        element on the front of the tile. ``value`` is the new content of
        the textarea. The default handler does nothing.

.. category_end

.. category_start

Environment changes
---------------

    .. py:method:: handle_size_change(self)

        The size of the current tile has been changed by the user.
        The default handler does nothing.

    .. py:method:: handle_doc_change(self, new_doc_name)

        The visible document in the main data has been changed.
        The default handler does nothing.

    .. py:method:: handle_row_change(self, row_index, doc_name)

        A new row has been selected in the main table.
        The default handler does nothing.

    .. py:method:: handle_text_select(self, selected_text)

        The has selected text within the main table.
        The default handler does nothing.

    .. py:method:: handle_cell_change(self, column_header, row_index, old_content, new_content, doc_name)

        A cell in the main data table has been changed.
        The default handler does nothing.

    .. py:method:: handle_freeform_text_change(self, new_content, doc_name)

        The text of a freeform data table has been changed.
        The default handler does nothing.

    .. py:method:: handle_pipe_update(self, pipe_name)

        The value of a pipe has changed.
        The default handler does nothing.

    .. py:method:: handle_doc_change(self, new_doc_name)

        The visible document in the main data has been changed.


.. category_end

.. category_start

Dynamic Options
---------------

    .. py:method:: modify_options(self)

        Sometimes you might want the options in a tile to vary based on some conditions.
        For example, you might want some options to appear or disappear based on the value
        of another boolean option. This can be accomplished by adding a ``modify_options`` method
        to your tile.

        ``modify_options`` is run any time the form on the back of a tile is (re)generated. This includes
        any time that an individual option is changed on the back of a tile. It must
        return the options, suitably revised. Refer to `Tile Structure <Tile-Structure.html>`__ to see what
        how the options list should look.

        You can add a "visible" key to an item in the option list. If you do, this will determine whether the
        option is visible. (If there is no such key, the option will be visible.) You can also hide an option
        simply by not including it in the revised options.

        Here's an example pattern:

        .. code-block:: python

            def opt_requirements(self, opt_name):
                reqs = {
                    "folds": lambda : self.cross_validate,
                    "test_fraction": lambda : not self.cross_validate,
                    "svc_balance": lambda : self.algorithm == "SVC",
                    "neighbors": lambda : self.algorithm == "KNeighbors",
                    "neighbor_weights": lambda : self.algorithm == "KNeighbors",
                    "max_iter": lambda : self.algorithm == "MLP",
                    "max_ngram": lambda : not self.feature_type == "wordvec",
                    "vocab_size": lambda : not self.feature_type == "wordvec",
                    "wordvec_model": lambda : self.feature_type == "wordvec",
                }
                result = True
                if opt_name in reqs:
                    result = reqs[opt_name]()
                return result

            def modify_options(self):
                new_options = []
                for opt in self.options:
                    opt["visible"] = self.opt_requirements(opt["name"])
                    new_options.append(opt)
                return new_options

    .. py:method:: handle_option_change(self, opt_name, value)

        Called when the user changes an individual option on the back of a tile. ``opt_name``
        is the name of the option and ``value`` is the new value.

.. category_end

.. category_start

Other
-----

    .. py:method:: handle_tile_message(self, event_name, data)

        This handler is called when the a message is sent using the :py:meth:`send_tile_message` command.
        The default handler looks like this:

        .. code-block:: python

            def handle_log_tile(self):
                summary = "Log from tile " + self.tile_name
                self.log_it(self.current_html, summary=summary)
                return


    .. py:method:: handle_log_tile(self)

        The user has selected :guilabel:`Log me` from the tile menu.

        This handler is called when the a message is sent using the :py:meth:`send_tile_message` command.

.. category_end
