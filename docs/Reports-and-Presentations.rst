Reports and Presentation
========================

The universe, such as we know it, can be divided into two large regions. One of these regions is constituted by
all of those things **inside** Tactic. The other region is those things **outside** of Tactic. Occasionally it is
necessary to leave the realm of Tactic, and venture forth into those other, lesser, realms. Fortunately,
it is possible to take the fruits of your Tactic labors with you, when you leave. There are multiple
methods for doing so.

First, you can always write code to create and fill a new collection object and export it to your library. This can then be
downloaded to your local computer. This is very general but can be laborious.

Alternatively, you can create reports and presentations. The relevant options are found in the  :menuselection:`Project` menu.
This options each take a log or notebook and convert it directly.
The result in both cases are standalone html files that can be viewed in a browser.

This should mostly be self-explanatory, but
there are a few special bits. First, any section that has the name `styles`, will be treated differently. Tactic
will look at the cells inside these sections and it will place there contents inside the standalone html files as
css. For example, you could have a markdown cell inside a `styles` with contents that looks like this:

.. code-block:: css

    ul {
        font-size: 36px;
        margin-top: 25px
    }
    ul ul {
        font-size: 30px;
        margin-top: 10px
    }
    ul ul ul {
        font-size: 24px;
        margin-top: 5px
    }
    .slide-content h5 {
        font-size: 20px;
    }

The various parts of reports and presentations have special class names associated with them. To find out what these
are, you can dig inside of a report or presentation.

You can also add styles to the part of the output of an individual cell in another way. You do this by editing the
summary text for the cell. (The summary text is what you see when you collapse an individual call.) You should add a
style string that looks like `style="margin-left:25px;margin-right:10px", or whatever.

There are also a few additional particularities of how Tactic converts notebooks to presentations;

-  Each slide is associated with the **section** of a report. Any cells outside of a section are ignored.
   The title of the slides is taken from the name of the section.
-  Each slide is wrapped in a `div` element with and `id` that is taken from the name of the section. In particular,
   the id is the name of the slide with spaces replaced by underscores. This can be helpful for attaching styles to
   individual slides.
-  There was something else but now I've forgotten what it was.
