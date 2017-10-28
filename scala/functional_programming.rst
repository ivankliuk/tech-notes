Functional Programming
======================

Higher order function
---------------------

A function but which performs one or both of the following things:

- Take other functions as arguments;
- Return functions as their results.

Function literal
----------------

.. _function_literal:

A function literal is an alternate syntax for defining a function.
It's useful for when you want to pass a function as an argument to a method
(especially a higher-order one like a fold or a filter operation) but you don't
want to define a separate function. Function literals are anonymous - they don't
have a name by default, but you can give them a name by binding them to
a variable:

.. code-block:: scala
    :caption: Usage

    (x: Int, y: Int) => x * y
    // res0: (Int, Int) => Int = $$Lambda$5584/1797607710@953f466

    // You can bind them to variables:
    val mul = (x: Int, y: Int) => x * y
    // mul: (Int, Int) => Int = $$Lambda$5586/1640763669@7d0a1a1e

    mul(3, 2)
    // res2: Int = 6

Lambda function
---------------

TODO

Tail recursion
--------------

TODO

Currying
--------

TODO

Option
------

.. code-block:: scala
    :caption: Rough definition

    object Option {
      def apply[A](x: A): Option[A] = if (x == null) None else Some(x)
      def empty[A] : Option[A] = None
    }

    sealed abstract class Option[+A] extends Product with Serializable {
      self => ???
    }

    final case class Some[+A](x: A) extends Option[A] {
      def isEmpty = false
      def get = x
    }

    case object None extends Option[Nothing] {
      def isEmpty = true
      def get = throw new NoSuchElementException("None.get")
    }


Either
------
TODO

Tuple
-----

Tuples combine a fixed number of items together so that they can be passed
around as whole. A tuple is immutable and can hold objects with different types,
unlike an array or list.
