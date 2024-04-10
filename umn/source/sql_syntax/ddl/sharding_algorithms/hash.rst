:original_name: ddm_10_0012.html

.. _ddm_10_0012:

HASH
====

Application Scenarios
---------------------

This algorithm features even distribution of data and sharding tables. Arithmetic operators such as equality (=) and IN operators are often used in SQL queries.

Instructions
------------

The sharding key must be CHAR, VARCHAR, INT, INTEGER, BIGINT, MEDIUMINT, SMALLINT, TINYINT, or DECIMAL (the precision can be 0). The sharding key must be DATE, DATETIME, or TIMESTAMP if you use HASH together with date functions.

Data Routing
------------

Determine the range of each database or table shard using 102400.

For example, if there are 8 shards in each schema, use formula 102400/8 = 12800 to calculate the range of each shard as follows: 0=[0,12799], 1=[12800,25599], 2=[25600,38399], 3=[38400,51199], 4=[51200,63999], 5=[64000,76799], 6=[76800,89599], and 7=[89600,102399].

To determine the route, calculate CRC32 value based on the sharding key value and divide the CRC value by 102400. Then check which range the remainder belongs to.

Calculation Method
------------------

**Method 1: Use a Non-date Sharding Key**

.. table:: **Table 1** Required calculation methods when the sharding key is not the DATE type

   +-----------------------+-----------------------------------------------------------------+---------------------------------------------------------------------+
   | Condition             | Calculation Method                                              | Example                                                             |
   +=======================+=================================================================+=====================================================================+
   | Non-date sharding key | Database routing result = crc32(Database sharding key) % 102400 | Database/Table shard: crc32(16) % 102400 = 49364;                   |
   |                       |                                                                 |                                                                     |
   |                       | Table routing result = crc32(Table sharding key) % 102400       | 49364 belongs to range 3=38400-51199, so data is routed to shard 3. |
   +-----------------------+-----------------------------------------------------------------+---------------------------------------------------------------------+

**Method 2: Use a Date Sharding Key**

.. table:: **Table 2** Supported date functions

   +---------------+--------------------------------------------------------+------------------------------+
   | Date Function | Calculation Method                                     | Example                      |
   +===============+========================================================+==============================+
   | year()        | year(yyyy-MM-dd)=yyyy                                  | year('2019-10-11')=2019      |
   +---------------+--------------------------------------------------------+------------------------------+
   | month()       | month(yyyy-MM-dd)=MM                                   | month('2019-10-11')=10       |
   +---------------+--------------------------------------------------------+------------------------------+
   | weekofyear()  | weekofyear(yyyy-MM-dd)=Week number of the current year | weekofyear ('2019-10-11')=41 |
   +---------------+--------------------------------------------------------+------------------------------+
   | day()         | day(yyyy-MM-dd)=dd                                     | day ('2019-10-11')=11        |
   +---------------+--------------------------------------------------------+------------------------------+

.. table:: **Table 3** Required calculation methods when the sharding key is the DATE type

   +-----------------------+--------------------------------------------------------------------------------+------------------------------------------------------------------+
   | Condition             | Calculation Method                                                             | Example                                                          |
   +=======================+================================================================================+==================================================================+
   | Date sharding key     | Database routing result = crc32(Date function(Database sharding key)) % 102400 | Database/Table shard: crc32(year('2019-10-11')) % 102400 = 5404; |
   |                       |                                                                                |                                                                  |
   |                       | Table routing result = crc32(Date function(Database sharding key)) % 102400    | 5404 belongs to range 0=0-12799, so data is routed to shard 0.   |
   +-----------------------+--------------------------------------------------------------------------------+------------------------------------------------------------------+

Syntax for Creating Tables
--------------------------

-  Assume that you use field ID as the sharding key and the HASH algorithm to shard databases:

   .. code-block::

      create table hash_tb (
          id int,
          name varchar(30) DEFAULT NULL,
          create_time datetime DEFAULT NULL,
          primary key(id)
      ) ENGINE=InnoDB DEFAULT CHARSET=utf8 dbpartition by hash (ID);

-  Assume that you use field ID as the sharding key and the hash algorithm to shard databases and tables:

   .. code-block::

      create table mod_hash_tb (
          id int,
          name varchar(30) DEFAULT NULL,
          create_time datetime DEFAULT NULL,
          primary key(id)
      ) ENGINE=InnoDB DEFAULT CHARSET=utf8
      dbpartition by hash (ID)
      tbpartition by hash (ID) tbpartitions 4;

Precautions
-----------

None
