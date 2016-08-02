Introduction
============

pkgix is a very lightweight package manager, intended to setup software in
environments where root access is not available or installing the software
system-wide is not desirable.

Package description files can be located inside repositories accessible via
multiple URLs. The following protocols are supported: ``file://`` (default),
``http://``, ``https://``, ``ftp://``.

Written in BASH making use of standard POSIX tools.

Setup
-----

At minimum, you only need to obtain the script file `pkgix
<https://raw.githubusercontent.com/pkgix/pkgix/master/bin/pkgix>`_.

By default pkgix looks for a repository in ``~/pkgix-repo/pkgs``. Repositories
can be specified using the ``-r`` flag, but it is recommended to export the
repository URL/path with ``PKGIX_REPOS="<repos...>"`` (separated by ``;``).
See the Repositories section below for list of known repositories.

.. rubric:: Recommended:

- Add ``<path-to-pkgix-repo>/bin`` to your ``PATH``.
- ``source "<path-to-pkgix-repo>/share/pkgix/helper-inc.sh"``; currently supported: bash, zsh.
  Provides the ``pkgix-activate`` and ``pkgix-deactivate`` functions; annotates
  shell prompt to indicate active prefix environment.

Example Usage
-------------

.. code-block:: sh

    # Install gcc 4.4 and make 3.80 into 'old-build-tools' from repository.
    $ pkgix install old-build-tools dev/gcc-4.4 dev/make-3.80

    # Starts a new shell in the chosen prefix environment.
    $ pkgix chenv old-build-tools

    # Add a remote repository. Additional URLs are processed in
    # order, until the requested package description file is found.
    $ pkgix -r https://raw.github.com/pkgix/pkgix-repo/master/pkgs install some-prefix dev/gcc-4.4

Known Repositories
------------------

List of known repository URLs:

1. `abs2pkgix <https://github.com/pkgix/abs2pkgix>`_: Converter from `ArchLinux
   <https://www.archlinux.org>`_ PKGBUILDs to pkgix package description files.
   Does not yet support all packages.
2. `pkgix-repo <https://github.com/pkgix/pkgix-repo>`_:
   ``https://raw.github.com/pkgix/pkgix-repo/master/pkgs``---experimental
   repository playground. Likely outdated! Maintaining this should not be the
   priority, as we have many excellent package repositories elsewhere, and it
   would be more useful to build converters.

