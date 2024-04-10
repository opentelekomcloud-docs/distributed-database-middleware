:original_name: ddm_api_01_0084.html

.. _ddm_api_01_0084:

Querying Parameters of a Specified DDM Instance
===============================================

Function
--------

This API is used to query parameters of a specified DDM instance.

Constraints
-----------

None

URI
---

GET /v3/{project_id}/instances/{instance_id}/configurations?offset={offset}&limit={limit}

.. table:: **Table 1** Path parameters

   =========== ========= ====== ==================================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ==================================
   project_id  Yes       String Project ID of a tenant in a region
   instance_id Yes       String DDM instance ID
   =========== ========= ====== ==================================

.. table:: **Table 2** Query parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                            |
   +=================+=================+=================+========================================================================================================+
   | offset          | No              | Integer         | Index offset.                                                                                          |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The query starts from the next piece of data indexed by this parameter. The value is **0** by default. |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The value must be a positive integer.                                                                  |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | limit           | No              | Integer         | A maximum of parameters to be queried.                                                                 |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | Value range: 1 to 128.                                                                                 |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | If the parameter value is not specified, 10 parameters are queried by default.                         |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 3** Request header parameters

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                          |
   +=================+=================+=================+======================================================================================================================+
   | X-Language      | No              | String          | Language.                                                                                                            |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+
   | X-Auth-Token    | Yes             | String          | User token.                                                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | It can be obtained by calling an IAM API. The value of **X-Subject-Token** in the response header is the user token. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +-------------------------+-----------------------------------------------------------------------------------------------------------+----------------------------------------------------+
   | Parameter               | Type                                                                                                      | Description                                        |
   +=========================+===========================================================================================================+====================================================+
   | updated                 | String                                                                                                    | Time when DDM instance parameters are last updated |
   +-------------------------+-----------------------------------------------------------------------------------------------------------+----------------------------------------------------+
   | configuration_parameter | Array of :ref:`ConfigurationParameterList <ddm_api_01_0084__response_configurationparameterlist>` objects | Information about DDM instance parameters          |
   +-------------------------+-----------------------------------------------------------------------------------------------------------+----------------------------------------------------+
   | offset                  | Integer                                                                                                   | Which page the server starts returning items       |
   +-------------------------+-----------------------------------------------------------------------------------------------------------+----------------------------------------------------+
   | limit                   | Integer                                                                                                   | Number of records displayed on each page           |
   +-------------------------+-----------------------------------------------------------------------------------------------------------+----------------------------------------------------+
   | total                   | Integer                                                                                                   | Total collections                                  |
   +-------------------------+-----------------------------------------------------------------------------------------------------------+----------------------------------------------------+

.. _ddm_api_01_0084__response_configurationparameterlist:

.. table:: **Table 5** ConfigurationParameterList

   ============ ====== ==========================================
   Parameter    Type   Description
   ============ ====== ==========================================
   name         String Parameter name
   value        String Parameter value
   need_restart String Whether the instance needs to be restarted
   read_only    String Whether the parameter is read-only
   value_range  String Parameter value range
   data_type    String Parameter type
   description  String Parameter description
   ============ ====== ==========================================

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

   GET https://{endpoint}/v3/{project_id}/instances/{instance_id}/configurations

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "updated" : "2021-11-09 03:26:52",
     "configuration_parameter" : [ {
       "name" : "temp_table_size_limit",
       "value" : "1000000",
       "need_restart" : "0",
       "read_only" : "0",
       "value_range" : "500000-2000000000",
       "data_type" : "integer",
       "description" : "Maximum size of the temporary table."
     } ],
     "offset" : 0,
     "limit" : 128,
     "total" : 22
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
