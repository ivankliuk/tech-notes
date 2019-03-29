Type inference
==============

When we call a function with an anonymous function for `f`, we have to specify
the type of its argument, here named `x`:

.. code-block:: scala
    :caption: Typed function literal

    def filter[A](l: List[A], f: A => Boolean): List[A] = l.filter(f)
    // filter: [A](l: List[A], f: A => Boolean)List[A]

    filter(List(-3, -2, -1, 0, 1, 2, 3), (x: Int) => x > 0)
    // res1: List[Int] = List(1, 2, 3)

    filter(List(-3, -2, -1, 0, 1, 2, 3), x => x > 0)
    // <console>:13: error: missing parameter type
    //        filter(List(-3, -2, -1, 0, 1, 2, 3), x => x > 0)
    //                                             ^

When a function definition contains multiple argument groups (in other words,
:ref:`curried <currying>`), type information flows from left to right across
these argument groups. The main reason for grouping the arguments this way is
to assist with type inference.

.. code-block:: scala
    :caption: Curried version

    filter(List(-3, -2, -1, 0, 1, 2, 3))(x => x > 0)
    res7: List[Int] = List(1, 2, 3)
