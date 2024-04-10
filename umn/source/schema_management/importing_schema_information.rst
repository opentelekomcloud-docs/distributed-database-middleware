:original_name: ddm_06_0007.html

.. _ddm_06_0007:

Importing Schema Information
============================

Scenarios
---------

When you deploy DR or migrate data across regions, you can import schema information in destination DDM instances. The imported information includes schema information and shard information, excluding service data and index data.

Precautions
-----------

The destination DDM instance has no schemas with the same name.

Procedure
---------

#. Log in to the DDM console, in the instance list, locate the DDM instance that you want to import schema information into and click its name.
#. On the displayed page, in the navigation pane, choose **Schemas**.
#. On the displayed page, click **Import Schema Information**.
#. On the displayed page, click **Select File** to select the required JSON file which has been exported in :ref:`Exporting Schema Information <ddm_06_0015>`.
#. Select the required data nodes, enter a database account with required permissions, and click **Finish**.

   .. note::

      -  The number of selected data nodes is the same as the number of data nodes imported into the DDM instance.

      -  Required permissions: SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, PROCESS, REFERENCES, INDEX, ALTER, SHOW DATABASES, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER WITH GRANT OPTION

         You can create a database account for the RDS for MySQL instance and assign it the above permissions in advance.
