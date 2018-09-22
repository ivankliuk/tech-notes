Functional Programming
======================

Higher order function
---------------------

A function but which performs one or both of the following things:

- Take other functions as arguments;
- Return functions as their results.

.. _function_literal:

Function literal
----------------

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

Referential transparency
------------------------

An expression is called referentially transparent if it can be replaced with
its corresponding value without changing the program's behavior. This requires
that the expression is pure, that is to say the expression value must be
the same for the same inputs and its evaluation must have no side effects.

.. code-block:: scala

    import cats.effect.IO
    import scala.concurrent.{ Await, Future}
    import scala.concurrent.ExecutionContext.Implicits.global
    import scala.concurrent.duration._

    val prnF = Future { println("Hello from Future!"); 1 }
    // Hello from Future!
    // prnF: scala.concurrent.Future[Int] = Future(Success(1))

    val prnIO = IO { println("Hello from IO!"); 1}
    // prnIO: cats.effect.IO[Int] = IO$684479575

    val fRes = for {
      f1 <- prnF
      f2 <- prnF
    } yield f1 + f2
    // fRes: scala.concurrent.Future[Int] = Future(<not completed>)

    Await.result(fRes, 2.seconds) == 2
    // res0: Boolean = true

    val ioRes = for {
      io1 <- prnIO
      io2 <- prnIO
    } yield io1 + io2
    // ioRes: cats.effect.IO[Int] = IO$985832276

    ioRes.unsafeRunSync() == 2
    // Hello from IO!
    // Hello from IO!
    // res1: Boolean = true
