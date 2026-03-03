:original_name: ddm_api_01_0023.html

.. _ddm_api_01_0023:

Restarting a DDM Instance (a V1 API)
====================================

Function
--------

This API is used to restart a DDM instance.

Constraints
-----------

-  This API is to be removed soon, so it is not recommended.
-  Use the latest API. For details, see :ref:`Restarting a DDM Instance (a V3 API) <en-us_topic_0000002181623846>`.

URI
---

POST /v1/{project_id}/instances/{instance_id}/action

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
   | X-Auth-Token    | Yes             | String          | User token.                                                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | It can be obtained by calling an IAM API. The value of **X-Subject-Token** in the response header is the user token. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+
   | Content-Type    | Yes             | String          | MIME type of the request body. Value range:                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | -  application/json                                                                                                  |
   |                 |                 |                 | -  application/json;charset=utf-8                                                                                    |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-----------+-----------+--------------------------------------------------------------------------------+---------------------------+
   | Parameter | Mandatory | Type                                                                           | Description               |
   +===========+===========+================================================================================+===========================+
   | restart   | No        | :ref:`RestarInstanceInfo <ddm_api_01_0023__request_restarinstanceinfo>` object | Restart-related parameter |
   +-----------+-----------+--------------------------------------------------------------------------------+---------------------------+

.. _ddm_api_01_0023__request_restarinstanceinfo:

.. table:: **Table 4** RestarInstanceInfo

   +-----------------+-----------------+-----------------+-----------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                         |
   +=================+=================+=================+=====================================================+
   | type            | No              | String          | Restart type, which can be **soft** or **hard**.    |
   |                 |                 |                 |                                                     |
   |                 |                 |                 | -  **soft**: Only the process is restarted.         |
   |                 |                 |                 | -  **hard**: The instance VM is forcibly restarted. |
   |                 |                 |                 |                                                     |
   |                 |                 |                 | Enumerated values:                                  |
   |                 |                 |                 |                                                     |
   |                 |                 |                 | -  **soft**                                         |
   |                 |                 |                 | -  **hard**                                         |
   +-----------------+-----------------+-----------------+-----------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 5** Response body parameters

   ============ ====== =================
   Parameter    Type   Description
   ============ ====== =================
   instanceId   String DDM instance ID
   instanceName String DDM instance name
   jobId        String Task ID
   ============ ====== =================

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

   POST https://ddm.eu-de.otc.t-systems.com/v1/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/action

   {
     "restart" : {
       "type" : "soft"
     }
   }

Example Response
----------------

**Status code: 200**

ok

.. code-block::

   {
     "instanceId" : "28e8841d0b9c4f6a9a30742ee60e1068in09",
     "instanceName" : "ddm-fb88-test",
     "jobId" : "1eb697c0-1842-43a3-8671-f562d0385cb9"
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
200         ok
400         bad request
500         server error
=========== ============

Error Codes
-----------

For details, see :ref:`Error Codes <ddm_api_01_0061>`.
