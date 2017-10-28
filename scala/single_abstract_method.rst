Single Abstract Method (SAM)
============================

Introduced in Scala 2.12.
If a trait or abstract class has exactly one abstract method, then it can be
presented as a :ref:`function literal <function_literal>`:

.. code-block:: scala

    trait Printable {

      // Exactly one abstract method
      def print(message: String): Unit

      // optional fields
      val name = "Printable Object"

    }

    // Object-oriented syntax
    new Printable {
        def print(message: String): Unit = println(message)
    }
    // res0: Printable = $anon$1@1e91fe2f

    // SAM syntax
    val prn: Printable = (msg: String) => println(msg)
    // prn: Printable = $anonfun$1@3de800ce

