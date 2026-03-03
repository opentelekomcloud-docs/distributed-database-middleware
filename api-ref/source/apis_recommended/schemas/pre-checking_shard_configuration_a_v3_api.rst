:original_name: en-us_topic_0000002332869333.html

.. _en-us_topic_0000002332869333:

Pre-checking Shard Configuration (a V3 API)
===========================================

Function
--------

This API is used to pre-check shard configuration to prevent shard configuration failures. For details about pre-check items, see the user guide.

This API returns the following synchronous pre-check items:

-  Table name length
-  Binlog full backup time of data nodes
-  Binlog enabled on data nodes
-  Retention period of binlogs on data nodes
-  Maximum number of physical tables

Constraints
-----------

None

URI
---

POST /v3/{project_id}/instances/{instance_id}/databases/{db_name}/migration/precheck

.. table:: **Table 1** URI parameters

   =========== ====== ========= ==================================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ==================================
   project_id  String Yes       Project ID of a tenant in a region
   instance_id String Yes       Instance ID
   db_name     String Yes       Schema name
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

   +------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Mandatory       | Type                                                                                                                                         | Description                                                                                                                                                       |
   +==================+=================+==============================================================================================================================================+===================================================================================================================================================================+
   | data_nodes       | Yes             | Array of :ref:`MigratePrecheckOpenRequest <en-us_topic_0000002332869333__en-us_topic_0000002285238422_request_createdatabasedetail>` objects | Data node information after the configuration.                                                                                                                    |
   |                  |                 |                                                                                                                                              |                                                                                                                                                                   |
   |                  |                 |                                                                                                                                              | The number of shards or data nodes after the configuration must be greater than that before the configuration.                                                    |
   +------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | new_shard_number | Yes             | String                                                                                                                                       | Number of shards after the configuration.                                                                                                                         |
   |                  |                 |                                                                                                                                              |                                                                                                                                                                   |
   |                  |                 |                                                                                                                                              | The number of shards or data nodes after the configuration must be greater than that before the configuration. A single instance supports a maximum of 64 shards. |
   +------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _en-us_topic_0000002332869333__en-us_topic_0000002285238422_request_createdatabasedetail:

.. table:: **Table 4** MigratePrecheckOpenRequest

   ========= ========= ====== =================
   Parameter Mandatory Type   Description
   ========= ========= ====== =================
   id        Yes       String Data node ID
   user      Yes       String Database user
   password  Yes       String Database password
   ========= ========= ====== =================

Example Request
---------------

Pre-verifying shard configuration

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/databases/ddm_db_test/migration/precheck

   {
     "new_shard_number": "9",
     "data_nodes": [
       {
         "id": "7edae0250ebc464897bd92b8d3e8b769in01",
         "user": "root",
         "password": "Gau***b123"
       }
     ]
   }

Response
--------

-  Normal response

   .. table:: **Table 5** Response body parameters

      +-------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter         | Type                                                                                                                               | Description                                                                                                                                                                                     |
      +===================+====================================================================================================================================+=================================================================================================================================================================================================+
      | job_id            | String                                                                                                                             | Pre-verification task ID. To obtain the result of an asynchronous task, see :ref:`Querying the Asynchronous Pre-check Result of Shard Configuration (a V3 API) <en-us_topic_0000002298949848>`. |
      +-------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | pre_check_results | Array of :ref:`PreCheckMigrateSyncResult <en-us_topic_0000002332869333__en-us_topic_0000002285238422_table13354337184813>` objects | Pre-verification results                                                                                                                                                                        |
      +-------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. _en-us_topic_0000002332869333__en-us_topic_0000002285238422_table13354337184813:

   .. table:: **Table 6** PreCheckMigrateSyncResult

      +-----------------------+-----------------------+-----------------------------+
      | Parameter             | Type                  | Description                 |
      +=======================+=======================+=============================+
      | name                  | String                | Check item                  |
      +-----------------------+-----------------------+-----------------------------+
      | status                | String                | Check result, which can be: |
      |                       |                       |                             |
      |                       |                       | -  **SUCCESS**: successful  |
      |                       |                       | -  **FAILED**: failed       |
      |                       |                       | -  **WARN**: Warning        |
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

   202

-  Abnormal

   For details, see :ref:`Status Codes <ddm_api_01_0060>`.

Error Codes
-----------

For details, see :ref:`Error Codes <ddm_api_01_0061>`.
