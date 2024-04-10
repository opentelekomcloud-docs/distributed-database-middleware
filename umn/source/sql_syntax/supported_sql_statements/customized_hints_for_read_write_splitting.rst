:original_name: ddm_03_0034.html

.. _ddm_03_0034:

Customized Hints for Read/Write Splitting
=========================================

DDM allows you to customize a hint to specify whether SQL statements are executed on the primary instance or its read replicas.

The following hint formats are supported:

Format 1

.. code-block:: text

   /*!mycat:db_type=host*/

Format 2

.. code-block:: text

   /*+ db_type=host */

**host** can be **master** or **slave**. **master** indicates a primary instance, and **slave** indicates a read replica.

Currently, this function only applies to SELECT statements.

.. note::

   After read/write splitting is enabled, write operations are performed only on the primary instance, and read operations are performed only on its read replicas. To read from the primary instance, you can customize a hint to forcibly perform read operations on the primary instance. This method is only suitable for queries.
