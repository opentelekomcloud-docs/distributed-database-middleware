:original_name: ddm_10_0004.html

.. _ddm_10_0004:

RIGHT_SHIFT
===========

Application Scenarios
---------------------

This algorithm applies if a large difference appears in high-digit part but a small difference in low-digit part of sharding key values. Using this algorithm ensures uniform distribution of remainders calculated from sharding key values. Therefore, data is evenly routed to different shards.

Instructions
------------

The sharding key value is an integer.

Data Routing
------------

The data route depends on the remainder of the new sharding key value divided by the number of database or table shards. To change the sharding key value, you need to convert the value into a binary number and right shift its bits to gain a new binary number. The number of moved bits is specified in DDL statements. Then, convert the new binary number into a decimal number. This decimal number is the changed sharding key value.

Calculation Method
------------------

.. table:: **Table 1** Required calculation methods

   +--------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | Condition                                  | Calculation Method                                                                                                                   | Example                                                             |
   +============================================+======================================================================================================================================+=====================================================================+
   | Database sharding key ≠ Table sharding key | Database routing result = Database sharding key value % Database shards                                                              | Database shard: (123456 >> 4) % 8 = 4                               |
   |                                            |                                                                                                                                      |                                                                     |
   |                                            | Table routing result = Table sharding key value % Table shards                                                                       | Table shard: (123456 >> 4) % 3 = 0                                  |
   +--------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | Database sharding key = Table sharding key | Database routing result = Sharding key value % Database shards                                                                       | Database shard: (123456 >> 4) % 8 = 4                               |
   |                                            |                                                                                                                                      |                                                                     |
   |                                            | Table routing result = (Sharding key value % Database shards) x Table shards + (Sharding key value / Database shards) % Table shards | Table table: ((123456 >> 4) % 8) x 3 + ((123456 >> 4) / 8) % 3 = 13 |
   +--------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+

Syntax for Creating Tables
--------------------------

.. code-block::

   create table RIGHT_SHIFT(
       id int,
       name varchar(30) DEFAULT NULL,
       create_time datetime DEFAULT NULL,
       primary key(id)
   ) ENGINE = InnoDB DEFAULT CHARSET = utf8
   dbpartition by RIGHT_SHIFT(id, 4)
   tbpartition by RIGHT_SHIFT(id, 4) tbpartitions 2;

Precautions
-----------

-  The number of shifts cannot exceed the number of bits occupied by the integer type.
