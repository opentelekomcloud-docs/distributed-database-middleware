:original_name: en-us_topic_0000002298949840.html

.. _en-us_topic_0000002298949840:

Querying Information About Tasks (a V3 API)
===========================================

Function
--------

This API is used to query information about tasks.

Constraints
-----------

None

URI
---

GET /v3/{project_id}/jobs

.. table:: **Table 1** Path parameters

   ========== ====== ========= ==================================
   Parameter  Type   Mandatory Description
   ========== ====== ========= ==================================
   project_id String Yes       Project ID of a tenant in a region
   ========== ====== ========= ==================================

.. table:: **Table 2** Query parameters

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                         |
   +=================+=================+=================+=====================================================================================================================+
   | offset          | No              | Integer         | Index offset.                                                                                                       |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | The query starts from the next piece of data indexed by this parameter. The value is **0** by default.              |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | The value must be a number but cannot be a negative number.                                                         |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | limit           | No              | Integer         | Maximum records to be queried.                                                                                      |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | Value range: **1** to **128**.                                                                                      |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | If the parameter value is not specified, 10 records are queried by default.                                         |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | start_time      | Yes             | Long            | Query start time in timestamp format, in milliseconds. It cannot be earlier than 30 days prior to the current time. |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | end_time        | Yes             | Long            | Query end time in timestamp format, in milliseconds.                                                                |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 3** Request header parameters

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token                                                                   |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Example Request
---------------

Querying information about tasks

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/jobs?start_time=1746028800000&end_time=1747319097182

Response
--------

-  Normal response

   .. table:: **Table 4** Response body parameters

      +-----------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | Parameter | Type                                                                                                                      | Description                                  |
      +===========+===========================================================================================================================+==============================================+
      | jobs      | Array of :ref:`JobItem <en-us_topic_0000002298949840__en-us_topic_0000002285962122_request_createdatabasedetail>` objects | Task list.                                   |
      +-----------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | offset    | Integer                                                                                                                   | Which page the server starts returning items |
      +-----------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | limit     | Integer                                                                                                                   | Number of records displayed on each page     |
      +-----------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | total     | Integer                                                                                                                   | Total number of records                      |
      +-----------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+

   .. _en-us_topic_0000002298949840__en-us_topic_0000002285962122_request_createdatabasedetail:

   .. table:: **Table 5** JobItem

      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                                                                                                                                                 |
      +=======================+=======================+=============================================================================================================================================================================================+
      | instance_id           | String                | Instance ID                                                                                                                                                                                 |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | instance_name         | String                | Instance name                                                                                                                                                                               |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | id                    | String                | Task ID                                                                                                                                                                                     |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | name                  | String                | Task name                                                                                                                                                                                   |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | status                | String                | Task execution status. The value can be:                                                                                                                                                    |
      |                       |                       |                                                                                                                                                                                             |
      |                       |                       | -  **Running**: The task is being executed.                                                                                                                                                 |
      |                       |                       | -  **Completed**: The task is successfully executed.                                                                                                                                        |
      |                       |                       | -  **Failed**: The task failed to be executed.                                                                                                                                              |
      |                       |                       | -  **Expanding**: A shard is being configured.                                                                                                                                              |
      |                       |                       | -  **Canceling**: Shard configuration is being canceled.                                                                                                                                    |
      |                       |                       | -  **Rollbacking**: Shard configuration is being rolled back.                                                                                                                               |
      |                       |                       | -  **RollbackSuccess**: Shard configuration is rolled back successfully.                                                                                                                    |
      |                       |                       | -  **CancelSuccess**: Shard configuration is canceled successfully.                                                                                                                         |
      |                       |                       | -  **ToBeSwitched**: The route is to be switched during shard configuration.                                                                                                                |
      |                       |                       | -  **Switching**: The route is being switched during shard configuration.                                                                                                                   |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | created_time          | String                | Creation time in the "yyyy-mm-ddThh:mm:ssZ" format.                                                                                                                                         |
      |                       |                       |                                                                                                                                                                                             |
      |                       |                       | **T** is the separator between the calendar and the hourly notation of time. **Z** indicates the time zone offset. For example, in the Central European time zone, the offset is **+0100**. |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | end_time              | String                | End time. The format is yyyy-mm-ddThh:mm:ssZ.                                                                                                                                               |
      |                       |                       |                                                                                                                                                                                             |
      |                       |                       | **T** is the separator between the calendar and the hourly notation of time. **Z** indicates the time zone offset. For example, in the Central European time zone, the offset is **+0100**. |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | process               | String                | Task execution progress                                                                                                                                                                     |
      |                       |                       |                                                                                                                                                                                             |
      |                       |                       | The execution progress (such as **"60%"**, indicating the task execution progress is 60%) is displayed only when the task is being executed. Otherwise, **""** is returned.                 |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | fail_reason           | String                | Task failure cause                                                                                                                                                                          |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | database_name         | String                | Name of the schema for which shard configuration is performed.                                                                                                                              |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | operations            | Array of strings      | Operations that can be performed on a shard configuration task. The options are as follows:                                                                                                 |
      |                       |                       |                                                                                                                                                                                             |
      |                       |                       | -  **modifySwitchingStrategy**: The route switching policy can be modified.                                                                                                                 |
      |                       |                       | -  **toBeCanceled**: The task is to be canceled.                                                                                                                                            |
      |                       |                       | -  **toBeRetried**: The task can be retried.                                                                                                                                                |
      |                       |                       | -  **toBeRolled**: The task can be rolled back.                                                                                                                                             |
      |                       |                       | -  **toBeSwitched**: The route is to be switched.                                                                                                                                           |
      |                       |                       | -  **toBeCleaned**: The task is to be deleted.                                                                                                                                              |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Normal response example

   .. code-block::

      {
        "jobs": [
          {
            "id": "92370d30-3ddc-4e05-b8ab-51662d824318",
            "name": "migrateLogicDb",
            "status": "ToBeSwitched",
            "created_time": "2025-05-20T15:05:13+0000",
            "end_time": "2025-05-20T15:05:13+0000",
            "process": "",
            "instance_name": "UTS-ddm-dtc-src",
            "instance_id": "733c7e8d73a54c27b8308ec784a8be8cin09",
            "operations": [
              "modifySwitchingStrategy",
              "toBeCanceled"
            ],
            "database_name": "db_e487",
            "fail_reason": ""
          },
          {
            "id": "10501cd3-0c19-498b-9ba4-8935ed447542",
            "name": "migrateLogicDb",
            "status": "Completed",
            "created_time": "2025-05-20T14:48:09+0000",
            "end_time": "2025-05-20T15:03:45+0000",
            "process": "",
            "instance_name": "UTS-ddm-dtc-src",
            "instance_id": "733c7e8d73a54c27b8308ec784a8be8cin09",
            "operations": [],
            "database_name": "db_e487",
            "fail_reason": ""
          },
          {
            "id": "57933931-9323-422d-8f3d-20a62eb00c4e",
            "name": "CreateInstance",
            "status": "Completed",
            "created_time": "2025-05-20T07:51:47+0000",
            "end_time": "2025-05-20T07:56:54+0000",
            "process": "",
            "instance_name": "UTS-ddm-dtc-src",
            "instance_id": "733c7e8d73a54c27b8308ec784a8be8cin09",
            "operations": [],
            "database_name": "",
            "fail_reason": ""
          }
        ],
        "offset": 0,
        "limit": 10,
        "total": 3
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
