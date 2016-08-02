Motivation
==========

The primary motivation behind pkgix was a restricted environment (no root
access, e.g. compute cluster) without specific software dependencies.
Furthermore, the dependencies should be the same across a variety of machines
(e.g. local workstation). In particular:

* require specific version of software, with many dependencies;
* restricted permissions;
* little storage space available;
* the now common language-specific package managers do not help;
* this has to happen on several machines.

Typically, one resorts to many instances of ``./configure && make && make
install`` (or equivalent for whatever software we need); the next best thing is
a collection of scripts to automate this. Now add upgrading this collection of
software and at some point we may just give up. The solution seemed obvious: of
course we need a package manager.

Although package management appears to be a solved problem, none of the
existing solutions seem to address all of the issues that initially sparked
creation of pkgix.  The goal was to require as few dependencies as possible,
i.e. BASH and a minimal set of external tools---in addition, the package
manager should:

* be able to install in an arbitrary prefix (no root!).
* resolve dependencies automatically;
* if, however, a dependency is already installed on the target system it will
  mark it as satisfied;
* provide the ability to upgrade, uninstall, and do general maintenance on a
  prefix;
* combine prefixes.

Related Software
----------------

* `LinuxBrew <https://github.com/Homebrew/linuxbrew>`_: Port of Homebrew to
  Linux.
* `Gentoo Prefix <https://wiki.gentoo.org/wiki/Project:Prefix>`_: Port of
  Gentoo packages to work with arbitrary prefixes.
* `NixOS <http://nixos.org>`_: Unfortunately requires root access once.

The main issue with the above is that they pull a large number of dependencies
that are usually already available on the user's system. One of the main goals
of pkgix is to reuse as many dependencies already present on the user's
system---to do this, several features were added to make this simpler (mainly
metapackages which can dynamically resolve to either another package or say
they are satisfied).
