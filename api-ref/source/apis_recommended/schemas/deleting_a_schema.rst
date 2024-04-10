:original_name: ddm_api_01_0031.html

.. _ddm_api_01_0031:

Deleting a Schema
=================

Function
--------

This API is used to delete a schema to release all its resources.

Constraints
-----------

None

URI
---

DELETE /v1/{project_id}/instances/{instance_id}/databases/{ddm_dbname}?delete_rds_data={delete_rds_data}

.. table:: **Table 1** Path parameters

   +-------------+-----------+--------+-------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                 |
   +=============+===========+========+=============================================================+
   | project_id  | Yes       | String | Project ID                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------+
   | instance_id | Yes       | String | DDM instance ID                                             |
   +-------------+-----------+--------+-------------------------------------------------------------+
   | ddm_dbname  | Yes       | String | Name of the schema to be queried, which is case-insensitive |
   +-------------+-----------+--------+-------------------------------------------------------------+

.. table:: **Table 2** Query parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                              |
   +=================+=================+=================+==========================================================================================================================+
   | delete_rds_data | No              | String          | Whether data stored on the associated DB instances is deleted. The value can be:                                         |
   |                 |                 |                 |                                                                                                                          |
   |                 |                 |                 | -  **true**: indicates that the data stored on the associated DB instances is deleted.                                   |
   |                 |                 |                 | -  **false**: indicates that the data stored on the associated DB instances is not deleted. It is left blank by default. |
   |                 |                 |                 |                                                                                                                          |
   |                 |                 |                 | Enumerated values:                                                                                                       |
   |                 |                 |                 |                                                                                                                          |
   |                 |                 |                 | -  **true**                                                                                                              |
   |                 |                 |                 | -  **false**                                                                                                             |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------+

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

   ========= ====== ====================================
   Parameter Type   Description
   ========= ====== ====================================
   job_id    String ID of the job for deleting a schema.
   ========= ====== ====================================

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

-  Request to delete a schema (including the data stored on associated DB instances)

   .. code-block:: text

      DELETE https://{endpoint}/v1/{project_id}/instances/{instance_id}/databases/{ddm_dbname}?delete_rds_data=true

-  Request to delete a schema (excluding the data stored on associated DB instances)

   .. code-block:: text

      DELETE https://{endpoint}/v1/{project_id}/instances/{instance_id}/databases/{ddm_dbname}?delete_rds_data=false

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "job_id" : "01a53563-6057-9ab3-6618-f135nxsj5h2s"
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
