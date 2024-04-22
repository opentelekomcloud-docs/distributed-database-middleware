:original_name: ddm_api_01_0015.html

.. _ddm_api_01_0015:

Querying DDM Engine Information
===============================

Function
--------

This API is used to query engines that DDM supports.

Constraints
-----------

None

URI
---

GET /v2/{project_id}/engines?offset={offset}&limit={limit}

.. table:: **Table 1** Path parameters

   ========== ========= ====== ==================================
   Parameter  Mandatory Type   Description
   ========== ========= ====== ==================================
   project_id Yes       String Project ID of a tenant in a region
   ========== ========= ====== ==================================

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
   | limit           | No              | Integer         | A maximum of engines to be queried.                                                                    |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | Value range: 1 to 128.                                                                                 |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | If the parameter value is not specified, 10 engines are queried by default.                            |
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

   +--------------+---------------------------------------------------------------------------------------+----------------------------------------------+
   | Parameter    | Type                                                                                  | Description                                  |
   +==============+=======================================================================================+==============================================+
   | engineGroups | Array of :ref:`EngineGroupsInfo <ddm_api_01_0015__response_enginegroupsinfo>` objects | Information of available engines             |
   +--------------+---------------------------------------------------------------------------------------+----------------------------------------------+
   | offset       | Integer                                                                               | Which page the server starts returning items |
   +--------------+---------------------------------------------------------------------------------------+----------------------------------------------+
   | limit        | Integer                                                                               | Number of records displayed on each page     |
   +--------------+---------------------------------------------------------------------------------------+----------------------------------------------+
   | total        | Integer                                                                               | Number of engine versions                    |
   +--------------+---------------------------------------------------------------------------------------+----------------------------------------------+

.. _ddm_api_01_0015__response_enginegroupsinfo:

.. table:: **Table 5** EngineGroupsInfo

   +------------+-----------------------------------------------------------------------------------+----------------+
   | Parameter  | Type                                                                              | Description    |
   +============+===================================================================================+================+
   | id         | String                                                                            | Engine ID      |
   +------------+-----------------------------------------------------------------------------------+----------------+
   | name       | String                                                                            | Engine name    |
   +------------+-----------------------------------------------------------------------------------+----------------+
   | version    | String                                                                            | Engine version |
   +------------+-----------------------------------------------------------------------------------+----------------+
   | supportAzs | Array of :ref:`SupportAzsInfo <ddm_api_01_0015__response_supportazsinfo>` objects | AZs            |
   +------------+-----------------------------------------------------------------------------------+----------------+

.. _ddm_api_01_0015__response_supportazsinfo:

.. table:: **Table 6** SupportAzsInfo

   ========= ======= ===================================
   Parameter Type    Description
   ========= ======= ===================================
   code      String  AZ code
   name      String  AZ name
   favored   Boolean Whether the current AZ is supported
   ========= ======= ===================================

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

   GET https://{endpoint}/v2/{project_id}/engines?offset={offset}&limit={limit}

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "engineGroups" : [ {
       "id" : "b6907aa2-aacb-3ac9-9782-b90b152d456c",
       "name" : "ddm",
       "version" : "3.0.8",
       "supportAzs" : [ {
         "code" : "az1",
         "name" : "az1",
         "favored" : false
       }, {
         "code" : "az2",
         "name" : "az2",
         "favored" : true
       } ]
     } ],
     "offset" : 0,
     "limit" : 128,
     "total" : 1
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
