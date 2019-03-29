Context Bound
=============

A context bound describes an implicit value. It is used to declare that for
some type `A`, there is an implicit value of type `B[A]` available.
The syntax goes like this:

.. code-block:: scala

    def f[A : B](a: A) = g(a) // where g requires an implicit value of type B[A]

How can `B[A]` implicit parameter be reached?

.. code-block:: scala

    def f[A : B](a: A) = {
      val ev = implicitly[B[A]]
      g(a)
    }

De-sugared version of Context Bound:

.. code-block:: scala

    def g[A](a: A)(implicit ev: B[A]) = g(a)
