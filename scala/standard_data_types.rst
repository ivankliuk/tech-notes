Standard Data Types
===================

Option
------

.. code-block:: scala
    :caption: Rough definition

    sealed trait Option[+A]
    final case class Some[+A](x: A) extends Option[A]
    case object None extends Option[Nothing]

Either
------

`Either` is a disjoint union of two types (also called Disjunction).

.. code-block:: scala
    :caption: Rough definition

    sealed trait Either[+E, +A]
    case class Left[+E](value: E) extends Either[E, Nothing]
    case class Right[+A](value: A) extends Either[Nothing, A]

Tuple
-----

Tuples combine a fixed number of items together so that they can be passed
around as whole. A tuple is immutable and can hold objects with different types,
unlike an `Array` or `List`.
Pairs and tuples of other arities are also algebraic data types.

.. code-block:: scala
    :caption: Tuple

    val p = ("Bob", 42)
    // p: (String, Int) = (Bob,42)

    // ("Bob", 42) is a syntactic sugar for:

    Tuple2[String, Int]("Bob", 42)
    // res0: (String, Int) = (Bob,42)

    p._1
    // res1: String = Bob

    p._2
    // res2: Int = 42

    p match { case (a, b) => b }
    // res3: Int = 42

List
====

.. code-block:: scala
    :caption: Rough definition

    sealed trait List[+A]
    case object Nil extends List[Nothing]
    case class Cons[+A](head: A, tail: List[A]) extends List[A]

Stream
======

`Stream` is also called *lazy list*.

.. code-block:: scala
    :caption: Rough definition

    sealed trait Stream[+A]
    case object Empty extends Stream[Nothing]
    case class Cons[+A](h: () => A, t: () => Stream[A]) extends Stream[A]
