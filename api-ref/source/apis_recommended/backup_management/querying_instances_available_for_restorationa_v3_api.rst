:original_name: en-us_topic_0000002332869369.html

.. _en-us_topic_0000002332869369:

Querying Instances Available for Restoration (a V3 API)
=======================================================

Function
--------

This API is used to query instances available for restoration.

Constraints
-----------

None

URI
---

GET /v3/{project_id}/instances/{instance_id}/backups/restorable-instances

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

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                  |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

.. table:: **Table 3** Query parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                            |
   +=================+=================+=================+========================================================================================================+
   | offset          | No              | Integer         | Index offset.                                                                                          |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The query starts from the next piece of data indexed by this parameter. The value is **0** by default. |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | The value must be a number but cannot be a negative number.                                            |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
   | limit           | No              | Integer         | Maximum records to be queried.                                                                         |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | Value range: **1** to **128**                                                                          |
   |                 |                 |                 |                                                                                                        |
   |                 |                 |                 | If the parameter value is not specified, 10 records are queried by default.                            |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+

Example Request
---------------

Querying instances available for restoration

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/backups/restorable-instances

Response
--------

-  Normal response

   .. table:: **Table 4** Response body parameters

      +-----------+----------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | Parameter | Type                                                                                                                                   | Description                                  |
      +===========+========================================================================================================================================+==============================================+
      | instances | Array of :ref:`QueryDDM4RestoreResp <en-us_topic_0000002332869369__en-us_topic_0000002320176057_request_createdatabasedetail>` objects | Associated data node instances.              |
      +-----------+----------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | offset    | Integer                                                                                                                                | Which page the server starts returning items |
      +-----------+----------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | limit     | Integer                                                                                                                                | Number of records displayed on each page     |
      +-----------+----------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | total     | Integer                                                                                                                                | Total number of records                      |
      +-----------+----------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+

   .. _en-us_topic_0000002332869369__en-us_topic_0000002320176057_request_createdatabasedetail:

   .. table:: **Table 5** QueryDDM4RestoreResp

      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                                                                    |
      +=======================+=======================+================================================================================================================+
      | instance_id           | String                | Instance ID                                                                                                    |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------+
      | instance_name         | String                | Instance name                                                                                                  |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------+
      | status                | String                | Instance status. It can be obtained from :ref:`DDM Instance Statuses <ddm_api_01_0064__section5119135310445>`. |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------+
      | available             | Boolean               | Available or not                                                                                               |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------+
      | unavailable_reason    | String                | Unavailability cause, which can be:                                                                            |
      |                       |                       |                                                                                                                |
      |                       |                       | -  There is a common account for the target instance.                                                          |
      |                       |                       | -  Another action is being performed on the target instance.                                                   |
      |                       |                       | -  The target instance has been associated with another DN.                                                    |
      |                       |                       | -  The instance has been frozen.                                                                               |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------+
      | vpc_name              | String                | Name of a VPC                                                                                                  |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------+

-  Normal response example

   .. code-block::

      {
        "instances": [
          {
            "instance_id": "3b65c609427c4b20bc0ae93e161dc7adin09",
            "instance_name": "ddm-agent-create-instance1",
            "status": "normal",
            "available": true,
            "unavailable_reason": "",
            "vpc_name": "vpc-ddm-172"
          }
        ],
        "offset": 0,
        "limit": 10,
        "total": 1
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
