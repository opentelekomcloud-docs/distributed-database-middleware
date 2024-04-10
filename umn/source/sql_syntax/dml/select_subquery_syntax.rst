:original_name: ddm-08-0012.html

.. _ddm-08-0012:

SELECT Subquery Syntax
======================

Subquery as Scalar Operand
--------------------------

Example

.. code-block::

   SELECT (SELECT id FROM test1 where id=1);
   SELECT (SELECT id FROM test2 where id=1)FROM test1;
   SELECT UPPER((SELECT name FROM test1 limit 1)) FROM test2;

Comparisons Using Subqueries
----------------------------

Syntax

.. code-block::

   non_subquery_operand comparison_operator (subquery)
   comparison_operator: = > < >= <= <> != <=> like

Example

.. code-block::

   select name from test1 where id > (select id from test2 where id=1);
   select name from test1 where id = (select id from test2 where id=1);
   select id from test1 where name like (select name from test2 where id=1);

Subqueries with ANY, IN, NOT IN, SOME,ALL,Exists,NOT Exists
-----------------------------------------------------------

Syntax

.. code-block::

   operand comparison_operator SOME (subquery)
   operand comparison_operator ALL (subquery)
   operand comparison_operator ANY (subquery)
   operand IN (subquery)
   operand not IN (subquery)
   operand exists (subquery)
   operand not exists (subquery)

Example

.. code-block::

   select id from test1 where id > any (select id from test2);
   select id from test1 where id > some (select id from test2);
   select id from test1 where id > all (select id from test2);
   select id from test1 where id in (select id from test2);
   select id from test1 where id not in (select id from test2);
   select id from test1 where exists (select id from test2 where id=1);
   select id from test1 where not exists (select id from test2 where id=1);

Derived Tables (Subqueries in the FROM Clause)
----------------------------------------------

Syntax

.. code-block::

   SELECT ... FROM (subquery) [AS] tbl_name ...

Example

.. code-block::

   select id from (select id,name from test2 where id>1) a  order by a.id;

Syntax Restrictions
-------------------

-  Each derived table must have an alias.
-  A derived table cannot be a correlated subquery.
-  In some cases, correct results cannot be obtained using a scalar subquery. Using JOIN instead is recommended to improve query performance.
-  Using subqueries in the HAVING clause and the JOIN ON condition is not supported.

-  Row subqueries are not supported.
