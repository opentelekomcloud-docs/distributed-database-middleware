:original_name: en-us_topic_0000002298790216.html

.. _en-us_topic_0000002298790216:

Creating a Parameter Group (a V3 API)
=====================================

Function
--------

This API is used to create a parameter group.

Constraints
-----------

None

URI
---

POST /v3/{project_id}/configurations

.. table:: **Table 1** Path parameters

   ========== ====== ========= ==================================
   Parameter  Type   Mandatory Description
   ========== ====== ========= ==================================
   project_id String Yes       Project ID of a tenant in a region
   ========== ====== ========= ==================================

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
   | Content-Type    | Yes             | String          | MIME type of the request body. Value range:                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | -  application/json                                                                                                  |
   |                 |                 |                 | -  application/json;charset=utf-8                                                                                    |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                          |
   +=================+=================+=================+======================================================================================================================================================+
   | name            | Yes             | String          | Parameter group name                                                                                                                                 |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description     | Yes             | String          | Parameter group description                                                                                                                          |
   |                 |                 |                 |                                                                                                                                                      |
   |                 |                 |                 | If the description contains more than 256 characters, the parameter group can still be created. The first 256 characters will be automatically used. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

Creating a parameter group

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/74f57817ca8f42e19318eb0e0ad41d18/configurations
   {
     "name": "param1688972688",
     "description": "test"
   }

Response
--------

-  Normal response

   .. table:: **Table 4** Response body parameters

      ========= ====== ====================
      Parameter Type   Description
      ========= ====== ====================
      id        String Parameter group ID
      name      String Parameter group name
      ========= ====== ====================

-  Normal response example

   .. code-block::

      {
        "id": "404f3bbb8a724f7697e7fb15a1b09370pr09",
        "name": "param1688972688"
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
