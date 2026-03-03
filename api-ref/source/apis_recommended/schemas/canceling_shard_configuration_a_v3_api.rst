:original_name: en-us_topic_0000002332869341.html

.. _en-us_topic_0000002332869341:

Canceling Shard Configuration (a V3 API)
========================================

Function
--------

This API is used to cancel shard configuration.

Constraints
-----------

The shard configuration task to be canceled must be in the **Running**, **Failed**, or **ToBeSwitched** state.

URI
---

PUT /v3/{project_id}/instances/{instance_id}/databases/{db_name}/migration/jobs/{job_id}/cancel

.. table:: **Table 1** Path parameters

   =========== ====== ========= ==================================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ==================================
   project_id  String Yes       Project ID of a tenant in a region
   instance_id String Yes       Instance ID
   db_name     String Yes       Schema name
   job_id      String Yes       ID of the shard configuration task
   =========== ====== ========= ==================================

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                  |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Example Request
---------------

Canceling shard configuration

.. code-block:: text

   PUT https://ddm.eu-de.otc.t-systems.com/v1/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/databases/ddm_db_test/migration/jobs/10501cd3-0c19-498b-9ba4-8935ed447542/cancel

Response
--------

-  Normal response

   .. table:: **Table 3** Response body parameters

      ========= ====== ================================================
      Parameter Type   Description
      ========= ====== ================================================
      job_id    String ID of the task for canceling shard configuration
      ========= ====== ================================================

-  Normal response example

   .. code-block::

      {
        "job_id":"xxxxxxxx-5d7e-4e1a-aeb4-9b1e6d0a4999"
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
