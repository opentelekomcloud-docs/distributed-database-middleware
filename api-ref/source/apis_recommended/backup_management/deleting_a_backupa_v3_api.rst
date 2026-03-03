:original_name: en-us_topic_0000002217069701.html

.. _en-us_topic_0000002217069701:

Deleting a Backup (a V3 API)
============================

Function
--------

This API is used to delete a specified backup.

Constraints
-----------

None

URI
---

DELETE /v3/{project_id}/backups/{backup_id}

.. table:: **Table 1** Path parameters

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                              |
   +=================+=================+=================+==========================================================================================================+
   | project_id      | Yes             | String          | Project ID of a tenant in a region                                                                       |
   |                 |                 |                 |                                                                                                          |
   |                 |                 |                 | For how to obtain a project ID, see :ref:`Obtaining a Project ID <ddm_api_01_0063>`.                     |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------+
   | backup_id       | Yes             | String          | Backup ID, which can be obtained from :ref:`Querying Backups (a V3 API) <en-us_topic_0000002181783554>`. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token                                                                   |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Example Request
---------------

Deleting a specified backup

.. code-block:: text

   DELETE https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/backups/c131f9339****5cdebe350228br09

Response
--------

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
