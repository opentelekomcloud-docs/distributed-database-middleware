:original_name: ddm_08_0024.html

.. _ddm_08_0024:

HINT-DB
=======

**Command Format:**

**/*+db=**\ *<physical_db_name>*\ **\*/ TRUNCATE TABLE** *<table_name>*

**Description:**

Deleting data in physical tables corresponding to *<table_name>* in *<physical_db_name>* does not affect physical tables in other database shards.

.. note::

   HINTs are instructions within a SQL statement that tell the optimizer to execute the statement in a flexible way.
