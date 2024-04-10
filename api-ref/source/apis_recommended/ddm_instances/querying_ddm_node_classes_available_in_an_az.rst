:original_name: ddm_api_01_0016.html

.. _ddm_api_01_0016:

Querying DDM Node Classes Available in an AZ
============================================

Function
--------

This API is used to query DDM node classes available in an AZ.

Constraints
-----------

None

URI
---

GET /v2/{project_id}/flavors?engine_id={engine_id}?offset={offset}&limit={limit}

.. table:: **Table 1** Path parameters

   ========== ========= ====== ==================================
   Parameter  Mandatory Type   Description
   ========== ========= ====== ==================================
   project_id Yes       String Project ID of a tenant in a region
   ========== ========= ====== ==================================

.. table:: **Table 2** Query parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                            |
   +=================+=================+=================+========================================================================================================+
   | engine_id       | Yes             | String          | Engine ID, which can be obtained by calling the API for querying DDM engine information.               |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | offset          | No              | Integer         | Index offset.                                                                                          |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The query starts from the next piece of data indexed by this parameter. The value is **0** by default. |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The value must be a positive integer.                                                                  |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | limit           | No              | Integer         | A maximum of node classes to be queried.                                                               |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | Value range: 1 to 128.                                                                                 |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | If the parameter value is not specified, 10 node classes are queried by default.                       |
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

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +---------------------+-----------------------------------------------------------------------------------------------------+----------------------------+
   | Parameter           | Type                                                                                                | Description                |
   +=====================+=====================================================================================================+============================+
   | computeFlavorGroups | Array of :ref:`ComputeFlavorGroupsInfo <ddm_api_01_0016__response_computeflavorgroupsinfo>` objects | Compute flavor information |
   +---------------------+-----------------------------------------------------------------------------------------------------+----------------------------+

.. _ddm_api_01_0016__response_computeflavorgroupsinfo:

.. table:: **Table 5** ComputeFlavorGroupsInfo

   +----------------+-----------------------------------------------------------------------------------+--------------------------------------------------------------------------+
   | Parameter      | Type                                                                              | Description                                                              |
   +================+===================================================================================+==========================================================================+
   | groupType      | String                                                                            | Compute resource architecture type. The value can be **x86** or **ARM**. |
   +----------------+-----------------------------------------------------------------------------------+--------------------------------------------------------------------------+
   | computeFlavors | Array of :ref:`ComputeFlavors <ddm_api_01_0016__response_computeflavors>` objects | Compute flavors                                                          |
   +----------------+-----------------------------------------------------------------------------------+--------------------------------------------------------------------------+
   | offset         | Integer                                                                           | Which page the server starts returning items                             |
   +----------------+-----------------------------------------------------------------------------------+--------------------------------------------------------------------------+
   | limit          | Integer                                                                           | Number of records displayed on each page                                 |
   +----------------+-----------------------------------------------------------------------------------+--------------------------------------------------------------------------+
   | total          | Integer                                                                           | Total number of compute flavors                                          |
   +----------------+-----------------------------------------------------------------------------------+--------------------------------------------------------------------------+

.. _ddm_api_01_0016__response_computeflavors:

.. table:: **Table 6** ComputeFlavors

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                               |
   +=======================+=======================+===========================================================================================================================+
   | id                    | String                | Flavor ID                                                                                                                 |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | typeCode              | String                | Resource type code                                                                                                        |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | code                  | String                | VM flavor types recorded in DDM                                                                                           |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | iaasCode              | String                | VM flavor types recorded by the IaaS layer                                                                                |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | cpu                   | String                | Number of CPUs                                                                                                            |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | mem                   | String                | Memory size, in GB                                                                                                        |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | maxConnections        | String                | Maximum number of connections                                                                                             |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | serverType            | String                | Compute resource type                                                                                                     |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | architecture          | String                | Compute resource architecture type. The value can be **x86** or **ARM**.                                                  |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | azStatus              | Map<String,String>    | Status of the AZ where node classes are available. The key is the AZ ID and the value is the AZ status. The value can be: |
   |                       |                       |                                                                                                                           |
   |                       |                       | -  **normal**: indicates that the node classes in the AZ are available.                                                   |
   |                       |                       | -  **unsupported**: indicates that the node classes are not supported by the AZ.                                          |
   |                       |                       | -  **sellout**: indicates that the node classes in the AZ are sold out.                                                   |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | regionStatus          | String                | Region status                                                                                                             |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | groupType             | String                | Compute resource architecture type. The value can be **x86** or **ARM**.                                                  |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | dbType                | String                | Engine type                                                                                                               |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+
   | extendFields          | Map<String,String>    | Extension field for storing AZ information                                                                                |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 7** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

**Status code: 500**

.. table:: **Table 8** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

Example Request
---------------

.. code-block:: text

   GET https://{endpoint}/v2/{project_id}/flavors?engine_id={engine_id}

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
       "computeFlavorGroups": [{
           "offset": 0,
           "limit": 100,
           "total": 3,
           "groupType": "X86",
           "computeFlavors": [{
                   "id": "7267235a-80b0-3fd4-892f-4f3dd0cd60e4",
                   "typeCode": "hws.resource.type.ddm",
                   "code": "ddm.2xlarge.2",
                   "iaasCode": "s2.xlarge.2",
                   "cpu": "8",
                   "mem": "16",
                   "maxConnections": null,
                   "serverType": "KVM",
                   "architecture": "X86",
                   "azStatus": {
                       "eu-de-03": "unsupported",
                       "eu-de-02": "normal",
                       "eu-de-01": "normal"
                   },
                   "regionStatus": "abandon",
                   "groupType": null,
                   "dbType": "DDM",
                   "extendFields": {
                       "azCode": "eu-de-03,eu-de-02,eu-de-01",
                       "azDescription": "eu-de-03,eu-de-02,eu-de-01"
                   }
               },
               {
                   "id": "8cfd2730-1d53-3349-acbb-12a741767f70",
                   "typeCode": "hws.resource.type.ddm",
                   "code": "ddm.4xlarge.2",
                   "iaasCode": "s2.xlarge.2",
                   "cpu": "16",
                   "mem": "32",
                   "maxConnections": null,
                   "serverType": "KVM",
                   "architecture": "X86",
                   "azStatus": {
                       "eu-de-03": "unsupported",
                       "eu-de-02": "normal",
                       "eu-de-01": "normal"
                   },
                   "regionStatus": "abandon",
                   "groupType": null,
                   "dbType": "DDM",
                   "extendFields": {
                       "azCode": "eu-de-03,eu-de-02,eu-de-01,",
                       "azDescription": "eu-de-03,eu-de-02,eu-de-01"
                   }
               },
               {
                   "id": "f8388a59-b2af-3be0-8fe5-7422755d4570",
                   "typeCode": "hws.resource.type.ddm",
                   "code": "ddm.8xlarge.2",
                   "iaasCode": "s2.xlarge.2",
                   "cpu": "32",
                   "mem": "64",
                   "maxConnections": null,
                   "serverType": "KVM",
                   "architecture": "X86",
                   "azStatus": {
                       "eu-de-03": "unsupported",
                       "eu-de-02": "normal",
                       "eu-de-01": "normal"
                   },
                   "regionStatus": "abandon",
                   "groupType": null,
                   "dbType": "DDM",
                   "extendFields": {
                       "azCode": "eu-de-03,eu-de-02,eu-de-01",
                       "azDescription": "eu-de-03,eu-de-02,eu-de-01"
                   }
               }
           ]
       }]
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
