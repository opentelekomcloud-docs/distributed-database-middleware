:original_name: en-us_topic_0000002298790192.html

.. _en-us_topic_0000002298790192:

Performing Shard Configuration (a V3 API)
=========================================

Function
--------

This API is used to add data nodes or shards to enhance data storage and provide better support for concurrency.

Constraints
-----------

The shard configuration task can only be performed after all pre-check items are passed. You can query the task status by calling the API for querying the task list.

URI
---

POST /v3/{project_id}/instances/{instance_id}/databases/{db_name}/migration

.. table:: **Table 1** Path parameters

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

   +-------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter               | Mandatory       | Type                                                                                                                                        | Description                                                                                                                                                                                                                                                                         |
   +=========================+=================+=============================================================================================================================================+=====================================================================================================================================================================================================================================================================================+
   | data_nodes              | Yes             | Array of :ref:`MigrateLogicDbOpenRequest <en-us_topic_0000002298790192__en-us_topic_0000002319757949_request_createdatabasedetail>` objects | Data nodes used for shard configuration.                                                                                                                                                                                                                                            |
   |                         |                 |                                                                                                                                             |                                                                                                                                                                                                                                                                                     |
   |                         |                 |                                                                                                                                             | The number of shards or data nodes after the configuration must be greater than that before the configuration.                                                                                                                                                                      |
   +-------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | new_shard_number        | Yes             | String                                                                                                                                      | Number of shards after the shard configuration.                                                                                                                                                                                                                                     |
   |                         |                 |                                                                                                                                             |                                                                                                                                                                                                                                                                                     |
   |                         |                 |                                                                                                                                             | The number of shards or data nodes after the configuration must be greater than that before the configuration. A single instance supports a maximum of 64 shards.                                                                                                                   |
   +-------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | switch_route_begin_time | No              | String                                                                                                                                      | Time when the automatic route switching starts (in the *hh*\ **:**\ *mm*\ **:**\ *ss* format, for example, **17:00:00**). The start time must be earlier than the end time, and the interval cannot be less than 60 minutes. Switching routes during off-peak hours is recommended. |
   +-------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | switch_route_end_time   | No              | String                                                                                                                                      | Time when the automatic route switching ends (in the *hh*\ **:**\ *mm*\ **:**\ *ss* format, for example, **18:00:00**). The end time must be later than the start time, and the interval cannot be less than 60 minutes. Switching routes during off-peak hours is recommended.     |
   +-------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | is_exclusive            | No              | Boolean                                                                                                                                     | Whether shard configuration exclusively occupies a node. The default value is **false**. The value can be:                                                                                                                                                                          |
   |                         |                 |                                                                                                                                             |                                                                                                                                                                                                                                                                                     |
   |                         |                 |                                                                                                                                             | -  **true**: It exclusively occupies a node.                                                                                                                                                                                                                                        |
   |                         |                 |                                                                                                                                             | -  **false**: It does not exclusively occupy a node.                                                                                                                                                                                                                                |
   |                         |                 |                                                                                                                                             |                                                                                                                                                                                                                                                                                     |
   |                         |                 |                                                                                                                                             | -  If this parameter is set to **true**, the execution node will be dedicated to configuring shards, so shard configuration is faster. If you are worried about not having enough nodes to handle your services, add more nodes before configuring shards.                          |
   |                         |                 |                                                                                                                                             | -  If this parameter is set to **true**, you need to enable load balancing for the default group and ensure that the number of nodes exceeds one.                                                                                                                                   |
   +-------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _en-us_topic_0000002298790192__en-us_topic_0000002319757949_request_createdatabasedetail:

.. table:: **Table 4** MigrateLogicDbOpenRequest

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                  |
   +=================+=================+=================+==============================================================================================================================================================================================================================================================================================================================+
   | id              | Yes             | String          | Data node ID                                                                                                                                                                                                                                                                                                                 |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | user            | Yes             | String          | Database user                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                 | -  Required permissions: SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, PROCESS, REFERENCES, INDEX, ALTER, SHOW DATABASES, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER WITH GRANT OPTION |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | password        | Yes             | String          | Database password                                                                                                                                                                                                                                                                                                            |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

Configuring shards

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/databases/ddm_db_test/migration

   {
     "new_shard_number": 9,
     "data_nodes": [
       {
         "id": "7edae0250ebc464897bd92b8d3e8b769in01",
         "user": "root",
         "password": "Ga***123"
       }
     ]
   }

Response
--------

-  Normal response

   .. table:: **Table 5** Response body parameters

      ========= ====== ==================================
      Parameter Type   Description
      ========= ====== ==================================
      job_id    String ID of the shard configuration task
      ========= ====== ==================================

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
