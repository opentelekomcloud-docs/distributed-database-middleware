:original_name: ddm_10_0013.html

.. _ddm_10_0013:

Range
=====

Application Scenarios
---------------------

This algorithm applies to routing data in different ranges to different shards. Less-than signs (<), greater-than signs (>), and BETWEEN ... AND ... are frequently used in SQL queries.

Instructions
------------

The sharding key can only be an integer, a date, or used in combination with a date function. If a date function is used, the sharding key must be DATE, DATETIME, or TIMESTAMP.

Data Routing
------------

Data is routed to different shards by the sharding key value based on algorithm metadata rules.

Metadata needs to be set when a table is created. For example, if there are eight shards in one schema, the metadata range can be [1-2]=0, [3-4]=1, [5-6]=2, [7-8]=3, [9-10]=4, [11-12]=5, [13-14]=6, and default=7. Data is routed to shards by the sharding key value based on the range.

Calculation Method
------------------

**Method 1: Use an Integer as the Sharding Key**

.. table:: **Table 1** Required calculation methods when the sharding key is the integer data type

   +-----------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Condition             | Calculation Method                                                                                                   | Example                                                                                         |
   +=======================+======================================================================================================================+=================================================================================================+
   | Integer sharding keys | Database routing result: Data is routed to different shards based on the sharding key and the preset metadata range. | Data is routed to shard1 if the sharding key value is 3 and the preset metadata range is [3-4]. |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+

**Method 2: Use a Date as the Sharding Key**

.. table:: **Table 2** Supported date functions

   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+
   | Date Function         | Calculation Method                                                                                                                                                                                                                             | Example                      |
   +=======================+================================================================================================================================================================================================================================================+==============================+
   | year()                | year(yyyy-MM-dd)=yyyy                                                                                                                                                                                                                          | year('2019-10-11')=2019      |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+
   | month()               | month(yyyy-MM-dd)=MM                                                                                                                                                                                                                           | month('2019-10-11')=10       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+
   | weekofyear()          | weekofyear(yyyy-MM-dd)=Week number of the current year                                                                                                                                                                                         | weekofyear ('2019-10-11')=41 |
   |                       |                                                                                                                                                                                                                                                |                              |
   |                       | .. note::                                                                                                                                                                                                                                      |                              |
   |                       |                                                                                                                                                                                                                                                |                              |
   |                       |    The Weekofyear() function is used to return the week number of a specific date represented by the date parameter in a year. For details, see `WEEK <https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_week>`__. |                              |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+
   | day()                 | day(yyyy-MM-dd)=dd                                                                                                                                                                                                                             | day ('2019-10-11')=11        |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+

.. table:: **Table 3** Calculation methods

   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | Condition         | Calculation Method                                                                                                                                    | Example                                                                                                                                 |
   +===================+=======================================================================================================================================================+=========================================================================================================================================+
   | Date sharding key | Database routing: Data is routed to different database shards based on the date function (database sharding key value) and the preset metadata range. | Data is routed to shard 4 based on the metadata range 9-10 when the sharding key value is 10: month(2019-10-11)=10 belongs to [9-10]=4. |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+

Syntax for Creating Tables
--------------------------

.. code-block:: text

   create table range_tb(
       id int,
       name varchar(30) DEFAULT NULL,
       create_time datetime DEFAULT NULL,
       primary key(id)
       )
   dbpartition by range(id)
   {
       1-2=0,
       3-4=1,
       5-6=2,
       7-8=3,
       9-10=4,
       11-12=5,
       13-14=6,
       default=7
   };

Precautions
-----------

None
