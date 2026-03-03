:original_name: ddm_api_01_0109.html

.. _ddm_api_01_0109:

Querying DDM Engine Information (a V3 API)
==========================================

Function
--------

This V3 API is used to query information about DDM engine.

Constraints
-----------

None

URI
---

-  URL format

GET /v3/{project_id}/engines?offset={offset}&limit={limit}

-  Parameter description

.. table:: **Table 1** Path parameters

   ========== ========= ====== ===================================
   Parameter  Mandatory Type   Description
   ========== ========= ====== ===================================
   project_id Yes       String Project ID of a tenant in a region.
   ========== ========= ====== ===================================

.. table:: **Table 2** Query parameters

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
   |                 |                 |                 | If the parameter value is not specified, 10 records are obtained by default.                           |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 3** Request header parameters

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                  |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Example Request
---------------

Querying DDM engine information

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/engines?offset=0&limit=10

Response
--------

-  Normal response

.. table:: **Table 4** Response body parameters

   +---------------+--------------------------------------------------------------------------------------+----------------------------------------------+
   | Parameter     | Type                                                                                 | Description                                  |
   +===============+======================================================================================+==============================================+
   | engine_groups | Array of :ref:`EngineGroupInfo <ddm_api_01_0109__response_enginegroupsinfo>` objects | Information of available engines             |
   +---------------+--------------------------------------------------------------------------------------+----------------------------------------------+
   | offset        | Integer                                                                              | Which page the server starts returning items |
   +---------------+--------------------------------------------------------------------------------------+----------------------------------------------+
   | limit         | Integer                                                                              | Number of records displayed on each page     |
   +---------------+--------------------------------------------------------------------------------------+----------------------------------------------+
   | total         | Integer                                                                              | Number of engine versions                    |
   +---------------+--------------------------------------------------------------------------------------+----------------------------------------------+

.. _ddm_api_01_0109__response_enginegroupsinfo:

.. table:: **Table 5** EngineGroupInfo

   ========= ====== ==============
   Parameter Type   Description
   ========= ====== ==============
   id        String Engine ID
   name      String Engine name
   version   String Engine version
   ========= ====== ==============

-  Normal response example

.. code-block::

   {
     "engine_groups": [
       {
         "id": "036dc44a-b560-4316-9e7f-e25a60f2aea2",
         "name": "ddm",
         "version": "3.1.0.8"
       }
     ],
     "offset": 0,
     "limit": 1,
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
