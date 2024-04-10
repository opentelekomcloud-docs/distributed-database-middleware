:original_name: ddm_api_01_0083.html

.. _ddm_api_01_0083:

Querying Details of a DDM Instance Node
=======================================

Function
--------

This API is used to query details of a DDM instance node.

Constraints
-----------

None

URI
---

GET /v1/{project_id}/instances/{instance_id}/nodes/{node_id}

.. table:: **Table 1** Path parameters

   =========== ========= ====== ==================================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ==================================
   project_id  Yes       String Project ID of a tenant in a region
   instance_id Yes       String DDM instance ID
   node_id     Yes       String DDM instance node ID
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

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------------+--------+---------------------------------------------------------------------------+
   | Parameter       | Type   | Description                                                               |
   +=================+========+===========================================================================+
   | status          | String | Node status For details, see :ref:`Status Description <ddm_api_01_0064>`. |
   +-----------------+--------+---------------------------------------------------------------------------+
   | name            | String | Node name                                                                 |
   +-----------------+--------+---------------------------------------------------------------------------+
   | node_id         | String | Node ID                                                                   |
   +-----------------+--------+---------------------------------------------------------------------------+
   | private_ip      | String | Private IP address of the node                                            |
   +-----------------+--------+---------------------------------------------------------------------------+
   | floating_ip     | String | Floating IP address of the node                                           |
   +-----------------+--------+---------------------------------------------------------------------------+
   | server_id       | String | VM ID                                                                     |
   +-----------------+--------+---------------------------------------------------------------------------+
   | subnet_name     | String | Subnet name                                                               |
   +-----------------+--------+---------------------------------------------------------------------------+
   | datavolume_id   | String | Data disk ID                                                              |
   +-----------------+--------+---------------------------------------------------------------------------+
   | res_subnet_ip   | String | IP address provided by the resource subnet                                |
   +-----------------+--------+---------------------------------------------------------------------------+
   | systemvolume_id | String | System disk ID                                                            |
   +-----------------+--------+---------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 4** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

**Status code: 500**

.. table:: **Table 5** Response body parameters

   =============== ====== ==================
   Parameter       Type   Description
   =============== ====== ==================
   errCode         String Service error code
   externalMessage String Error message
   =============== ====== ==================

Example Request
---------------

.. code-block:: text

   GET https://{endpoint}/v1/{project_id}/instances/{instance_id}/nodes/{node_id}

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "status" : "normal",
     "name" : "ddm2-test_node_01",
     "node_id" : "4a2b97b7f5e3462c9c78aae93b46ed83no09",
     "private_ip" : "192.168.0.160",
     "floating_ip" : "100.65.78.158",
     "server_id" : "8bd4d0bd-f63e-489a-95b6-50351f9657e6",
     "subnet_name": "manageSubnet",
     "datavolume_id" : "30ade9fb-26de-4d1f-af08-c376974b9d86",
     "res_subnet_ip" : "172.16.15.224",
     "systemvolume_id" : "88d7de55-f886-4929-ae7c-04d842959700"
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
