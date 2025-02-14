:original_name: ddm_08_0015.html

.. _ddm_08_0015:

SHOW RULE
=========

**Command Format 1:**

**show rule**;

It is used to view the sharding rule of each logical table in a certain schema.

Command output:

|image1|

**Command Format 2:**

**show rule from** *<table_name>*;

It is used to view the sharding rule of a specific logical table in a certain schema.

Command output:

|image2|

**Output Details:**

**TABLE_NAME**: indicates the name of the logical table.

**BROADCAST**: specifies whether the table is a broadcast table. **0** indicates that the table is not a broadcast table. **1** indicates the table is a broadcast table.

**DB_PARTITION_KEY**: indicates the database sharding key. Leave this field blank if database sharding is not required.

**DB_PARTITION_POLICY**: indicates the database sharding algorithm. The value can be **HASH**, **YYYYMM**, **YYYYDD**, and **YYYYWEEK**.

**DB_PARTITION_COUNT**: indicates the number of database shards.

**DB_PARTITION_OFFSET**: indicates where a new database shard starts from.

**PARTITION_RANGE**: indicates the sharding range when the database sharding algorithm is range.

**TB_PARTITION_KEY**: indicates the table sharding key. Leave this field blank if table sharding is not required.

**TB_PARTITION_POLICY**: indicates the table sharding algorithm. The value can be **HASH**, **MM**, **DD**, **MMDD**, or **WEEK**.

**TB_PARTITION_COUNT**: indicates the number of physical tables in each database shard.

**TB_PARTITION_OFFSET**: indicates where a new physical table starts from.

.. |image1| image:: /_static/images/en-us_image_0000001733146413.png
.. |image2| image:: /_static/images/en-us_image_0000001733266529.png
