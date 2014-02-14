Incremental Compiler
====================

At the heart of the design of Inca is the incremental compilation.
This document discusses the vision behind incremental compilation, and
the technical details of the implementation.

Vision
------

It seems to me that the concept of files and hierarchy of directory is
obsolete. It is a very bad way of organizing most data, that usually
requires multiple parent directories. A common solution is to end up
with a system of tags, and a search feature to look up individual files.
Individual files, which are essentially blocks of bytes, are useful as
a way to store structured data, so they will be the basic storage
of a source components, and the compiled component.

However, in the programming world, it seems unthinkable to not have a file
system hierarchy to store a project. C is entirely based on the concept of
compilation units, which are individual files. Java has a complete package
hierarchy along with a convention to have one file for one class. This is a
fundamental violation of the DRY principle, as directories mirror packages
declaration and filenames mirror class names. I believe it would make much more
sense to have a single files with all definitions of the program, and let an
external tool organizing the browsing by packages and classes.

This justifies the idea of having an incremental compiler, which would
basically stores the whole program in memory. A programmer could interact with
the compiler by setting characters at specific positions, and the compiler
would incrementally compile the program, doing only the work necessary for the
difference. This should hopefully lead to very fast compilation, and offer
immediate feedback to the programmer.

Tools like Eclipse are actually attempting to do something very similar. They
provide a complete browser by packages and classes, have a complete semantics
understanding of the program, and offer immediate feedback with compilation
error. Inca is designed to be used in exactly such an environment, and
the standard compiler will be built with a fully incremental interface.

The hope is to simplify the build process as much as possible. Relying on an
external build tool to be smart about recompiling files one by one seem to be
the wrong way to go. The issue stems from the fact that current compilers are
still based on the notion of compiling files one by one, which forces us to use
additional tools to organize the build process. In Inca, the whole build
process will be baked in with the language implementation.

Implementation
--------------
