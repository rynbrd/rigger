Rig Builder
===========
A tool to build OS images in a repeatable fashion. Used primarily to seed Rig
with images that are useful.

How It Works
------------
Builder's primary purpose is to enforce repeatability in the image build
process while maintaining ease of use. It maintains specific versions of its
own dependencies in an effort to minimize the effects of version changes. It
uses [Packer](http://packer.io) for all the heavy lifting and sets constraints
around how Packer is called.

Builder has two directories related to the image build process. These are:

- __templates__: Image templates are stored in subdirectories of this path.
  Each template should have a template.json which Packer will execute. Builder
  will cd to the template's directory before calling Packer easing the use of
  relative paths in the template.json file.

- __images__: When applicable image outputs are placed in this location.

Builder keeps its cached dependencies, as well as a log of the last run, in
_.data_. The Packer cache is also kept under this location.

Calling Builder
---------------
Builder is currently called as follows:

  ./builder TEMPLATE VERSION [NAME=VALUE [...]]

- __TEMPLATE__: This is the name of a subdirectory under _templates_ containin
  the image definition.

- __VERSION__: This is the version of the image to build. This is passed to
  Packer as the _version_ user variable.

- __NAME=VALUE__: Additional user variables to pass to Packer.

License
-------
This software project is licensed under the BSD-derived license and is
copyright (c) 2013 Ryan Bourgeois. A copy of the license is included in the
LICENSE file. If it is missing then a copy may be found on the project page.
