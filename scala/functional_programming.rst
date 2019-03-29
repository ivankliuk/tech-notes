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

A => B => C = ???

The arrow => in front of the argument type B means that the function f takes its
second argument by name and may choose not to evaluate it

def foldRight[B](z: => B)(f: (A, => B) => B): B = ???

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


Underscore notation for anonymous functions

The anonymous function (x,y) => x + y can be written as _ + _ in situations where the types of x and y could be inferred by Scala. This is a useful shorthand in cases where the function parameters are mentioned just once in the body of the function. Each underscore in an anonymous function expression like _ + _ introduces a new (unnamed) function parameter and references it.

Polymorphic function
--------------------
We’re using the term polymorphism in a slightly different way than you might
 be used to if you’re familiar with object-oriented programming, where that
 term usually connotes some form of subtyping or inheritance rela- tionship. T
 here are no interfaces or subtyping here in this example. The kind of
 polymorphism we’re using here is sometimes called parametric polymorphism.

Monomorphic functions operate on only one type of data.
Polymorphic functions work for any type it’s given.

Tail recursion
--------------

A call is said to be in tail position if the caller does nothing other than
return the value of the recursive call.

`scala.annotation.tailrec` annotation gets information about whether method is
optimised. You will then get a warning if they are not optimised by the compiler
and compilation will fail.

.. code-block:: scala
    :caption: Failed tail recursive function

    import scala.annotation.tailrec

    @tailrec
    def factorial(n: Int): Int = {
    // Such functions is often called `go` or `loop` by convention.
      def go(n: Int, acc: Int): Int =
        if (n <= 0) acc
        else go(n - 1, n * acc)
      go(n, 1)
    }

    // <console>:13: error: @tailrec annotated method contains no recursive calls
    //        def factorial(n: Int): Int = {

.. code-block:: scala
    :caption: Working recursive function

    import scala.annotation.tailrec

    def factorial(n: Int): Int = {
      @tailrec
      def go(n: Int, acc: Int): Int =
        if (n <= 0) acc
        else go(n - 1, n * acc)
      go(n, 1)
    }

.. _currying:

Currying
--------

.. code-block:: scala

    (a: Int) => (b: Int) => (c: Int) => (d: Int) => a * b * c * d
    // res0: Int => (Int => (Int => (Int => Int))) = $$Lambda$5542/173054796@5b1bbcc

    res0(1)
    // res1: Int => (Int => (Int => Int)) = $$Lambda$5543/1868653446@18f63d41

    res1(1, 2, 3, 4)
    // <console>:13: error: 3 more arguments than can be applied to method apply: (v1: Int)Int => (Int => (Int => Int)) in trait Function1
    //        res1(1, 2, 3, 4)
    //                ^

Side effects
------------

A function has a side effect if it does something other than simply return
a result, for example:

- Modifying a variable
- Modifying a data structure in place
- Setting a field on an object
- Throwing an exception or halting with an error
- Printing to the console or reading user input
- Reading from or writing to a file
- Drawing on the screen


Referential transparency
------------------------

An expression is called referentially transparent if it can be replaced with
its corresponding value without changing the program's behavior. This requires
that the expression is pure, that is to say the expression value must be
the same for the same inputs and its evaluation must have no side effects.

.. code-block:: scala
    :caption: String vs. StringBuilder

    val x = new StringBuilder("Hello")
    // x: StringBuilder = Hello

    val y = x.append(", World")
    // y: StringBuilder = Hello, World

    val r1 = y.toString
    // r1: String = Hello, World

    val r2 = y.toString
    // r2: String = Hello, World

    // r1 and r2 are the same

    val x = new StringBuilder("Hello")
    // x: StringBuilder = Hello

    val r1 = x.append(", World").toString
    // r1: String = Hello, World

    scala> val r2 = x.append(", World").toString
    // r2: String = Hello, World, World

    // r1 and r2 are not the same because of StringBuilder has internal state
    // and is not a pure function.

.. code-block:: scala
    :caption: Future vs. IO

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

RT expressions does not depend on context and may be reasoned about locally,
        whereas the meaning of non-RT expressions is context-dependent and requires more global reasoning.

Exceptions break RT and introduce context dependence, Exceptions are not type-safe.
     The type of failingFn, Int => Int tells us
        nothing about the fact that exceptions may occur, and the compiler will
            certainly not force callers of failingFn to make a decision about
                how to handle those excep- tions. If we forget to check for
                    an exception in failingFn, this won’t be detected until runtime.

The primary benefit of exceptions: they allow us to consolidate and centralize
error-handling logic, rather than being forced to distribute this logic
throughout our codebase. The technique we use is based on an old idea: instead
of throwing an exception, we return a value indicating that an exceptional
condition has occurred.

Strictness and laziness
-----------------------

In general, the unevaluated form of an expression is called a thunk, and we
 can force the thunk to evaluate the expression and get a result.

scala> def maybeTwice(b: Boolean, i: => Int) = if (b) i+i else 0
maybeTwice: (b: Boolean, i: => Int)Int
scala> val x = maybeTwice(true, { println("hi"); 1+41 })
hi
hi
x: Int = 84


scala> def maybeTwice2(b: Boolean, i: => Int) = { | lazyvalj=i
     |   if (b) j+j else 0
|}
maybeTwice: (b: Boolean, i: => Int)Int
scala> val x = maybeTwice2(true, { println("hi"); 1+41 })
hi
x: Int = 84


separation of concerns
We want to separate the description of computations from actually running them.
More generally speaking, laziness lets us separate the description of an expression from the evaluation of that expression.
This gives us a powerful ability—we may choose to describe a “larger” expression than we need, and then evaluate only a por- tion of it.


Corecursion
-----------

Corecursion is a type of operation that is dual to recursion.
Whereas recursion works analytically, starting on data further from a base case
and breaking it down into smaller data and repeating until one reaches a base
case, corecursion works synthetically, starting from a base case and building
it up, iteratively producing data further removed from a base case.

.. code-block:: scala
    :caption: Corecursive Fibonacci stream

    def fibFrom(a: Int, b: Int): Stream[Int] = a #:: fibFrom(b, a + b)
    // fibFrom: (a: Int, b: Int)Stream[Int]
    
    fibFrom(0, 1).take(10).toList
    // res0: List[Int] = List(0, 1, 1, 2, 3, 5, 8, 13, 21, 34)

Purely functional state
-----------------------

Here's the class with mutable state:

.. code-block:: scala
    :caption: Stateful class

    class User(var age: Int, var name: String) {
      def setAge(newAge: Int): Int = {
        this.age = newAge
        age
      }

      def setName(newName: String): String = {
        this.name = newName
        name
      }
    }

This is the same class but refactored to provide purely functional state:

.. code-block:: scala
    :caption: Stateless class

    class User(age: Int, name: String) {
      def setAge(newAge: Int): (Int, User) = (newAge, new User(newAge, this.name))

      def setName(newName: String): (String, User) = (newName, new User(this.age, newName))
    }

Methods `setAge` and `setName` have a type of form
Each of our functions has a type of the form `RNG => (A, RNG)` for some type `A`.
Functions of this type are called state actions or state transitions because
they transform RNG states from one to the next. These state actions can be
combined using combinators.

