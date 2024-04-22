:original_name: ddm_api_01_0020.html

.. _ddm_api_01_0020:

Modifying the Name of a DDM Instance
====================================

Function
--------

This API is used to modify the name of a DDM instance.

Constraints
-----------

None

URI
---

PUT /v1/{project_id}/instances/{instance_id}/modify-name

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

   +-----------------+-----------------+-----------------+-------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                           |
   +=================+=================+=================+=======================================================+
   | name            | Yes             | String          | Name of a DDM instance, which:                        |
   |                 |                 |                 |                                                       |
   |                 |                 |                 | -  Can include 4 to 64 characters.                    |
   |                 |                 |                 | -  Must start with a letter.                          |
   |                 |                 |                 | -  Can contain only letters, digits, and hyphens (-). |
   |                 |                 |                 |                                                       |
   |                 |                 |                 | Minimum length: 4 characters                          |
   |                 |                 |                 |                                                       |
   |                 |                 |                 | Maximum length: 64 characters                         |
   +-----------------+-----------------+-----------------+-------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   ========= ====== =================
   Parameter Type   Description
   ========= ====== =================
   name      String DDM instance name
   ========= ====== =================

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

   PUT https://{endpoint}/v1/{project_id}/instances/{instance_id}/modify-name

   {
     "name" : "DDM-test-04"
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "name" : "DDM-test-04"
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
