A bunch of notes that I need to take into account for the final design

collection: make the performence of operations (append, prepend, etc) explicit
in the signature (or at the very least in documentation) of the collection.
Generic operations on things like Seq like in Scala do not seem to make sense
since the implementation should depend a lot on the exact representation.
