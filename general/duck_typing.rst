.. _duck_typing:

Duck typing
===========

Duck typing is an approach to determine whether an object can be used for
a particular purpose or not.
With normal typing, suitability is determined by an object's type.
In duck typing, an object's suitability is determined by the presence
of certain methods and properties, rather than the type of the object itself.

The name comes from the phrase "If it looks like a duck and quacks like a duck,
it's a duck".

.. code-block:: Python
    :caption: Duck typing

    class Duck:
        def quack(self):
            return "Quack!"

    class Cat:
        def quack(self):
            return "Cats quack sometimes!"

    def quack_me(entity):
        # We expect the interface here, not the type.
        print(entity.quack())

    quack_me(Duck())
    # Quack!

    quack_me(Cat())
    # Cats quack sometimes!

Scala has its own approach to leverage duck typing called
:ref:`structural type <structural_type>`.
