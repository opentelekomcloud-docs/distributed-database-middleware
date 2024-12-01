:original_name: ddm_08_0009.html

.. _ddm_08_0009:

UPDATE
======

Common Syntax
-------------

.. code-block::

   UPDATE table_reference
   SET col_name1={expr1} [, col_name2={expr2}] ...
   [WHERE where_condition]

Syntax Restrictions
-------------------

-  Subqueries are not supported, including correlated and non-correlated subqueries.

-  Cross-shard subquery is not supported.

-  The WHERE condition in the UPDATE statement does not support arithmetic expressions and their subqueries.

-  Modifying broadcast tables is not supported during an update of multiple tables. (Data in columns of a broadcast table cannot be on the left of SET assignment statements).

-  Updating the sharding key field of a logical table is not supported because this operation may cause data redistribution.

-  Setting **datetime** to **1582** or any value smaller in UPDATE statements is not supported.

-  UPDATE cannot be used to update sharding key value **DEFAULT**.

-  Repeatedly updating the same field in an UPDATE statement is not supported.

-  Updating a sharding key using UPDATE JOIN syntax is not supported.

-  UPDATE cannot be used to update self-joins.

-  Referencing other object columns in assignment statements or expressions may cause unexpected update results. Example:

   update tbl_1 a,tbl_2 b set a.name=concat(b.name,'aaaa'),b.name=concat(a.name,'bbbb') on a.id=b.id

-  UPDATE JOIN supports only joins with WHERE conditions.
