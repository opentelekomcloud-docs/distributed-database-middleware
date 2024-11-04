:original_name: ddm_08_0005.html

.. _ddm_08_0005:

INSERT
======

INSERT is used to insert data into database objects.

Common Syntax
-------------

.. code-block::

   INSERT [INTO] tbl_name
   [(col_name,...)]
   {VALUES | VALUE} ({expr },...),(...),...
   [ ON DUPLICATE KEY UPDATE
   col_name=expr
   [, col_name=expr] ... ]
   OR
   INSERT [INTO] tbl_name
   SET col_name={expr | DEFAULT}, ...
   [ ON DUPLICATE KEY UPDATE
   col_name=expr [, col_name=expr] ... ]

Syntax Restrictions
-------------------

-  INSERT DELAYED is not supported.
-  Only INSERT statements that contain sharding fields are supported.
-  PARTITION syntax is not supported. Partitioned tables are not recommended.
-  Setting **datetime** to **1582** or any value smaller in INSERT statements is not supported.
-  INSERT cannot be used to insert sharding key value **DEFAULT**.
-  If you specify an auto-increment key value in an INSERT statement and execute it on a sharded table, the auto-increment key value of the inserted data entry changes. Auto-increment key values of data entries inserted subsequently will increase based on the first inserted data entry unless you specify a new auto-increment key value.
-  Referencing a table column in function REPEAT of the VALUES statement is not supported, for example, INSERT INTO T(NAME) VALUES(REPEAT(ID,3)).

Use Constraints
---------------

-  If the sharding key value in the INSERT statement is invalid, data is routed to database shard 0 or table shard 0 by default.
-  Do not use functions VERSION, DATABASE, or USER in the INSERT statement. When you execute such as functions, you may not obtain the expected results because its results depend on whether it pushed to data nodes for execution.
