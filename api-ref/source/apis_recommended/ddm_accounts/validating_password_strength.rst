:original_name: ddm_api_01_0102.html

.. _ddm_api_01_0102:

Validating Password Strength
============================

Function
--------

This API is used to check whether an instance password is a weak password.

URI
---

POST /v3/{project_id}/weak-password-verification

.. table:: **Table 1** Path parameters

   ========== ========= ====== ==================================
   Parameter  Mandatory Type   Description
   ========== ========= ====== ==================================
   project_id Yes       String Project ID of a tenant in a region
   ========== ========= ====== ==================================

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                          |
   +=================+=================+=================+======================================================================================================================+
   | x-auth-token    | Yes             | String          | User token.                                                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | It can be obtained by calling an IAM API. The value of **X-Subject-Token** in the response header is the user token. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   ========= ========= ====== ================================
   Parameter Mandatory Type   Description
   ========= ========= ====== ================================
   password  Yes       String Character string to be validated
   ========= ========= ====== ================================

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Type    | Description                                                                                                                                                                                                                                               |
   +==================+=========+===========================================================================================================================================================================================================================================================+
   | is_weak_password | Boolean | Whether the password is a weak password. The value can be: **true**: indicating that the password is a weak password. Such a password is not recommended. **false**: indicating that the password is not a weak password. Such a password is recommended. |
   +------------------+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

   POST https://{endpoint}/v3/{project_id}/weak-password-verification

   {
     "password" : "xxx"
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "is_weak_password" : true
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
