Rigger
======
A tool to build OS images in a repeatable fashion.

How It Works
------------
Rigger's primary purpose is to enforce repeatability in the image build process
while maintaining ease of use. It maintains specific versions of its own
dependencies in an effort to minimize the effects of version changes. It uses
[Packer](packer) for all the heavy lifting and sets constraints around how
Packer is called.

Rigger has two directories related to the image build process. These are:

- __sources__ Image sources are stored in subdirectories of this path. Each
  source should have a template.json which Packer will execute. Rigger will cd
  to the sources's directory before calling Packer easing the use of relative
  paths in the template.json file.

- __artifacts__ Build outputs are placed in this location. The path to this is
  passed to the packer template in the _artifacts_ user variable.

Rigger keeps a cache of its dependencies, as well as a log of the last run, in
_.data_. The Packer cache is also kept under this location.

Calling Rigger
---------------
Rigger is currently called as follows:

  ./rigger -s source -v version [-p platforms] [-b branch] [-u name=value [...]]

- __source__ - This is the name of a subdirectory under _sources_ containing
  the image source definition. It may also be a git repo in which case it is
  cloned into a directory under sources. Subsequent calls will stash and fetch
  changes.

- __version__ - This is the version of the image to build. This is passed to
  Packer as the _version_ user variable.

- __platforms__ - A comma separated list of platforms to build for. Default to
  all platforms in a source.

- __branch__ - If source is a git repo then this branch will be checked out.

- __name=value__ - Additional user variables to pass to Packer.

License
-------
This software project is licensed under the BSD-derived license and is
copyright (c) 2014 Ryan Bourgeois. A copy of the license is included in the
LICENSE file. If it is missing then a copy may be found on the project page.

[packer]: http://packer.io "Packer"
