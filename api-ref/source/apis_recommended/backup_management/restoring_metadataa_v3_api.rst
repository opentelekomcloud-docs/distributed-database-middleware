:original_name: en-us_topic_0000002298949884.html

.. _en-us_topic_0000002298949884:

Restoring Metadata (a V3 API)
=============================

Function
--------

This API is used to restore metadata.

.. _en-us_topic_0000002298949884__en-us_topic_0000002285536546_section5205164312213:

Constraints
-----------

Metadata restoration mainly restores the metadata of your DDM instance to a new DDM instance. It starts after a point-in-time recovery (PITR) for the associated data nodes is complete.

.. note::

   PITR indicates that a data node has been restored to a specified point in time.

   For details about how to perform PITR on RDS for MySQL, see section "Data Restorations" > "Restoring Data to RDS for MySQL" > "PITR: Restoring a DB Instance to a Point in Time" in *Working with RDS for MySQL*.

   You can also refer to section "Backup and Restoration" in *RDS for MySQL API Reference*.

URI
---

POST /v3/{project_id}/instances/{instance_id}/backups/metadata-recovery

.. table:: **Table 1** Path parameters

   =========== ====== ========= ==================================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ==================================
   project_id  String Yes       Project ID of a tenant in a region
   instance_id String Yes       Instance ID
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

   +-----------+-----------+---------------------------------------------------------------------------------------------------------------+-----------------------------+
   | Parameter | Mandatory | Type                                                                                                          | Description                 |
   +===========+===========+===============================================================================================================+=============================+
   | source    | Yes       | :ref:`RestoreMetaDataSource <en-us_topic_0000002298949884__en-us_topic_0000002285536546_table10196164513265>` | Source instance information |
   +-----------+-----------+---------------------------------------------------------------------------------------------------------------+-----------------------------+
   | target    | Yes       | :ref:`RestoreMetaDataTarget <en-us_topic_0000002298949884__en-us_topic_0000002285536546_table0849632152920>`  | Target instance information |
   +-----------+-----------+---------------------------------------------------------------------------------------------------------------+-----------------------------+

.. _en-us_topic_0000002298949884__en-us_topic_0000002285536546_table10196164513265:

.. table:: **Table 4** RestoreMetaDataSource

   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------+
   | Parameter    | Mandatory | Type   | Description                                                                                                        |
   +==============+===========+========+====================================================================================================================+
   | restore_time | No        | Long   | Restoration timestamp, accurate to milliseconds. (Either **backup_id** or **restore_time** needs to be specified.) |
   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------+
   | backup_id    | No        | String | Backup ID. (Either **restore_time** or **backup_id** needs to be specified.)                                       |
   +--------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------+

.. _en-us_topic_0000002298949884__en-us_topic_0000002285536546_table0849632152920:

.. table:: **Table 5** RestoreMetaDataTarget

   +-----------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type             | Description                                                                                                                                                       |
   +=================+=================+==================+===================================================================================================================================================================+
   | data_nodes      | Yes             | Array of strings | Target data nodes.                                                                                                                                                |
   |                 |                 |                  |                                                                                                                                                                   |
   |                 |                 |                  | The data nodes are in the same VPC and subnet as the DDM instance and can communicate with the DDM instance.                                                      |
   |                 |                 |                  |                                                                                                                                                                   |
   |                 |                 |                  | PITR has been completed on the data nodes. For details, see :ref:`Constraints <en-us_topic_0000002298949884__en-us_topic_0000002285536546_section5205164312213>`. |
   +-----------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | instance_id     | Yes             | String           | Target instance ID. It can be obtained from :ref:`Querying Instances Available for Restoration (a V3 API) <en-us_topic_0000002332869369>`.                        |
   +-----------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

Restoring metadata

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/backups/metadata-recovery

   {
     "source": {
       "backup_id": "defa45b24d314e878fde930a61732e9dbr09"
     },
     "target": {
       "instance_id": "2f0324a93859487eb5566d75951fcd2din09",
       "data_nodes": [
         "f4e2949e9b9b4d60b42c89ed39bfe34cin01"
       ]
     }
   }

Response
--------

-  Normal response

   .. table:: **Table 6** Response body parameters

      ========= ====== ===========
      Parameter Type   Description
      ========= ====== ===========
      job_id    String Task ID
      ========= ====== ===========

-  Normal response example

   .. code-block::

      {
        "job_id": "09902ee7866649b8908ec209bfee2747"
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
