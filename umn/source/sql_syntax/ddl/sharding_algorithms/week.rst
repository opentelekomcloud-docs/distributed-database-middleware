:original_name: ddm_10_0017.html

.. _ddm_10_0017:

WEEK
====

Application Scenarios
---------------------

This algorithm applies when you want to shard data by day in a week. One table shard for one weekday is recommended.

Instructions
------------

-  The sharding key must be DATE, DATETIME, or TIMESTAMP.
-  This algorithm can be used only for table sharding. It cannot be used for database sharding.

Data Routing
------------

Use the day number of a week in the sharding key value to find the remainder. This remainder determines which table shard your data is routed to and serves as the name suffix of each table shard.

For example, if the sharding key value is **2019-01-15**, the calculation of the table shard is: Day number in a week mod Table shards, that is, 3 mod 7 = 3.

.. note::

   For details on how to calculate a weekday for any particular date, see `WEEKDAY(date) <https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_weekday>`__.

   Run the following SQL statement to query the WEEKDAY value for a specified date:

   .. code-block::

      mysql> SELECT WEEKDAY('2019-01-15');
                    -> 1

   If the value returned from the above SQL statement is **1**, the weekday for date 2019-01-15 is Tuesday. Sunday is the first day of the week, so Tuesday is the third day of the week.

Calculation Method
------------------

.. table:: **Table 1** Required calculation methods

   +-----------------------+----------------------------------------------------------------+--------------------------------+
   | Condition             | Calculation Method                                             | Example                        |
   +=======================+================================================================+================================+
   | None                  | Table routing result = Table sharding key value % Table shards | Sharding key value: 2019-01-15 |
   |                       |                                                                |                                |
   |                       |                                                                | Table shard: 3 mod 7= 3        |
   +-----------------------+----------------------------------------------------------------+--------------------------------+

Syntax for Creating Tables
--------------------------

.. code-block::

   create table test_week_tb (
       id int,
       name varchar(30) DEFAULT NULL,
       create_time datetime DEFAULT NULL,
       primary key(id)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8
   dbpartition by HASH(name)
   tbpartition by WEEK(create_time) tbpartitions 7;

Precautions
-----------

Table shards in each database shard cannot exceed 7 because there are 7 days in a week.
