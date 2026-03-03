:original_name: en-us_topic_0000002298790184.html

.. _en-us_topic_0000002298790184:

Querying Data Nodes Available for Creating a Schema (a V3 API)
==============================================================

Function
--------

This API is used to query data nodes that can be used for creating a schema.

Constraints
-----------

None

URI
---

GET /v3/{project_id}/instances/{instance_id}/available-data-nodes

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

Querying data nodes that can be used for creating a schema

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/74f57817ca8f42e19318eb0e0ad41d18/instances/2f0324a93859487eb5566d75951fcd2din09/available-data-nodes?offset=0&limit=10

Response
--------

-  Normal response

   .. table:: **Table 4** Response body parameters

      +------------+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | Parameter  | Type                                                                                                                                  | Description                                  |
      +============+=======================================================================================================================================+==============================================+
      | data_nodes | Array of :ref:`AvailableDnInstance <en-us_topic_0000002298790184__en-us_topic_0000002320635281_request_createdatabasedetail>` objects | Instance list                                |
      +------------+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | offset     | Integer                                                                                                                               | Which page the server starts returning items |
      +------------+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | limit      | Integer                                                                                                                               | Number of records displayed on each page     |
      +------------+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | total      | Integer                                                                                                                               | Total number of records                      |
      +------------+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+

   .. _en-us_topic_0000002298790184__en-us_topic_0000002320635281_request_createdatabasedetail:

   .. table:: **Table 5** AvailableDnInstance

      +----------------+---------+-------------------------------------------------------------------------------------------------------------+
      | Parameter      | Type    | Description                                                                                                 |
      +================+=========+=============================================================================================================+
      | id             | String  | Instance ID                                                                                                 |
      +----------------+---------+-------------------------------------------------------------------------------------------------------------+
      | name           | String  | Instance name                                                                                               |
      +----------------+---------+-------------------------------------------------------------------------------------------------------------+
      | status         | String  | Instance status. It can be obtained from :ref:`Data Node Statuses <ddm_api_01_0064__section9317162963412>`. |
      +----------------+---------+-------------------------------------------------------------------------------------------------------------+
      | engine_name    | String  | Engine name                                                                                                 |
      +----------------+---------+-------------------------------------------------------------------------------------------------------------+
      | engine_version | String  | Engine version                                                                                              |
      +----------------+---------+-------------------------------------------------------------------------------------------------------------+
      | private_ip     | String  | Private IP address of an instance                                                                           |
      +----------------+---------+-------------------------------------------------------------------------------------------------------------+
      | port           | Integer | Instance port                                                                                               |
      +----------------+---------+-------------------------------------------------------------------------------------------------------------+
      | time_zone      | String  | Time zone of an instance                                                                                    |
      +----------------+---------+-------------------------------------------------------------------------------------------------------------+

-  Normal response example

   .. code-block::

      {
        "data_nodes": [
          {
            "id": "7edae0250ebc464897bd92b8d3e8b769in01",
            "status": "normal",
            "name": "UTS-rds-dtc-src",
            "engine_name": "mysql",
            "engine_version": "8.0",
            "private_ip": "172.16.223.151",
            "port": 3306,
            "time_zone": "UTC+08:00"
          }
        ],
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
