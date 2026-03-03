:original_name: en-us_topic_0000002298949848.html

.. _en-us_topic_0000002298949848:

Querying the Asynchronous Pre-check Result of Shard Configuration (a V3 API)
============================================================================

Function
--------

This API is used to query the pre-check result of a shard configuration task that takes some time to execute. For details about pre-check items, see the user guide.

The asynchronous pre-check items are as follows:

-  Broadcast table consistency
-  Character set and collation of source shards
-  SQL statements for creating physical stables.
-  Primary keys
-  Access to DB instances
-  DB instance parameters
-  DB instance storage space
-  DB instance time zone

Constraints
-----------

None

URI
---

GET /v3/{project_id}/instances/{instance_id}/databases/{db_name}/migration/precheck/{job_id}

.. table:: **Table 1** Path parameters

   +-------------+--------+-----------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter   | Type   | Mandatory | Description                                                                                                                             |
   +=============+========+===========+=========================================================================================================================================+
   | project_id  | String | Yes       | Project ID of a tenant in a region                                                                                                      |
   +-------------+--------+-----------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | instance_id | String | Yes       | Instance ID                                                                                                                             |
   +-------------+--------+-----------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | db_name     | String | Yes       | Schema name                                                                                                                             |
   +-------------+--------+-----------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | job_id      | String | Yes       | Pre-verification task ID, which can be obtained from :ref:`Pre-checking Shard Configuration (a V3 API) <en-us_topic_0000002332869333>`. |
   +-------------+--------+-----------+-----------------------------------------------------------------------------------------------------------------------------------------+

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

Querying the asynchronous pre-check result of shard configuration

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/733c7e8d73a54c27b8308ec784a8be8cin09/databases/db_3c46/migration/precheck/daab28f6-efd8-4c5b-bccb-85b4162373c4

Response
--------

.. table:: **Table 3** Response body parameters

   +-------------------+-------------------------------------------------------------------------------------------------------------------------+--------------------------+
   | Parameter         | Type                                                                                                                    | Description              |
   +===================+=========================================================================================================================+==========================+
   | job_id            | String                                                                                                                  | Pre-verification task ID |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------+--------------------------+
   | pre_check_results | Array of :ref:`PreCheckResult <en-us_topic_0000002298949848__en-us_topic_0000002285181692_table13354337184813>` objects | Pre-verification results |
   +-------------------+-------------------------------------------------------------------------------------------------------------------------+--------------------------+

.. _en-us_topic_0000002298949848__en-us_topic_0000002285181692_table13354337184813:

.. table:: **Table 4** PreCheckResult

   +-----------------------+-----------------------+-----------------------------+
   | Parameter             | Type                  | Description                 |
   +=======================+=======================+=============================+
   | name                  | String                | Check item                  |
   +-----------------------+-----------------------+-----------------------------+
   | status                | String                | Check result, which can be: |
   |                       |                       |                             |
   |                       |                       | **SUCCESS**: successful     |
   |                       |                       |                             |
   |                       |                       | **FAILED**: failed          |
   |                       |                       |                             |
   |                       |                       | **WARN**: Warning           |
   +-----------------------+-----------------------+-----------------------------+
   | note                  | String                | Prompt information          |
   +-----------------------+-----------------------+-----------------------------+
   | handling_suggestion   | String                | Modification suggestions    |
   +-----------------------+-----------------------+-----------------------------+
   | error_message         | String                | Error message               |
   +-----------------------+-----------------------+-----------------------------+
   | error_detail_message  | String                | Error details               |
   +-----------------------+-----------------------+-----------------------------+

-  Normal response example

   .. code-block::

      {
        "job_id": "65c77858-e6a2-4694-8810-ab0b501b0003",
        "pre_check_results": [
          {
            "name": "Expire time of binlog in associated DN instances",
            "status": "SUCCESS",
            "note": "",
            "handling_suggestion": "Configuring shards require expiration of binlog more than 7 days(604800 seconds), please change binlog_expire_logs_seconds",
            "error_message": "",
            "error_detail_message": ""
          },
          {
            "name": "Tables with overwhelming table partitions",
            "status": "SUCCESS",
            "note": "",
            "handling_suggestion": "Every single row from source table will be recalculated and routed to all new partition table when shard number is changed. Because your partition table number will be overwhelming after configuring shard, shard configuring will take too long to finish. Please contact customer service.",
            "error_message": "",
            "error_detail_message": ""
          }
        ]
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
