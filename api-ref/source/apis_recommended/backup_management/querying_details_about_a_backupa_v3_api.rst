:original_name: en-us_topic_0000002332869361.html

.. _en-us_topic_0000002332869361:

Querying Details About a Backup (a V3 API)
==========================================

Function
--------

This API is used to query details about a backup.

Constraints
-----------

None

URI
---

GET /v3/{project_id}/instances/{instance_id}/backups/{backup_id}

.. table:: **Table 1** Path parameters

   +-------------+--------+-----------+----------------------------------------------------------------------------------------------------------+
   | Parameter   | Type   | Mandatory | Description                                                                                              |
   +=============+========+===========+==========================================================================================================+
   | project_id  | String | Yes       | Project ID of a tenant in a region                                                                       |
   +-------------+--------+-----------+----------------------------------------------------------------------------------------------------------+
   | instance_id | String | Yes       | Instance ID                                                                                              |
   +-------------+--------+-----------+----------------------------------------------------------------------------------------------------------+
   | backup_id   | String | Yes       | Backup ID, which can be obtained from :ref:`Querying Backups (a V3 API) <en-us_topic_0000002181783554>`. |
   +-------------+--------+-----------+----------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                  |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Example Request
---------------

Querying details about a backup

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/74f57817ca8f42e19318eb0e0ad41d18/instances/2f0324a93859487eb5566d75951fcd2din09/backups/cfea30126a884f46887b4e9211460fc1br09

Response
--------

-  Normal response

   .. table:: **Table 3** Response body parameters

      +--------------------+-----------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter          | Type                                                                                                                        | Description           |
      +====================+=============================================================================================================================+=======================+
      | id                 | String                                                                                                                      | Backup ID             |
      +--------------------+-----------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | name               | String                                                                                                                      | Backup name           |
      +--------------------+-----------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | instance_id        | String                                                                                                                      | Instance ID           |
      +--------------------+-----------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | instance_name      | String                                                                                                                      | Instance name         |
      +--------------------+-----------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | related_data_nodes | Array of :ref:`RelatedDn <en-us_topic_0000002332869361__en-us_topic_0000002319891341_request_createdatabasedetail>` objects | Associated data nodes |
      +--------------------+-----------------------------------------------------------------------------------------------------------------------------+-----------------------+

   .. _en-us_topic_0000002332869361__en-us_topic_0000002319891341_request_createdatabasedetail:

   .. table:: **Table 4** RelatedDn

      ============= ====== ==============
      Parameter     Type   Description
      ============= ====== ==============
      instance_id   String Data node ID
      instance_name String Data node name
      ============= ====== ==============

-  Normal response example

   .. code-block::

      {
        "id": "09902ee7866649b8908ec209bfee2747br09",
        "name": "Backup-ddm-diagnose3-2u8g-1-4bfGfxqdESTHbkKm5XrWLg-2025052005400",
        "instance_id": "34970585d4964f2a8d6d9ea8d303398bin09",
        "instance_name": "ddm-diagnose3-2u8g-1-4bfGfxqdESTHbkKm5XrWLg",
        "related_data_nodes": [
          {
            "instance_id": "fc33739e5d2741529e21d87a7b5923fain01",
            "instance_name": "mysql_rds_related_ddm_for_diagnose3_01"
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
