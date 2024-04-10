:original_name: ddm-08-0022.html

.. _ddm-08-0022:

Checking DDL Consistency of Physical Tables in One Logical Table
================================================================

**Purpose:** To check DDL consistency of physical tables in a specific logical table

**Command Format:**

.. code-block:: text

   check table <table_name>

**Command Output:**

If the returned result set is empty, DDL results of physical tables in this logical table are consistent.

|image1|

If the returned result set is not empty, there are physical tables with inconsistent DDL results.

|image2|

**Output Details:**

Each row displays details of a physical table with inconsistent DDL results.

-  **DATABASE_NAME**: indicates the database shard containing the physical table.
-  **TABLE_NAME**: indicates the name of the physical table.
-  **TABLE_TYPE**: indicates the type of the logical table that the physical table belongs to.
-  **EXTRA_COLUMNS**: indicates extra columns in the physical table.
-  **MISSING_COLUMNS**: indicates missing columns in the physical table.
-  **DIFFERENT_COLUMNS**: indicates name and type columns whose attributes are inconsistent in the physical table.
-  **KEY_DIFF**: indicates inconsistent indexes in the physical table.
-  **ENGINE_DIFF**: indicates inconsistent engines in the physical table.
-  **CHARSET_DIFF**: indicates inconsistent character sets in the physical table.
-  **COLLATE_DIFF**: indicates inconsistent collations in the physical table.
-  **EXTRA_PARTITIONS**: indicates extra partitions in the physical table. This field is only available to partitioned tables.
-  **MISSING_PARTITIONS**: indicates missing partitions in the physical table. This field is only available to partitioned tables.
-  **DIFFERENT_PARTITIONS**: indicates partitions with inconsistent attributes in the physical table. This field is only available to partitioned tables.
-  **EXTRA_INFO**: indicates other information such as missing physical tables.

.. |image1| image:: /_static/images/en-us_image_0000001733266429.png
.. |image2| image:: /_static/images/en-us_image_0000001685147494.png
