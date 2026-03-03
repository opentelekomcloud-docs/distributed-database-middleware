:original_name: ddm_api_01_0105_0.html

.. _ddm_api_01_0105_0:

Obtaining Parameter Templates (a V3 API)
========================================

Function
--------

This API is used to obtain parameter templates, including all default and custom parameter templates.

Constraints
-----------

None

URI
---

-  URL format

GET /v3/{project_id}/configurations?offset={offset}&limit={limit}

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
   |                 |                 |                 | Value range: 1 to 128.                                                                                 |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | If the parameter value is not specified, 10 records are obtained by default.                           |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 3** Parameter description

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                  |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Example Request
---------------

Obtaining parameter templates

.. code-block:: text

   GET https:/ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/configurations?offset=0&limit=10

Response
--------

-  Normal response

.. table:: **Table 4** Response body parameters

   +----------------+------------------------------------------------------------------------------------------+----------------------------------------------+
   | Parameter      | Type                                                                                     | Description                                  |
   +================+==========================================================================================+==============================================+
   | configurations | Array of :ref:`ConfigurationInfo <ddm_api_01_0105_0__response_enginegroupsinfo>` objects | Information of available engines             |
   +----------------+------------------------------------------------------------------------------------------+----------------------------------------------+
   | offset         | Integer                                                                                  | Which page the server starts returning items |
   +----------------+------------------------------------------------------------------------------------------+----------------------------------------------+
   | limit          | Integer                                                                                  | Number of records displayed on each page     |
   +----------------+------------------------------------------------------------------------------------------+----------------------------------------------+
   | total          | Integer                                                                                  | Number of engine versions                    |
   +----------------+------------------------------------------------------------------------------------------+----------------------------------------------+

.. _ddm_api_01_0105_0__response_enginegroupsinfo:

.. table:: **Table 5** ConfigurationInfo

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                 |
   +=======================+=======================+=============================================================================================================================================================================================+
   | id                    | String                | Parameter template ID                                                                                                                                                                       |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | name                  | String                | Parameter template name                                                                                                                                                                     |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description           | String                | Parameter template description                                                                                                                                                              |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | datastore_name        | String                | Database type. The value is fixed at **ddm**.                                                                                                                                               |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | created               | String                | Creation time. The format is yyyy-MM-ddTHH:mm:ssZ.                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                             |
   |                       |                       | **T** is the separator between the calendar and the hourly notation of time. **Z** indicates the time zone offset. For example, in the Central European time zone, the offset is **+0100**. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | updated               | String                | Update time. The format is yyyy-MM-ddTHH:mm:ssZ.                                                                                                                                            |
   |                       |                       |                                                                                                                                                                                             |
   |                       |                       | **T** is the separator between the calendar and the hourly notation of time. **Z** indicates the time zone offset. For example, in the Central European time zone, the offset is **+0100**. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | user_defined          | Boolean               | Whether the parameter template is a custom template. The value can be:                                                                                                                      |
   |                       |                       |                                                                                                                                                                                             |
   |                       |                       | **false**: The parameter template is a default template.                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                             |
   |                       |                       | **true**: The parameter template is a custom template.                                                                                                                                      |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Normal response example

.. code-block::

   {
     "configurations": [
       {
         "id": "2aa71dc81e2c47699229b7aa26038f9dpr09",
         "name": "ddm-param1724812533",
         "description": "",
         "datastore_name": "ddm",
         "created": "2021-12-14T07:46:22+0100",
         "updated": "2021-12-14T07:46:22+0100",
         "user_defined": false
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
