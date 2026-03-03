:original_name: ddm_api_01_0085.html

.. _ddm_api_01_0085:

Modifying Parameters of a DDM Instance (a V3 API)
=================================================

Function
--------

This API is used to modify parameters of a DDM instance.

Constraints
-----------

None

URI
---

PUT /v3/{project_id}/instances/{instance_id}/configurations

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
   | Content-Type    | Yes             | String          | MIME type of the request body. Value range:                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | -  application/json                                                                                                  |
   |                 |                 |                 | -  application/json;charset=utf-8                                                                                    |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-----------------+-----------------+--------------------+------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type               | Description                                                                                    |
   +=================+=================+====================+================================================================================================+
   | values          | Yes             | Map<String,String> | Parameter values defined by users based on a default parameter template.                       |
   |                 |                 |                    |                                                                                                |
   |                 |                 |                    | -  **key**: parameter name. If a parameter name is left empty, its value is not to be changed. |
   |                 |                 |                    | -  **value**: parameter value.                                                                 |
   +-----------------+-----------------+--------------------+------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   =========== ======= ==========================================
   Parameter   Type    Description
   =========== ======= ==========================================
   nodeList    String  DDM instance nodes
   needRestart Boolean Whether the instance needs to be restarted
   jobId       String  Task ID
   configId    String  Parameter group ID
   configName  String  Parameter group name
   =========== ======= ==========================================

**Status code: 400**

.. table:: **Table 5** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

**Status code: 500**

.. table:: **Table 6** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

Example Request
---------------

.. code-block:: text

   PUT https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/configurations

   {
     "values" : {
       "long_query_time" : 2
     }
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "nodeList" : null,
     "needRestart" : "false",
     "jobId" : "9fe84a77-6a6b-4b03-9a3e-db910a548657",
     "configId" : null,
     "configName" : null
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
