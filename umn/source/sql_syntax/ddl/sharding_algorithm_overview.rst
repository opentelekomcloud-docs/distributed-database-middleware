:original_name: ddm_03_0038.html

.. _ddm_03_0038:

Sharding Algorithm Overview
===========================

Supported Sharding Algorithms
-----------------------------

DDM supports database sharding, table sharding, and a variety of sharding algorithms.

.. table:: **Table 1** Sharding algorithms

   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | Algorithm   | Description                                                                              | Database Sharding Supported | Table Sharding Supported |
   +=============+==========================================================================================+=============================+==========================+
   | MOD_HASH    | Performing a simple modulo operation                                                     | Yes                         | Yes                      |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | MOD_HASH_CI | Performing a simple modulo operation (case-insensitive)                                  | Yes                         | Yes                      |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | HASH        | Performing a simple modulo operation                                                     | Yes                         | Yes                      |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | RANGE       | Performing a RANGE-based operation                                                       | Yes                         | No                       |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | RIGHT_SHIFT | Arithmetic right shifting of a sharding key value and then performing a modulo operation | Yes                         | Yes                      |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | YYYYMM      | Getting a hash code for a YearMonth object and then performing a modulo operation        | Yes                         | Yes                      |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | YYYYDD      | Getting a hash code for a YearDay object and then performing a modulo operation          | Yes                         | Yes                      |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | YYYYWEEK    | Getting a hash code for a YearWeek object and then performing a modulo operation         | Yes                         | Yes                      |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | MM          | Getting a hash code for a MONTH object and then performing a modulo operation            | No                          | Yes                      |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | DD          | Getting a hash code for a DAY object and then performing a modulo operation              | No                          | Yes                      |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | MMDD        | Getting a hash code for a MonthDay object and then performing a modulo operation         | No                          | Yes                      |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+
   | WEEK        | Getting a hash code for a WEEK object and then performing a modulo operation             | No                          | Yes                      |
   +-------------+------------------------------------------------------------------------------------------+-----------------------------+--------------------------+

.. note::

   -  Database and table sharding keys cannot be left blank.
   -  In DDM, sharding of a logical table is defined by the sharding function (number of shards and routing algorithm) and the sharding key (MySQL data type).
   -  If a logical table uses different database and table sharding algorithms, DDM will perform full-shard or full-table scanning when you do not specify database and table conditions in SQL queries.

Data Type of Sharding Algorithms
--------------------------------

Different sharding algorithms support different data types. The following table lists supported data types.

.. table:: **Table 2** Supported data types

   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | Sharding Algorithm | TINYINT | SMALLINT | MEDIUMINT | INTEGER | INT | BIGINT | CHAR | VARCHAR | DATE | DATETIME | TIMESTAMP | Others |
   +====================+=========+==========+===========+=========+=====+========+======+=========+======+==========+===========+========+
   | MOD_HASH           | Y       | Y        | Y         | Y       | Y   | Y      | Y    | Y       | N    | N        | N         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | MOD_HASH_CI        | Y       | Y        | Y         | Y       | Y   | Y      | Y    | Y       | N    | N        | N         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | HASH               | Y       | Y        | Y         | Y       | Y   | Y      | Y    | Y       | N    | N        | N         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | RANGE              | Y       | Y        | Y         | Y       | Y   | Y      | N    | N       | N    | N        | N         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | RIGHT_SHIFT        | Y       | Y        | Y         | Y       | Y   | Y      | N    | N       | N    | N        | N         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | YYYYMM             | N       | N        | N         | N       | N   | N      | N    | N       | Y    | Y        | Y         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | YYYYDD             | N       | N        | N         | N       | N   | N      | N    | N       | Y    | Y        | Y         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | YYYYWEEK           | N       | N        | N         | N       | N   | N      | N    | N       | Y    | Y        | Y         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | MM                 | N       | N        | N         | N       | N   | N      | N    | N       | Y    | Y        | Y         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | DD                 | N       | N        | N         | N       | N   | N      | N    | N       | Y    | Y        | Y         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | MMDD               | N       | N        | N         | N       | N   | N      | N    | N       | Y    | Y        | Y         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+
   | WEEK               | N       | N        | N         | N       | N   | N      | N    | N       | Y    | Y        | Y         | N      |
   +--------------------+---------+----------+-----------+---------+-----+--------+------+---------+------+----------+-----------+--------+

.. note::

   **Y** indicates that the data type is supported, and **N** indicates that the data type is not supported.

Table Creation Syntax of Sharding Algorithms
--------------------------------------------

DDM is compatible with table creation syntax of MySQL databases and adds keyword **partition_options** for databases and tables sharding.

.. code-block::

   CREATE TABLE [IF NOT EXISTS] tbl_name
   (create_definition,...)
   [table_options]
   [partition_options]
    partition_options:
     DBPARTITION BY
          {{RANGE|HASH|MOD_HASH|RIGHT_SHIFT|YYYYMM|YYYYWEEK|YYYYDD}([column])}
         [TBPARTITION BY
   {{HASH|MOD_HASH|UNI_HASH|RIGHT_SHIFT|YYYYMM|YYYYWEEK|YYYYDD}(column)}
             [TBPARTITIONS num]
         ]
