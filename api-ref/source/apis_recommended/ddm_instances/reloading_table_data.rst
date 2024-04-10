:original_name: ddm_api_01_0024.html

.. _ddm_api_01_0024:

Reloading Table Data
====================

Function
--------

This API is used to reload table data of the destination DDM instance for cross-region DR.

Constraints
-----------

None

URI
---

POST /v1/{project_id}/instances/{instance_id}/reload-config

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

Response Parameters
-------------------

**Status code: 200**

No response parameters

**Status code: 400**

.. table:: **Table 3** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

**Status code: 500**

.. table:: **Table 4** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

Example Request
---------------

.. code-block:: text

   POST https://{endpoint}/v1/{project_id}/instances/{instance_id}/reload_config

   { }

Example Response
----------------

**Status code: 200**

ok

.. code-block::

   { }

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
