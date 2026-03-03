:original_name: ddm_api_01_0114.html

.. _ddm_api_01_0114:

Enabling or Disabling SSL (a V3 API)
====================================

Function
--------

This API is used to configure SSL to encrypt connections.

Constraints
-----------

None

URI
---

POST /v3/{project_id}/instances/{instance_id}/switch-ssl

.. table:: **Table 1** Path parameters

   =========== ========= ====== ===================================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ===================================
   project_id  Yes       String Project ID of a tenant in a region.
   instance_id Yes       String DDM instance ID.
   =========== ========= ====== ===================================

Request
-------

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

.. table:: **Table 3** Request body parameters

   +-----------------+-----------------+-----------------+-----------------------------+
   | Parameter       | Mandatory       | Type            | Description                 |
   +=================+=================+=================+=============================+
   | ssl_enabled     | Yes             | Boolean         | **true**: SSL is enabled.   |
   |                 |                 |                 |                             |
   |                 |                 |                 | **false**: SSL is disabled. |
   +-----------------+-----------------+-----------------+-----------------------------+

Example Request
---------------

Enabling SSL

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/switch-ssl
   {
     "ssl_enabled" : true
   }

Response Parameters
-------------------

-  Normal response

   .. table:: **Table 4** Response body parameters

      ========= ====== ===========
      Parameter Type   Description
      ========= ====== ===========
      job_id    String Job ID.
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
