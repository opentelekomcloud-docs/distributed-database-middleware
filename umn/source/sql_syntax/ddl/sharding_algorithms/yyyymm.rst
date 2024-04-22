:original_name: ddm_10_0006.html

.. _ddm_10_0006:

YYYYMM
======

Application Scenarios
---------------------

This algorithm applies when data is routed to shards by year and month. You are advised to use this algorithm together with tbpartition YYYYMM(ShardKey).

Instructions
------------

The sharding key must be DATE, DATETIME, or TIMESTAMP.

Data Routing
------------

The data route depends on the remainder of the sharding key hash value divided by database shards. Enter the year and month into the hash function to obtain the hash value.

For example, YYYYMM ('2012-12-31 12:12:12') is equivalent to (2012 x 12 + 12) % D. D is the number of database or table shards.

Calculation Method
------------------

.. table:: **Table 1** Required calculation methods

   +--------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------+
   | Condition                                  | Calculation Method                                                         | Example                                      |
   +============================================+============================================================================+==============================================+
   | Database sharding key ≠ Table sharding key | Sharding key: yyyy-MM-dd                                                   | Sharding key: 2012-11-20                     |
   |                                            |                                                                            |                                              |
   |                                            | Database routing result = (yyyy x 12 + MM) % Database shards               | Database shard: (2012 x 12 + 11) % 8 = 3     |
   |                                            |                                                                            |                                              |
   |                                            | Table routing result = (yyyy x 12 + MM) % Table shards                     | Table shard: (2012 x 12 + 11) % 3 = 2        |
   +--------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------+
   | Database sharding key = Table sharding key | Sharding key: yyyy-MM-dd                                                   | Sharding key: 2012-11-20                     |
   |                                            |                                                                            |                                              |
   |                                            | Table routing result = (yyyy x 12 + MM) % (Database shards x Table shards) | Table shard: (2012 x 12 + 11) % (8 x 3) = 11 |
   |                                            |                                                                            |                                              |
   |                                            | Database routing result = Table routing result/Table shards                | Database shard: 11 % 3 = 3                   |
   |                                            |                                                                            |                                              |
   |                                            | .. note::                                                                  |                                              |
   |                                            |                                                                            |                                              |
   |                                            |    Database routing result is rounded off to the nearest integer.          |                                              |
   +--------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------+

Syntax for Creating Tables
--------------------------

Assume that there are already 8 physical databases in your database instance. Now you want to shard data by year and month and require that data of the same month be stored in one table and each month within two years should correspond to an independent table, so that you can query data from a physical table in a physical database by the sharding key.

In this scenario, you can select the YYYYMM algorithm. Then create 24 physical tables for 24 months of the two years, each month corresponding to one table. Since you already have 8 physical databases, three physical tables should be created in each of them. The following is an example SQL statement for creating a table:

.. code-block::

   create table test_yyyymm_tb(
       id int,
       name varchar(30) DEFAULT NULL,
       create_time datetime DEFAULT NULL,
       primary key(id)
   ) ENGINE = InnoDB DEFAULT CHARSET = utf8
   dbpartition by YYYYMM(create_time)
   tbpartition by YYYYMM(create_time) tbpartitions 3;

Syntax for creating tables when only database sharding is required:

.. code-block::

   create table YYYYMM(
       id int,
       name varchar(30) DEFAULT NULL,
       create_time datetime DEFAULT NULL,
       primary key(id)
   ) ENGINE = InnoDB DEFAULT CHARSET = utf8
   dbpartition by YYYYMM(create_time);

Precautions
-----------

-  This YYYYMM algorithm does not apply if each month of a year corresponds to one database shard. The number of tables must be fixed if database and table sharding is both required.
-  Data of the same month in different years may be routed to the same database or table. The result depends on the number of tables.
