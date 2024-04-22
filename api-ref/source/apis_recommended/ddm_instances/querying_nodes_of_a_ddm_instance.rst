:original_name: ddm_api_01_0082.html

.. _ddm_api_01_0082:

Querying Nodes of a DDM Instance
================================

Function
--------

This API is used to query nodes of a DDM instance.

Constraints
-----------

None

URI
---

GET /v1/{project_id}/instances/{instance_id}/nodes?offset={offset}&limit={limit}

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
   | limit           | No              | Integer         | A maximum of nodes to be queried.                                                                      |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | Value range: 1 to 128.                                                                                 |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | If the parameter value is not specified, 10 nodes are queried by default.                              |
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

   +-----------+-----------------------------------------------------------------------+-----------------------------------------------+
   | Parameter | Type                                                                  | Description                                   |
   +===========+=======================================================================+===============================================+
   | nodes     | Array of :ref:`NodeList <ddm_api_01_0082__response_nodelist>` objects | Instance node information                     |
   +-----------+-----------------------------------------------------------------------+-----------------------------------------------+
   | offset    | Integer                                                               | Which page the server starts returning items. |
   +-----------+-----------------------------------------------------------------------+-----------------------------------------------+
   | limit     | Integer                                                               | Number of records displayed on each page      |
   +-----------+-----------------------------------------------------------------------+-----------------------------------------------+
   | total     | Integer                                                               | Number of DDM instance nodes                  |
   +-----------+-----------------------------------------------------------------------+-----------------------------------------------+

.. _ddm_api_01_0082__response_nodelist:

.. table:: **Table 5** NodeList

   +-----------+--------+---------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                               |
   +===========+========+===========================================================================+
   | port      | String | Port                                                                      |
   +-----------+--------+---------------------------------------------------------------------------+
   | status    | String | Node status For details, see :ref:`Status Description <ddm_api_01_0064>`. |
   +-----------+--------+---------------------------------------------------------------------------+
   | node_id   | String | Node ID                                                                   |
   +-----------+--------+---------------------------------------------------------------------------+
   | ip        | String | ip                                                                        |
   +-----------+--------+---------------------------------------------------------------------------+

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

   GET https://{endpoint}/v1/{project_id}/instances/{instance_id}/nodes?offset={offset}&limit={limit}

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "nodes" : [ {
       "port" : "5066",
       "status" : "normal",
       "node_id" : "4a2b97b7f5e3462c9c78aae93b46ed83no09",
       "ip" : "192.168.0.160"
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
