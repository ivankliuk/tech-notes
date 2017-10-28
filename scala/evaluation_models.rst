Evaluation models
=================

- Eager computations happen immediately
- Lazy computations happen on access.
- Memoized computations are run once on first access, after which the results are cached.

`val` is eager and memoized:

.. code-block:: scala
    :caption: Usage

    val x = {
      println("Computing X")
      math.random
    }

    // Computing X
    // x: Double = 0.2800286720619266
    x // first access
    // res0: Double = 0.2800286720619266
    x // second access
    // res1: Double = 0.2800286720619266

`def` is lazy and not memoized:

.. code-block:: scala
    :caption: Usage

    def y = {
      println("Computing Y")
      math.random
    }

    // y: Double
    y // first access
    // Computing Y
    // res0: Double = 0.8868971918220552
    y // second access
    // Computing Y
    // res1: Double = 0.3816438919323032

`lazy val` is lazy and memoized. The code is not run until we access it for
the first time (lazy). The result is then cached and re-used on subsequent
accesses (memoized):

.. code-block:: scala
    :caption: Usage

    lazy val z = {
      println("Computing Z")
      math.random
     }

    // z: Double = <lazy>
    z // first access
    // Computing Z
    // res4: Double = 0.9968902519993859
    z // second access
    // res5: Double = 0.9968902519993859


**Recap**

======== ====== ==================
Scala    Cats   Properties
======== ====== ==================
val      Now    eager, memoized
lazy val Later  lazy, memoized
def      Always lazy, not memoized
======== ====== ==================