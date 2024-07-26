:original_name: ddm_08_0025.html

.. _ddm_08_0025:

HINT-TABLE
==========

HINTs are instructions within a SQL statement that tell the optimizer to execute the statement in a flexible way. This section describes how to use HINT syntax to delete data from a table.

**Command Format:**

**/*+table=**\ *<physical_table_name>*\ **\*/ TRUNCATE TABLE** *<table_name>*

**Description:**

Deleting data in physical table *<physical_table_name>* in the current database shard does not affect other physical tables.

**Example output before the table is deleted:**

|image1|

**Example output after the table is deleted:**

|image2|

.. note::

   Hints are valid only for sharded tables.

.. |image1| image:: /_static/images/en-us_image_0000001685307430.png
.. |image2| image:: /_static/images/en-us_image_0000001733266617.png
