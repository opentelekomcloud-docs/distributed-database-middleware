:original_name: ddm_08_0007.html

.. _ddm_08_0007:

REPLACE
=======

REPLACE is used to insert rows into or replace rows in a table.

Common Syntax
-------------

.. code-block::

   replace into table(col1,col2,col3)
   values(value1,value2,value3)

Syntax Constraints
------------------

-  PARTITION syntax is not supported.
-  If an auto-increment table has no ID, you can insert a data record with a specified ID using REPLACE, but no ID is generated.

Use Constraints
---------------

-  If the sharding key value in the REPLACE statement is invalid, data is routed to database shard 0 or table shard 0 by default.
-  Do not use functions VERSION, DATABASE, or USER in the REPLACE statement. When you execute such as functions, you may not obtain the expected results because its results depend on whether it pushed to data nodes for execution.
