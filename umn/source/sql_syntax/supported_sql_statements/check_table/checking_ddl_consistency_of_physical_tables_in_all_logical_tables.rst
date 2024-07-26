:original_name: ddm_08_0021.html

.. _ddm_08_0021:

Checking DDL Consistency of Physical Tables in All Logical Tables
=================================================================

**Purpose:** To check DDL consistency of all logical tables in one schema

**Command Format:**

.. code-block:: text

    check table

**Command Output:**

The following output is returned if DDL check results of all logical tables are consistent.

|image1|

The following output is returned if there are logical tables with inconsistent DDL check results.

|image2|

**Output Details:**

Each row contains the check result of a logical table.

-  **DATABASE_NAME**: indicates the schema name.
-  **TABLE_NAME**: indicates the logical table name.
-  **TABLE_TYPE**: indicates the logical table type.

   -  **SINGLE**: indicates that the logical table is unsharded.
   -  **BROADCAST**: indicates that the table is a broadcast table.
   -  **SHARDING**: indicates that the table is sharded.

-  **DDL_CONSISTENCY**: indicates whether DDL results of all physical tables corresponding to the logical table are consistent.
-  **TOTAL_COUNT**: indicates the number of physical tables in the logical table.
-  **INCONSISTENT_COUNT**: indicates the number of physical tables with inconsistent DDL results.
-  **DETAILS**: indicates names of the physical tables with inconsistent DDL check results.

.. |image1| image:: /_static/images/en-us_image_0000001685307210.png
.. |image2| image:: /_static/images/en-us_image_0000001733146277.png
