Implicits
=========

``implicitly`` method summons any value from implicit scope

.. code-block:: scala
    :caption: Definition

    def implicitly[A](implicit value: A): A = value


.. code-block:: scala
    :caption: Usage

    import Base64Instances._

    implicitly[Base64Writer[String]]
    // res0: Base64Writer[String] = Base64Instances$$anon$1@1a4415a7


Implicit Scope: the compiler searches for candidate instances in the implicit
scope at the call site, which roughly consists of:

- local or inherited definitions;
- imported definitions;
- definitions in the companion object of the type class or the parameter type.


When the compiler searches for an implicit it looks for one matching the
type or subtype. Thus we can use variance annota􏰀tions to control type class
instance selection to some extent.

TODO