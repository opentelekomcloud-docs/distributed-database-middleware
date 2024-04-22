:original_name: ddm_10_0016.html

.. _ddm_10_0016:

MMDD
====

Application Scenarios
---------------------

This algorithm applies when you want to shard data by day in a year. One table shard for one day (at most 366 days in a year) is recommended.

Instructions
------------

-  The sharding key must be DATE, DATETIME, or TIMESTAMP.
-  This algorithm can be used only for table sharding. It cannot be used for database sharding.

Data Routing
------------

Use the day number of a year in the sharding key value to find the remainder. This remainder determines which table shard your data is routed to and serves as the name suffix of each table shard.

For example, if the sharding key value is **2019-01-15**, the calculation of the table shard is: Day number in a year mod Table shards, that is, 15 mod 366 = 15.

Calculation Method
------------------

.. table:: **Table 1** Required calculation methods

   +-----------------------+----------------------------------------------------------------+--------------------------------+
   | Condition             | Calculation Method                                             | Example                        |
   +=======================+================================================================+================================+
   | None                  | Table routing result = Table sharding key value % Table shards | Sharding key value: 2019-01-15 |
   |                       |                                                                |                                |
   |                       |                                                                | Table shard: 15 % 366= 15      |
   +-----------------------+----------------------------------------------------------------+--------------------------------+

Syntax for Creating Tables
--------------------------

.. code-block::

   create table test_mmdd_tb (
       id int,
       name varchar(30) DEFAULT NULL,
       create_time datetime DEFAULT NULL,
       primary key(id)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8
   dbpartition by MOD_HASH(name)
   tbpartition by MMDD(create_time) tbpartitions 366;

Precautions
-----------

Table shards in each database shard cannot exceed 366 because there are at most 366 days in a year.
