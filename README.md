The Inca Programming Language
=============================

This repository contains the design of the Inca programming language.
This is (obviously) a work in progress. Hopefully implementation will
follow at some point.

Overview
--------

Inca is an experimental language created to explore some design possibilites
for future programming languages. It introduces some radical concepts that,
to the best of my knowledge, are not present in other programming languages.
One such concept is incrementallity (hence the name INCa), which is
developed more in the corresponding [document](incremental.md). For proper
incremental compilation, the language needs to rely on a well design module
system. Inca basically uses the `trait` mechanism of Scala, described
in [Scalable Component Abstraction](http://lampwww.epfl.ch/~odersky/papers/ScalableComponent.pdf).

Inca is more than just another programming language. It aims at being a
complete development system. In this sense, the design of Inca is strongly
influenciated by the potential tooling around the language. For example, Inca
does not recognize a concept of file or compilation unit. A program &mdash or
rather a component &mdash is always fully represented in the RAM of a running
compiler. The end goal is to use an editor aware of this system, that will
provide a clean structuration of the program according to the components, and
not the filenames. The incremental and interactive compiler will be the basis
to build such editors.
