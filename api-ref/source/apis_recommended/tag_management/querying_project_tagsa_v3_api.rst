:original_name: en-us_topic_0000002332869377.html

.. _en-us_topic_0000002332869377:

Querying Project Tags (a V3 API)
================================

Function
--------

This API is used to query project tags.

Constraints
-----------

None

URI
---

GET /v3/{project_id}/instances/tags

.. table:: **Table 1** Path parameters

   ========== ========= ====== ==================================
   Parameter  Mandatory Type   Description
   ========== ========= ====== ==================================
   project_id Yes       String Project ID of a tenant in a region
   ========== ========= ====== ==================================

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

Querying project tags

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/74f57817ca8f42e19318eb0e0ad41d18/instances/tags?limit=10&offset=0

Response
--------

-  Normal response

.. table:: **Table 4** Response body parameters

   +-------------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
   | Parameter   | Type                                                                                                                      | Description                                  |
   +=============+===========================================================================================================================+==============================================+
   | tags        | Array of :ref:`ProjectTag <en-us_topic_0000002332869377__en-us_topic_0000002285956790_response_enginegroupsinfo>` objects | Tag list                                     |
   +-------------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
   | offset      | Integer                                                                                                                   | Which page the server starts returning items |
   +-------------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
   | limit       | Integer                                                                                                                   | Number of records displayed on each page     |
   +-------------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
   | total_count | Integer                                                                                                                   | Total number of records                      |
   +-------------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+

.. _en-us_topic_0000002332869377__en-us_topic_0000002285956790_response_enginegroupsinfo:

.. table:: **Table 5** ProjectTag

   ========= ================ ===========
   Parameter Type             Description
   ========= ================ ===========
   key       String           Tag key
   values    Array of strings Tag values
   ========= ================ ===========

-  Normal response example

.. code-block::

   {
     "tags": [
       {
         "key": "11",
         "values": [
           "11"
         ]
       },
       {
         "key": "12",
         "values": [
           "12"
         ]
       }
     ],
     "offset": 0,
     "limit": 10,
     "total_count": 2
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
