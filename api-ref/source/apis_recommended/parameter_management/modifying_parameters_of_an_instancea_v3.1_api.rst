:original_name: en-us_topic_0000002181623854.html

.. _en-us_topic_0000002181623854:

Modifying Parameters of an Instance (a V3.1 API)
================================================

Function
--------

This API is used to modify parameters of a DDM instance.

Constraints
-----------

The values of the modified parameters must be within the value range defined on the DDM console. For details about the range of parameter values, see "Parameter Template Management" > "Instance Parameters" in *Distributed Database Middleware User Guide*. You can also call the API in :ref:`Obtaining Parameters in a Specified Parameter Template (a V3 API) <ddm_api_01_0106>` to query the value range of a parameter.

URI
---

PUT /v3.1/{project_id}/instances/{instance_id}/configurations

.. table:: **Table 1** URI parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                          |
   +=================+=================+=================+======================================================================================+
   | project_id      | Yes             | String          | Project ID of a tenant in a region                                                   |
   |                 |                 |                 |                                                                                      |
   |                 |                 |                 | For how to obtain a project ID, see :ref:`Obtaining a Project ID <ddm_api_01_0063>`. |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------+
   | instance_id     | Yes             | String          | DDM instance ID                                                                      |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------+

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

   +-----------------+-----------------+--------------------+------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type               | Description                                                                                    |
   +=================+=================+====================+================================================================================================+
   | values          | Yes             | Map<String,String> | Parameter values defined by users based on a default parameter template.                       |
   |                 |                 |                    |                                                                                                |
   |                 |                 |                    | -  **key**: parameter name. If a parameter name is left empty, its value is not to be changed. |
   |                 |                 |                    | -  **value**: indicates the parameter value.                                                   |
   +-----------------+-----------------+--------------------+------------------------------------------------------------------------------------------------+

Example Request
---------------

Changing the value of **long_query_time** to **2**. The value indicates that the query is considered as a slow query if its execution duration is greater than or equal to 2 seconds.

.. code-block:: text

   PUT https://ddm.eu-de.otc.t-systems.com/v3.1/619d3e78f61b4be68bc5aa0b59edcf7b/instances/1f5c9fd6cd984056ba89c8c87cc03278in09/configurations

   {
     "values" : {
       "long_query_time" : "2"
     }
   }

Response
--------

-  Normal response

   .. table:: **Table 4** Response body parameters

      ============ ======= ==========================================
      Parameter    Type    Description
      ============ ======= ==========================================
      need_restart Boolean Whether the instance needs to be restarted
      ============ ======= ==========================================

-  Normal response example

   .. code-block::

      {
        "need_restart": false
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
