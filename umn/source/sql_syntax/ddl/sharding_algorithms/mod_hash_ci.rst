:original_name: ddm_12_0007.html

.. _ddm_12_0007:

MOD_HASH_CI
===========

Application Scenarios
---------------------

This algorithm applies if you want to route data to different database shards by user ID or order ID.

Instructions
------------

The sharding key must be CHAR, VARCHAR, INT, INTEGER, BIGINT, MEDIUMINT, SMALLINT, TINYINT, or DECIMAL (the precision can be 0).

Data Routing
------------

The data route depends on the remainder of the sharding key value divided by database or table shards. MOD_HASH is case-sensitive, but MOD_HASH_CI is not.

Calculation Method
------------------

**Method 1: Use an Integer as the Sharding Key**

.. table:: **Table 1** Required calculation methods when the sharding key is the integer data type

   +--------------------------------------------+------------------------------------------------------------------------------+--------------------------------+
   | Condition                                  | Calculation Method                                                           | Example                        |
   +============================================+==============================================================================+================================+
   | Database sharding key ≠ Table sharding key | Database routing result = Database sharding key value % Database shards      | Database shard: 16 % 8 = 0     |
   |                                            |                                                                              |                                |
   |                                            | Table routing result = Table sharding key value % Table shards               | Table shard: 16 % 3 = 1        |
   +--------------------------------------------+------------------------------------------------------------------------------+--------------------------------+
   | Database sharding key = Table sharding key | Table routing result = Sharding key value % (Database shards x Table shards) | Table shard: 16 % (8 x 3) = 16 |
   |                                            |                                                                              |                                |
   |                                            | Database routing result = Table routing result/Table shards                  | Database shard: 16/3 = 5       |
   |                                            |                                                                              |                                |
   |                                            | .. note::                                                                    |                                |
   |                                            |                                                                              |                                |
   |                                            |    Database routing result is rounded off to the nearest integer.            |                                |
   +--------------------------------------------+------------------------------------------------------------------------------+--------------------------------+

**Method 2: Use a String as the Sharding Key**

.. table:: **Table 2** Required calculation methods when the sharding key is the string data type

   +--------------------------------------------+------------------------------------------------------------------------------------+----------------------------------------------------+
   | Condition                                  | Calculation Method                                                                 | Example                                            |
   +============================================+====================================================================================+====================================================+
   | Database sharding key ≠ Table sharding key | Database routing result = hash(Database sharding key value) % Database shards      | hash('abc') = 'abc'.toUpperCase().hashCode()=64578 |
   |                                            |                                                                                    |                                                    |
   |                                            | Table routing result = hash(Table sharding key value) % Table shards               | Database shard: 64578 % 8 = 2;                     |
   |                                            |                                                                                    |                                                    |
   |                                            |                                                                                    | Table shard: 64578 % 3 = 0;                        |
   +--------------------------------------------+------------------------------------------------------------------------------------+----------------------------------------------------+
   | Database sharding key = Table sharding key | Table routing result = hash(Sharding key value) % (Database shards x Table shards) | hash('abc') = 'abc'.toUpperCase().hashCode()=64578 |
   |                                            |                                                                                    |                                                    |
   |                                            | Database routing result = Table routing result/Table shards                        | Table shard: 64578 % (8 x 3) = 18                  |
   |                                            |                                                                                    |                                                    |
   |                                            | .. note::                                                                          | Database shard: 18/3 = 6                           |
   |                                            |                                                                                    |                                                    |
   |                                            |    Database routing result is rounded off to the nearest integer.                  |                                                    |
   +--------------------------------------------+------------------------------------------------------------------------------------+----------------------------------------------------+

Syntax for Creating Tables
--------------------------

-  Assume that you use field **ID** as the sharding key to shard databases based on MOD_HASH_CI:

   .. code-block::

      create table mod_hash_ci_tb(
          id int,
          name varchar(30) DEFAULT NULL,
          create_time datetime DEFAULT NULL,
          primary key(id)
      ) ENGINE = InnoDB DEFAULT CHARSET = utf8 dbpartition by mod_hash_ci(id);

-  Assume that you use field **ID** as the sharding key to shard databases and tables based on MOD_HASH_CI:

   .. code-block::

      create table mod_hash_ci_tb(
          id int,
          name varchar(30) DEFAULT NULL,
          create_time datetime DEFAULT NULL,
          primary key(id)
      ) ENGINE = InnoDB DEFAULT CHARSET = utf8
      dbpartition by mod_hash_ci(id)
      tbpartition by mod_hash_ci(id) tbpartitions 4;

Precautions
-----------

The MOD_HASH_CI algorithm is a simple way to find the remainder of the sharding key value divided by shards. This algorithm features even distribution of sharding key values to ensure even results.
