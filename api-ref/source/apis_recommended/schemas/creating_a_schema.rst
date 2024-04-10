:original_name: ddm_16_0001.html

.. _ddm_16_0001:

Creating a Schema
=================

Function
--------

This API is used to create a schema.

Constraints
-----------

Before creating a schema, ensure that you have associated RDS instances with your DDM instance and that the RDS instances are not associated with other DDM instances.

URI
---

POST /v1/{project_id}/instances/{instance_id}/databases

.. table:: **Table 1** Path parameters

   =========== ========= ====== ==================================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ==================================
   project_id  Yes       String Project ID of a tenant in a region
   instance_id Yes       String DDM instance ID
   =========== ========= ====== ==================================

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                          |
   +=================+=================+=================+======================================================================================================================+
   | X-Auth-Token    | Yes             | String          | User token                                                                                                           |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | It can be obtained by calling an IAM API. The value of **X-Subject-Token** in the response header is the user token. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-----------+-----------+------------------------------------------------------------------------------------------+--------------------+
   | Parameter | Mandatory | Type                                                                                     | Description        |
   +===========+===========+==========================================================================================+====================+
   | databases | Yes       | Array of :ref:`CreateDatabaseDetail <ddm_16_0001__request_createdatabasedetail>` objects | Schema information |
   +-----------+-----------+------------------------------------------------------------------------------------------+--------------------+

.. _ddm_16_0001__request_createdatabasedetail:

.. table:: **Table 4** CreateDatabaseDetail

   +-----------------+-----------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type                                                                                         | Description                                                                                                                                                                                       |
   +=================+=================+==============================================================================================+===================================================================================================================================================================================================+
   | name            | Yes             | String                                                                                       | Schema name, which:                                                                                                                                                                               |
   |                 |                 |                                                                                              |                                                                                                                                                                                                   |
   |                 |                 |                                                                                              | -  Can include 2 to 48 characters.                                                                                                                                                                |
   |                 |                 |                                                                                              | -  Must start with a letter.                                                                                                                                                                      |
   |                 |                 |                                                                                              | -  Contains only lowercase letters, digits, and underscores (_).                                                                                                                                  |
   |                 |                 |                                                                                              | -  Cannot contain keywords **information_schema**, **mysql, performance_schema**, or **sys**.                                                                                                     |
   |                 |                 |                                                                                              |                                                                                                                                                                                                   |
   |                 |                 |                                                                                              | Minimum length: 2 characters                                                                                                                                                                      |
   |                 |                 |                                                                                              |                                                                                                                                                                                                   |
   |                 |                 |                                                                                              | Maximum length: 48 characters                                                                                                                                                                     |
   +-----------------+-----------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | shard_mode      | Yes             | String                                                                                       | Sharding mode of the schema. The value can be:                                                                                                                                                    |
   |                 |                 |                                                                                              |                                                                                                                                                                                                   |
   |                 |                 |                                                                                              | -  **cluster**: indicates that the schema is in sharded mode.                                                                                                                                     |
   |                 |                 |                                                                                              | -  **single**: indicates that the schema is in unsharded mode.                                                                                                                                    |
   |                 |                 |                                                                                              |                                                                                                                                                                                                   |
   |                 |                 |                                                                                              | Enumerated values:                                                                                                                                                                                |
   |                 |                 |                                                                                              |                                                                                                                                                                                                   |
   |                 |                 |                                                                                              | -  **cluster**                                                                                                                                                                                    |
   |                 |                 |                                                                                              | -  **single**                                                                                                                                                                                     |
   +-----------------+-----------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | shard_number    | Yes             | Integer                                                                                      | Number of shards in the same working mode                                                                                                                                                         |
   |                 |                 |                                                                                              |                                                                                                                                                                                                   |
   |                 |                 |                                                                                              | -  If **shard_unit** is not empty, the value is the product of **shard_unit** multiplied by the associated RDS instances.                                                                         |
   |                 |                 |                                                                                              | -  If **shard_unit** is left blank, the value must be greater than the number of associated RDS instances and less than or equal to the product of the associated RDS instances multiplied by 64. |
   +-----------------+-----------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | shard_unit      | No              | Integer                                                                                      | Number of shards per RDS instance This parameter is optional.                                                                                                                                     |
   |                 |                 |                                                                                              |                                                                                                                                                                                                   |
   |                 |                 |                                                                                              | -  The value is **1** if the schema is unsharded.                                                                                                                                                 |
   |                 |                 |                                                                                              | -  The value ranges from **1** to **64** if the schema is sharded.                                                                                                                                |
   |                 |                 |                                                                                              |                                                                                                                                                                                                   |
   |                 |                 |                                                                                              | Minimum value: **1**                                                                                                                                                                              |
   |                 |                 |                                                                                              |                                                                                                                                                                                                   |
   |                 |                 |                                                                                              | Maximum value: **64**                                                                                                                                                                             |
   +-----------------+-----------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | used_rds        | Yes             | Array of :ref:`DatabaseInstabcesParam <ddm_16_0001__request_databaseinstabcesparam>` objects | RDS instances associated with the schema                                                                                                                                                          |
   +-----------------+-----------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ddm_16_0001__request_databaseinstabcesparam:

.. table:: **Table 5** DatabaseInstabcesParam

   +---------------+-----------+--------+--------------------------------------------------------+
   | Parameter     | Mandatory | Type   | Description                                            |
   +===============+===========+========+========================================================+
   | id            | Yes       | String | ID of the RDS instance associated with the schema      |
   +---------------+-----------+--------+--------------------------------------------------------+
   | adminUser     | Yes       | String | Username for logging in to the associated RDS instance |
   +---------------+-----------+--------+--------------------------------------------------------+
   | adminPassword | Yes       | String | Password for logging in to the associated RDS instance |
   +---------------+-----------+--------+--------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 6** Response body parameters

   +-----------+-------------------------------------------------------------------------------------------------------------+--------------------------------------+
   | Parameter | Type                                                                                                        | Description                          |
   +===========+=============================================================================================================+======================================+
   | databases | Array of :ref:`CreateDatabaseDetailResponses <ddm_16_0001__response_createdatabasedetailresponses>` objects | Schema information                   |
   +-----------+-------------------------------------------------------------------------------------------------------------+--------------------------------------+
   | job_id    | String                                                                                                      | ID of the job for creating a schema. |
   +-----------+-------------------------------------------------------------------------------------------------------------+--------------------------------------+

.. _ddm_16_0001__response_createdatabasedetailresponses:

.. table:: **Table 7** CreateDatabaseDetailResponses

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   name      String Schema name
   ========= ====== ===========

**Status code: 400**

.. table:: **Table 8** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

**Status code: 500**

.. table:: **Table 9** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

Example Request
---------------

The following is an example request of creating a schema and associating it with an existing DDM account.

.. code-block:: text

   POST https://{endpoint}/v1/{project_id}/instances/{instance_id}/databases

   {
     "databases" : [ {
       "name" : "mytestdb",
       "shard_mode" : "cluster",
       "shard_number" : 8,
       "shard_unit" : 8,
       "used_rds" : [ {
         "id" : "f296c394f13f48449d715bf99af07e59in01",
         "adminUser" : "root",
         "adminPassword" : "PassWord_234"
       } ]
     } ]
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "databases" : [ {
       "name" : "mytestdb"
     } ],
     "job_id" : "68a55553-4057-4d05-b074-d6£090e08a50"
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
