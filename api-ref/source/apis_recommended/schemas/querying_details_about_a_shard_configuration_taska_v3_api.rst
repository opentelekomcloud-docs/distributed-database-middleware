:original_name: en-us_topic_0000002332909545.html

.. _en-us_topic_0000002332909545:

Querying Details About a Shard Configuration Task (a V3 API)
============================================================

Function
--------

This API is used to query details about a shard configuration task.

Constraints
-----------

None

URI
---

GET /v3/{project_id}/instances/{instance_id}/databases/{db_name}/migration/jobs/{job_id}

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

Querying details about a shard configuration task

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/74f57817ca8f42e19318eb0e0ad41d18/instances/733c7e8d73a54c27b8308ec784a8be8cin09/databases/db_e487/migration/jobs/10501cd3-0c19-498b-9ba4-8935ed447542

Response
--------

-  Normal response

   .. table:: **Table 3** Response body parameters

      +------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
      | Parameter              | Type                                                                                                                     | Description                                                                                                              |
      +========================+==========================================================================================================================+==========================================================================================================================+
      | instance_name          | String                                                                                                                   | Instance name                                                                                                            |
      +------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
      | original_shard_num     | Integer                                                                                                                  | Total number of shards before configuration                                                                              |
      +------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
      | after_shard_num        | Integer                                                                                                                  | Total number of shards after configuration                                                                               |
      +------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
      | original_dn_info_list  | Array of :ref:`DnInfo <en-us_topic_0000002332909545__en-us_topic_0000002285238426_request_createdatabasedetail>` objects | Information about data nodes before configuration                                                                        |
      +------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
      | after_dn_info_list     | Array of :ref:`DnInfo <en-us_topic_0000002332909545__en-us_topic_0000002285238426_request_createdatabasedetail>` objects | Information about data nodes after configuration                                                                         |
      +------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
      | switch_route_is_manual | Boolean                                                                                                                  | Whether manual route switching is used.                                                                                  |
      |                        |                                                                                                                          |                                                                                                                          |
      |                        |                                                                                                                          | -  **true**: Manual route switching is used.                                                                             |
      |                        |                                                                                                                          | -  **false**: Automatic route switching is used.                                                                         |
      +------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
      | auto_switch_begin_time | String                                                                                                                   | Time when the automatic route switching starts (in the *hh*\ **:**\ *mm*\ **:**\ *ss* format, for example, **17:00:00**) |
      +------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
      | auto_switch_end_time   | String                                                                                                                   | Time when the automatic route switching ends (in the *hh*\ **:**\ *mm*\ **:**\ *ss* format, for example, **18:00:00**)   |
      +------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
      | node_id_for_migrate    | String                                                                                                                   | Node where shard configuration is performed                                                                              |
      +------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
      | is_exclusive           | Boolean                                                                                                                  | Whether shard configuration exclusively occupies a node. The value can be:                                               |
      |                        |                                                                                                                          |                                                                                                                          |
      |                        |                                                                                                                          | -  **true**: It exclusively occupies a node.                                                                             |
      |                        |                                                                                                                          | -  **false**: It does not exclusively occupy a node.                                                                     |
      +------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+

   .. _en-us_topic_0000002332909545__en-us_topic_0000002285238426_request_createdatabasedetail:

   .. table:: **Table 4** DnInfo

      ================ ====== ==============
      Parameter        Type   Description
      ================ ====== ==============
      dn_instance_id   String Data node ID
      dn_instance_name String Data node name
      ================ ====== ==============

-  Normal response example

   .. code-block::

      {
        "instance_name": "UTS-src",
        "original_shard_num": 8,
        "after_shard_num": 9,
        "original_dn_info_list": [
          {
            "dn_instance_id": "7edae0250ebc464897bd92b8d3e8b769in01",
            "dn_instance_name": "UTS-rds-src"
          }
        ],
        "after_dn_info_list": [
          {
            "dn_instance_id": "7edae0250ebc464897bd92b8d3e8b769in01",
            "dn_instance_name": "UTS-rds-src"
          }
        ],
        "switch_route_is_manual": true,
        "auto_switch_begin_time": "",
        "auto_switch_end_time": "",
        "node_id_for_migrate": "0c12161a26a4426c9bc72efe4ff05224no09",
        "is_exclusive": false
      }

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
