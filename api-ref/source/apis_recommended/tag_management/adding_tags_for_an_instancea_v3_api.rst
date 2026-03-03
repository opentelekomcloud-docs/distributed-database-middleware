:original_name: en-us_topic_0000002298790240.html

.. _en-us_topic_0000002298790240:

Adding Tags for an Instance (a V3 API)
======================================

Function
--------

This API is used to add tags for an instance.

Constraints
-----------

A maximum of 20 tags can be added for an instance. The tag key must be unique.

If the request body contains duplicated keys, an error message will be reported when the API is called.

If the key in the request body is the same as an existing key in a specified instance, the value of the **value** parameter that corresponds to the existing key is overwritten.

URI
---

POST /v3/{project_id}/instances/{instance_id}/tags/create

.. table:: **Table 1** Path parameters

   =========== ========= ====== ==================================
   Parameter   Mandatory Type   Description
   =========== ========= ====== ==================================
   project_id  Yes       String Project ID of a tenant in a region
   instance_id Yes       String Instance ID
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

   +-----------+-----------+----------------------------------------------------------------------------------------------------------------------+-------------+
   | Parameter | Mandatory | Type                                                                                                                 | Description |
   +===========+===========+======================================================================================================================+=============+
   | tags      | Yes       | Array of :ref:`ResourceTag <en-us_topic_0000002298790240__en-us_topic_0000002286061168_table10196164513265>` objects | Tag list    |
   +-----------+-----------+----------------------------------------------------------------------------------------------------------------------+-------------+

.. _en-us_topic_0000002298790240__en-us_topic_0000002286061168_table10196164513265:

.. table:: **Table 4** ResourceTag

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                   |
   +=================+=================+=================+===============================================================================================+
   | key             | Yes             | String          | Tag key                                                                                       |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 | This parameter is mandatory and cannot be left empty. The key:                                |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 | -  Must be unique for each instance.                                                          |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 | -  Can contain 1 to 36 characters.                                                            |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 | -  Cannot be an empty string or start with **\_sys\_**, and cannot start or end with a space. |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 | -  Cannot contain:                                                                            |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 |    Non-printable ASCII characters (0-31), "``*``", "<", ">", "\\", ",", "|", "/"              |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------+
   | value           | Yes             | String          | Tag value                                                                                     |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 | This parameter is mandatory. The value:                                                       |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 | -  Is an empty string by default if it is not set.                                            |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 | -  Can contain 0 to 43 characters.                                                            |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 | -  Cannot contain the following characters:                                                   |
   |                 |                 |                 |                                                                                               |
   |                 |                 |                 |    Non-printable ASCII characters (0-31), "``*``", "<", ">", "\\", ",", "|"                   |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------+

Example Request
---------------

Adding tags for an instance

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/74f57817ca8f42e19318eb0e0ad41d18/instances/2f0324a93859487eb5566d75951fcd2din09/tags/create

   {
     "tags": [
       {
         "key": "key",
         "value": "value"
       }
     ]
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
