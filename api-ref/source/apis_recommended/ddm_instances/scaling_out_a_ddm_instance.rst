:original_name: ddm_api_01_0025.html

.. _ddm_api_01_0025:

Scaling Out a DDM Instance
==========================

Function
--------

This API is used to scale out a specified DDM instance.

Constraints
-----------

Make sure that the associated RDS instances are available and not undergoing other operations.

URI
---

POST /v2/{project_id}/instances/{instance_id}/action/enlarge

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

   +-------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type    | Description                                                                                                                          |
   +=============+===========+=========+======================================================================================================================================+
   | flavor_id   | Yes       | String  | Flavor ID of the VM for deploying the DDM instance that is to be scaled out                                                          |
   +-------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------+
   | node_number | Yes       | Integer | Number of nodes to be added                                                                                                          |
   +-------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------+
   | group_id    | No        | String  | Group ID, which specifies the node group that is scaled out. This parameter must be specified if there are more than one node group. |
   +-------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------+
   | is_auto_pay | No        | Boolean | The function has not been supported, and this field is reserved.                                                                     |
   +-------------+-----------+---------+--------------------------------------------------------------------------------------------------------------------------------------+

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

      POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/action/enlarge

      {
        "flavor_id" : "8f2e696c-a9c1-30bd-af90-25522bc67606",
        "node_number" : 1
      }

-  Example request where the DDM instance has more than one group

   .. code-block:: text

      POST https://{endpoint}/v2/{project_id}/instances/{instance_id}/action/enlarge

      {
        "flavor_id" : "8f2e696c-a9c1-30bd-af90-25522bc67606",
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
     "instanceName" : "BUG-ddm-fb88-test",
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
