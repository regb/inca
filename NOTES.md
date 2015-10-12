NOTES
=====

A bunch of notes that I need to take into account for the final design

collection
----------

Make the performence of operations (append, prepend, etc) explicit
in the signature (or at the very least in documentation) of the collection.
Generic operations on things like Seq like in Scala do not seem to make sense
since the implementation should depend a lot on the exact representation.

A type should be defined by the operations that can be applied on it, not by the time complexity of its operation:
	- We should not have both an array and a linkedlist, they have the same abstract interface which is the concept of a sequence
	- Even a sequence could simply be seen as a map with keys being integer, but then you might lost the conecpt of size and continuity of the data

Focus on pure abstract data (unbounded integers, real instead of bitvectors,
floating point). Also focus on data structure without knowing complexity of
operations (only notion of sequence(order)/set/map). The programmer should
NEVER try to optimize the code, the compiler will always do it. This means NO
feature for improving optimization, only focus on correctness. Bad experience
with all the tricks for improving scala speed.. in the end it is no better
than writing pure C.

Basic Types
-----------

Int should be a mathematical integer, we should have rational number, infinite
precision etc. Maybe provide bitvector and float type as well.


dynamic vs static typing
------------------------

Dynamic typing is overall more flexible. It truly lets the programmer dictates
what is the right way to do things, instead of being told what is alright by
a compiler. On the other hand, static typing tend to ensure safe programs. If
we assume the programmer is very smart, dynamic typing seems like a better approach.
If we go with static typing, we will need a very flexible system.

Techniques such as soft typing, where the compiler tries to prove error at compile time
instead of proving the absence of error, could be a good trade-off.

Tooling
-------

The design of the language must take into account the way tools like debugguer, profiler
and IDEs will be used.

Object Oriented Programming
---------------------------

I am not the biggest fan of object oriented programming. I think in most case
decomposition into data and functionalities (struct and procedures in C for
example) is a much cleaner approach than the patchwork of data and behaviour
that object oriented prone. However, it seems object oriented programming is
very useful to solve some domain of application, notable GUI programming. The
inheritence pattern is also a neat solution in many cases where you need to
work with a collection of data that can have small variations.

Imperative vs Functional Programming
------------------------------------

Functional programming is without any doubt a much superior programming paradigm
than imperative programming. However, there are many cases in which imperative
programming is just better than functional programming. There is no reason to elitist
there, we need to enable both paradigm in the language and let the programmer
makes the best decision.

Comments
--------

A good comment is a comment not writen, comments should only be used to explain
the why, not the how and (probably) not the what


Performence vs Safety vs Convenience
------------------------------------

There are a lot of trade-offs between performence reachable with the language versus
the safety that you guarentee and the convenience that you offer the programmer. Finding
the sweet spot there is not easy.

A language is designed for programmers, compilers and static analyzer, in no
particular order.  None of those 3 target audiences should be ignored during
design. Compile time is usually something we can sacrifice, but the compiler should not be too
slow without good reasons. Also there are limits in that area and a language like Scala
might be overstepping them.

Also, as important as performence can be, do not forget that an OS is writen in
C, not in Inca.

Syntax
------

whitespace as a syntax element is a bad idea

people don't like lisp parentheses. Don't know why, but worth keeping in mind if you want the language to be popular.

However, some people don't like language without lisp parentheses...

JSON is better than XML and it would be nice to be somehow corresponding to the basic types of the language

Synthesis
---------

We need to incorporate elements of synthesis. Data structure can be defined as relation and
automatically synthesized into code.

choose(x => s + 3 == 2) like construct in Leon (should be called epsilon actually)

Macros
------

Macro should be in the core design. Or something like LMS. Things like choose
could then be extended through this interface. In particular, individual
synthesis theories could be implemented as macro or LMS, which means as some
sort of librabray (user defined).


Miscelaneous
------------

  * facultative parenthesis (like scala) are evil
  * The programmer knows best, do not try to force it to use some things, like layout (python) ...
    A programmer is a human and thus can often solve a very difficult problem for a computer, we
    should trust him in some cases.
  * Native support is often as good as feel-like-native library support: REGEXP and maybe context free grammar
  * Non determinism
  * everything is an expression sounds like an elegant concept
  * Possibility to define sequence of operators, so that we can write expressions
    such as 1 < x < 10 which would return a boolean.




