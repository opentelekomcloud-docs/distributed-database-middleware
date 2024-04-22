:original_name: ddm_02_0013.html

.. _ddm_02_0013:

Step 2: Create a Schema and Associate It with an RDS for MySQL Instance
=======================================================================

Procedure
---------

#. Log in to the DDM console, and in the navigation pane, choose **Instances**. In the instance list, locate the required DDM instance and click **Create Schema** in the **Operation** column.
#. On the displayed page, specify a sharding mode, enter a schema name, set the number of shards, select the required DDM accounts, and click **Next**.

   .. table:: **Table 1** Parameter description

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                              |
      +===================================+==========================================================================================================================================================================================================================+
      | Sharding                          | -  **Sharded**: indicates that one schema can be associated with multiple data nodes, and all shards will be evenly distributed across the nodes.                                                                        |
      |                                   | -  **Unsharded**: indicates that one schema can be associated with only one data node, and only one shard can be created on the data node.                                                                               |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Schema                            | The name contains 2 to 48 characters and must start with a lowercase letter. Only lowercase letters, digits, and underscores (_) are allowed.                                                                            |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Account                           | The DDM account that needs to be associated with the schema.                                                                                                                                                             |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Data Nodes                        | Select only the data nodes that are in the same VPC as your DDM instance and not in use by other data nodes. DDM will create databases on the selected data nodes without affecting their existing databases and tables. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Shards                            | The total shards are the shards on all data nodes. There cannot be more data nodes than there are shards in the schema. Each data node must have at least one shard assigned. Recommended shards per data node: 8 to 64. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **DB Instance Connection** page, enter a database account with the required permissions and click **Test Connection**.

   .. note::

      Required permissions: SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, PROCESS, REFERENCES, INDEX, ALTER, SHOW DATABASES, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER WITH GRANT OPTION

      You can create a database account for the RDS for MySQL instance and assign it the above permissions in advance.

#. After the test becomes successful, click **Finish**.
