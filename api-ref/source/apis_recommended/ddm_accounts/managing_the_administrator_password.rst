:original_name: ddm_api_01_0101.html

.. _ddm_api_01_0101:

Managing the Administrator Password
===================================

Function
--------

If it is the first time to call this API, it is used to create an administrator and reset its password for a DDM instance. Then this API can only be used to update the administrator password.

URI
---

PUT /v3/{project_id}/instances/{instance_id}/admin-user

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
   | x-auth-token    | Yes             | String          | User token.                                                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | It can be obtained by calling an IAM API. The value of **X-Subject-Token** in the response header is the user token. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                             |
   +=================+=================+=================+=========================================================================================================================================================================================================================================+
   | name            | Yes             | String          | Username of the administrator. The username:                                                                                                                                                                                            |
   |                 |                 |                 |                                                                                                                                                                                                                                         |
   |                 |                 |                 | -  Can include 1 to 32 characters.                                                                                                                                                                                                      |
   |                 |                 |                 | -  Must start with a letter.                                                                                                                                                                                                            |
   |                 |                 |                 | -  Can contain only letters, digits, and underscores (_).                                                                                                                                                                               |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | password        | Yes             | String          | Password of the administrator. The password:                                                                                                                                                                                            |
   |                 |                 |                 |                                                                                                                                                                                                                                         |
   |                 |                 |                 | -  Can include 8 to 32 characters.                                                                                                                                                                                                      |
   |                 |                 |                 | -  Must be a combination of uppercase letters, lowercase letters, digits, and the following special characters: ``~!@#%^*-_=+?`` Must be a strong password to improve security and prevent security risks such as brute force cracking. |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   =========== ====== ===============
   Parameter   Type   Description
   =========== ====== ===============
   instance_id String DDM instance ID
   job_id      String Task ID
   =========== ====== ===============

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

   PUT https://{endpoint}/v3/{project_id}/instances/{instance_id}/admin-user

   {
     "name" : "root",
     "password" : "****"
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "instance_id" : "175f5aff-****-****-****-d0858982bbec",
     "job_id" : "b9e057a0-f0fb-4987-9d21-f3a7550b32e7"
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
