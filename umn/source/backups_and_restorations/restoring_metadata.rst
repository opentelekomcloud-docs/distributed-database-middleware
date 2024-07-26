:original_name: ddm_06_0017.html

.. _ddm_06_0017:

Restoring Metadata
==================

DDM automatically backs up DDM instance metadata at 02:00 UTC+00:00 every day and retains the backup data for 30 days. Metadata backup is also triggered by key operations, such as deleting a schema, deleting data after shard configuration, and deleting instances.

When you delete a schema by mistake or your RDS for MySQL instances become abnormal, metadata restoration allows you to restore your DDM instance metadata and match the metadata with the RDS instance that has completed PITR to re-establish the relationship between your DDM instance and RDS instance. Metadata restoration supports only RDS for MySQL.

To restore metadata of a DDM instance, you can specify a point in time by referring to :ref:`Restoring Metadata to a Point in Time <ddm_06_0017__section128315484524>`, or using an available backup by referring to :ref:`Restoring Metadata Using Backups <ddm_06_0017__section132806221525>`.

Metadata restoration mainly restores the metadata of your DDM instance to a new DDM instance. It starts after a point-in-time recovery (PITR) for the associated data nodes is complete.

Prerequisites
-------------

-  There is a source DDM instance available and associated with an RDS for MySQL instance. This DB instance is the source data node.
-  The source data node has been restored to a specified time point.

Constraints
-----------

-  The destination DDM instance is not associated with any RDS for MySQL instance and has no schemas or accounts.
-  Restoration is not supported if the destination DDM instance is in the primary network and its associated RDS for MySQL instance is in the extended network.
-  The source DDM instance must be of the version 2.3.2.11 or later, and the destination DDM instance must be of the version 3.0.8 or later.
-  Time points that data can be restored to depend on the backup policy set on original data nodes.

.. _ddm_06_0017__section128315484524:

Restoring Metadata to a Point in Time
-------------------------------------

#. Log in to the DDM console.

#. .. _ddm_06_0017__li4793191882712:

   :ref:`Create a new DDM instance <ddm_06_0132>` and use it as the destination DDM instance. For details, see\ :ref:`Creating a DDM Instance <ddm_06_0132>`.

#. In the DDM instance list, locate the source instance and click its name.

#. In the navigation pane on the left, choose **Backups & Restorations**.

#. Click **Restore Metadata**.

#. On the displayed page, specify a time point. The source DDM instance will select an appropriate DDM metadata backup closest to the time point.

   .. table:: **Table 1** Parameter description

      +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                | Description                                                                                                                                                 |
      +==========================+=============================================================================================================================================================+
      | Restore To               | Specify a point in time. DDM will restore metadata to this point in time using the most recent backup.                                                      |
      +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Destination DDM Instance | Select the DDM instance created in :ref:`2 <ddm_06_0017__li4793191882712>`.                                                                                 |
      +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Destination Data Nodes   | Select the RDS for MySQL instances that have completed PITR. DDM will match the selected data nodes with shard information in the selected metadata backup. |
      +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**. If a message is displayed indicating that the metadata is restored successfully, the restoration is complete.

.. _ddm_06_0017__section132806221525:

Restoring Metadata Using Backups
--------------------------------

#. Log in to the DDM console.

#. .. _ddm_06_0017__li881143742017:

   :ref:`Create a new DDM instance <ddm_06_0132>` and use it as the destination DDM instance. For details, see\ :ref:`Creating a DDM Instance <ddm_06_0132>`.

#. In the DDM instance list, locate the source instance and click its name.

#. In the navigation pane on the left, choose **Backups**.

#. Locate the required backup based on the instance name and backup time and click **Restore** in the **Operation** column.

#. On the displayed page, configure required parameters.

   .. table:: **Table 2** Parameter description

      +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                | Description                                                                                                                                                 |
      +==========================+=============================================================================================================================================================+
      | Backup Name              | Name of the backup to be restored.                                                                                                                          |
      +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Destination DDM Instance | Select the DDM instance created in :ref:`2 <ddm_06_0017__li881143742017>`.                                                                                  |
      +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Destination Data Nodes   | Select the RDS for MySQL instances that have completed PITR. DDM will match the selected data nodes with shard information in the selected metadata backup. |
      +--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**. If a message is displayed indicating that the metadata is restored successfully, the restoration is complete.
