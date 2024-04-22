:original_name: ddm_01_0016.html

.. _ddm_01_0016:

Core Functions
==============

.. table:: **Table 1** DDM main functions

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Function                          | Description                                                                                                                                                                                                                                                                                                                                                             |
   +===================================+=========================================================================================================================================================================================================================================================================================================================================================================+
   | Horizontal sharding               | Select a sharding key when creating a logical table. DDM will generate a sharding rule and horizontally shard data.                                                                                                                                                                                                                                                     |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Flexible shard configuration      | DDM supports both compute and storage scaling. You can add nodes to a DDM instance or scale up its node class. Alternatively, increase shards or data nodes to distribute data from one large table to multiple tables or scale out storage resources. Compute scaling is undetectable to your applications. Storage scaling minimizes service interruption to seconds. |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Distributed transactions          | DDM processes three types of transactions, including single-shard, FREE, and Extended Architecture (XA).                                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   | -  Single-shard: Transactions cannot be committed across shards.                                                                                                                                                                                                                                                                                                        |
   |                                   | -  FREE: Transactions are committed across shards. A transaction is not rolled back when it fails to be executed by any shard, causing data inconsistency.                                                                                                                                                                                                              |
   |                                   | -  XA: Transactions are committed in two phases. If a transaction fails to be executed by any shard, all work done will be rolled back to ensure data consistency.                                                                                                                                                                                                      |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Highly compatible SQL syntax      | DDM is highly compatible with the MySQL licenses and syntax.                                                                                                                                                                                                                                                                                                            |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Read and write splitting          | Read and write requests can be split without modifying the application code, and this is totally transparent to applications. You only need to create read replicas for a MySQL instance associated with your DDM instance and configure a read policy, and a large number of concurrent requests can read data from those read replicas.                               |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Global sequence                   | DDM allows you to use globally unique, distributed, and ascending SNs as primary or unique keys or to meet your requirements in specific scenarios.                                                                                                                                                                                                                     |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DDM console                       | The DDM console enables you to manage and maintain DDM instances, schemas, and accounts.                                                                                                                                                                                                                                                                                |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Related Services
----------------

-  VPC

   DDM instances are deployed in an isolated VPC and you can configure IP addresses and bandwidth for accessing these DDM instances and use a security group to control access to them.

-  ECS

   You can access your DDM instance through an ECS.

-  Relational Database Service (RDS)

   After you create a DDM instance, you can associate it with RDS for MySQL instances in the same VPC to obtain separated storage resources.

-  GaussDB(for MySQL)

   After you create a DDM instance, you can associate it with GaussDB(for MySQL) instances in the same VPC to obtain separated storage resources.

-  Cloud Trace Service (CTS)

   CTS records operations on your DDM resources for later query, audit, and backtrack.

-  Elastic Load Balance (ELB)

   ELB distributes incoming traffic to multiple backend servers based on the forwarding policy to balance workloads. So, it can expand external service capabilities of DDM and eliminate single points of failure (SPOFs) to improve service availability.


.. figure:: /_static/images/en-us_image_0000001700277302.png
   :alt: **Figure 1** Relationship among DDM, VPC, ECS, and data nodes

   **Figure 1** Relationship among DDM, VPC, ECS, and data nodes
