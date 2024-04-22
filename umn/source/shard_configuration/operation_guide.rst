:original_name: ddm_03_0071.html

.. _ddm_03_0071:

Operation Guide
===============

This section uses an RDS for MySQL instance as an example to describe how to configure shards for a schema.

Prerequisites
-------------

-  There is a DDM instance with available schemas.
-  There is an RDS for MySQL instance in the same VPC as the DDM instance, and is not associated with any other DDM instances. If adding data nodes is required, ensure that the new data nodes are in the same VPC as the DDM instance.
-  The kernel version of the DDM instance must be 3.0.8.3 or later. The latest kernel version is recommended.
-  Ensure that the instances to be associated with your schema cannot be in read-only states.

Procedure
---------

#. Log in to the DDM console. In the instance list, locate the instance that you want to configure shards for and click its name.

#. On the displayed page, choose **Schemas** to view schemas of the DDM instance.

#. In the schema list, locate the schema that you want to configure shards for and click **Configure Shards** in the **Operation** column.

#. On the **Configure Shards** page, configure the required parameters and click **Test Availability**.

   .. note::

      -  Tables without primary keys do not support shard configuration.
      -  **Total Shards After Configuration** defaults to the total number of existing shards in the schema. If you want to increase shards, change the default value to the new total number of shards, and DDM will distribute all shards evenly to all data nodes.
      -  You can increase data nodes or shards. Data will be redistributed across all shards if one or more shards are added.
      -  Existing instances are selected by default in the data node list, but you still need to input the required password for testing connections.
      -  The number of physical shards per data node in the schema cannot exceed 64. If more than 64 shards are required, contact DDM technical support.
      -  Required permissions: SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, PROCESS, REFERENCES, INDEX, ALTER, SHOW DATABASES, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER WITH GRANT OPTION

#. After the test is successful, click **Next** to go to the **Precheck** page.

   .. note::

      -  Precheck is not the start of shard configuration. The configuration task does not start until you click **OK**.
      -  Handle risks first if any. You can also ignore the risks if you ensure that they do not affect your services.

#. After all check items are complete, click **Configure shards**.

#. View progress at the Task Center or run command **show migrate status** on your SQL client to view progress. A shard configuration task consists of two phases: full migration and incremental migration.


   .. figure:: /_static/images/en-us_image_0000001685307342.png
      :alt: **Figure 1** Run the required command to view task progress

      **Figure 1** Run the required command to view task progress

   .. note::

      The number of returned records corresponds to the number of source RDS instances.

      **SOURCE_RDS**: indicates the source RDS instance.

      **MIGRATE_ID**: indicates the scale-out task ID.

      **SUCCEED_TABLE_STRUCTURE**: indicates the number of physical tables whose structure data has been migrated.

      **TOTAL_TABLE_STRUCTURE**: indicates the total number of physical tables whose structure data is to be migrated.

      **SUCCEED_TABLE_DATA**: indicates the number of physical tables whose data records have been migrated.

      **TOTAL_TABLE_DATA**: indicates the number of physical tables whose data records are to be migrated.

      **SUCCEED_INDEX_DATA**: indicates the number of physical tables whose indexes have been migrated.

      **TOTAL_INDEX_DATA**: indicates the number of physical tables whose data records are to be migrated.

      **FULL_SUCCEED_COUNT**: indicates the objects that have finished a full migration in the current scale-out subtask.

      **FULL_TOTAL_COUNT**: indicates all objects that need to be migrated by a full migration in the current scale-out subtask.

      **FULL_PERCENTAGE**: indicates the percentage of migrated objects in the full migration in the current scale-out subtask.

      Aggregate total objects to be migrated in a full migration and migrated objects in each scale-out subtask. The total objects to be migrated and migrated in all subtasks are displayed in the progress bar at Task Center.

#. At the Task Center, click **View Log** to view task logs.

#. If you select **Manual** for route switchover, click **Switch Route** at Task Center after data is completely migrated. If you select **Automatic**, the route is automatically switched over within the specified time.

   .. note::

      -  Switching route is critical for a shard configuration task. Before the route is switched, you can cancel a shard configuration task, and data in original databases is not affected.
      -  If new RDS for MySQL instances are added, write operations will be disabled during route switchover. If the number of shards is increased, read and write operations are both disabled during route switchover.
      -  Switching route during off-peak hours is recommended. This is because data validation is required during this process, increasing the switchover time. How long route switchover requires depends on the volume of the data involved.

#. Click **Clear** in the **Operation** column to delete the data migrated from original RDS for MySQL instances.

#. Carefully read information in the dialog box, confirm that the task is correct, and click **Yes**.

#. Wait till the source data is cleared.

#. Run the following commands after the shard configuration is complete:

   **show data node**: used to view the relationship between new data nodes and shards

   **show db status**: used to view the estimated usage of schema disks.
