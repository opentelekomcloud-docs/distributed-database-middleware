:original_name: ddm_api_01_0100.html

.. _ddm_api_01_0100:

Querying DB Instances Available for Creating a Schema
=====================================================

Function
--------

This API is used to query DB instances that can be used for creating a schema.

Constraints
-----------

None

URI
---

GET /v1/{project_id}/instances/{instance_id}/rds?offset={offset}&limit={limit}

.. table:: **Table 1** Path parameters

   =========== ========= ====== ==================================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ==================================
   project_id  Yes       String Project ID of a tenant in a region
   instance_id Yes       String DDM instance ID
   =========== ========= ====== ==================================

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
   | limit           | No              | Integer         | Maximum records to be queried.                                                                         |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | Value range: 1 to 128.                                                                                 |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | If the parameter value is not specified, 10 is used by default.                                        |
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

   +-----------+-------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | Parameter | Type                                                                                            | Description                                         |
   +===========+=================================================================================================+=====================================================+
   | instances | Array of :ref:`QueryAvailableRdsList <ddm_api_01_0100__response_queryavailablerdslist>` objects | DB instances that can be used for creating a schema |
   +-----------+-------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | offset    | Integer                                                                                         | Which page the server starts returning items        |
   +-----------+-------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | limit     | Integer                                                                                         | Number of records displayed on each page            |
   +-----------+-------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | total     | Integer                                                                                         | Total collections                                   |
   +-----------+-------------------------------------------------------------------------------------------------+-----------------------------------------------------+

.. _ddm_api_01_0100__response_queryavailablerdslist:

.. table:: **Table 5** QueryAvailableRdsList

   +-----------------------+---------+----------------------------------------------------------+
   | Parameter             | Type    | Description                                              |
   +=======================+=========+==========================================================+
   | id                    | String  | DB instance ID                                           |
   +-----------------------+---------+----------------------------------------------------------+
   | projectId             | String  | Project ID of the tenant that the DB instance belongs to |
   +-----------------------+---------+----------------------------------------------------------+
   | status                | String  | DB instance status                                       |
   +-----------------------+---------+----------------------------------------------------------+
   | name                  | String  | DB instance name                                         |
   +-----------------------+---------+----------------------------------------------------------+
   | engineName            | String  | Engine name of the DB instance                           |
   +-----------------------+---------+----------------------------------------------------------+
   | engineSoftwareVersion | String  | Engine version of the DB instance                        |
   +-----------------------+---------+----------------------------------------------------------+
   | privateIp             | String  | Private IP address for connecting to the DB instance     |
   +-----------------------+---------+----------------------------------------------------------+
   | mode                  | String  | DB instance type (primary/standby or single-node)        |
   +-----------------------+---------+----------------------------------------------------------+
   | port                  | Integer | Port for connecting to the DB instance                   |
   +-----------------------+---------+----------------------------------------------------------+
   | azCode                | String  | AZ                                                       |
   +-----------------------+---------+----------------------------------------------------------+
   | timeZone              | String  | Time zone                                                |
   +-----------------------+---------+----------------------------------------------------------+

**Status code: 400**

.. table:: **Table 6** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

**Status code: 500**

.. table:: **Table 7** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

Example Request
---------------

.. code-block:: text

   GET https://{endpoint}/v1/{project_id}/instances/{instance_id}/rds?offset={offset}&limit={limit}

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "instances" : [ {
       "id" : "c6f68fed9e74478c8679479a07d7d568in01",
       "projectId" : "055d9f4ee780d4d42f96c01c1bc3c50c",
       "status" : "normal",
       "name" : "test-ddm",
       "engineName" : "mysql",
       "engineSoftwareVersion" : "5.7",
       "privateIp" : "192.168.23.97",
       "mode" : "Ha",
       "port" : 3306,
       "azCode" : "az1az1",
       "timeZone" : "UTC+08: 00"
     }, {
       "id" : "337e2598c2a64cb5935079f85996731din01",
       "projectId" : "055d9f4ee780d4d42f96c01c1bc3c50c",
       "status" : "normal",
       "name" : "test-ddm",
       "engineName" : "mysql",
       "engineSoftwareVersion" : "5.7",
       "privateIp" : "192.168.23.221",
       "mode" : "Ha",
       "port" : 3306,
       "azCode" : "az1az1",
       "timeZone" : "UTC+08: 00"
     } ],
     "offset" : 0,
     "limit" : 6,
     "total" : 2
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
