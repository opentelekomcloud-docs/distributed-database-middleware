:original_name: ddm_api_01_0080.html

.. _ddm_api_01_0080:

Modifying the Read Policy of the Associated DB Instance
=======================================================

Function
--------

This API is used to modify the read policy of the DB instance associated with a DDM instance.

Constraints
-----------

Make sure that the associated RDS instances are available and not undergoing other operations.

URI
---

PUT /v2/{project_id}/instances/{instance_id}/action/read-write-strategy

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

.. table:: **Table 3** Request body parameters

   +-----------------+-----------------+----------------------+---------------------------------------------------------------+
   | Parameter       | Mandatory       | Type                 | Description                                                   |
   +=================+=================+======================+===============================================================+
   | read_weight     | Yes             | Map<String, Integer> | Read weights of the primary DB instance and its read replicas |
   |                 |                 |                      |                                                               |
   |                 |                 |                      | -  key: DB instance ID                                        |
   |                 |                 |                      | -  value: read weight parameter                               |
   +-----------------+-----------------+----------------------+---------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   =========== ======= ===================================
   Parameter   Type    Description
   =========== ======= ===================================
   success     Boolean Whether the operation is successful
   instance_id String  DDM instance ID
   =========== ======= ===================================

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

   PUT https://{endpoint}/v2/{project_id}/instances/{instance_id}/action/read-write-strategy

   {
     "read_weight" : {
       "395298ae6fb9496d95939ed556474983in01" : 60,
       "38ef52c365a14b7caeb7333137900e96in01" : 50
     }
   }

Example Response
----------------

**Status code: 200**

ok

.. code-block::

   {
     "success" : true,
     "instance_id" : "175f5aff-xxxx-xxxx-xxxx-d0858982bbec"
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
