:original_name: ddm_api_01_0026.html

.. _ddm_api_01_0026:

Scaling In a DDM instance
=========================

Function
--------

This API is used to remove nodes from a specified DDM instance.

Constraints
-----------

Make sure that the associated RDS instances are available and not undergoing other operations.

URI
---

POST /v2/{project_id}/instances/{instance_id}/action/reduce

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

.. table:: **Table 3** Request body parameters

   +-------------+-----------+---------+---------------------------------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type    | Description                                                                                                                     |
   +=============+===========+=========+=================================================================================================================================+
   | node_number | Yes       | Integer | Number of nodes to be removed. The maximum value is the instance nodes minus 1.                                                 |
   +-------------+-----------+---------+---------------------------------------------------------------------------------------------------------------------------------+
   | group_id    | No        | String  | Group ID, which specifies the group that is scaled out. This parameter must be specified if there are more than one node group. |
   +-------------+-----------+---------+---------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   ============ ====== =================
   Parameter    Type   Description
   ============ ====== =================
   instanceId   String DDM instance ID
   instanceName String DDM instance name
   jobId        String Task ID
   ============ ====== =================

**Status code: 400**

.. table:: **Table 5** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

**Status code: 500**

.. table:: **Table 6** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

Example Request
---------------

-  Example request

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/action/reduce

      {
        "node_number" : 2
      }

-  Example request where the DDM instance has more than one group

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/action/reduce

      {
        "group_id" : "f080abf2010d45118068c28c8958f5fcgr09",
        "node_number" : 1
      }

Example Response
----------------

**Status code: 200**

ok

.. code-block::

   {
     "instanceId" : "28e8841d0b9c4f6a9a30742ee60e1068in09",
     "instanceName" : "ddm-test",
     "jobId" : "1eb697c0-1842-43a3-8671-f562d0385cb9"
   }

**Status code: 400**

bad request

.. code-block::

   {
     "externalMessage" : "Parameter error.",
     "errCode" : "DBS.280001"
   }

**Status code: 500**

server error

.. code-block::

   {
     "externalMessage" : "Server failure.",
     "errCode" : "DBS.200412"
   }

Status Codes
------------

=========== ============
Status Code Description
=========== ============
200         ok
400         bad request
500         server error
=========== ============

Error Codes
-----------

For details, see :ref:`Error Codes <ddm_api_01_0061>`.
