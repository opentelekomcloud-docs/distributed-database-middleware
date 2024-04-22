:original_name: ddm_10_0008.html

.. _ddm_10_0008:

YYYYWEEK
========

Application Scenarios
---------------------

This algorithm applies when data is routed to shards by week. You are advised to use this algorithm together with tbpartition YYYYWEEK(ShardKey).

Instructions
------------

The sharding key must be DATE, DATETIME, or TIMESTAMP.

Data Routing
------------

Use the hash function and enter the year and the week of the year specified in the sharding key value to calculate the hash value. The data route depends on the remainder of the hash value divided by the number of database or table shards.

For example, YYYYWEEK('2012-12-31 12:12:12') is equivalent to (2013 x 54 + 1) % D. D is the number of database or table shards.

.. note::

   -  2012-12-31 is the first week of 2013, so the calculation is 2013 x 54 + 1.
   -  For details on how to use YYYYWEEK, see `YEARWEEK Function <https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_yearweek>`__.

Calculation Method
------------------

.. table:: **Table 1** Required calculation methods

   +--------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------+
   | Condition                                  | Calculation Method                                                                               | Example                                       |
   +============================================+==================================================================================================+===============================================+
   | Database sharding key ≠ Table sharding key | Sharding key: yyyy-MM-dd                                                                         | Sharding key: 2012-12-31                      |
   |                                            |                                                                                                  |                                               |
   |                                            | Database routing result = (yyyy x 54 + Week of the current year) % Database shards               | Database shard: (2013 x 54 + 1) % 8 = 7       |
   |                                            |                                                                                                  |                                               |
   |                                            | Table routing result = (yyyy x 54 + Week of the current year) % Table shards                     | Table shard: (2013 x 54 + 1) % 3 = 1          |
   +--------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------+
   | Database sharding key = Table sharding key | Sharding key: yyyy-MM-dd                                                                         | Sharding key: 2012-12-31                      |
   |                                            |                                                                                                  |                                               |
   |                                            | Table routing result = (yyyy x 54 + Week of the current year) % (Database shards x Table shards) | Database shard: (2013 x 54 + 1) % (8 x 3) = 7 |
   |                                            |                                                                                                  |                                               |
   |                                            | Database routing result = Table routing result/Table shards                                      | Database shard: 7/3 = 2                       |
   |                                            |                                                                                                  |                                               |
   |                                            | .. note::                                                                                        |                                               |
   |                                            |                                                                                                  |                                               |
   |                                            |    Database routing result is rounded off to the nearest integer.                                |                                               |
   +--------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------+

Syntax for Creating Tables
--------------------------

Assume that there are already 8 physical databases in your database instance. Now you want to shard data by week and require that data of the same week be stored in one table and each week within two years should correspond to an independent table, so that you can query data from a physical table in a physical database by the sharding key.

In this scenario, you can select the YYYYWEEK algorithm. Then create at least 106 physical tables for 53 (rounded off) weeks of the two years, each week corresponding to one table. Since you already have 8 physical databases, 14 (14 x 8 = 112 > 106) physical tables should be created in each of them. The number of tables should be an integral multiple of databases. The following is an example SQL statement for creating a table:

.. code-block::

   create table test_yyyymm_tb(
       id int,
       name varchar(30) DEFAULT NULL,
       create_time datetime DEFAULT NULL,
       primary key(id)
   ) ENGINE = InnoDB DEFAULT CHARSET = utf8
   dbpartition by YYYYWEEK(create_time)
   tbpartition by YYYYWEEK(create_time) tbpartitions 14;

Syntax for creating tables when only database sharding is required:

.. code-block::

   create table YYYYWEEK(
       id int,
       name varchar(30) DEFAULT NULL,
       create_time datetime DEFAULT NULL,
       primary key(id)
   ) ENGINE = InnoDB DEFAULT CHARSET = utf8
   dbpartition by YYYYWEEK(create_time);

Precautions
-----------

-  This YYYYWEEK algorithm does not apply if each week of a year corresponds to one database shard. The number of tables must be fixed if database and table sharding is both required.
-  Data of the same week in different years may be routed to the same shard.
