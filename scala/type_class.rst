Type class
==========

Type class is a tool used in functional programming to enable
:ref:`ad-hoc polymorphism <ad-hoc_polymorphism>`.

Type class consists of:

- The type class itself;
- Instances for particular types;
- The interface methods that we expose to users. The ways of specifying an
  interface: Interface Objects and Interface Syntax.

.. code-block:: scala
    :caption: Type class

    trait Base64Writer[A] {
      def toBase64(value: A): String
    }

.. code-block:: scala
    :caption: Instances

    object Base64Instances {

      implicit val stringWriter: Base64Writer[String] =
        new Base64Writer[String] {
          def toBase64(value: String): String = {
            val message = value.getBytes
            java.util.Base64.getEncoder.encodeToString(message)
          }
        }

      implicit val integerWriter: Base64Writer[Int] =

        new Base64Writer[Int] {
          def toBase64(value: Int): String = {
            val message = value.toString.getBytes
            java.util.Base64.getEncoder.encodeToString(message)
          }
        }

    }

.. code-block:: scala
    :caption: Interface object

    object Base64 {
      def toBase64[A](value: A)(implicit w: Base64Writer[A]): String =
        w.toBase64(value)
    }

    import Base64Instances._

    Base64.toBase64("Hello world!")
    // res0: String = SGVsbG8gd29ybGQh

    Base64.toBase64(42)
    // res1: String = NDI=

.. code-block:: scala
    :caption: Interface syntax

    object Base64WriterSyntax {

      implicit class Base64WriterOps[A](value: A) {
        def toBase64(implicit w: Base64Writer[A]): String =
          w.toBase64(value)
      }

    import Base64Instances._
    import Base64WriterSyntax._

    "Hello world!".toBase64
    // res0: String = SGVsbG8gd29ybGQh

    42.toBase64
    // res1: String = NDI=
