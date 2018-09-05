Distributed systems
===================

*Distributed system* is a collection of resources that are instructed to achieve
a specific task.

*Node (worker)* is a independent computational resource.

*Controller* is a worker which takes responsibility of coordination
the other nodes to ensure consistency and optimal use of resources. It checks
for worker availability and it's health status. If controller is determined that
redundancy is required it will promote a node into a *leader* which take the
ownership of the task assigned. The leader will assign the task to *peers*.

*Cluster* is a group of nodes managed by controller.

*Consensus (gossip) protocol* is a form of communication between nodes in the
cluster. It's used for configuration management, leader election, health
status etc. `Apache Zookeeper <https://zookeeper.apache.org/>`_ is a
centralized service for maintaining metadata about a cluster of distributed
nodes which implements consensus protocol itself.

