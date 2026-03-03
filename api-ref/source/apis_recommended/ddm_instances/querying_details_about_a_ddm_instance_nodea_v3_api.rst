:original_name: en-us_topic_0000002181783550.html

.. _en-us_topic_0000002181783550:

Querying Details About a DDM Instance Node (a V3 API)
=====================================================

Function
--------

This API is used to query details about an instance node.

Constraints
-----------

None

URI
---

GET /v3/{project_id}/instances/{instance_id}/nodes/{node_id}

.. table:: **Table 1** Path parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                          |
   +=================+=================+=================+======================================================================================+
   | project_id      | Yes             | String          | Project ID of a tenant in a region.                                                  |
   |                 |                 |                 |                                                                                      |
   |                 |                 |                 | For how to obtain a project ID, see :ref:`Obtaining a Project ID <ddm_api_01_0063>`. |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------+
   | instance_id     | Yes             | String          | DDM instance ID                                                                      |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------+
   | node_id         | Yes             | String          | Node ID                                                                              |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------+

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

Example Request
---------------

Querying details about an instance node

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/nodes/4a2b97b7f5e3462c9c78aae93b46ed83no09

Response Parameters
-------------------

-  Normal response

   .. table:: **Table 3** Response body parameters

      +------------+--------+--------------------------------------------------------------------------------------------------+
      | Parameter  | Type   | Description                                                                                      |
      +============+========+==================================================================================================+
      | status     | String | Node status. For details, see :ref:`DDM Node Statuses <ddm_api_01_0064__section13481912102019>`. |
      +------------+--------+--------------------------------------------------------------------------------------------------+
      | name       | String | Node name                                                                                        |
      +------------+--------+--------------------------------------------------------------------------------------------------+
      | id         | String | Node ID                                                                                          |
      +------------+--------+--------------------------------------------------------------------------------------------------+
      | private_ip | String | Private IP address of the node                                                                   |
      +------------+--------+--------------------------------------------------------------------------------------------------+
      | group_id   | String | Group ID                                                                                         |
      +------------+--------+--------------------------------------------------------------------------------------------------+
      | az_code    | String | AZ                                                                                               |
      +------------+--------+--------------------------------------------------------------------------------------------------+
      | subnet_id  | String | Subnet ID.                                                                                       |
      +------------+--------+--------------------------------------------------------------------------------------------------+

-  Normal response example

   .. code-block::

      {
        "id": "8d5601f17b30****da1e69181173cdno09",
        "private_ip": "172.16.203.68",
        "status": "normal",
        "name": "ddm-ag****de2_node_01",
        "subnet_id": "d27cdc75***b6-b2ab-fec93af33538",
        "az_code": "eu-de-01",
        "group_id": "148a54****41ba6ed231487e73ccgr09"
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
