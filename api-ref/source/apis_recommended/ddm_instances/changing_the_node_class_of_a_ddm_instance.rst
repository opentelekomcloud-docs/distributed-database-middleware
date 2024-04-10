:original_name: ddm_api_01_0017.html

.. _ddm_api_01_0017:

Changing the Node Class of a DDM Instance
=========================================

Function
--------

This API is used to change the node class of a DDM instance.

Constraints
-----------

-  The node class can be changed only when the corresponding DDM instance is normal.
-  The new node class cannot be the same as the original one.
-  Node classes of c6s series cannot be changed to those classes of c6 series.

URI
---

PUT /v3/{project_id}/instances/{instance_id}/flavor

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
   | x-auth-token    | Yes             | String          | User token.                                                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | It can be obtained by calling an IAM API. The value of **X-Subject-Token** in the response header is the user token. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-------------+-----------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type    | Description                                                                                                                                                                                                                                     |
   +=============+===========+=========+=================================================================================================================================================================================================================================================+
   | spec_code   | Yes       | String  | Resource specification code of the new node class                                                                                                                                                                                               |
   +-------------+-----------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | group_id    | No        | String  | This parameter is not required if the instance has only one node group. Each instance has one node group by default. If you need to create multiple node groups, set this parameter to the ID of the group whose node class you want to change. |
   +-------------+-----------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | is_auto_pay | No        | Boolean | The function has not been supported, and this field is reserved.                                                                                                                                                                                |
   +-------------+-----------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   ========= ====== =======================================
   Parameter Type   Description
   ========= ====== =======================================
   job_id    String ID of the task for changing node class.
   ========= ====== =======================================

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

.. code-block:: text

   PUT https://{endpoint}/v3/{project_id}/instances/{instance_id}/flavor

   {
     "spec_code" : "ddm.8xlarge.2",
     "group_id" : "3e5a9063d3b84729b0a3310fad3a0942gr09"
     }

Example Response
----------------

**Status code: 200**

ok

.. code-block::

   {
     "job_id" : "2x414788a5112333a02390e2eb0ea227"
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
200         OK
400         bad request
500         server error
=========== ============

Error Codes
-----------

For details, see :ref:`Error Codes <ddm_api_01_0061>`.
