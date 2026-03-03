:original_name: ddm_api_01_0094.html

.. _ddm_api_01_0094:

Creating an Instance Group (a V3 API)
=====================================

Function
--------

This API is used to create a DDM instance group.

Constraints
-----------

None

URI
---

-  URL format

   POST /v3/{project_id}/instances/{instance_id}/groups

-  Parameter description

   .. table:: **Table 1** URI parameters

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

   +-----------------+-----------------+-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type                                                                        | Description                                                                                                            |
   +=================+=================+=============================================================================+========================================================================================================================+
   | name            | Yes             | String                                                                      | Name of a DDM instance group, which:                                                                                   |
   |                 |                 |                                                                             |                                                                                                                        |
   |                 |                 |                                                                             | -  Can include 4 to 64 characters.                                                                                     |
   |                 |                 |                                                                             | -  Must start with a letter.                                                                                           |
   |                 |                 |                                                                             | -  Can contain only letters, digits, underscores (_), and hyphens (-).                                                 |
   |                 |                 |                                                                             |                                                                                                                        |
   |                 |                 |                                                                             | Minimum characters: **4**                                                                                              |
   |                 |                 |                                                                             |                                                                                                                        |
   |                 |                 |                                                                             | Maximum characters: **64**                                                                                             |
   +-----------------+-----------------+-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | type            | Yes             | String                                                                      | Type of the instance group.                                                                                            |
   |                 |                 |                                                                             |                                                                                                                        |
   |                 |                 |                                                                             | **rw**: read/write group                                                                                               |
   |                 |                 |                                                                             |                                                                                                                        |
   |                 |                 |                                                                             | **r**: read-only group                                                                                                 |
   +-----------------+-----------------+-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | flavor_id       | No              | String                                                                      | Flavor ID. (Either the flavor ID or flavor code must be specified.)                                                    |
   |                 |                 |                                                                             |                                                                                                                        |
   |                 |                 |                                                                             | It can be obtained by referring to :ref:`Querying DDM Node Classes Available in Each AZ (a V3 API) <ddm_api_01_0110>`. |
   +-----------------+-----------------+-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | flavor_ref      | No              | String                                                                      | Flavor code. (Either the flavor ID or flavor code must be specified.)                                                  |
   |                 |                 |                                                                             |                                                                                                                        |
   |                 |                 |                                                                             | It can be obtained by referring to :ref:`Querying DDM Node Classes Available in Each AZ (a V3 API) <ddm_api_01_0110>`. |
   +-----------------+-----------------+-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | nodes           | Yes             | Array of :ref:`Table NodeInfo <ddm_api_01_0094__table139410421011>` objects | Node information list.                                                                                                 |
   |                 |                 |                                                                             |                                                                                                                        |
   |                 |                 |                                                                             | Minimum value: **1**                                                                                                   |
   |                 |                 |                                                                             |                                                                                                                        |
   |                 |                 |                                                                             | Maximum value: **32**                                                                                                  |
   +-----------------+-----------------+-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+

.. _ddm_api_01_0094__table139410421011:

.. table:: **Table 4** NodeInfo

   +----------------+-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter      | Mandatory | Type   | Description                                                                                                                                               |
   +================+===========+========+===========================================================================================================================================================+
   | available_zone | Yes       | String | AZ where the node is located. The value cannot be empty. For details, see `Regions and Endpoints <https://docs.otc.t-systems.com/endpoint/index.html>`__. |
   +----------------+-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subnet_id      | Yes       | String | Subnet ID.                                                                                                                                                |
   +----------------+-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

Create a DDM instance group. The group type is read/write and the number of nodes is 1.

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/groups
   {
       "name": "group-1",
       "type": "rw",
       "flavor_id": "a615922f-0ed8-3691-aad4-a595185febba",
        "nodes": [
           {
               "available_zone": "az1",
               "subnet_id": "ead1e945-ca89-45dd-bcce-4a30b2054c22"
           }
       ]
   }

Create a DDM instance group. The group type is read/write, the number of nodes is 1, and the flavor code is **ddm.large.2**.

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/groups
   {
       "name": "group-1",
       "type": "rw",
       "flavor_ref": "ddm.large.2",
        "nodes": [
           {
               "available_zone": "az1",
               "subnet_id": "ead1e945-ca89-45dd-bcce-4a30b2054c22"
           }
       ]
   }

Create a DDM instance group. The group type is read-only and the number of nodes is 1.

.. code-block:: text

   POST https://{endpoint}/v3/{project_id}/instances/{instance_id}/groups
   {
       "name": "group-2",
       "type": "r",
       "flavor_id": "a615922f-0ed8-3691-aad4-a595185febba",
        "nodes": [
           {
               "available_zone": "az1",
               "subnet_id": "ead1e945-ca89-45dd-bcce-4a30b2054c22"
           }
       ]
   }

Create a DDM instance group. The group type is read/write and the number of nodes is 2.

.. code-block:: text

   POST https://{endpoint}/v3/{project_id}/instances/{instance_id}/groups
   {
       "name": "group-3",
       "type": "rw",
       "flavor_id": "a615922f-0ed8-3691-aad4-a595185febba",
        "nodes": [
           {
               "available_zone": "az1",
               "subnet_id": "ead1e945-ca89-45dd-bcce-4a30b2054c22"
           },
           {
               "available_zone": "az2",
               "subnet_id": "ead1e945-ca89-45dd-bcce-4a30b2054c22"
           }
       ]
   }

Response
--------

-  Normal response

   .. table:: **Table 5** Response body parameters

      +-----------------------+-----------------------+----------------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                                |
      +=======================+=======================+============================================================================+
      | job_id                | String                | ID of the job for creating an instance group.                              |
      |                       |                       |                                                                            |
      |                       |                       | This parameter is returned only when pay-per-use instances are created.    |
      +-----------------------+-----------------------+----------------------------------------------------------------------------+
      | group_id              | String                | Group ID.                                                                  |
      |                       |                       |                                                                            |
      |                       |                       | This parameter is returned only for the creation of pay-per-use instances. |
      +-----------------------+-----------------------+----------------------------------------------------------------------------+

-  Normal response example

   .. code-block::

      {
        "job_id" : "1eb697c0-1842-43a3-8671-f562d038****",
       "group_id": "b4153b807b1a4f83870bf868fcc4f4ea****"
      }

-  Abnormal response

   For details, see :ref:`Abnormal Request Results <ddm_api_01_0059>`.

Status Code
-----------

-  Normal

   202

-  Abnormal

   For details, see :ref:`Status Codes <ddm_api_01_0060>`.

Error Codes
-----------

For details, see :ref:`Error Codes <ddm_api_01_0061>`.
