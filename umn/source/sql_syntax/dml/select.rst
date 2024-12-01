:original_name: ddm_08_0006.html

.. _ddm_08_0006:

SELECT
======

SELECT is generally used to query data in one or more tables.

Common Syntax
-------------

.. code-block::

   SELECT
   [ALL | DISTINCT | DISTINCTROW ]
   select_expr
   [, select_expr ...]
   [FROM table_references [WHERE where_condition]
   [GROUP BY {col_name | expr | position} [ASC | DESC], ...]
   [HAVING where_condition] [ORDER BY {col_name | expr | position} [ASC | DESC], ...]
   [LIMIT {[offset,] row_count | row_count OFFSET offset}]

.. table:: **Table 1** Supported syntax

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Syntax                | Description                                                                                                                                                                                                                 |
   +=======================+=============================================================================================================================================================================================================================+
   | select_expr           | Indicates a column that you want to query.                                                                                                                                                                                  |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | FROM table_references | Indicates the tables that you want to query.                                                                                                                                                                                |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | WHERE                 | Followed by an expression to filter for rows that meet certain criteria.                                                                                                                                                    |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | GROUP BY              | Groups the clauses used in SQL in sequence. GROUP BY indicates relationships between statements and supports column names. For example, the HAVING clause must be after the GROUP BY clause and before the ORDER BY clause. |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ORDER BY              | Indicates relationships between statements. Sorting by column name or by a specified order such as ASC and DESC is supported.                                                                                               |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | LIMIT/OFFSET          | Restrains the offset and size of output result sets, for example, one or two values can be input after LIMIT.                                                                                                               |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Syntax Description
------------------

-  An empty string cannot be used as an alias.

-  The SELECT... GROUP BY... WITH ROLLUP QUERY statement is not supported. (When the queried table is a sharded table, you cannot obtain the expected result)

-  Neither STRAIGHT_JOIN nor NATURAL JOIN is supported.

-  The SELECT FOR UPDATE statement supports only simple queries and does not support JOIN, GROUP BY, ORDER BY, or LIMIT.

-  Each SELECT statement in UNION does not support multiple columns with the same name, for example,

   SELECT id, id, name FROM t1 UNION SELECT pk, pk, name FROM t2 is not supported because this statement has duplicate column names.

-  User-defined sequencing similar to **ORDER BY FIELD(id,1,2,3)** is not supported.
