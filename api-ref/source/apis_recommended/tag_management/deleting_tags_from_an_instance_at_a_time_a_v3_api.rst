:original_name: en-us_topic_0000002332909585.html

.. _en-us_topic_0000002332909585:

Deleting Tags from an Instance at a Time (a V3 API)
===================================================

Function
--------

This API is used to delete tags from an instance at a time.

Constraints
-----------

If the tag to be deleted does not exist, the system deems the deletion operation successful by default. The tag structure in the request body cannot be missing, and the key cannot be left blank or an empty string.

URI
---

POST /v3/{project_id}/instances/{instance_id}/tags/delete

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

   +-----------+-----------+----------------------------------------------------------------------------------------------------------------------------+-------------+
   | Parameter | Mandatory | Type                                                                                                                       | Description |
   +===========+===========+============================================================================================================================+=============+
   | tags      | Yes       | Array of :ref:`DeleteResourceTag <en-us_topic_0000002332909585__en-us_topic_0000002320630453_table10196164513265>` objects | Tag list    |
   +-----------+-----------+----------------------------------------------------------------------------------------------------------------------------+-------------+

.. _en-us_topic_0000002332909585__en-us_topic_0000002320630453_table10196164513265:

.. table:: **Table 4** DeleteResourceTag

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                 |
   +=================+=================+=================+=============================================================================+
   | key             | Yes             | String          | Tag key                                                                     |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------+
   | value           | No              | String          | Tag value                                                                   |
   |                 |                 |                 |                                                                             |
   |                 |                 |                 | This parameter is optional. The value:                                      |
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

Deleting tags from an instance at a time

.. code-block:: text

   POST https://ddm.eu-de.otc.t-systems.com/v3/74f57817ca8f42e19318eb0e0ad41d18/instances/af87aa6635074bd493c6d2106381ecb3in09/tags/delete

   {
     "tags": [
       {
         "key": "test",
         "value": "test"
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
