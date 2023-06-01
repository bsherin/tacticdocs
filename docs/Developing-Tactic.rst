Developing Tactic
=================
These are the instructions to use if you want to edit the Tactic source yourself and run it locally.

This really isn't enough to get started, so it's mostly for me.

.. role:: bash(code)
   :language: bash

Initial setup
--------------

#. `Install Node.js and npm <https://docs.npmjs.com/downloading-and-installing-node-js-and-npm>`__
#. `Install Docker <https://docs.docker.com/get-docker/>`__ and start it.
#. Clone the `tactic git repository <https://github.com/bsherin/tactic>`__

   a. You might need to make a directory named "persist" at the top level of the cloned project.

#. In a terminal, in the directory associated with the project, run :bash:`npm install` to install all of the various
   Javascript dependencies

For this all to work, you need to somehow have a local mongo database with the appropriate starting material.
There's no easy solution for that yet.

Building steps
-------------

To build development javascript files:

   * Run :bash:`npm run build`

To build production javascript bundles:

    * Run :bash:`npm run build-production`

To build docker images:

    * Run :bash:`dbuild all` to build x86 images
    * Run :bash:`dbuild_arm all` to build arm64 images (needed for Apple silicon).

Starting tactic
---------------

To start tactic, cd into the tactic_app directory then run:

.. code-block:: bash

    start_tactic.sh --root <path to project root> --mdir <path to mongo data> --arm64 --dev

Get rid of the --arm64 flag if you've built x86 images. Get rid of the --dev flag if you want to use the
production bundles.