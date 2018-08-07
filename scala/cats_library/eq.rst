Eq
==

Scala’s built-in `==` operator works for any pair of objects, no matter what
types we compare. Ideally, Scala shouldn’t let us compare two types that can
never be equal.

.. code-block:: scala
    :caption: Typical problem

    scala> 42 == "hello"
    // <console>:1: warning: comparing values of types Int and String using `==' will always yield false
    //        42 == "hello"
    //           ^
    // res0: Boolean = false

`Eq` is designed to support type-safe equality.

.. code-block:: scala
    :caption: Type-safe equality

    import cats.implicits._

    42 === "hello"
    // <console>:2: error: type mismatch;
    //  found   : String("hello")
    //  required: Int
    //        42 === "hello"
    //               ^

    "world" === "hello"
    // res3: Boolean = false

    "world" =!= "hello"
    // res4: Boolean = true
