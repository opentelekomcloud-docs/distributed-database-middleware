:original_name: ddm_api_01_0029.html

.. _ddm_api_01_0029:

Querying Schemas
================

Function
--------

This API is used to query schemas of a DDM instance.

Constraints
-----------

None

URI
---

GET /v1/{project_id}/instances/{instance_id}/databases?offset={offset}&limit={limit}

.. table:: **Table 1** Path parameters

   =========== ========= ====== ===============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ===============
   project_id  Yes       String Project ID
   instance_id Yes       String DDM instance ID
   =========== ========= ====== ===============

.. table:: **Table 2** Query parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                            |
   +=================+=================+=================+========================================================================================================+
   | offset          | No              | Integer         | Index offset.                                                                                          |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The query starts from the next piece of data indexed by this parameter. The value is **0** by default. |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The value must be a positive integer.                                                                  |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | limit           | No              | Integer         | Maximum schemas to be queried.                                                                         |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | Value range: 1 to 128.                                                                                 |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | If the parameter value is not specified, 10 schemas are queried by default.                            |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 3** Request header parameters

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

.. table:: **Table 4** Response body parameters

   +-----------+-------------------------------------------------------------------------------------+--------------------+
   | Parameter | Type                                                                                | Description        |
   +===========+=====================================================================================+====================+
   | databases | Array of :ref:`GetDatabaseInfo <ddm_api_01_0029__response_getdatabaseinfo>` objects | Schema information |
   +-----------+-------------------------------------------------------------------------------------+--------------------+
   | total     | Integer                                                                             | Total records      |
   +-----------+-------------------------------------------------------------------------------------+--------------------+

.. _ddm_api_01_0029__response_getdatabaseinfo:

.. table:: **Table 5** GetDatabaseInfo

   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                      | Description                                                                                             |
   +=======================+===========================================================================================+=========================================================================================================+
   | name                  | String                                                                                    | Schema name                                                                                             |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | shard_mode            | String                                                                                    | Sharding mode of the schema                                                                             |
   |                       |                                                                                           |                                                                                                         |
   |                       |                                                                                           | -  **cluster**: indicates that the schema is in sharded mode.                                           |
   |                       |                                                                                           | -  **single**: indicates that the schema is in unsharded mode.                                          |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | shard_number          | Integer                                                                                   | Number of shards in the same working mode                                                               |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | status                | String                                                                                    | Schema status. For details about this parameter value, see :ref:`Status Description <ddm_api_01_0064>`. |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | created               | Integer                                                                                   | Time when the schema is created                                                                         |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | used_rds              | Array of :ref:`GetDatabaseUsedRds <ddm_api_01_0029__response_getdatabaseusedrds>` objects | RDS instances associated with the schema                                                                |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | shard_unit            | Integer                                                                                   | Number of shards per RDS instance                                                                       |
   +-----------------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+

.. _ddm_api_01_0029__response_getdatabaseusedrds:

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

   GET https://{endpoint}/v1/{project_id}/instances/{instance_id}/databases?offset={offset}&limit={limit}

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
       "databases": [{
           "status": "RUNNING",
           "created": 1642063713625,
           "name": "mytestdb170",
           "shard_mode": "cluster",
           "shard_number": 8,
           "shard_unit": 8,
           "used_rds": [{
               "id": "c6f68fed9e74478c8679479a07d7d568in01",
               "status": "normal",
               "name": "rds-test"
           }]
       }],
       "total": 172
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
