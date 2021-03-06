.. _conan_get:


conan get
==========

.. code-block:: bash

	$ conan get [-h] [--package PACKAGE] [--remote REMOTE] [--raw] reference [path]


Gets a file or list a directory of a given reference or package.

.. code-block:: bash

    positional arguments:
      reference             package recipe reference
      path                  Path to the file or directory. If not specified will
                            get the conafile if only a reference is specified and
                            a conaninfo.txt file contents if the package is also
                            specified

    optional arguments:
      -h, --help            show this help message and exit
      --package PACKAGE, -p PACKAGE
                            package ID
      --remote REMOTE, -r REMOTE
                            Get from this specific remote
      --raw, -raw           Do not decorate the text


**Examples**:

- Print the conanfile.py from a remote package:

.. code-block:: bash

	$ conan get zlib/1.2.8@conan/stable -r conan-center


- List the files for a local package recipe:

.. code-block:: bash

    $ conan get zlib/1.2.11@conan/stable .

    Listing directory '.':
     CMakeLists.txt
     conanfile.py
     conanmanifest.txt

- Print a file from a recipe folder:

.. code-block:: bash

    $ conan get zlib/1.2.11@conan/stable conanmanifest.txt

- Print the conaninfo.txt file for a binary package:

.. code-block:: bash

    $ conan get zlib/1.2.11@conan/stable -p 09512ff863f37e98ed748eadd9c6df3e4ea424a8

.. code-block:: text

    [settings]
        arch=x86_64
        build_type=Release
        compiler=apple-clang
        compiler.version=8.1
        os=Macos

    [requires]


    [options]
       # ...


- List the files from a binary package in a remote:

.. code-block:: bash

    $ conan get zlib/1.2.11@conan/stable . -p 09512ff863f37e98ed748eadd9c6df3e4ea424a8 -r conan-center

    Listing directory '.':
     conan_package.tgz
     conaninfo.txt
     conanmanifest.txt
