:original_name: ddm_08_0026.html

.. _ddm_08_0026:

HINT-DB/TABLE
=============

**Command Format:**

**/*+db=**\ *<physical_db_name>*\ **,table=**\ *<physical_table_name>*\ **\*/ TRUNCATE TABLE** *<table_name>*

**Description:**

Deleting data in physical table *<physical_table_name>* in database shard *<physical_db_name>* does not affect other physical tables.

.. note::

   Hints are valid only for sharded tables.
