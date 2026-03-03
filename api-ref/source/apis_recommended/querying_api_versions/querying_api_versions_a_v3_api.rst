:original_name: ddm_api_01_0108.html

.. _ddm_api_01_0108:

Querying API Versions (a V3 API)
================================

Function
--------

This API is used to query API versions.

Constraints
-----------

None

URI
---

-  URL format

GET /

-  Parameter description

   None

Request Parameters
------------------

None

Example Request
---------------

Querying API versions

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/

Response
--------

-  Normal response

.. table:: **Table 1** Response body parameters

   +-----------+---------------------------------------------------------------------------------+------------------------------------------+
   | Parameter | Type                                                                            | Description                              |
   +===========+=================================================================================+==========================================+
   | versions  | Array of :ref:`ApiVersion <ddm_api_01_0108__response_enginegroupsinfo>` objects | API version information including links. |
   +-----------+---------------------------------------------------------------------------------+------------------------------------------+

.. _ddm_api_01_0108__response_enginegroupsinfo:

.. table:: **Table 2** ApiVersion

   +-----------------------+-------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                    | Description                                                                                                                                                                      |
   +=======================+=========================================================================+==================================================================================================================================================================================+
   | id                    | String                                                                  | API version, for example, **v1** or **v3**.                                                                                                                                      |
   +-----------------------+-------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | links                 | Array of :ref:`LinkInfo <ddm_api_01_0108__table17903623103418>` objects | API link information. The value is empty when the version is **v1** or **v3**.                                                                                                   |
   +-----------------------+-------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status                | String                                                                  | Version status.                                                                                                                                                                  |
   |                       |                                                                         |                                                                                                                                                                                  |
   |                       |                                                                         | **CURRENT**: recommended version.                                                                                                                                                |
   |                       |                                                                         |                                                                                                                                                                                  |
   |                       |                                                                         | **SUPPORTED**: earlier version which is still supported.                                                                                                                         |
   |                       |                                                                         |                                                                                                                                                                                  |
   |                       |                                                                         | **DEPRECATED**: deprecated version which may be deleted later.                                                                                                                   |
   +-----------------------+-------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | version               | String                                                                  | If microversions are supported by APIs of the given version, the maximum microversion supported will be displayed. If microversions are not supported, this field will be empty. |
   +-----------------------+-------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | updated               | String                                                                  | Version update time. The format is yyyy-mm-dd Thh:mm:ssZ. **T** is the separator between the calendar and the hourly notation of time. **Z** indicates the UTC.                  |
   +-----------------------+-------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ddm_api_01_0108__table17903623103418:

.. table:: **Table 3** LinkInfo

   +-----------+--------+------------------------------------------------------------------+
   | Parameter | Type   | Description                                                      |
   +===========+========+==================================================================+
   | href      | String | URL of the API.                                                  |
   +-----------+--------+------------------------------------------------------------------+
   | rel       | String | Its value is **self**, indicating that **href** is a local link. |
   +-----------+--------+------------------------------------------------------------------+

-  Normal response example

.. code-block::

   {
     "versions": [
       {
         "id": "v3",
         "links": [],
         "status": "CURRENT",
         "updated": "2019-01-15T12:00:00Z",
         "version":""
       },
       {
         "id": "v1",
         "links": [],
         "status": "DEPRECATED",
         "updated": "2017-02-07T17:34:02Z",
         "version":""
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
