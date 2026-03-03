:original_name: en-us_topic_0000002299876902.html

.. _en-us_topic_0000002299876902:

Deleting Multiple Nodes from an Instance at a Time (a V3 API)
=============================================================

Function
--------

This API is used to delete multiple nodes from an instance at a time.

Constraints
-----------

Nodes in different groups cannot be deleted at the same time.

URI
---

POST /v3/{project_id}/instances/{instance_id}/nodes/batch-delete

.. table:: **Table 1** Path parameters

   =========== ========= ====== ==================================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ==================================
   project_id  Yes       String Project ID of a tenant in a region
   instance_id Yes       String DDM instance ID
   =========== ========= ====== ==================================

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

Request
-------

.. table:: **Table 3** Request body parameters

   +-----------+-----------+------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type             | Description                                                                                                                                                                 |
   +===========+===========+==================+=============================================================================================================================================================================+
   | node_ids  | Yes       | Array of strings | ID list of nodes to be deleted. Only nodes in the same group can be selected. After a specified node is deleted from a group, there must be at least one node in the group. |
   +-----------+-----------+------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

Deleting nodes

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/nodes/batch-delete
   {
     "node_ids": ["116ba14da45678d28ecd83a38c218907no02"]
   }

Response Parameters
-------------------

-  Normal response

   .. table:: **Table 4** Response body parameters

      ========= ====== ===========
      Parameter Type   Description
      ========= ====== ===========
      job_id    String Task ID
      ========= ====== ===========

-  Normal response example

   .. code-block::

      {
        "job_id" : "9fe84a77-6a6b-4b03-9a3e-db910a548657"
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
