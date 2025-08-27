 <!-- Dellinger doc rev. 2.0 -->
Welcome to the Intel Curated Repo of cligen
============================================

You can find the full, unaltered Readme.MD from the cligen project
below.

This repo contains the source for branches of cligen that are curated
and updated to contain all security fixes. This includes older versions that have
had security fixes backported to them.

Branches with Intel fixes (and Intel version numbers) have been created for all
supported releases. The currently supported branches and their planned support timeframes are listed on the [milestones page]https://github.com/joannaklimiuk/test-wiki2/milestones

The following flags were set for IPAS compliance:
```
compiler -D_FORTIFY_SOURCE=2 -fstack-protector-strong -fPIE -fPIC -fcf-protection=full -fstack-clash-protection
linker -Wl,-z,relro,-z,now
```

Other Intel information, including build commands, can be found on the [wiki](https://github.com/joannaklimiuk/test-wiki2/wiki).

***FAQ***

*How do I know all CVEs are fixed for supported branches?

That's a great question. We do everything with GitHub Issues. If you want to see what CVEs have been fixed for what
branches, just search on closed issues.

*How do you know you haven't broken anything with the branches where fixes have been backported?

Before commits are made to our repository, we ensure all available unit tests pass. This of course
doesn't mean something hasn't broken; just that there isn't a unit test that detects it. If you feel you are getting
an incorrect result, please file an Issue (https://github.com/joannaklimiuk/test-wiki2/issues).

*What do you do to prepare a branch for curation?

We start with the raw upstream source. Once we have that, we create a branch for our curated changes. That branch is always called "\<upstream branch or tag name\>-Intel". Once the branch is created, we make two Intel specific changes:
- Embed an Intelized version number (ex. "cligen 7.5.0-Intel")
- Change the default release build options to create a binary compliant with IPAS compiler flag expectations

After this, any relevant CVEs are backported to the branch.

*What happens when a new CVE is published for cligen?

The steps are simple:
- The curation team will determine which branches are affected by the new CVE
- GitHub Issues will be created for each affected branch
- When the branches are patched, the corresponding Issues will be closed with information about which commit
fixes the issue.

### How long will you be supporting these branches?

Each branch is supported for 2-years from its release date. The exceptions to this are:

1. The vendor is maintaining that product for longer than our two year support window. In that case we will support it for as long as the vendor supports their product.
2. There are no new branch releases. I.e if there latest release is further than 2-years old we will continue to support it until a new release is made.
3. The vendor is maintaining the branch for less than 2-years. In that case we will follow suit and only support it as long as they support it, despite it being less than 2 years.

To take any guesswork out of how long things will be kept up to date, Milestones (https://github.com/joannaklimiuk/test-wiki2/milestones) have been created for each individually supported branch if it goes EOL before the upstream cligen branch. If an internal release doesn't fall into that category, it is covered by blanket milestones corresponding to upstream support.


*The version of cligen I want support for isn't here.  Can you support it?

File a New Issue (https://github.com/joannaklimiuk/test-wiki2/issues/new/choose) and let's talk.

*Is this only source or are you also supplying binaries?

At this particular time, we are only supply source. If you want binaries, please file a New Issue (https://github.com/joannaklimiuk/test-wiki2/issues/new/choose).

*I have a question that isn't answered here.  What do I do?

Please file a New Issue: (https://github.com/joannaklimiuk/test-wiki2/issues/new/choose)!

----------------------------------------------------------------------------------------------------------


# CLIgen

[![Build Status](https://github.com/clicon/cligen/actions/workflows/ci.yml/badge.svg)](https://github.com/clicon/cligen/actions/workflows/ci.yml) [![codecov](https://codecov.io/gh/clicon/cligen/branch/master/graph/badge.svg?token=6HXN51SARU)](https://codecov.io/gh/clicon/cligen) <a href="https://scan.coverity.com/projects/cligen"><img alt="Coverity Scan Build Status" src="https://scan.coverity.com/projects/29565/badge.svg"/></a>

CLIgen is a Command-Line Interface generator.

Well, actually it is not really a generator, since it does
not _generate_ code for CLI:s. Instead, it builds and interprets
datastructures (a parse-tree) which a library (libcligen) interprets
in runtime.  It is fast and efficient and helps you develop CLI:s
easier. You enter a CLI syntax in a text file, and 
write callback functions in C. The callback functions add the semantics, that is, what the
commands in the CLI are supposed to do. 

The main documentation is the [cligen tutorial](cligen_tutorial.pdf)
which is usually kept up-to-date and is probably the best way to
understand CLIgen.

Some background material can be found on the [CLIgen project page](https://www.cligen.se).

CLIgen is _not_ a system in itself, you need to build your own
'backend'.  There is another co-project: 'clixon' which is
a whole system where you load dynamic frontend and backend
modules. See [CLIXON project page](https://www.clicon.org) and [CLIXON
github](https://github.com/clicon/clixon). Clixon provides a
system with embedded database, commit semantics, YANG and NETCONF
interface, etc. CLIgen is a part of clixon but can be used by itself.

The source code here is built and installed using:
```
  configure;
  make;
  sudo make install.
```

The source builds a single library. If you build applications, you should include cligen.h and link with the library.

There are several example applications:
* cligen_hello Simplest possible. Just builds a 'hello world' greeting by in-line C
* cligen_file Read a syntax specification from file. You must supply the file.
* cligen_tutorial Samples of techniques used in [cligen_tutorial.pdf](cligen_tutorial.pdf)

See also [Changelog](CHANGELOG.md).

For building the C reference documentation using doxygen, do: `make doc` and place your browser at `doc/index.html`.

CLIgen is dual license. Either Apache License, Version 2.0 or GNU
General Public License Version 2. You choose.

I can be found at olof@hagsand.se.

## getline

CLIgen uses getline with the following copyright:

Copyright (C) 1991, 1992, 1993 by Chris Thewalt (thewalt@ce.berkeley.edu)

Permission to use, copy, modify, and distribute this software 
for any purpose and without fee is hereby granted, provided
that the above copyright notices appear in all copies and that both the
copyright notice and this permission notice appear in supporting
documentation.  This software is provided "as is" without express or
implied warranty.
