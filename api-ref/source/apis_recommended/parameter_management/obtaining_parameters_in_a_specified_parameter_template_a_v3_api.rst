:original_name: ddm_api_01_0106.html

.. _ddm_api_01_0106:

Obtaining Parameters in a Specified Parameter Template (a V3 API)
=================================================================

Function
--------

This API is used to obtain information about a specified parameter template.

Constraints
-----------

None

URI
---

-  URL format

GET /v3/{project_id}/configurations/{config_id}

-  Parameter description

.. table:: **Table 1** Path parameters

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                   |
   +=================+=================+=================+===============================================================================================+
   | project_id      | Yes             | String          | Project ID of a tenant in a region.                                                           |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------+
   | config_id       | Yes             | String          | Parameter template ID.                                                                        |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 | When this parameter is empty (not space), the URL of the parameter template list is obtained. |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Parameter description

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                  |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Example Request
---------------

Obtaining information about a specified parameter template

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/configurations/2aa71dc81e2c47699229b7aa26038f9dpr09

Response
--------

-  Normal response

.. table:: **Table 3** Response body parameters

   +--------------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                | Type                                                                                         | Description                                                                                                                                                                                 |
   +==========================+==============================================================================================+=============================================================================================================================================================================================+
   | id                       | String                                                                                       | Parameter template ID                                                                                                                                                                       |
   +--------------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | name                     | String                                                                                       | Parameter template name                                                                                                                                                                     |
   +--------------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | datastore_name           | String                                                                                       | Database name. The value is fixed at **ddm**.                                                                                                                                               |
   +--------------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description              | String                                                                                       | Parameter template description.                                                                                                                                                             |
   +--------------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | created                  | String                                                                                       | Creation time. The format is yyyy-MM-ddTHH:mm:ssZ.                                                                                                                                          |
   |                          |                                                                                              |                                                                                                                                                                                             |
   |                          |                                                                                              | **T** is the separator between the calendar and the hourly notation of time. **Z** indicates the time zone offset. For example, in the Central European time zone, the offset is **+0100**. |
   +--------------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | updated                  | String                                                                                       | Update time. The format is yyyy-MM-ddTHH:mm:ssZ.                                                                                                                                            |
   |                          |                                                                                              |                                                                                                                                                                                             |
   |                          |                                                                                              | **T** is the separator between the calendar and the hourly notation of time. **Z** indicates the time zone offset. For example, in the Central European time zone, the offset is **+0100**. |
   +--------------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | configuration_parameters | Array of :ref:`ConfigurationParameters <ddm_api_01_0106__response_enginegroupsinfo>` objects | Parameters defined by users based on a default parameter template                                                                                                                           |
   +--------------------------+----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ddm_api_01_0106__response_enginegroupsinfo:

.. table:: **Table 4** ConfigurationParameters

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                    |
   +=======================+=======================+================================================================================================+
   | name                  | String                | Parameter name                                                                                 |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------+
   | value                 | String                | Parameter value                                                                                |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------+
   | restart_required      | Boolean               | Whether a restart is required. The value can be:                                               |
   |                       |                       |                                                                                                |
   |                       |                       | -  **false**: indicates that a restart is not required.                                        |
   |                       |                       | -  **true**: indicates that a restart is required.                                             |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------+
   | readonly              | Boolean               | Whether the parameter is read-only. The value can be:                                          |
   |                       |                       |                                                                                                |
   |                       |                       | -  **false**: indicates that the parameter is not read-only.                                   |
   |                       |                       | -  **true**: indicates that the parameter is read-only.                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------+
   | value_range           | String                | Value range.                                                                                   |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------+
   | type                  | String                | Parameter type. The value can be **string**, **integer**, **boolean**, **list**, or **float**. |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------+
   | description           | String                | Parameter description                                                                          |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------+

-  Normal response example

.. code-block::

   {
     "id": "07fc12a8e0e94df7a3fcf53d0b5e1605pr01",
     "name": "default-ddm-test",
     "datastore_name": "ddm",
     "description": "Default parameter group for ddm-test",
     "created": "2020-05-05T04:40:51+0100",
     "updated": "2020-05-05T04:40:51+0100",
     "configuration_parameters": [
       {
         "name": "auto_increment_increment",
         "value": "1",
         "restart_required": false,
         "readonly": true,
         "value_range": "1-65535",
         "type": "integer",
         "description": "auto_increment_increment and auto_increment_offset are intended for use with master-to-master replication, and can be used to control the operation of AUTO_INCREMENT columns."
       },
       {
         "name": "autocommit",
         "value": "ON",
         "restart_required": false,
         "readonly": true,
         "value_range": "ON|OFF",
         "type": "boolean",
         "description": "The autocommit mode. If set to ON, all changes to a table take effect immediately. If set to OFF, you must use COMMIT to accept a transaction or ROLLBACK to cancel it. "
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
