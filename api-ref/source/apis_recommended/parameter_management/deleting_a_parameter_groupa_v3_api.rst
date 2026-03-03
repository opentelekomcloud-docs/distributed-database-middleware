:original_name: en-us_topic_0000002332909561.html

.. _en-us_topic_0000002332909561:

Deleting a Parameter Group (a V3 API)
=====================================

Function
--------

This API is used to delete a parameter group.

Constraints
-----------

None

URI
---

DELETE /v3/{project_id}/configurations/{config_id}

.. table:: **Table 1** Path parameters

   ========== ====== ========= ==================================
   Parameter  Type   Mandatory Description
   ========== ====== ========= ==================================
   project_id String Yes       Project ID of a tenant in a region
   config_id  String Yes       Parameter group ID
   ========== ====== ========= ==================================

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

Deleting a parameter group

.. code-block:: text

   DELETE https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/configurations/2aa71dc81e2c47699229b7aa26038f9dpr09

Response
--------

-  Normal response

   None

-  Normal response example

   None

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
