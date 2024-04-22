:original_name: ddm_11_0002.html

.. _ddm_11_0002:

Key Operations Recorded by CTS
==============================

Cloud Trace Service (CTS) records operations related to DDM for further query, audit, and backtrack.

.. table:: **Table 1** DDM operations that can be recorded by CTS

   +----------------------------------------------------+----------------+-------------------------+
   | Operation                                          | Resource Type  | Trace Name              |
   +====================================================+================+=========================+
   | Applying a parameter template                      | parameterGroup | applyParameterGroup     |
   +----------------------------------------------------+----------------+-------------------------+
   | Clearing metadata after a schema is scaled out     | logicDB        | cleanMigrateLogicDB     |
   +----------------------------------------------------+----------------+-------------------------+
   | Clearing user resources                            | all            | cleanupUserAllResources |
   +----------------------------------------------------+----------------+-------------------------+
   | Replicating a parameter template                   | parameterGroup | copyParameterGroup      |
   +----------------------------------------------------+----------------+-------------------------+
   | Creating a DDM instance                            | instance       | createInstance          |
   +----------------------------------------------------+----------------+-------------------------+
   | Creating a schema                                  | logicDB        | createLogicDB           |
   +----------------------------------------------------+----------------+-------------------------+
   | Creating a parameter template                      | parameterGroup | createParameterGroup    |
   +----------------------------------------------------+----------------+-------------------------+
   | Creating an account                                | user           | createUser              |
   +----------------------------------------------------+----------------+-------------------------+
   | Deleting a DDM instance                            | instance       | deleteInstance          |
   +----------------------------------------------------+----------------+-------------------------+
   | Deleting a schema                                  | logicDB        | deleteLogicDB           |
   +----------------------------------------------------+----------------+-------------------------+
   | Deleting a parameter template                      | parameterGroup | deleteParameterGroup    |
   +----------------------------------------------------+----------------+-------------------------+
   | Deleting an account                                | user           | deleteUser              |
   +----------------------------------------------------+----------------+-------------------------+
   | Scaling out a DDM instance                         | instance       | enlargeNode             |
   +----------------------------------------------------+----------------+-------------------------+
   | Restarting a DDM instance                          | instance       | instanceRestart         |
   +----------------------------------------------------+----------------+-------------------------+
   | Importing schema information                       | instance       | loadMetadata            |
   +----------------------------------------------------+----------------+-------------------------+
   | Switching the route during scaling                 | logicDB        | manualSwitchRoute       |
   +----------------------------------------------------+----------------+-------------------------+
   | Scaling out a schema                               | logicDB        | migrateLogicDB          |
   +----------------------------------------------------+----------------+-------------------------+
   | Modifying a parameter template                     | parameterGroup | modifyParameterGroup    |
   +----------------------------------------------------+----------------+-------------------------+
   | Changing the route switching time                  | logicDB        | modifyRouteSwitchTime   |
   +----------------------------------------------------+----------------+-------------------------+
   | Modifying an account                               | user           | modifyUser              |
   +----------------------------------------------------+----------------+-------------------------+
   | Scaling in a DDM instance                          | instance       | reduceNode              |
   +----------------------------------------------------+----------------+-------------------------+
   | Resetting a parameter template                     | parameterGroup | resetParameterGroup     |
   +----------------------------------------------------+----------------+-------------------------+
   | Resetting the password of an account               | user           | resetUserPassword       |
   +----------------------------------------------------+----------------+-------------------------+
   | Changing node class                                | instance       | resizeFlavor            |
   +----------------------------------------------------+----------------+-------------------------+
   | Restoring DB instance data                         | instance       | restoreInstance         |
   +----------------------------------------------------+----------------+-------------------------+
   | Retrying to scale out a schema                     | logicDB        | retryMigrateLogicDB     |
   +----------------------------------------------------+----------------+-------------------------+
   | Rolling back the version upgrade of a DDM instance | instance       | rollback                |
   +----------------------------------------------------+----------------+-------------------------+
   | Rolling back a schema scaling task                 | logicDB        | rollbackMigrateLogicDB  |
   +----------------------------------------------------+----------------+-------------------------+
   | Configuring access control                         | instance       | switchIpGroup           |
   +----------------------------------------------------+----------------+-------------------------+
   | Synchronizing data node information                | instance       | synRdsinfo              |
   +----------------------------------------------------+----------------+-------------------------+
   | Upgrading the version of a DDM Instance            | instance       | upgrade                 |
   +----------------------------------------------------+----------------+-------------------------+
   | Creating a node group                              | group          | createGroup             |
   +----------------------------------------------------+----------------+-------------------------+
   | Modifying the floating IP address                  | instance       | modifyIp                |
   +----------------------------------------------------+----------------+-------------------------+
   | Modifying the name of an instance                  | instance       | modifyName              |
   +----------------------------------------------------+----------------+-------------------------+
