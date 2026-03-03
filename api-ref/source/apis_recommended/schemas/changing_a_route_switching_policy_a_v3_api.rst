:original_name: en-us_topic_0000002332869349.html

.. _en-us_topic_0000002332869349:

Changing a Route Switching Policy (a V3 API)
============================================

Function
--------

This API is used to change a route switching policy.

Constraints
-----------

Only the route switching policy of a shard configuration task in the **ToBeSwitched** state can be changed.

URI
---

PUT /v3/{project_id}/instances/{instance_id}/databases/{db_name}/migration/jobs/{job_id}/route-switch-strategy

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

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                          |
   +=================+=================+=================+======================================================================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | It can be obtained by calling an IAM API. The value of **X-Subject-Token** in the response header is the user token. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+
   | Content-Type    | Yes             | String          | MIME type of the request body. Value range:                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | -  application/json                                                                                                  |
   |                 |                 |                 | -  application/json;charset=utf-8                                                                                    |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter               | Mandatory       | Type            | Description                                                                                                                                    |
   +=========================+=================+=================+================================================================================================================================================+
   | switch_route_begin_time | No              | String          | Time when the automatic route switching starts (in the *hh*\ **:**\ *mm*\ **:**\ *ss* format, for example, **17:00:00**)                       |
   |                         |                 |                 |                                                                                                                                                |
   |                         |                 |                 | -  If **switch_route_begin_time** and **switch_route_end_time** are not included in the request body, a manual route switching policy is used. |
   |                         |                 |                 | -  The interval between the start time and end time cannot exceed 1 hour.                                                                      |
   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | switch_route_end_time   | No              | String          | Time when the automatic route switching ends (in the *hh*\ **:**\ *mm*\ **:**\ *ss* format, for example, **18:00:00**)                         |
   |                         |                 |                 |                                                                                                                                                |
   |                         |                 |                 | -  If **switch_route_begin_time** and **switch_route_end_time** are not included in the request body, a manual route switching policy is used. |
   |                         |                 |                 | -  The interval between the start time and end time cannot exceed 1 hour.                                                                      |
   +-------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

Configuring an automatic route switching policy

.. code-block:: text

   PUT https://{endpoint}/v3/{project_id}/instances/{instance_id}/databases/{db_name}/migration/jobs/{job_id}/route-switch-strategy

   {
     "switch_route_begin_time": "17:00:00",
     "switch_route_end_time": "18:00:00"
   }

Configuring a manual route switching policy

.. code-block:: text

   PUT https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/databases/ddm_db_test/migration/jobs/10501cd3-0c19-498b-9ba4-8935ed447542/route-switch-strategy

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
