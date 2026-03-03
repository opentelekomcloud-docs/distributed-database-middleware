:original_name: en-us_topic_0000002298949892.html

.. _en-us_topic_0000002298949892:

Querying Instance Tags (a V3 API)
=================================

Function
--------

This API is used to query instance tags.

Constraints
-----------

None

URI
---

GET /v3/{project_id}/instances/{instance_id}/tags

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

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | X-Auth-Token    | Yes             | String          | User token.                                                                  |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | You can obtain the token by calling the IAM API used to obtain a user token. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Example Request
---------------

Querying instance tags

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/74f57817ca8f42e19318eb0e0ad41d18/instances/2f0324a93859487eb5566d75951fcd2din09/tags

Response
--------

-  Normal response

.. table:: **Table 3** Response body parameters

   +-----------+-------------------------------------------------------------------------------------------------------------------------------------+-------------+
   | Parameter | Type                                                                                                                                | Description |
   +===========+=====================================================================================================================================+=============+
   | tags      | Array of :ref:`QueryInstanceTagInfo <en-us_topic_0000002298949892__en-us_topic_0000002320557369_response_enginegroupsinfo>` objects | Tag list    |
   +-----------+-------------------------------------------------------------------------------------------------------------------------------------+-------------+

.. _en-us_topic_0000002298949892__en-us_topic_0000002320557369_response_enginegroupsinfo:

.. table:: **Table 4** QueryInstanceTagInfo

   ========= ====== ===========
   Parameter Type   Description
   ========= ====== ===========
   key       String Tag key
   value     String Tag value
   ========= ====== ===========

-  Normal response example

.. code-block::

   {
     "tags": [
       {
         "key": "test",
         "value": "1"
       }
     ]
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
