Tile Reference Intro
===========================

This section of the Tactic documentation has the nitty-gritty information you'll need to create and modify
tiles. In fact, the :doc:`Tile-Commands` and :doc:`Object-Oriented-API` pages are probably the pages you'll refer
to most often in all of the Tactic documentation.

The page :doc:`Tile-Structure` is for advanced users who want to fully understand the underlying structure
of Tactic tile classes. The existence of the Tile Creator has mostly made this irrelevant, however.

The key pages here are :doc:`Tile-Commands` and :doc:`Object-Oriented-API`. All of the commands listed in
:doc:`Tile-Commands` are methods of the base tile class, and are accessed by typing ``self.command_name``. In contrast,
the :doc:`Object-Oriented-API` defines a number of otherr objects, such as an object corresponding to your resource
library and collection associated with a project. All of the functionality in the Object-Oriented-API is also
covered by the commands in Tile-Commands. But, where the Object-Oriented API can be used, it is generally easier
to remember and produces code that is easier to read.

The Object-Oriented API is a more recent innovation. This means that, if you look at old tiles in the repository,
they will use Tile-Commands where the Object-Oriented API would now be preferred.

This tile reference also covers a number of other special topics.