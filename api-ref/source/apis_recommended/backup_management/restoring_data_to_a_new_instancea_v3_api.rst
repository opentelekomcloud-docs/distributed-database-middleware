:original_name: en-us_topic_0000002298790232.html

.. _en-us_topic_0000002298790232:

Restoring Data to a New Instance (a V3 API)
===========================================

Function
--------

This API is used to restore data to a new instance.

Constraints
-----------

None

URI
---

POST /v3/{project_id}/instances/{instance_id}/backups/recovery

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

   +---------------------+-----------+--------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------+
   | Parameter           | Mandatory | Type                                                                                                                     | Description                                          |
   +=====================+===========+==========================================================================================================================+======================================================+
   | source              | Yes       | :ref:`RestoreInstSource <en-us_topic_0000002298790232__en-us_topic_0000002285479842_table10196164513265>`                | Source instance information.                         |
   +---------------------+-----------+--------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------+
   | target              | Yes       | :ref:`RestoreInstTarget <en-us_topic_0000002298790232__en-us_topic_0000002285479842_table0849632152920>`                 | Target instance information.                         |
   +---------------------+-----------+--------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------+
   | data_node_relations | Yes       | Array of :ref:`DataNodeRelation <en-us_topic_0000002298790232__en-us_topic_0000002285479842_table9604141614406>` objects | Association between the source and target data nodes |
   +---------------------+-----------+--------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------+

.. _en-us_topic_0000002298790232__en-us_topic_0000002285479842_table10196164513265:

.. table:: **Table 4** RestoreInstSource

   ============ ========= ====== =======================================
   Parameter    Mandatory Type   Description
   ============ ========= ====== =======================================
   instance_id  Yes       String Source instance ID.
   restore_time Yes       Long   Restoration timestamp, in milliseconds.
   ============ ========= ====== =======================================

.. _en-us_topic_0000002298790232__en-us_topic_0000002285479842_table0849632152920:

.. table:: **Table 5** RestoreInstTarget

   +-------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                                                                                |
   +=============+===========+========+============================================================================================================================================+
   | instance_id | Yes       | String | Target instance ID. It can be obtained from :ref:`Querying Instances Available for Restoration (a V3 API) <en-us_topic_0000002332869369>`. |
   +-------------+-----------+--------+--------------------------------------------------------------------------------------------------------------------------------------------+

.. _en-us_topic_0000002298790232__en-us_topic_0000002285479842_table9604141614406:

.. table:: **Table 6** DataNodeRelation

   +--------------------+-----------+--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter          | Mandatory | Type   | Description                                                                                                                                                                |
   +====================+===========+========+============================================================================================================================================================================+
   | source_instance_id | Yes       | String | Source data node ID. It can be obtained from :ref:`Querying Data Nodes Associated with an Instance at a Restoration Time Point (a V3 API) <en-us_topic_0000002298949876>`. |
   +--------------------+-----------+--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | target_instance_id | Yes       | String | Target data node ID. It can be obtained from :ref:`Querying Data Nodes Available to Restore Data to a Point in Time (a V3 API) <en-us_topic_0000002332909569>`.            |
   +--------------------+-----------+--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

Restoring data to a new instance

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/backups/recovery

   {
     "source": {
       "instance_id": "733c7e8d73a54c27b8308ec784a8be8cin09",
       "restore_time": 1747732352076
     },
     "target": {
       "instance_id": "2f0324a93859487eb5566d75951fcd2din09"
     },
     "data_node_relations": [
       {
         "source_instance_id": "7edae0250ebc464897bd92b8d3e8b769in01",
         "target_instance_id": "f4e2949e9b9b4d60b42c89ed39bfe34cin01"
       }
     ]
   }

Response
--------

-  Normal response

   .. table:: **Table 7** Response body parameters

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
