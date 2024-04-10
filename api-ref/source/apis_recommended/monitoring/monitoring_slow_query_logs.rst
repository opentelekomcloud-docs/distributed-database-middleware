:original_name: ddm_api_01_0090.html

.. _ddm_api_01_0090:

Monitoring Slow Query Logs
==========================

Function
--------

This API is used to query the SQL statements that take a long time to execute on the DDM instance within a specified time range.

Constraints
-----------

None

URI
---

GET /v2/{project_id}/instances/{instance_id}/slowlog?curPage={curPage}&perPage={perPage}&startDate={startDate}&endDate={endDate}

.. table:: **Table 1** Path parameters

   =========== ========= ====== ===============
   Parameter   Mandatory Type   Description
   =========== ========= ====== ===============
   project_id  Yes       String Project ID
   instance_id Yes       String DDM instance ID
   =========== ========= ====== ===============

.. table:: **Table 2** Query parameters

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                              |
   +=================+=================+=================+==========================================================================================+
   | curPage         | Yes             | String          | Which page the server starts returning items. The start value cannot be less than **1**. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------+
   | perPage         | Yes             | String          | Number of records displayed on each page                                                 |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------+
   | startDate       | Yes             | String          | Start time. The format is UNIX timestamp, in milliseconds.                               |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------+
   | endDate         | Yes             | String          | End time. The format is UNIX timestamp, in milliseconds.                                 |
   |                 |                 |                 |                                                                                          |
   |                 |                 |                 | The interval between the start time and the end time must be no more than 7 days.        |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------+

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

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +-------------+-----------------------------------------------------------------------------+-----------------------------------+
   | Parameter   | Type                                                                        | Description                       |
   +=============+=============================================================================+===================================+
   | totalRecord | Integer                                                                     | Number of slow query logs         |
   +-------------+-----------------------------------------------------------------------------+-----------------------------------+
   | slowLogList | Array of :ref:`SlowLogList <ddm_api_01_0090__response_slowloglist>` objects | Information about slow query logs |
   +-------------+-----------------------------------------------------------------------------+-----------------------------------+

.. _ddm_api_01_0090__response_slowloglist:

.. table:: **Table 5** SlowLogList

   +--------------+--------+---------------------------------------------------------------------------------------------------------------+
   | Parameter    | Type   | Description                                                                                                   |
   +==============+========+===============================================================================================================+
   | users        | String | Username of the DDM account for executing the slow SQL statement                                              |
   +--------------+--------+---------------------------------------------------------------------------------------------------------------+
   | database     | String | Name of the schema where the slow SQL statement is executed                                                   |
   +--------------+--------+---------------------------------------------------------------------------------------------------------------+
   | querySample  | String | Syntax for executing the slow SQL statement                                                                   |
   +--------------+--------+---------------------------------------------------------------------------------------------------------------+
   | logTime      | String | Time when the slow SQL statement starts to be executed                                                        |
   +--------------+--------+---------------------------------------------------------------------------------------------------------------+
   | time         | String | Time for a SQL statement to execute, accurate to milliseconds                                                 |
   +--------------+--------+---------------------------------------------------------------------------------------------------------------+
   | shards       | String | Name of the physical shard                                                                                    |
   +--------------+--------+---------------------------------------------------------------------------------------------------------------+
   | rowsExamined | String | Number of rows affected by the SQL statements that take a long time to execute                                |
   +--------------+--------+---------------------------------------------------------------------------------------------------------------+
   | host         | String | Client IP address. This IP address may involve personal data. Anonymizing the IP address data is recommended. |
   +--------------+--------+---------------------------------------------------------------------------------------------------------------+
   | ddmNodeId    | String | ID of the DDM node for executing the slow SQL statement                                                       |
   +--------------+--------+---------------------------------------------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 6** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

**Status code: 500**

.. table:: **Table 7** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

Example Request
---------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/instances/{instance_id}/slowlog?curPage={curPage}&perPage={perPage}&startDate={startDate}&endDate={endDate}

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "totalRecord" : 2,
     "slowLogList" : [ {
       "users" : "testddm",
       "database" : "test1",
       "querySample" : "select id, sleep(3) from test",
       "logTime" : "2021-04-26T02:40:21",
       "time" : "12002",
       "shards" : "test1_0000",
       "rowsExamined" : "4",
       "host" : "192.168.16.18",
       "ddmNodeId":"47667f9ed2a54af7ba9ca46d8d37c26f****"
     } ]
   }

**Status code: 400**

bad request

.. code-block::

   {
     "externalMessage" : "Parameter error.",
     "errCode" : "DBS.280001"
   }

**Status code: 500**

server error

.. code-block::

   {
     "externalMessage" : "Server failure.",
     "errCode" : "DBS.200412"
   }

Status Codes
------------

=========== ============
Status Code Description
=========== ============
200         OK
400         bad request
500         server error
=========== ============

Error Codes
-----------

For details, see :ref:`Error Codes <ddm_api_01_0061>`.
