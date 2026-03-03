:original_name: ddm_api_01_0104.html

.. _ddm_api_01_0104:

Exporting Schema Metadata (a V3 API)
====================================

Function
--------

This API is used to export all schema metadata about distribution of physical shards on data nodes.

Constraints
-----------

None

URI
---

GET /v3/{project_id}/instances/{instance_id}/schema-metadata

.. table:: **Table 1** Path parameters

   =========== ====== ========= ==================================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ==================================
   project_id  String Yes       Project ID of a tenant in a region
   instance_id String Yes       DDM instance ID
   =========== ====== ========= ==================================

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token                                                                   |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Example Request
---------------

.. code-block::

   Exporting schema metadata
   GET https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/schema-metadata

Response
--------

-  Normal response

   .. table:: **Table 3** Response body parameters

      +---------------------------+--------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+
      | Parameter                 | Type                                                                           | Description                                                                                          |
      +===========================+================================================================================+======================================================================================================+
      | compressed_databases_info | String                                                                         | Distribution information of physical shards in a schema. This information is compressed and encoded. |
      +---------------------------+--------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+
      | data_nodes                | Array of :ref:`DNInstanceInfo <ddm_api_01_0104__table133072020144710>` objects | Information about data nodes                                                                         |
      +---------------------------+--------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+

   .. _ddm_api_01_0104__table133072020144710:

   .. table:: **Table 4** DNInstanceInfo

      ============== ======= ==============
      Parameter      Type    Description
      ============== ======= ==============
      instance_id    String  Data node ID
      instance_name  String  Data node name
      access_host    String  Access address
      access_port    Integer Access port
      engine         String  Engine type
      engine_version String  Engine version
      ============== ======= ==============

-  Normal response example

   .. code-block::

      {
          "compressed_databases_info": "H4sIAAAAAAAAAN3cTW/bRhgE4P/Csw7aL4rUtQUKX3wo0lMQCPxYNQJsOjApIIWR/17K1RvDPgQ9...",
          "data_nodes": [{
              "instance_id": "91b1272b09364ddeb999f1295bf0506ain01",
              "instance_name": "rds-for-ddm-01",
              "access_host": "172.16.192.110",
              "access_port": 3306,
              "engine": "mysql",
              "engine_version": "5.7"
          }]
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
