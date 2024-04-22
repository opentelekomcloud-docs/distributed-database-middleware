:original_name: ddm-08-0008.html

.. _ddm-08-0008:

DELETE
======

DELETE is used to delete rows that meet conditions from a table.

Common Syntax
-------------

.. code-block:: text

   DELETE [IGNORE]
   FROM tbl_name [WHERE where_condition]

Syntax Restrictions
-------------------

-  The WHERE clause does not support subqueries, including correlated and non-correlated subqueries.
-  Data in reference tables cannot be deleted when multiple tables are deleted at a time.
-  PARTITION clauses are not supported.
