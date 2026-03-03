:original_name: en-us_topic_0000002332869385.html

.. _en-us_topic_0000002332869385:

Changing an Instance Tag (a V3 API)
===================================

Function
--------

This API is used to change an instance tag.

Constraints
-----------

None

URI
---

PUT /v3/{project_id}/instances/{instance_id}/tags/{key}

.. table:: **Table 1** Path parameters

   =========== ========= ====== ==================================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ==================================
   project_id  Yes       String Project ID of a tenant in a region
   instance_id Yes       String Instance ID
   key         Yes       String Tag key
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
   | Content-Type    | Yes             | String          | MIME type of the request body. Value range:                                                                          |
   |                 |                 |                 |                                                                                                                      |
   |                 |                 |                 | -  application/json                                                                                                  |
   |                 |                 |                 | -  application/json;charset=utf-8                                                                                    |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                 |
   +=================+=================+=================+=============================================================================+
   | value           | Yes             | String          | Tag value. The value:                                                       |
   |                 |                 |                 |                                                                             |
   |                 |                 |                 | -  Is an empty string by default if it is not set.                          |
   |                 |                 |                 |                                                                             |
   |                 |                 |                 | -  Can contain 0 to 43 characters.                                          |
   |                 |                 |                 |                                                                             |
   |                 |                 |                 | -  Cannot contain the following characters:                                 |
   |                 |                 |                 |                                                                             |
   |                 |                 |                 |    Non-printable ASCII characters (0-31), "``*``", "<", ">", "\\", ",", "|" |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------+

Example Request
---------------

Changing an instance tag

.. code-block:: text

   PUT https://ddm.eu-de.otc.t-systems.com/v3/74f57817ca8f42e19318eb0e0ad41d18/instances/2f0324a93859487eb5566d75951fcd2din09/tags/key

   {
     "value": "value"
   }

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
