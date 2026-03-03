:original_name: ddm_api_01_0064.html

.. _ddm_api_01_0064:

Status Description
==================

.. _ddm_api_01_0064__section5119135310445:

DDM Instance Statuses
---------------------

.. table:: **Table 1** DDM instance statuses

   ================= =============================================
   Status            Description
   ================= =============================================
   CREATING          The DDM instance is being created.
   CREATEFAILED      The DDM instance fails to be created.
   RUNNING           The DDM instance is running and available.
   ERROR             The DDM instance is faulty.
   RESTARTING        The DDM instance is being restarted.
   RESIZING          Class of the DDM instance fail to be changed.
   GROWING           A DDM instance is being scaled out.
   REDUCING          A DDM instance is being scaled in.
   RESTORE           A DDM instance is being restored.
   BACKUP            A DDM instance is being backed up.
   MODIFY_NAME       A DDM instance name is being changed.
   RESET_PASSWORD    A password is being reset.
   MIGRATE_DATABASE  Shards of a schema are being configured.
   SET_CONFIGURATION The instance parameters are being updated.
   CREATE_GROUP      Creating a group
   DELETE_GROUP      Deleting a group
   SWITCH_SSL        Configuring SSL
   ================= =============================================

.. _ddm_api_01_0064__section1650415194513:

DDM Schema Statuses
-------------------

.. table:: **Table 2** DDM schema statuses

   ================ ====================================
   Status           Description
   ================ ====================================
   CREATING         The schema is being created.
   RUNNING          The schema is running and available.
   CREATE_FAILED    The schema fails to be created.
   DELETING         The schema is being deleted.
   EXPANDING        The schema is being scaled out.
   EXPANDING FAILED The schema fails to be scaled out.
   ROLLING BACK     The schema is being rolled back.
   ================ ====================================

.. _ddm_api_01_0064__section13481912102019:

DDM Node Statuses
-----------------

.. table:: **Table 3** Node statuses

   =========== ========================================
   Status      Description
   =========== ========================================
   normal      The node is running normally.
   abnormal    The node is abnormal.
   creating    The DDM instance is being created.
   createfail  The DDM instance fails to be created.
   enlargefail The DDM instance fails to be scaled out.
   resizing    The node class is being changed.
   =========== ========================================

.. _ddm_api_01_0064__section1820916618277:

Task Statuses
-------------

.. table:: **Table 4** Task status description

   ====================== ============================
   Status                 Description
   ====================== ============================
   CreateInstance         Creating a DB Instance
   DeleteInstance         Deleting a DB instance
   EnlargeNode            Changing a node class
   EnlargeNode            Adding nodes
   ReduceNode             Deleting nodes
   RestartInstance        Rebooting a DB instance
   BindEIP                Binding an EIP
   UnbindEIP              Unbinding an EIP
   RestoreInstance        Restoring DB instance data
   loadMetadata           Importing schema information
   migrateLogicDb         Configuring shards
   retryMigrateLogicDb    Retrying shard configuration
   deleteConsistentBackup Deleting a consistent backup
   CreateGroup            Creating a group
   DeleteGroup            Deleting a group
   RestartNode            Restarting a node
   ====================== ============================

.. _ddm_api_01_0064__section9317162963412:

Data Node Statuses
------------------

.. table:: **Table 5** Data node statuses

   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status                           | Description                                                                                                                                         |
   +==================================+=====================================================================================================================================================+
   | Normal                           | A DB instance is available.                                                                                                                         |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Abnormal                         | A DB instance is abnormal.                                                                                                                          |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Creating                         | A DB instance is being created.                                                                                                                     |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Creation failed                  | A DB instance fails to be created.                                                                                                                  |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Switchover in progress           | A standby DB instance is being switched over to the primary DB instance.                                                                            |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Changing type to primary/standby | A single DB instance is being changed to primary/standby DB instances.                                                                              |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Rebooting                        | A DB instance is being rebooted.                                                                                                                    |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Changing port                    | The DB instance port is being changed.                                                                                                              |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Changing instance class          | The CPU or memory of a DB instance is being modified.                                                                                               |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Scaling up                       | Storage space of a DB instance is being scaled up.                                                                                                  |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Backing up                       | A DB instance is being backed up.                                                                                                                   |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Restoring                        | A DB instance is in the process of being restored from a backup.                                                                                    |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Restore failed                   | A DB instance fails to be restored.                                                                                                                 |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Storage full                     | Storage space of a DB instance is full. Data cannot be written to databases. You need to scale up the storage space to make the instance available. |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleted                          | A DB instance has been deleted and will not be displayed in the instance list.                                                                      |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter change. Pending reboot | A modification to a database parameter is waiting for an instance reboot before it can take effect.                                                 |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ddm_api_01_0064__section15461171610716:

Backup Statuses
---------------

.. table:: **Table 6** Backup statuses

   +------------+-------------------------------------------------------------------------+
   | Status     | Description                                                             |
   +============+=========================================================================+
   | creating   | A backup is being created.                                              |
   +------------+-------------------------------------------------------------------------+
   | normal     | A backup is normal and available.                                       |
   +------------+-------------------------------------------------------------------------+
   | deleted    | A backup has been deleted and will not be displayed in the backup list. |
   +------------+-------------------------------------------------------------------------+
   | createfail | A backup fails to be created.                                           |
   +------------+-------------------------------------------------------------------------+

.. _ddm_api_01_0064__section7167152035513:

AZ Statuses
-----------

.. table:: **Table 7** AZ statuses

   =========== =============================================
   Status      Description
   =========== =============================================
   normal      The node classes in the AZ are available.
   unsupported The node classes are not supported by the AZ.
   sellout     The node classes in the AZ are sold out.
   =========== =============================================
