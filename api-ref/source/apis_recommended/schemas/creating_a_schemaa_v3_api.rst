:original_name: ddm_api_01_0115.html

.. _ddm_api_01_0115:

Creating a Schema (a V3 API)
============================

Function
--------

This API is used to create a schema.

Constraints
-----------

Before creating a schema, ensure that an RDS instance has been created, is in the normal state, and is not associated with other DDM instances.

URI
---

-  URL format

   POST /v3/{project_id}/instances/{instance_id}/databases

-  Parameter description

.. table:: **Table 1** Path parameters

   =========== ====== ========= ===================================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ===================================
   project_id  String Yes       Project ID of a tenant in a region.
   instance_id String Yes       DDM instance ID.
   =========== ====== ========= ===================================

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

   +-----------------+-----------------+--------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type                                                                                             | Description                                                                                                                                                                                                          |
   +=================+=================+==================================================================================================+======================================================================================================================================================================================================================+
   | name            | Yes             | String                                                                                           | Schema name, which:                                                                                                                                                                                                  |
   |                 |                 |                                                                                                  |                                                                                                                                                                                                                      |
   |                 |                 |                                                                                                  | -  Can include 2 to 48 characters.                                                                                                                                                                                   |
   |                 |                 |                                                                                                  | -  Must start with a lowercase letter.                                                                                                                                                                               |
   |                 |                 |                                                                                                  | -  Contains only lowercase letters, digits, and underscores (_).                                                                                                                                                     |
   |                 |                 |                                                                                                  | -  Cannot contain keywords **information_schema**, **mysql, performance_schema**, or **sys**.                                                                                                                        |
   +-----------------+-----------------+--------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | shard_mode      | Yes             | String                                                                                           | Sharding mode of the schema. The value can be:                                                                                                                                                                       |
   |                 |                 |                                                                                                  |                                                                                                                                                                                                                      |
   |                 |                 |                                                                                                  | -  **cluster**: indicates that the schema is in sharded mode.                                                                                                                                                        |
   |                 |                 |                                                                                                  | -  **single**: indicates that the schema is in unsharded mode.                                                                                                                                                       |
   |                 |                 |                                                                                                  |                                                                                                                                                                                                                      |
   |                 |                 |                                                                                                  | Enumerated values:                                                                                                                                                                                                   |
   |                 |                 |                                                                                                  |                                                                                                                                                                                                                      |
   |                 |                 |                                                                                                  | -  **cluster**                                                                                                                                                                                                       |
   |                 |                 |                                                                                                  | -  **single**                                                                                                                                                                                                        |
   +-----------------+-----------------+--------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | shard_number    | Yes             | Integer                                                                                          | Number of shards in the same working mode. The value must be greater than or equal to the number of associated RDS instances and less than or equal to the product of the associated RDS instances multiplied by 64. |
   +-----------------+-----------------+--------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | dn_instances    | Yes             | Array of :ref:`DatabaseDnInstanceInfo <ddm_api_01_0115__request_databaseinstabcesparam>` objects | RDS instances associated with the schema                                                                                                                                                                             |
   +-----------------+-----------------+--------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _ddm_api_01_0115__request_databaseinstabcesparam:

.. table:: **Table 4** DatabaseDnInstanceInfo

   +---------------+-----------+--------+--------------------------------------------------------+
   | Parameter     | Mandatory | Type   | Description                                            |
   +===============+===========+========+========================================================+
   | id            | Yes       | String | ID of the RDS instance associated with the schema      |
   +---------------+-----------+--------+--------------------------------------------------------+
   | user_name     | Yes       | String | Username for logging in to the associated RDS instance |
   +---------------+-----------+--------+--------------------------------------------------------+
   | user_password | Yes       | String | Password for logging in to the associated RDS instance |
   +---------------+-----------+--------+--------------------------------------------------------+

Example Request
---------------

-  Creating a schema and associating it with an existing DDM account

   .. code-block:: text

      POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/databases
      {
        "name": "mytestdb",
        "shard_mode": "cluster",
        "shard_number": 8,
        "dn_instances": [
          {
            "id": "f296c394f13f48449d715bf99af07e59in01",
            "user_name": "root",
            "user_password": "PassWord_234"
          }
        ]
      }

Response
--------

-  Normal response

   .. table:: **Table 5** Response body parameters

      ========= ====== ===================================
      Parameter Type   Description
      ========= ====== ===================================
      job_id    String ID of the job for deleting a schema
      name      String Schema name
      ========= ====== ===================================

-  Normal response example

   .. code-block::

      {
      "job_id": "eff1d289-xxxx-xxxx-8b9f-463ea07c000c",
        "name": "mytestdb"
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
