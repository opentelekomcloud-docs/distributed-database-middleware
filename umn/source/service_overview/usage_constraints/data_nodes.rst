:original_name: ddm_01_0005.html

.. _ddm_01_0005:

Data Nodes
==========

Constraints on data nodes are as follows:

-  Data nodes can be only RDS for MySQL and GaussDB(for MySQL) instances of versions 5.7 and 8.0.
-  DDM cannot connect to MySQL instances using SSL connections.
-  Case sensitivity support cannot be enabled for MySQL instances.

   .. note::

      -  If you are using MySQL 5.7, select **Case insensitive** for **Table Name** when you create a MySQL instance, or set **lower_case_table_names** to **1** on the **Parameters** page after you complete the creation.
      -  If you are using MySQL 8.0, select **Case insensitive** for **Table Name** when you create a MySQL instance.

-  Modifying configurations of a data node may result in an exception in using your DDM instance. After the modification, click **Synchronize Data Node Information** on the **Data Nodes** page to synchronize changes from the data node to DDM.
-  DDM data nodes do not support GBK character sets.
