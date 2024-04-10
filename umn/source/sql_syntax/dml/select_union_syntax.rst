:original_name: ddm-08-0011.html

.. _ddm-08-0011:

SELECT UNION Syntax
===================

Common Syntax
-------------

.. code-block::

   SELECT ...UNION [ALL | DISTINCT]
   SELECT ...[UNION [ALL | DISTINCT] SELECT ...]

Example
-------

.. code-block::

   select userid from user union select orderid from ordertbl order by userid;
   select userid from user union (select orderid from ordertbl group by orderid) order by userid;

Syntax Restrictions
-------------------

SELECT statements in UNION do not support duplicate column names.
