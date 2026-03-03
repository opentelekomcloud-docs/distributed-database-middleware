:original_name: ddm_api_01_0112.html

.. _ddm_api_01_0112:

Obtaining Information About a Task with a Specified ID (a V3 API)
=================================================================

Function
--------

This API is used to obtain information about a task with a specified ID in the DDM task center.

Constraints
-----------

None

URI
---

-  URL format

   GET /v3/{project_id}/jobs/{job_id}

-  Parameter description

   .. table:: **Table 1** Parameter descriptions

      ========== ========= ====== ===================================
      Parameter  Mandatory Type   Description
      ========== ========= ====== ===================================
      project_id Yes       String Project ID of a tenant in a region.
      job_id     Yes       String Task ID
      ========== ========= ====== ===================================

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

Obtaining information about a task with a specified ID

.. code-block:: text

   GET https://ddm.eu-de.otc.t-systems.com/v3/619d3e78f61b4be68bc5aa0b59edcf7b/31b8ae23-c687-4d80-b7b4-42a66c9bb886

Response
--------

-  Normal response

   .. table:: **Table 3** Response body parameters

      +-----------+-------------------------------------------------------------------------------------+-------------------+
      | Parameter | Type                                                                                | Description       |
      +===========+=====================================================================================+===================+
      | job       | :ref:`JobInfo <ddm_api_01_0112__response_getinstanceenginesdetailsresponse>` object | Task information. |
      +-----------+-------------------------------------------------------------------------------------+-------------------+

   .. _ddm_api_01_0112__response_getinstanceenginesdetailsresponse:

   .. table:: **Table 4** JobInfo

      +-----------------------+--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Type                                                         | Description                                                                                                                                                                                 |
      +=======================+==============================================================+=============================================================================================================================================================================================+
      | id                    | String                                                       | Task ID                                                                                                                                                                                     |
      +-----------------------+--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | name                  | String                                                       | Task name                                                                                                                                                                                   |
      |                       |                                                              |                                                                                                                                                                                             |
      |                       |                                                              | For details, see :ref:`Task Statuses <ddm_api_01_0064__section1820916618277>`.                                                                                                              |
      +-----------------------+--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | status                | String                                                       | Task execution status. The value can be:                                                                                                                                                    |
      |                       |                                                              |                                                                                                                                                                                             |
      |                       |                                                              | **Running**: The task is being executed. **Completed**: The task is successfully executed. **Failed**: The task fails to be executed.                                                       |
      +-----------------------+--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | created_time          | String                                                       | Creation time in the "yyyy-mm-ddThh:mm:ssZ" format.                                                                                                                                         |
      |                       |                                                              |                                                                                                                                                                                             |
      |                       |                                                              | **T** is the separator between the calendar and the hourly notation of time. **Z** indicates the time zone offset. For example, in the Central European time zone, the offset is **+0100**. |
      +-----------------------+--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | end_time              | String                                                       | End time. The format is yyyy-mm-ddThh:mm:ssZ.                                                                                                                                               |
      |                       |                                                              |                                                                                                                                                                                             |
      |                       |                                                              | **T** is the separator between the calendar and the hourly notation of time. **Z** indicates the time zone offset. For example, in the Central European time zone, the offset is **+0100**. |
      +-----------------------+--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | process               | String                                                       | Task execution progress                                                                                                                                                                     |
      |                       |                                                              |                                                                                                                                                                                             |
      |                       |                                                              | The execution progress (such as **"60%"**, indicating the task execution progress is 60%) is displayed only when the task is being executed. Otherwise, **""** is returned.                 |
      +-----------------------+--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | instance              | :ref:`Instance <ddm_api_01_0112__table1984917222610>` object | Instance on which the task is executed                                                                                                                                                      |
      +-----------------------+--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. _ddm_api_01_0112__table1984917222610:

   .. table:: **Table 5** Instance

      ========= ====== =============
      Parameter Type   Description
      ========= ====== =============
      id        String Instance ID
      name      String Instance name
      ========= ====== =============

-  Normal response example

   .. code-block::

      {
          "job": {
              "id": "31b8ae23-c687-4d80-b7b4-42a66c9bb886",
              "name": "CreateInstance",
              "status": "Running",
              "created_time": "2018-08-06T10:41:14+0100",
              "end_time": "2018-08-06T16:41:14+0100",
              "process": "60%",
              "instance": {
                  "id": "a48e43ff268f4c0e879652d65e63d0fbin09",
                  "name": "DDM-test"
              }
          }
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
