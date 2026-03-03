:original_name: ddm_api_01_0113.html

.. _ddm_api_01_0113:

Deleting an Instance (a V3 API)
===============================

Function
--------

This API is used to delete a DDM instance to release all its resources.

Constraints
-----------

None

URI
---

-  URL format

   DELETE /v3/{project_id}/instances/{instance_id}

-  Parameter description

   .. table:: **Table 1** Path parameters

      =========== ========= ====== ===================================
      Parameter   Mandatory Type   Description
      =========== ========= ====== ===================================
      project_id  Yes       String Project ID of a tenant in a region.
      instance_id Yes       String DDM instance ID.
      =========== ========= ====== ===================================

   .. table:: **Table 2** Query parameters

      +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------+
      | Parameter       | Mandatory       | Type            | Description                                                                                                              |
      +=================+=================+=================+==========================================================================================================================+
      | delete_dn_data  | No              | Boolean         | Whether data stored on the associated DB instances is deleted. This parameter is left empty by default.                  |
      |                 |                 |                 |                                                                                                                          |
      |                 |                 |                 | **true**: indicates that the data stored on the associated DB instances is deleted.                                      |
      |                 |                 |                 |                                                                                                                          |
      |                 |                 |                 | **false** or leaving this parameter empty: indicates that the data stored on the associated DB instances is not deleted. |
      +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 3** Request header parameters

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                  |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Example Request
---------------

Deleting an instance (including the data stored on associated DB instances)

.. code-block:: text

   DELETE https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09?delete_dn_data=true

Deleting an instance (excluding the data stored on associated DB instances)

.. code-block:: text

   DELETE https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09?delete_dn_data=false

Response
--------

-  Normal response

   .. table:: **Table 4** Response body parameters

      ========= ====== =======================================
      Parameter Type   Description
      ========= ====== =======================================
      job_id    String ID of the job for deleting an instance.
      ========= ====== =======================================

-  Normal response example

   .. code-block::

      {
       "job_id": "eff1d289-xxxx-xxxx-8b9f-463ea07c000c"
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
