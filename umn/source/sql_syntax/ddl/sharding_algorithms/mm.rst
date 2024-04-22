:original_name: ddm_10_0014.html

.. _ddm_10_0014:

MM
==

Application Scenarios
---------------------

This algorithm applies if you want to shard data by month. One table shard for one month is recommended, and its name is the month number.

Instructions
------------

-  The sharding key must be DATE, DATETIME, or TIMESTAMP.
-  This algorithm can be used only for table sharding. It cannot be used for database sharding.

Data Routing
------------

Use the month number in the sharding key value to find the remainder. This remainder determines which table shard your data is routed to and serves as the name suffix of each table shard.

For example, if the sharding key value is **2019-01-15**, the calculation of the table shard is: Month mod Shards or 1 mod 12 = 1.

Calculation Method
------------------

.. table:: **Table 1** Required calculation methods

   +-----------------------+----------------------------------------------------------------+--------------------------------+
   | Condition             | Calculation Method                                             | Example                        |
   +=======================+================================================================+================================+
   | None                  | Table routing result = Table sharding key value % Table shards | Sharding key value: 2019-01-15 |
   |                       |                                                                |                                |
   |                       |                                                                | Table shard: 1 mod 12 = 1      |
   +-----------------------+----------------------------------------------------------------+--------------------------------+

Syntax for Creating Tables
--------------------------

.. code-block::

   create table test_mm_tb (
       id int,
       name varchar(30) DEFAULT NULL,
       create_time datetime DEFAULT NULL,
       primary key(id)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8
   dbpartition by MOD_HASH(id)
   tbpartition by MM(create_time) tbpartitions 12;

Precautions
-----------

Table shards in each database shard cannot exceed 12 because there are only 12 months a year.
