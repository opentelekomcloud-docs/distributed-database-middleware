:original_name: en-us_topic_0000002298949868.html

.. _en-us_topic_0000002298949868:

Switching Routes (a V3 API)
===========================

Function
--------

This API is used to switch read and write requests to a new instance. During the switching process, one or two intermittent disconnections may occur but do not affect services. You are advised to switch routes during off-peak hours.

Constraints
-----------

You can only switch routes when a shard configuration task is in the **ToBeSwitched** state.

URI
---

PUT /v3/{project_id}/instances/{instance_id}/databases/{db_name}/migration/jobs/{job_id}/route-switch

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

Configuring route switching

.. code-block:: text

   PUT https://ddm.eu-de.otc.t-systems.com/v3/74f57817ca8f42e19318eb0e0ad41d18/instances/733c7e8d73a54c27b8308ec784a8be8cin09/databases/db_e487/migration/jobs/10501cd3-0c19-498b-9ba4-8935ed447542/route-switch

Response
--------

-  Normal response

   None

-  Normal response example

   None

-  Abnormal response

   For details, see :ref:`Abnormal Request Results <ddm_api_01_0059>`.

Status Codes
------------

-  Normal

   200

-  Abnormal

   For details, see :ref:`Status Codes <ddm_api_01_0060>`.

Error Codes
-----------

For details, see :ref:`Error Codes <ddm_api_01_0061>`.
