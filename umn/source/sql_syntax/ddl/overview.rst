:original_name: ddm_12_0006.html

.. _ddm_12_0006:

Overview
========

DDM supports common DDL operations, such as creating databases, creating tables, and modifying table structure, but the implementation method is different from that in common MySQL databases.

DDL Statements that Can Be Executed on a MySQL Client
-----------------------------------------------------

-  TRUNCATE

   Example:

   .. code-block:: text

      TRUNCATE TABLE t1

   Deletes all data from table t1.

   TRUNCATE TABLE deletes all data from a table and has the DROP permission. In logic, TRUNCATE TABLE is similar to the DELETE statement for deleting all rows from a table.

-  ALTER TABLE

   Example:

   .. code-block:: text

      ALTER TABLE t2 DROP COLUMN c, DROP COLUMN d;

   Deletes columns c and d fom table t2.

   ALTER can add or delete a column, create or drop an index, change the type of an existing column, rename columns or tables, or change the storage engine or comments of a table.

-  DROP INDEX

   Example:

   .. code-block:: text

      DROP INDEX `PRIMARY` ON t;

   Deletes primary key from table t.

-  CREATE INDEX

   Example:

   .. code-block:: text

      CREATE INDEX part_of_name ON customer (name(10));

   Creates an index using the first 10 characters in column name (assuming that there are non-binary character strings in column name).

   CREATE INDEX can add an index to an existing table.
