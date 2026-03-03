:original_name: ddm_api_01_0111.html

.. _ddm_api_01_0111:

Scaling Out a DDM Instance (a V3 API)
=====================================

Function
--------

This API is used to scale out a specified DDM instance.

Constraints
-----------

Make sure that the associated RDS instances are available and not undergoing other operations.

URI
---

-  URL format

   POST /v3/{project_id}/instances/{instance_id}/nodes

-  Parameter description

   .. table:: **Table 1** Path parameters

      =========== ========= ====== ===================================
      Parameter   Mandatory Type   Description
      =========== ========= ====== ===================================
      project_id  Yes       String Project ID of a tenant in a region.
      instance_id Yes       String DDM instance ID.
      =========== ========= ====== ===================================

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

   +-----------------+-----------------+------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type                                                                               | Description                                                                                                                     |
   +=================+=================+====================================================================================+=================================================================================================================================+
   | group_id        | No              | String                                                                             | Group ID, which specifies the group that is scaled out. This parameter must be specified if there are more than one node group. |
   |                 |                 |                                                                                    |                                                                                                                                 |
   |                 |                 |                                                                                    | It can be obtained from :ref:`Obtaining the Instance Group Information (a V3 API) <ddm_api_01_0093>`.                           |
   +-----------------+-----------------+------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | subnet_id       | No              | String                                                                             | Subnet ID. This parameter is mandatory when there are more than one subnet in the node group.                                   |
   +-----------------+-----------------+------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | nodes           | Yes             | Array of :ref:`Table EnlargeNodeInfo <ddm_api_01_0111__table139410421011>` objects | Node information list.                                                                                                          |
   |                 |                 |                                                                                    |                                                                                                                                 |
   |                 |                 |                                                                                    | The list can include at least one node.                                                                                         |
   |                 |                 |                                                                                    |                                                                                                                                 |
   |                 |                 |                                                                                    | The list can include a maximum of 32 nodes.                                                                                     |
   +-----------------+-----------------+------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+

.. _ddm_api_01_0111__table139410421011:

.. table:: **Table 4** EnlargeNodeInfo

   +----------------+-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter      | Mandatory | Type   | Description                                                                                                                                               |
   +================+===========+========+===========================================================================================================================================================+
   | available_zone | Yes       | String | AZ where the node is located. The value cannot be empty. For details, see `Regions and Endpoints <https://docs.otc.t-systems.com/endpoint/index.html>`__. |
   +----------------+-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

Scaling out a DDM instance. The number of nodes to be added is 1.

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/nodes
   {
        "nodes": [
           {
               "available_zone": "az1"
           }
       ]
   }

Scaling out a DDM instance that has more than one group. The number of nodes to be added is 1.

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/nodes
   {
       "group_id": "efd077a3a50e460c8ba62e1956363299gr09",
       "subnet_id": "ead1e945-ca89-45dd-bcce-4a30b2054c22",
        "nodes": [
           {
               "available_zone": "az1"
           }
       ]
   }

Response
--------

-  Normal response

   .. table:: **Table 5** Response body parameters

      ========= ====== ============================
      Parameter Type   Description
      ========= ====== ============================
      job_id    String ID of a node scale-out task.
      ========= ====== ============================

-  Normal response example

   .. code-block::

      {
        "job_id": "eff1d289-4d03-4942-8b9f-463ea07c000c"
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
