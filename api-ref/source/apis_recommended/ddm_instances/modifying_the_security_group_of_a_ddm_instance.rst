:original_name: ddm_api_01_0021.html

.. _ddm_api_01_0021:

Modifying the Security Group of a DDM Instance
==============================================

Function
--------

This API is used to modify the security group of a DDM instance.

Constraints
-----------

None

URI
---

PUT /v1/{project_id}/instances/{instance_id}/modify-security-group

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

   +-------------------+-----------+--------+---------------------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory | Type   | Description                                                                                                   |
   +===================+===========+========+===============================================================================================================+
   | security_group_id | Yes       | String | Security group ID. The default value is the original security group ID. You can change the value as required. |
   +-------------------+-----------+--------+---------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   ================= ====== =================
   Parameter         Type   Description
   ================= ====== =================
   security_group_id String Security group ID
   ================= ====== =================

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

   PUT https://{endpoint}/v1/{project_id}/instances/{instance_id}/modify-security-group

   {
     "security_group_id" : "035b70ed-319b-4086-9fd7-62a2e8548b2e"
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "security_group_id" : "035b70ed-319b-4086-9fd7-62a2e8548b2e"
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
