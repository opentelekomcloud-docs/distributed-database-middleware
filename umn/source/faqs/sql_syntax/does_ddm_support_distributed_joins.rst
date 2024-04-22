:original_name: ddm_04_0015.html

.. _ddm_04_0015:

Does DDM Support Distributed JOINs?
===================================

Yes. DDM supports distributed JOINs.

-  Redundant fields are added during table design.
-  Cross-shard JOIN is implemented by using broadcast tables, ER shards, and ShareJoin.
-  Currently, DDM does not allow cross-schema update or deletion of multiple tables.
