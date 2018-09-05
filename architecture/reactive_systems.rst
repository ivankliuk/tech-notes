Reactive principles
===================

.. image :: /images/reactive_principles.svg
   :alt: Reactive principles

Responsive
----------

The system consistently responds in a timely fashion.

Resilient
---------

The system remains responsive, even when failures occur. Resilience is achieved
by replication, isolation and delegation: failures are isolated to a single
component, recovery is delegated to an external component.

Elastic
-------

The system remains responsive, despite increases (or decreases) in the system
load: scaling up provides responsiveness during peak, while scale down improves
cost effectiveness.

Message Driven
--------------

The system is built on a foundation of asynchronous, non-blocking messages. It
provides loose coupling, isolation and location transparency.
