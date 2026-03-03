:original_name: ddm_api_01_0116.html

.. _ddm_api_01_0116:

Deleting a Schema (a V3 API)
============================

Function
--------

This API is used to delete a schema to release all its resources.

Constraints
-----------

None

URI
---

-  URL format

   DELETE /v3/{project_id}/instances/{instance_id}/databases/{database_name}?delete_dn_data={delete_dn_data}

-  Parameter description

   .. table:: **Table 1** Path parameters

      ============= ========= ====== ===================================
      Parameter     Mandatory Type   Description
      ============= ========= ====== ===================================
      project_id    Yes       String Project ID of a tenant in a region.
      instance_id   Yes       String DDM instance ID
      database_name Yes       String Schema name
      ============= ========= ====== ===================================

   .. table:: **Table 2** Query parameters

      +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------+
      | Parameter       | Mandatory       | Type            | Description                                                                              |
      +=================+=================+=================+==========================================================================================+
      | delete_dn_data  | Yes             | Boolean         | Whether data stored on the associated DB instances is deleted. The value can be:         |
      |                 |                 |                 |                                                                                          |
      |                 |                 |                 | **true**: indicates that the data stored on the associated DB instances is deleted.      |
      |                 |                 |                 |                                                                                          |
      |                 |                 |                 | **false**: indicates that the data stored on the associated DB instances is not deleted. |
      +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------+

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

Request
-------

-  Request Parameters

   None

-  URI example

   -  Deleting a schema (including the data stored on associated DB instances)

      .. code-block:: text

         DELETE https://{endpoint}/v3/{project_id}/instances/{instance_id}/databases/{database_name}?delete_dn_data=true

   -  Deleting a schema (excluding the data stored on associated DB instances)

      .. code-block:: text

         DELETE https://{endpoint}/v3/{project_id}/instances/{instance_id}/databases/{database_name}?delete_dn_data=false

Response
--------

-  Normal response

   .. table:: **Table 4** Response body parameters

      ============= ====== ===================================
      Parameter     Type   Description
      ============= ====== ===================================
      job_id        String ID of the job for deleting a schema
      database_name String Schema name
      ============= ====== ===================================

-  Normal response example

   .. code-block::

      {
      "job_id": "eff1d289-xxxx-xxxx-8b9f-463ea07c000c",
       "database_name": "test"
      }

-  Abnormal response

   For details, see :ref:`Abnormal Request Results <ddm_api_01_0059>`.

Status Codes
------------

-  Normal

   202

-  Abnormal

   For details, see :ref:`Status Codes <ddm_api_01_0060>`.

Error Codes
-----------

For details, see :ref:`Error Codes <ddm_api_01_0061>`.
