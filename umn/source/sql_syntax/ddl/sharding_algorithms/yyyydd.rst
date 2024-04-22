:original_name: ddm_10_0007.html

.. _ddm_10_0007:

YYYYDD
======

Application Scenarios
---------------------

This algorithm applies when data is routed to shards by year and day. You are advised to use this algorithm together with tbpartition YYYYDD(ShardKey).

Instructions
------------

The sharding key must be DATE, DATETIME, or TIMESTAMP.

Data Routing
------------

Use the hash function and enter the year and the day of the year specified in the sharding key value to calculate the hash value. The data route depends on the remainder of the hash value divided by the number of database or table shards.

For example, YYYYDD('2012-12-31 12:12:12') is equivalent to (2012 x 366 + 366) % D. D is the number of database or table shards.

.. note::

   2012-12-31 is the 366th day of 2012, so the calculation is 2012 x 366 + 366.

Calculation Method
------------------

.. table:: **Table 1** Required calculation methods

   +--------------------------------------------+--------------------------------------------------------------------------------------------------+--------------------------------------------------+
   | Condition                                  | Calculation Method                                                                               | Example                                          |
   +============================================+==================================================================================================+==================================================+
   | Database sharding key ≠ Table sharding key | Sharding key: yyyy-MM-dd                                                                         | Sharding key: 2012-12-31                         |
   |                                            |                                                                                                  |                                                  |
   |                                            | Database routing result = (yyyy x 366 + Day of the current year) % Database shards               | Database shard: (2012 x 366 + 366) % 8 = 6       |
   |                                            |                                                                                                  |                                                  |
   |                                            | Table routing result = (yyyy x 366 + Day of the current year) % Table shards                     | Table shard: (2012 x 366 + 366) % 3 = 0          |
   +--------------------------------------------+--------------------------------------------------------------------------------------------------+--------------------------------------------------+
   | Database sharding key = Table sharding key | Sharding key: yyyy-MM-dd                                                                         | Sharding key: 2012-12-31                         |
   |                                            |                                                                                                  |                                                  |
   |                                            | Table routing result = (yyyy x 366 + Day of the current year) % (Database shards x Table shards) | Database shard: (2012 x 366 + 366) % (8 x 3) = 6 |
   |                                            |                                                                                                  |                                                  |
   |                                            | Database routing result = Table routing result/Table shards                                      | Database shard: 6/3 = 2                          |
   |                                            |                                                                                                  |                                                  |
   |                                            | .. note::                                                                                        |                                                  |
   |                                            |                                                                                                  |                                                  |
   |                                            |    Database routing result is rounded off to the nearest integer.                                |                                                  |
   +--------------------------------------------+--------------------------------------------------------------------------------------------------+--------------------------------------------------+

Syntax for Creating Tables
--------------------------

Assume that there are already 8 physical databases in your database instance. Now you want to shard data by year and day and require that data of the same day be stored in one table and each day within two years should correspond to an independent table, so that you can query data from a physical table in a physical database by the sharding key.

In this scenario, you can select the YYYYDD algorithm. Then create at least 732 physical tables for 732 days of the two years (366 days for one year), each day corresponding to one table. Since you already have 8 physical databases, 92 (732/8 = 91.5, rounded up to 92) physical tables should be created in each of them. The number of tables should be an integral multiple of databases. The following is an example SQL statement for creating a table:

.. code-block::

   create table test_yyyydd_tb (
           id int,
           name varchar(30) DEFAULT NULL,
           create_time datetime DEFAULT NULL,
           primary key(id)
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8
       dbpartition by YYYYDD(create_time)
       tbpartition by YYYYDD(create_time) tbpartitions 92;

Syntax for creating tables when only database sharding is required:

.. code-block::

   create table YYYYDD(
       id int,
       name varchar(30) DEFAULT NULL,
       create_time datetime DEFAULT NULL,
       primary key(id)
   ) ENGINE = InnoDB DEFAULT CHARSET = utf8
   dbpartition by YYYYDD(create_time);

Precautions
-----------

-  This YYYYDD algorithm does not apply if each day of a year corresponds to one database shard. The number of tables must be fixed if database and table sharding is both required.
-  Data of the same day in different years may be routed to the same shard. The result depends on the number of tables.
