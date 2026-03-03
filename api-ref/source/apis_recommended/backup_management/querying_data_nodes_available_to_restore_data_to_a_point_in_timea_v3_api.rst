:original_name: en-us_topic_0000002332909569.html

.. _en-us_topic_0000002332909569:

Querying Data Nodes Available to Restore Data to a Point in Time (a V3 API)
===========================================================================

Function
--------

This API is used to query data nodes available for restoration.

Constraints
-----------

You must call the API for querying the restoration time range first.

URI
---

GET /v3/{project_id}/instances/{instance_id}/backups/restorable-data-node

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

   +-----------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory       | Type            | Description                                                                                                                                                                                                 |
   +=======================+=================+=================+=============================================================================================================================================================================================================+
   | target_instance_id    | Yes             | String          | Target instance that data will be restored to                                                                                                                                                               |
   |                       |                 |                 |                                                                                                                                                                                                             |
   |                       |                 |                 | The instance can be selected from those whose **available** parameter is set to **true** in the API of :ref:`Querying Instances Available for Restoration (a V3 API) <en-us_topic_0000002332869369>`.       |
   +-----------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | source_dn_instance_id | Yes             | String          | Associated data node. The ID of the data node can be obtained from the API of :ref:`Querying Data Nodes Associated with an Instance at a Restoration Time Point (a V3 API) <en-us_topic_0000002298949876>`. |
   +-----------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | restore_time          | Yes             | Integer         | Restoration timestamp, in milliseconds.                                                                                                                                                                     |
   |                       |                 |                 |                                                                                                                                                                                                             |
   |                       |                 |                 | The value of this parameter can be obtained from the API of :ref:`Querying the Restoration Time Range (a V3 API) <en-us_topic_0000002298790224>`.                                                           |
   +-----------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | offset                | No              | Integer         | Index offset.                                                                                                                                                                                               |
   |                       |                 |                 |                                                                                                                                                                                                             |
   |                       |                 |                 | The query starts from the next piece of data indexed by this parameter. The value is **0** by default.                                                                                                      |
   |                       |                 |                 |                                                                                                                                                                                                             |
   |                       |                 |                 | The value must be a number but cannot be a negative number.                                                                                                                                                 |
   +-----------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | limit                 | No              | Integer         | Maximum records to be queried.                                                                                                                                                                              |
   |                       |                 |                 |                                                                                                                                                                                                             |
   |                       |                 |                 | Value range: **1** to **128**                                                                                                                                                                               |
   |                       |                 |                 |                                                                                                                                                                                                             |
   |                       |                 |                 | If the parameter value is not specified, 10 records are queried by default.                                                                                                                                 |
   +-----------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

Querying data nodes available for restoration

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/74f57817ca8f42e19318eb0e0ad41d18/instances/733c7e8d73a54c27b8308ec784a8be8cin09/backups/restorable-data-node?source_dn_instance_id=41c239a1e9bd4cd2aabd678bab45a886in01&target_instance_id=2f0324a93859487eb5566d75951fcd2din09&restore_time=1747730765390

Response
--------

-  Normal response

   .. table:: **Table 4** Response body parameters

      +-------------------+----------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | Parameter         | Type                                                                                                                       | Description                                  |
      +===================+============================================================================================================================+==============================================+
      | target_data_nodes | Array of :ref:`TargetDn4Restore <en-us_topic_0000002332909569__en-us_topic_0000002320089125_table171311812132111>` objects | Available target data nodes                  |
      +-------------------+----------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | offset            | Integer                                                                                                                    | Which page the server starts returning items |
      +-------------------+----------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | limit             | Integer                                                                                                                    | Number of records displayed on each page     |
      +-------------------+----------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+
      | total             | Integer                                                                                                                    | Total number of records                      |
      +-------------------+----------------------------------------------------------------------------------------------------------------------------+----------------------------------------------+

   .. _en-us_topic_0000002332909569__en-us_topic_0000002320089125_table171311812132111:

   .. table:: **Table 5** TargetDn4Restore

      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                                                                  |
      +=======================+=======================+==============================================================================================================+
      | instance_id           | String                | Instance ID                                                                                                  |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------+
      | instance_name         | String                | Instance name                                                                                                |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------+
      | engine_name           | String                | Engine name                                                                                                  |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------+
      | status                | String                | Data node status. It can be obtained from :ref:`Data Node Statuses <ddm_api_01_0064__section9317162963412>`. |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------+
      | available             | Boolean               | Available or not                                                                                             |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------+
      | unavailable_reason    | String                | Unavailability cause, which can be:                                                                          |
      |                       |                       |                                                                                                              |
      |                       |                       | -  The target data node and target instance are not in the same VPC.                                         |
      |                       |                       | -  The target data node is associated with other instances.                                                  |
      |                       |                       | -  The data node is abnormal.                                                                                |
      |                       |                       | -  The version of the target data node is earlier than that of the source data node.                         |
      |                       |                       | -  The engine of the target data node is different from that of the source data node.                        |
      |                       |                       | -  The target data node is read-only.                                                                        |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------+
      | vpc_name              | String                | Name of a VPC                                                                                                |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------+
      | private_ip            | String                | Private IP address                                                                                           |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------+

-  Normal response example

   .. code-block::

      {
          "target_data_nodes": [{
              "instance_name": "rds-f0e2",
              "instance_id": "55c26c79139446868919c5b8b2cbb542in01",
              "engine_name": "mysql",
              "status": "normal",
              "available": true,
              "unavailable_reason": "",
              "vpc_name": "vpc-ddm-172",
              "private_ip": "172.16.248.115"
          }, {
              "instance_name": "mysql_80_4u8g_single_2",
              "instance_id": "c5ee103325294f37a8a42e88ba51947ain01",
              "engine_name": "mysql",
              "status": "normal",
              "available": true,
              "unavailable_reason": "",
              "vpc_name": "vpc-ddm-172",
              "private_ip": "172.16.192.156"
          }],
          "offset": 0,
          "limit": 2,
          "total": 192
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
