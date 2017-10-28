General
=======

Iterable/iterator
-----------------

An iterable object is an object that implements ``__iter__``. ``__iter__`` is
expected to return an iterator object.

An iterator is an object that implements ``next``.
``next`` is expected to return the next element of the iterable object that
returned it, and raise a ``StopIteration`` exception when no more elements are
available.
