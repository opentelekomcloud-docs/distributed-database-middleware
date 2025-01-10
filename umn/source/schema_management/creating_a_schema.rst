:original_name: ddm_06_0006.html

.. _ddm_06_0006:

Creating a Schema
=================

Prerequisites
-------------

-  You have logged in to the DDM console.
-  The DDM instance is in the **Running** state.
-  Do not modify or delete the internal accounts (DDMRW*, DDMR*, and DDMREP*) created on data nodes. Otherwise, services will be affected.

   .. note::

      -  The internal account name is in the format: Fixed prefix (such as DDMRW, DDMR, or DDMREP) + Hash value of the data node ID.
      -  A random password is generated, which contains 16 to 32 characters.
      -  All instances associated with one schema must have the same major MySQL version.
      -  Multiple schemas can be created in a DDM instance and associated with the same data node. One DDM instance can be associated with either RDS for MySQL or GaussDB(for MySQL) instances, but not both, and it cannot be associated with multiple RDS for MySQL instances with different versions. Otherwise, metadata restoration will fail.
      -  One data node cannot be associated with schemas in different DDM instances.
      -  If you create a sharded schema, more than one shard will be generated in the schema. Shard names follow the rule: *<schemaname>*\ \_\ *<number>*. *<number>* here indicates a four-digit number starting from 0000. This number will be incremented by one. For example, if a schema name is **db_cbb5** and there are 2 shards, the shard names are **db_cbb5_0000** and **db_cbb5_0001**.
      -  Read-only instances cannot be associated with the schema as data nodes.

Procedure
---------

#. In the navigation pane, choose **Instances**. In the instance list, locate the DDM instance that you want to create a schema for and click **Create Schema** in the **Operation** column.

#. On the **Create Schema** page, set required parameters by referring to :ref:`Table 1 <ddm_06_0006__table5532135017574>`, and click **Next**.

   .. _ddm_06_0006__table5532135017574:

   .. table:: **Table 1** Parameter description

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                 |
      +===================================+=============================================================================================================================================================================================================================+
      | Sharding                          | -  **Sharded**: indicates that one schema can be associated with multiple data nodes, and all shards will be evenly distributed across the nodes.                                                                           |
      |                                   | -  **Unsharded**: indicates that one schema can be associated with only one data node, and only one shard can be created on the RDS instance.                                                                               |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Schema                            | The name contains 2 to 48 characters and must start with a lowercase letter. Only lowercase letters, digits, and underscores (_) are allowed.                                                                               |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Account                           | The DDM account that needs to be associated with the schema.                                                                                                                                                                |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Data Nodes                        | Select only the data nodes that are in the same VPC as your DDM instance and not in use by other DDM instances. DDM will create databases on the selected data nodes without affecting their existing databases and tables. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Shards                            | The total shards are the shards on all data nodes. There cannot be more data nodes than there are shards in the schema. Each data node has to have at least one shard assigned. Recommended shards per data node: 8 to 64.  |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Enter a database account with the required permissions and click **Test Connection**.

   .. note::

      Required permissions: SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, PROCESS, REFERENCES, INDEX, ALTER, SHOW DATABASES, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER WITH GRANT OPTION

      You can create a database account for the RDS for MySQL instance and assign it the above permissions in advance.

#. After the test becomes successful, click **Finish**.
