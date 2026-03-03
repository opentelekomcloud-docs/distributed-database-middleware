:original_name: en-us_topic_0000002181783542.html

.. _en-us_topic_0000002181783542:

Deleting an Instance Group (a V3 API)
=====================================

Function
--------

This API is used to delete a DDM instance group.

Constraints
-----------

None

URI
---

DELETE /v3/{project_id}/instances/{instance_id}/groups/{group_id}

.. table:: **Table 1** Parameter description

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                     |
   +=================+=================+=================+=================================================================================================================+
   | project_id      | Yes             | String          | Project ID of a tenant in a region                                                                              |
   |                 |                 |                 |                                                                                                                 |
   |                 |                 |                 | For how to obtain a project ID, see :ref:`Obtaining a Project ID <ddm_api_01_0063>`.                            |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------+
   | instance_id     | Yes             | String          | DDM instance ID                                                                                                 |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------+
   | group_id        | Yes             | String          | Group ID. It can be obtained from :ref:`Obtaining the Instance Group Information (a V3 API) <ddm_api_01_0093>`. |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------+

Request
-------

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

Deleting a DDM instance group

.. code-block:: text

   DELETE https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/groups/b4153b807b1a4f83870bf868fcc4f4eagr09

Response
--------

-  Normal response

   .. table:: **Table 3** Response body parameters

      ========= ====== ===================================
      Parameter Type   Description
      ========= ====== ===================================
      job_id    String ID of the job for deleting a group.
      ========= ====== ===================================

-  Normal response example

   .. code-block::

      {
        "job_id": "3ae783f3-844e-4051-abd5-b9cc65899785"
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
