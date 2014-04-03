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

- __sources__ Image sources are stored in subdirectories of this path. Each
  source should have a template.json which Packer will execute. Builder will cd
  to the sources's directory before calling Packer easing the use of relative
  paths in the template.json file.

- __artifacts__ Image builder outputs are placed in this location. The path to
  this is passed to the packer template in the _artifacts_ user variable.

Builder keeps its cached dependencies, as well as a log of the last run, in
_.data_. The Packer cache is also kept under this location.

Calling Builder
---------------
Builder is currently called as follows:

  ./builder -s SOURCE -v VERSION [-p PLATFORMS] [-u NAME=VALUE [...]]

- __SOURCE__ This is the name of a subdirectory under _sources_ containing the
  image source definition.

- __VERSION__ This is the version of the image to build. This is passed to
  Packer as the _version_ user variable.

- __PLATFORMS__ The platforms to build for. Default to all platforms in a
  source.

- __NAME=VALUE__ Additional user variables to pass to Packer.

License
-------
This software project is licensed under the BSD-derived license and is
copyright (c) 2014 Ryan Bourgeois. A copy of the license is included in the
LICENSE file. If it is missing then a copy may be found on the project page.
