:original_name: en-us_topic_0000002217144121.html

.. _en-us_topic_0000002217144121:

Restarting a DDM Node (a V3 API)
================================

Function
--------

This API is used to restart a specific node.

Constraints
-----------

None

URI
---

POST /v3/{project_id}/instances/{instance_id}/nodes/{node_id}/restart

.. table:: **Table 1** URI parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                          |
   +=================+=================+=================+======================================================================================+
   | project_id      | Yes             | String          | Project ID of a tenant in a region                                                   |
   |                 |                 |                 |                                                                                      |
   |                 |                 |                 | For how to obtain a project ID, see :ref:`Obtaining a Project ID <ddm_api_01_0063>`. |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------+
   | instance_id     | Yes             | String          | DDM instance ID                                                                      |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------+
   | node_id         | Yes             | String          | DDM instance node ID                                                                 |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request header parameter

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                  |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Example Request
---------------

Restarting a node

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/nodes/4a2b97b7f5e3462c9c78aae93b46ed83no09/restart

Response Parameters
-------------------

-  Normal response

   .. table:: **Table 3** Response body parameters

      ========= ====== ===========
      Parameter Type   Description
      ========= ====== ===========
      job_id    String Job ID
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
