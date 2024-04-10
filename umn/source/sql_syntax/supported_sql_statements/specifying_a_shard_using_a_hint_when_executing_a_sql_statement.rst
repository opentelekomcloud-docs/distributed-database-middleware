:original_name: ddm_03_0040.html

.. _ddm_03_0040:

Specifying a Shard Using a Hint When Executing a SQL Statement
==============================================================

**Command Format:**

.. code-block:: text

   /*+db=<physical_db_name>*/ <your query>;

**Description:**

Specify a shard by configuring *<physical_db_name>* and execute a SQL statement on the shard.

**Example:**

.. code-block:: text

   /*+db=test_0000*/ select * from t1;

**Restrictions:**

-  The hint is valid only for SELECT, DML, and TRUNCATE statements.
-  The hint works only under the text protocol, rather than the Prepare protocol.
