:original_name: ddm_03_0069.html

.. _ddm_03_0069:

Assessment
==========

Before changing shards, you need to carry out a preliminary evaluation and determine the number of new shards, whether to scale up the current DDM node class, and the number of required data nodes and their specifications.

-  Data volume: Run **show db status** to query the volume of data involved.
-  DDM node class: Determine nodes of the DDM instance and vCPUs and memory size of each node.
-  Data node class: Determine the number of data nodes and vCPUs and memory size of each node.
-  Business scale: Analyze current service scale and growth trend.
