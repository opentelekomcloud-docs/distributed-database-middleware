:original_name: ddm_api_01_0030.html

.. _ddm_api_01_0030:

Querying Details of a Schema
============================

Function
--------

This API is used to query details about a schema.

Constraints
-----------

None

URI
---

GET /v1/{project_id}/instances/{instance_id}/databases/{ddm_dbname}

.. table:: **Table 1** Path parameters

   +-------------+-----------+--------+-------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                 |
   +=============+===========+========+=============================================================+
   | project_id  | Yes       | String | Project ID                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------+
   | instance_id | Yes       | String | DDM instance ID                                             |
   +-------------+-----------+--------+-------------------------------------------------------------+
   | ddm_dbname  | Yes       | String | Name of the schema to be queried, which is case-insensitive |
   +-------------+-----------+--------+-------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                          |
   +=================+=================+=================+======================================================================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | It can be obtained by calling an IAM API. The value of **X-Subject-Token** in the response header is the user token. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+-------------------------------------------------------------------------------------------+--------------------+
   | Parameter | Type                                                                                      | Description        |
   +===========+===========================================================================================+====================+
   | database  | :ref:`GetDatabaseResponseBean <ddm_api_01_0030__response_getdatabaseresponsebean>` object | Schema information |
   +-----------+-------------------------------------------------------------------------------------------+--------------------+

.. _ddm_api_01_0030__response_getdatabaseresponsebean:

.. table:: **Table 4** GetDatabaseResponseBean

   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                      | Description                                                                                             |
   +=======================+===========================================================================================+=========================================================================================================+
   | name                  | String                                                                                    | Schema name                                                                                             |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | created               | String                                                                                    | Time when the schema is created                                                                         |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | status                | String                                                                                    | Schema status. For details about this parameter value, see :ref:`Status Description <ddm_api_01_0064>`. |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | updated               | String                                                                                    | Time when the DDM instance is last updated                                                              |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | databases             | Array of :ref:`GetDatabases <ddm_api_01_0030__response_getdatabases>` objects             | Sharding information of the schema                                                                      |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | shard_mode            | String                                                                                    | Sharding mode of the schema                                                                             |
   |                       |                                                                                           |                                                                                                         |
   |                       |                                                                                           | -  **cluster**: indicates that the schema is in sharded mode.                                           |
   |                       |                                                                                           | -  **single**: indicates that the schema is in unsharded mode.                                          |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | shard_number          | Integer                                                                                   | Number of shards in the same working mode                                                               |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | shard_unit            | Integer                                                                                   | Number of shards per RDS instance                                                                       |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | dataVips              | Array of strings                                                                          | IP address and port number for connecting to the schema                                                 |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | used_rds              | Array of :ref:`GetDatabaseUsedRds <ddm_api_01_0030__response_getdatabaseusedrds>` objects | Associated RDS instances                                                                                |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+

.. _ddm_api_01_0030__response_getdatabases:

.. table:: **Table 5** GetDatabases

   ========= ======= ===================================================
   Parameter Type    Description
   ========= ======= ===================================================
   dbslot    Integer Number of shards
   name      String  Shard name
   status    String  Shard status
   created   String  Time when the shard is created
   updated   String  Time when the shard is last updated
   id        String  ID of the RDS instance where the shard is located
   idName    String  Name of the RDS instance where the shard is located
   ========= ======= ===================================================

.. _ddm_api_01_0030__response_getdatabaseusedrds:

.. table:: **Table 6** GetDatabaseUsedRds

   +-----------+--------+----------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                |
   +===========+========+============================================================================+
   | id        | String | Node ID of the associated RDS instance                                     |
   +-----------+--------+----------------------------------------------------------------------------+
   | name      | String | Name of the associated RDS instance                                        |
   +-----------+--------+----------------------------------------------------------------------------+
   | status    | String | Status of the associated RDS instance                                      |
   +-----------+--------+----------------------------------------------------------------------------+
   | error_msg | String | Response message. This parameter is not returned if no abnormality occurs. |
   +-----------+--------+----------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 7** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

**Status code: 500**

.. table:: **Table 8** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

Example Request
---------------

.. code-block:: text

   GET https://{endpoint} /v1/{project_id}/instances/{instance_id}/databases/{ddm_dbname}

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "database" : {
       "name" : "db_7567",
       "created" : 1604631243234,
       "status" : "RUNNING",
       "updated" : 1604631243234,
       "databases" : [ {
         "id" : "e70a82534a364492b795c5080e3a1591in01",
         "name" : "db_7567_0000",
         "idName" : "db_7567_0000",
         "dbslot" : 0,
         "status" : "RUNNING",
         "created" : 1604631243234,
         "updated" : 1604631243234
       }, {
         "id" : "e70a82534a364492b795c5080e3a1591in01",
         "name" : "db_7567_0001",
         "idName" : "db_7567_0001",
         "dbslot" : 1,
         "status" : "RUNNING",
         "created" : 1604631243234,
         "updated" : 1604631243234
       }, {
         "id" : "e70a82534a364492b795c5080e3a1591in01",
         "name" : "db_7567_0002",
         "idName" : "db_7567_0002",
         "dbslot" : 2,
         "status" : "RUNNING",
         "created" : 1604631243234,
         "updated" : 1604631243234
       }, {
         "id" : "e70a82534a364492b795c5080e3a1591in01",
         "name" : "db_7567_0003",
         "idName" : "db_7567_0003",
         "dbslot" : 3,
         "status" : "RUNNING",
         "created" : 1604631243234,
         "updated" : 1604631243234
       }, {
         "id" : "e70a82534a364492b795c5080e3a1591in01",
         "name" : "db_7567_0004",
         "idName" : "db_7567_0004",
         "dbslot" : 4,
         "status" : "RUNNING",
         "created" : 1604631243234,
         "updated" : 1604631243234
       }, {
         "id" : "e70a82534a364492b795c5080e3a1591in01",
         "name" : "db_7567_0005",
         "idName" : "db_7567_0005",
         "dbslot" : 5,
         "status" : "RUNNING",
         "created" : 1604631243234,
         "updated" : 1604631243234
       }, {
         "id" : "e70a82534a364492b795c5080e3a1591in01",
         "name" : "db_7567_0006",
         "idName" : "db_7567_0006",
         "dbslot" : 6,
         "status" : "RUNNING",
         "created" : 1604631243234,
         "updated" : 1604631243234
       }, {
         "id" : "e70a82534a364492b795c5080e3a1591in01",
         "name" : "db_7567_0007",
         "idName" : "db_7567_0007",
         "dbslot" : 7,
         "status" : "RUNNING",
         "created" : 1604631243234,
         "updated" : 1604631243234
       } ],
       "shard_mode" : "cluster",
       "shard_number" : 8,
       "shard_unit" : 8,
       "dataVips" : [ {
         "192.168.185.97:5066"
       } ],
       "used_rds" : [ {
         "id" : "e70a82534a364492b795c5080e3a1591in01",
         "name" : "rds-5338",
         "status" : "normal"
       } ]
     }
   }

**Status code: 400**

bad request

.. code-block::

   {
     "externalMessage" : "Parameter error.",
     "errCode" : "DBS.280001"
   }

**Status code: 500**

server error

.. code-block::

   {
     "externalMessage" : "Server failure.",
     "errCode" : "DBS.200412"
   }

Status Codes
------------

=========== ============
Status Code Description
=========== ============
200         OK
400         bad request
500         server error
=========== ============

Error Codes
-----------

For details, see :ref:`Error Codes <ddm_api_01_0061>`.
