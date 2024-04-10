:original_name: ddm_10_0015.html

.. _ddm_10_0015:

DD
==

Application Scenarios
---------------------

This algorithm applies if you want to shard data by date. One table shard for one day is recommended, and its name is the day number.

Instructions
------------

-  The sharding key must be DATE, DATETIME, or TIMESTAMP.
-  This algorithm can be used only for table sharding. It cannot be used for database sharding.

Data Routing
------------

Use the day number in the sharding key value to find the remainder. This remainder determines which table shard your data is routed to and serves as the name suffix of the table shard.

For example, if the sharding key value is **2019-01-15**, the calculation of the table shard is: Day number in a month mod Table shards, that is, 15 mod 31 = 15.

Calculation Method
------------------

.. table:: **Table 1** Required calculation methods

   +-----------------------+----------------------------------------------------------------+--------------------------------+
   | Condition             | Calculation Method                                             | Example                        |
   +=======================+================================================================+================================+
   | None                  | Table routing result = Table sharding key value % Table shards | Sharding key value: 2019-01-15 |
   |                       |                                                                |                                |
   |                       |                                                                | Table shard: 15 mod 31 = 15    |
   +-----------------------+----------------------------------------------------------------+--------------------------------+

Syntax for Creating Tables
--------------------------

.. code-block::

   create table test_dd_tb (
       id int,
       name varchar(30) DEFAULT NULL,
       create_time datetime DEFAULT NULL,
       primary key(id)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8
   dbpartition by MOD_HASH(id)
   tbpartition by DD(create_time) tbpartitions 31;

Precautions
-----------

Table shards in each database shard cannot exceed 31 because there are at most 31 days in a month.
