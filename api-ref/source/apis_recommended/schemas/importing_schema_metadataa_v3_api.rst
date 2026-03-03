:original_name: ddm_api_01_0105.html

.. _ddm_api_01_0105:

Importing Schema Metadata (a V3 API)
====================================

Function
--------

This API is used to import distribution information of physical shards in all schemas and use it to create schemas that contain the same physical shards and distribution relationship.

Constraints
-----------

-  Ensure that the selected data nodes are not associated with other DDM instances and no schemas are created.
-  The selected data nodes have no physical shards with the same name, for example, db_test_0000.
-  The current DDM instance has no schemas with the same name.

URI
---

POST /v3/{project_id}/instances/{instance_id}/schema-metadata

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

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                          |
   +=================+=================+=================+======================================================================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | It can be obtained by calling an IAM API. The value of **X-Subject-Token** in the response header is the user token. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+
   | Content-Type    | Yes             | String          | MIME type of the request body. Value range:                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | -  application/json                                                                                                  |
   |                 |                 |                 | -  application/json;charset=utf-8                                                                                    |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +---------------------------+---------------------------------------------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                 | Type                                              | Mandatory       | Description                                                                                                                                                                             |
   +===========================+===================================================+=================+=========================================================================================================================================================================================+
   | compressed_databases_info | String                                            | Yes             | Distribution information of physical shards in a schema. This information is compressed and encoded. For the method to obtain the information, see section "Exporting Schema Metadata." |
   +---------------------------+---------------------------------------------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | dn_instance               | :ref:`DnInstance <ddm_api_01_0105__table1126032>` | Yes             | Data nodes required for creating a schema. The number of data nodes should be consistent with the exported schema metadata and meet the following constraints:                          |
   |                           |                                                   |                 |                                                                                                                                                                                         |
   |                           |                                                   |                 | -  The data nodes are not associated with other DDM instances for creating a schema.                                                                                                    |
   |                           |                                                   |                 | -  The data nodes have no physical shards with the same name, for example, **db_test_0000**.                                                                                            |
   |                           |                                                   |                 | -  The data nodes must be in the same VPC as your DDM instance and not associated with other DDM instances.                                                                             |
   |                           |                                                   |                 | -  The data nodes must be in the **Running** or **Backing up** state                                                                                                                    |
   +---------------------------+---------------------------------------------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ddm_api_01_0105__table1126032:

.. table:: **Table 4** DnInstance

   ============== ====== ========= ====================================
   Parameter      Type   Mandatory Description
   ============== ====== ========= ====================================
   dn_instance_id String Yes       Data node ID
   admin_user     String Yes       Username for accessing the data node
   admin_password String Yes       Password for accessing the data node
   ============== ====== ========= ====================================

Example Request
---------------

Importing schema metadata

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/schema-metadata
   {
       "compressed_databases_info":"H4sIAAAAAAAAAN3cTW/bRhgE4P/Csw7aL4rUtQUKX3wo0lMQCPxYNQJsOjApIIWR/17K1RvDPgQ9...",
       "dn_instance":[
           {
               "dn_instance_id":"91b1272b09364ddeb999f1295bf0506ain01",
               "admin_user":"root",
               "admin_password":"PassWord_234"
           }
       ]
   }

Response
--------

-  Normal response

   .. table:: **Table 5** Response body parameters

      ============= ====== =================
      Parameter     Type   Description
      ============= ====== =================
      instance_id   String DDM instance ID
      instance_name String DDM instance name
      job_id        String Task ID
      ============= ====== =================

-  Normal response example

   .. code-block::

      {
        "job_id":"441d5677-b76a-4dd4-a97a",
        "instance_id":"91b1272b09364ddeb999f1295bf0506ain09",
        "instance_name":"ddm-test-01"
      }

-  Abnormal response

   For details, see :ref:`Abnormal Request Results <ddm_api_01_0059>`.

Status Codes
------------

-  Normal

   202

-  Abnormal

   For details, see :ref:`Status Codes <ddm_api_01_0060>`.

Error Codes
-----------

For details, see :ref:`Error Codes <ddm_api_01_0061>`.
