:original_name: ddm_api_01_0117.html

.. _ddm_api_01_0117:

Monitoring Slow Query Logs (a V3 API)
=====================================

Function
--------

This API is used to query the SQL statements that take a long time to execute on the DDM instance within a specified time range.

Constraints
-----------

None

URI
---

-  URL format

GET /v3/{project_id}/instances/{instance_id}/slow-logs?offset={offset}&limit={limit}&start_date={start_date}&end_date={end_date}

-  Parameter description

.. table:: **Table 1** Path parameters

   =========== ========= ====== ================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ================
   project_id  Yes       String Project ID.
   instance_id Yes       String DDM instance ID.
   =========== ========= ====== ================

.. table:: **Table 2** Query parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                            |
   +=================+=================+=================+========================================================================================================+
   | offset          | No              | String          | Index offset.                                                                                          |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The query starts from the next piece of data indexed by this parameter. The value is **0** by default. |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The value must be a number but cannot be a negative number.                                            |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | limit           | No              | String          | Maximum records to be queried.                                                                         |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The value ranges from 1 to 100.                                                                        |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | If the parameter value is not specified, 10 records are obtained by default.                           |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | start_date      | Yes             | String          | Start time. The format is UNIX timestamp, in milliseconds.                                             |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | end_date        | Yes             | String          | End time. The format is UNIX timestamp, in milliseconds.                                               |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The interval between the start time and the end time must be no more than 7 days.                      |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 3** Request header parameters

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                          |
   +=================+=================+=================+======================================================================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | It can be obtained by calling an IAM API. The value of **X-Subject-Token** in the response header is the user token. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

Querying slow query logs on the DDM instance within a specified time range

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/slow-logs?offset=0&limit=10&start_date=1729872000000&end_date=1729927839000

Response
--------

-  Normal response

.. table:: **Table 4** Response body parameters

   +---------------+-------------------------------------------------------------------------------+-----------------------------------+
   | Parameter     | Type                                                                          | Description                       |
   +===============+===============================================================================+===================================+
   | total_record  | Integer                                                                       | Number of slow query logs         |
   +---------------+-------------------------------------------------------------------------------+-----------------------------------+
   | slow_log_list | Array of :ref:`SlowLogs <ddm_api_01_0117__response_enginegroupsinfo>` objects | Information about slow query logs |
   +---------------+-------------------------------------------------------------------------------+-----------------------------------+

.. _ddm_api_01_0117__response_enginegroupsinfo:

.. table:: **Table 5** SlowLogs

   +---------------+--------+---------------------------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                                                   |
   +===============+========+===============================================================================================================+
   | users         | String | Username of the DDM account for executing the slow SQL statement                                              |
   +---------------+--------+---------------------------------------------------------------------------------------------------------------+
   | database      | String | Name of the schema where the slow SQL statement is executed                                                   |
   +---------------+--------+---------------------------------------------------------------------------------------------------------------+
   | query_sample  | String | Syntax for executing the slow SQL statement                                                                   |
   +---------------+--------+---------------------------------------------------------------------------------------------------------------+
   | log_time      | String | Time when the slow SQL statement starts to be executed. The format is **yyyy-mm-ddThh:mm:ssZ**.               |
   +---------------+--------+---------------------------------------------------------------------------------------------------------------+
   | time          | String | Time for a SQL statement to execute, accurate to milliseconds                                                 |
   +---------------+--------+---------------------------------------------------------------------------------------------------------------+
   | shards        | String | Names of physical shards in the schema                                                                        |
   +---------------+--------+---------------------------------------------------------------------------------------------------------------+
   | node_id       | String | Node ID                                                                                                       |
   +---------------+--------+---------------------------------------------------------------------------------------------------------------+
   | rows_examined | String | Number of rows affected by the SQL statements that take a long time to execute                                |
   +---------------+--------+---------------------------------------------------------------------------------------------------------------+
   | host          | String | Client IP address. This IP address may involve personal data. Anonymizing the IP address data is recommended. |
   +---------------+--------+---------------------------------------------------------------------------------------------------------------+

-  Normal response example

.. code-block::

   {
       "total_record": 1,
       "slow_log_list": [
           {
               "users": "testddm",
               "database": "test1",
               "query_sample": "select id, sleep(3) from test",
               "log_time": "2024-10-26T07:30:00",
               "shards": "",
               "rows_examined": "1",
               "node_id": "xxxxx2f8f44546f493d084d0c6b94ecfno09",
               "host": "192.168.x.x",
               "time": "3002"
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
