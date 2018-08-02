.. _structural_type:

Structural type
===============

Structural Type allow to set a behaviour very similar to what dynamic
languages allow to do when they support :ref:`duck typing <duck_typing>`.

The methods in a structural type are called via reflection, which is a lot
slower on the JVM than a regular method call. You can define it either
as a function parameter or as a type one.

.. code-block:: scala
    :caption: Structural type definitions

    val printSound = (animal: {def sound(): String}) => println(animal.sound())
    // printSound: AnyRef{def sound(): String} => Unit = $$Lambda$5991/712224434@1dd12065

    def printSound1[A <: { def sound(): String }](animal: A): Unit = println(animal.sound())
    // printSound1: [A <: AnyRef{def sound(): String}](animal: A)Unit

    class Dog {
      def sound(): String = "Woof!"
    }

    val dog = new Dog()
    // dog: Dog = Dog@47d057ea

    printSound(dog)
    // Woof!

    printSound1(dog)
    // Woof!


An interface of object you're passing as the parameter must have exactly
the same signature as the structural type definition:

.. code-block:: scala
    :caption: Interface object

    def printSound(animal: {def sound(): String}): Unit = println(animal.sound())
    // printSound: (animal: AnyRef{def sound(): String})Unit

    class WhiteCat {
      def sound = "Meow!"
    }

    class RedCat {
      val sound = "Meow-meow!"
    }

    class BlackCat {
      def sound(): String = "Meow-meow-meow!"
    }

    printSound(new WhiteCat())
    // <console>:14: error: type mismatch;
    //  found   : WhiteCat
    //  required: AnyRef{def sound(): String}
               printSound(new WhiteCat())
                          ^

    printSound(new RedCat)
    // <console>:14: error: type mismatch;
    //  found   : RedCat
    //  required: AnyRef{def sound(): String}
               printSound(new RedCat)
                          ^

    printSound(new BlackCat)
    // Meow-meow-meow!
