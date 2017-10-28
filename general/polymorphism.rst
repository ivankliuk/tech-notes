Polymorphism
============

Polymorphism is the provision of a single interface to entities of different
types.

Polymorphism types:

.. _ad-hoc_polymorphism:

- Ad-hoc polymorphism: when a function has different implementations depending
  on a limited range of individually specified types and combinations.
  Ad-hoc polymorphism is supported in many languages using function overloading.
  All of the following works due to add operation (``__add__`` method) is
  implemented for ``list``, ``float``, ``int`` etc.

.. code-block:: python
    :caption: Ad-hoc polymorphism (Python)

        >>> [1, 2, 3] + [4, 5, 6]
        [1, 2, 3, 4, 5, 6]
        >>> 1 + 2
        3
        >>> 4.5 + 1
        5.5

- Parametric polymorphism (generics): when code is written without mention of
  any specific type and thus can be used transparently with any number of new
  types.

.. code-block:: scala
    :caption: Parametric polymorphism (Scala)

        class Stack[T] {
          private var elements: List[T] = Nil

          def push(x: T): Unit = elements = x :: elements

          def isEmpty: Boolean = elements.isEmpty

          def pop: T = {
            val (x, xs) = (elements.head, elements.tail)
            elements = xs
            x
          }
        }

        val stackOfInts = new Stack[Int]
        // stackOfInts: Stack[Int] = Stack@4cd70290
        stackOfInts.push(1)
        stackOfInts.push(2)
        stackOfInts.push(3)
        stackOfInts.pop
        // res1: Int = 3
        stackOfInts.pop
        // res2: Int = 2

        val stackOfStrings = new Stack[String]
        // stackOfStrings: Stack[String] = Stack@2da3e198
        stackOfStrings.push("a")
        stackOfStrings.push("b")
        stackOfStrings.push("c")
        stackOfStrings.pop
        // res9: String = c
        stackOfStrings.pop
        // res10: String = b

- Subtyping: refers to compatibility of interfaces. A type *Duck* is a subtype
  of *Bird* if every function that can be invoked on an object of type *Bird*
  can also be invoked on an object of type *Duck*.

.. code-block:: scala
    :caption: Subtyping (Scala)

      trait Bird {
        val sound: String
      }

      class Duck extends Bird {
        override val sound: String = "Quack!"
      }

      class Owl extends Bird {
        override val sound: String = "Hoot!"
      }

      def getSound(bird: Bird): String = bird.sound

      val owl = new Owl
      // owl: Owl = Owl@199697be

      val duck = new Duck
      // duck: Duck = Duck@c03ff84

      getSound(owl)
      // res1: String = Hoot!

      getSound(duck)
      // res2: String = Quack!


TODO: http://www.cmi.ac.in/~madhavan/courses/pl2009/lecturenotes/lecture-notes/node28.html