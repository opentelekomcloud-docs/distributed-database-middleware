:original_name: ddm_api_01_0110.html

.. _ddm_api_01_0110:

Querying DDM Node Classes Available in Each AZ (a V3 API)
=========================================================

Function
--------

This V3 API is used to query DDM node classes available in an AZ.

Constraints
-----------

None

URI
---

-  URL format

GET /v3/{project_id}/flavors?engine_id={engine_id}&offset={offset}&limit={limit}&engine_version={engine_version}&available_zones={available_zones}

-  Parameter description

.. table:: **Table 1** Path parameters

   ========== ========= ====== ===================================
   Parameter  Mandatory Type   Description
   ========== ========= ====== ===================================
   project_id Yes       String Project ID of a tenant in a region.
   ========== ========= ====== ===================================

.. table:: **Table 2** Query parameters

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                   |
   +=================+=================+=================+===============================================================================================================================================================================================================+
   | engine_id       | No              | String          | Engine ID, which can be obtained by calling the API for querying DDM engine information. At least one of **engine_id** and **engine_version** must be specified.                                              |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | engine_version  | No              | String          | Engine version, which can be obtained by calling the API for querying DDM engine information. At least one of **engine_id** and **engine_version** must be specified.                                         |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | available_zones | No              | String          | AZs. Use commas (,) to separate multiple AZs, for example, **eu-de-01,eu-de-02**. The value cannot be empty. For details, see `Regions and Endpoints <https://docs.otc.t-systems.com/endpoint/index.html>`__. |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | offset          | No              | Integer         | Index offset.                                                                                                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                                               |
   |                 |                 |                 | The query starts from the next piece of data indexed by this parameter. The value is **0** by default.                                                                                                        |
   |                 |                 |                 |                                                                                                                                                                                                               |
   |                 |                 |                 | The value must be a number but cannot be a negative number.                                                                                                                                                   |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | limit           | No              | Integer         | Maximum records to be queried.                                                                                                                                                                                |
   |                 |                 |                 |                                                                                                                                                                                                               |
   |                 |                 |                 | Value range: **1** to **128**                                                                                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                                               |
   |                 |                 |                 | If the parameter value is not specified, 10 records are obtained by default.                                                                                                                                  |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

Querying DDM node classes available in an AZ

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/flavors?engine_id=xxxxxx-xxxx-xxxx-f7ab-100f2cd33008&engine_version=3.x.x.x&available_zones=eu-de-01,eu-de-02&offset=0&limit=10

Response
--------

-  Normal response

.. table:: **Table 4** Response body parameters

   +---------------+--------------------------------------------------------------------------------------+-----------------------+
   | Parameter     | Type                                                                                 | Description           |
   +===============+======================================================================================+=======================+
   | flavor_groups | Array of :ref:`FlavorGroupInfo <ddm_api_01_0110__response_enginegroupsinfo>` objects | List of node classes. |
   +---------------+--------------------------------------------------------------------------------------+-----------------------+

.. _ddm_api_01_0110__response_enginegroupsinfo:

.. table:: **Table 5** FlavorGroupInfo

   +------------+---------------------------------------------------------------------+--------------------------------------------------------------------------+
   | Parameter  | Type                                                                | Description                                                              |
   +============+=====================================================================+==========================================================================+
   | flavors    | Array of :ref:`Flavor <ddm_api_01_0110__table325112318591>` objects | Node class information.                                                  |
   +------------+---------------------------------------------------------------------+--------------------------------------------------------------------------+
   | group_type | String                                                              | Compute resource architecture type. The value can be **X86** or **ARM**. |
   +------------+---------------------------------------------------------------------+--------------------------------------------------------------------------+
   | offset     | Integer                                                             | Which page the server starts returning items                             |
   +------------+---------------------------------------------------------------------+--------------------------------------------------------------------------+
   | limit      | Integer                                                             | Number of records displayed on each page                                 |
   +------------+---------------------------------------------------------------------+--------------------------------------------------------------------------+
   | total      | Integer                                                             | Number of engine versions                                                |
   +------------+---------------------------------------------------------------------+--------------------------------------------------------------------------+

.. _ddm_api_01_0110__table325112318591:

.. table:: **Table 6** Flavor

   +-----------+-----------------------------------------------------------------------------+-----------------------------------------------------------------+
   | Parameter | Type                                                                        | Description                                                     |
   +===========+=============================================================================+=================================================================+
   | az_infos  | Array of :ref:`AvailableZone <ddm_api_01_0110__table1948114211710>` objects | AZ information. The value can be:                               |
   +-----------+-----------------------------------------------------------------------------+-----------------------------------------------------------------+
   | id        | String                                                                      | Node class ID.                                                  |
   +-----------+-----------------------------------------------------------------------------+-----------------------------------------------------------------+
   | spec_code | String                                                                      | Resource specification code.                                    |
   +-----------+-----------------------------------------------------------------------------+-----------------------------------------------------------------+
   | vcpus     | String                                                                      | Number of vCPUs. For example, the value **1** indicates 1 vCPU. |
   +-----------+-----------------------------------------------------------------------------+-----------------------------------------------------------------+
   | ram       | String                                                                      | Memory size in GB.                                              |
   +-----------+-----------------------------------------------------------------------------+-----------------------------------------------------------------+

.. _ddm_api_01_0110__table1948114211710:

.. table:: **Table 7** AvailableZone

   +--------------+---------+------------------------------------------------------------------------------------------------+
   | Parameter    | Type    | Description                                                                                    |
   +==============+=========+================================================================================================+
   | code         | String  | AZ code.                                                                                       |
   +--------------+---------+------------------------------------------------------------------------------------------------+
   | description  | String  | AZ description.                                                                                |
   +--------------+---------+------------------------------------------------------------------------------------------------+
   | status       | String  | AZ status. It can be obtained from :ref:`AZ Statuses <ddm_api_01_0064__section7167152035513>`. |
   +--------------+---------+------------------------------------------------------------------------------------------------+
   | support_ipv6 | Boolean | Whether IPv6 is supported.                                                                     |
   +--------------+---------+------------------------------------------------------------------------------------------------+

-  Normal response example

.. code-block::

   {
     "flavor_groups": [
       {
         "offset": 0,
         "limit": 1,
         "total": 4,
         "group_type": "X86",
         "flavors": [
           {
             "id": "xxxxx-xxxx-xxxx-xxxx-xxxxxxxx",
             "spec_code": "ddm.c6.xlarge.2",
             "vcpus": "4",
             "ram": "8",
             "az_infos": [
               {
                 "code": "eu-de-01",
                 "status": "normal",
                 "description": "eu-de-01",
                 "support_ipv6": true
               }
             ]
           }
         ]
       },
       {
         "offset": 0,
         "limit": 1,
         "total": 5,
         "group_type": "ARM",
         "flavors": [
           {
             "id": "xxxxx-xxxx-xxxx-xxxx-xxxxxxxx",
             "spec_code": "ddm.kc1.large.2",
             "vcpus": "2",
             "ram": "4",
             "az_infos": [
               {
                 "code": "eu-de-01",
                 "status": "normal",
                 "description": "eu-de-01",
                 "support_ipv6": true
               }
             ]
           }
         ]
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
