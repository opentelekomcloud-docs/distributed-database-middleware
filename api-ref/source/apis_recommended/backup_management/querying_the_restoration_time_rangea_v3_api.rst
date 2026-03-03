:original_name: en-us_topic_0000002298790224.html

.. _en-us_topic_0000002298790224:

Querying the Restoration Time Range (a V3 API)
==============================================

Function
--------

This API is used to query the restoration time range of an instance.

The intersection between the restoration time range of an instance and those of all data nodes associated with the instance is used.

Constraints
-----------

None

URI
---

GET /v3/{project_id}/instances/{instance_id}/backups/restorable-time-interval

.. table:: **Table 1** Path parameters

   =========== ====== ========= ==================================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ==================================
   project_id  String Yes       Project ID of a tenant in a region
   instance_id String Yes       Instance ID
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

.. table:: **Table 3** Query parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                            |
   +=================+=================+=================+========================================================================================================+
   | offset          | No              | Integer         | Index offset.                                                                                          |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The query starts from the next piece of data indexed by this parameter. The value is **0** by default. |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The value must be a number but cannot be a negative number.                                            |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | limit           | No              | Integer         | Maximum records to be queried.                                                                         |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | Value range: **1** to **128**                                                                          |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | If the parameter value is not specified, 10 records are queried by default.                            |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+

Example Request
---------------

Querying the restoration time range

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/backups/restorable-time-interval

Response
--------

-  Normal response

   .. table:: **Table 4** Response body parameters

      +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | Parameter                 | Type                                                                                                                                  | Description                                  |
      +===========================+=======================================================================================================================================+==============================================+
      | restorable_time_intervals | Array of :ref:`RestoreTimeInterval <en-us_topic_0000002298790224__en-us_topic_0000002285479838_request_createdatabasedetail>` objects | Time ranges                                  |
      +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | offset                    | Integer                                                                                                                               | Which page the server starts returning items |
      +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | limit                     | Integer                                                                                                                               | Number of records displayed on each page     |
      +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | total                     | Integer                                                                                                                               | Total number of records                      |
      +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+

   .. _en-us_topic_0000002298790224__en-us_topic_0000002285479838_request_createdatabasedetail:

   .. table:: **Table 5** RestoreTimeInterval

      +------------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter  | Type   | Description                                                                                                                                                                                                                                                                                                            |
      +============+========+========================================================================================================================================================================================================================================================================================================================+
      | start_time | String | Start time in UTC, accurate to milliseconds. The format is *yyyy*\ **-**\ *mm*\ **-**\ *ddThh*\ **:**\ *mm*\ **:**\ *ssZ*. **T** is the separator between the calendar and the hourly notation of time. **Z** indicates the time zone offset. For example, in the Central European time zone, the offset is **+0100**. |
      +------------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | end_time   | String | End time in UTC, accurate to milliseconds. The format is *yyyy*\ **-**\ *mm*\ **-**\ *ddThh*\ **:**\ *mm*\ **:**\ *ssZ*. **T** is the separator between the calendar and the hourly notation of time. **Z** indicates the time zone offset. For example, in the Central European time zone, the offset is **+0100**.   |
      +------------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Normal response example

   .. code-block::

      {
          "restorable_time_intervals": [{
              "start_time": "2025-05-20T09:40:40+0000",
              "end_time": "2025-05-21T11:15:43+0000"
          }],
          "offset": 0,
          "limit": 10,
          "total": 1
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
