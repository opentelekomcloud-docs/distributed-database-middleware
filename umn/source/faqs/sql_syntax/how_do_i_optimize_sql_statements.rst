:original_name: ddm_04_0016.html

.. _ddm_04_0016:

How Do I Optimize SQL Statements?
=================================

-  You are advised to use INNER instead of LEFT JOIN or RIGHT JOIN.
-  When LEFT JOIN or RIGHT JOIN is used, ON is preferentially executed, and WHERE is executed at the end. Therefore, when using LEFT JOIN or RIGHT JOIN, ensure that the conditions are judged in the ON statement to reduce the execution of WHERE.
-  When possible, use JOIN instead of subqueries to avoid full scanning of large tables.
