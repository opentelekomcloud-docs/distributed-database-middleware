:original_name: ddm-08-0010.html

.. _ddm-08-0010:

SELECT JOIN Syntax
==================

Common Syntax
-------------

table_references:

.. code-block::

   table_reference [, table_reference] ...

table_reference:

.. code-block::

   table_factor | join_table

table_factor:

.. code-block::

   tbl_name [[AS] alias]
   | table_subquery [AS] alias
   | ( table_references )

join_table:

.. code-block::

   table_reference [INNER | CROSS] JOIN table_factor [join_condition]
   | table_reference {LEFT|RIGHT} [OUTER] JOIN table_reference join_condition
   | table_reference [{LEFT|RIGHT} [OUTER]] JOIN table_factor

join_condition:

.. code-block::

   ON conditional_expr
   | USING (column_list)

Syntax Restrictions
-------------------

SELECT STRAIGHT_JOIN and NATURAL JOIN are not supported.

Example
-------

.. code-block::

   select id,name from test1 where id=1;
   select distinct id,name from test1 where id>=1;
   select id,name from test1 order by id limit 2 offset 2;
   select id,name from test1 order by id limit 2,2;
   select  1+1,'test',id,id*1.1,now() from test1 limit 3;
   select  current_date,current_timestamp;
   select abs(sum(id)) from test1;
