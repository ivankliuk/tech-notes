General
=======

Shortcuts to simplify imports:

- ``import cats._`` imports all of Cats’ type classes in one go;
- ``import cats.instances.all._`` imports all of the type class instances for the standard library in one go;
- ``import cats.syntax.all._`` imports all of the syntax in one go;
- ``import cats.implicits._`` imports all of the standard type class instances and all of the syntax in one go.

The easiest way to import:

.. code-block:: scala

    import cats._
    import cats.implicits._

