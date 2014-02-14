Components
==========

We manage complexity with abstraction. Inca provides a very powerfull system of
abstraction, entirely copied from Scala, in the form of `trait`, `requires` and
abstract `type` declaration. This abstraction mechanism enables programmer to
abstract over the required components, which typical `include` and `import` of
C/C++/Java does not allow. A java statement such as:

    import a.B

imports into the scope the exact definition of B. If the client then wishes to
abstract over B, B needs to be an interface, and the client will need some
mecanism to have a concrete instance of type B injected at runtime. This leads
to complex framework of dependency injections and some runtime configuration
code. In Scala, a similar import can be made using trait:

    trait App { this: a.B =>
      //use content of B here
    }

This is known as the cake pattern and allows to easily 
abstract over the dependencies of the module, and is entirely supported by
the language. Inca uses the same system of traits as Scala, and does
not even provide packages. So traits are the basic way to organize software
in Inca.

Traits are also very useful to export an API for a client. A typical trait
for a standard `sys` library could be defined as:

    trait sys {
      def println(str: String): Unit
    }

the code is very concise since it does not provide any implementation.
The implementation of the component can be defined in a separated program:

    trait sysimpl extends sys {
      def println(str: String): Unit = {...}
    }

Note that the first definition is a full, valid, program that can be compiled
by the Inca compiler, while the second one relies on a top level value of sys,
which Inca could compile assuming it was made aware of the first component.  In
the end, Inca can generate two different components `sys.o` and `sysimpl.o`.
Note that there is no fundamental difference, both are fully defined programs
exporting one trait. It simply happens that one of them is abstract, while the
other one defines all implementation and can be instantiated easily.

Now if one wants to program against the sys interface, it suffices to load
the `sys.o` component in the compiler and start build a program relying on sys.
`sys.o` being very small, the overhead of parsing and storing the definitions
is minimal. Now one can write an app:

    trait App { this: sys =>
      println("Hello World")
    }

The app can be compiled into `App.o`, without any need for the implementation
of the `sys` module. In fact, the actual implementation can be provided later
at the C equivalent of link time. One can imagine that step as a meta programming step where the whole programs are wrapped around:

    trait _root_ { this: sys with App =>

    }

And an actual executable can be produce via `new _root_ extends App with
sysimpl`. Not that this stage still allows for any sort of concrete
instantiation of the abstract dependencies.
