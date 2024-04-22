:original_name: ddm_api_01_0060.html

.. _ddm_api_01_0060:

Status Codes
============

Normal
------

:ref:`Table 1 <ddm_api_01_0060__table11812530035>` lists the status codes that may be returned.

.. _ddm_api_01_0060__table11812530035:

.. table:: **Table 1** Normal status codes

   =========== ======= ===================================================
   Status Code Message Description
   =========== ======= ===================================================
   200         OK      The request has been processed successfully.
   202         OK      The asynchronous request is submitted successfully.
   =========== ======= ===================================================

Abnormal
--------

:ref:`Table 2 <ddm_api_01_0060__table3690182516187>` lists the status codes that may be returned.

.. _ddm_api_01_0060__table3690182516187:

.. table:: **Table 2** Abnormal status codes

   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
   | Status Code           | Message                  | Description                                                                                                   |
   +=======================+==========================+===============================================================================================================+
   | 400                   | Bad Request              | The server fails to process the request. The possible causes are as follows:                                  |
   |                       |                          |                                                                                                               |
   |                       |                          | -  The request could not be parsed by the server due to incorrect syntax.                                     |
   |                       |                          | -  Request parameters are incorrect.                                                                          |
   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
   | 401                   | Unauthorized             | Necessary credentials (for example, username and password) required for user authentication are not provided. |
   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
   | 403                   | Forbidden                | You are forbidden to access the page requested.                                                               |
   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
   | 404                   | Not Found                | The request failed because the requested resource could not be found on the server.                           |
   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
   | 405                   | Method Not Allowed       | You are not allowed to use the method specified in the request.                                               |
   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
   | 409                   | Conflict                 | The request could not be processed due to a conflict with the current resource status.                        |
   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
   | 413                   | Request Entity Too Large | The requested resource exceeds the resource quota.                                                            |
   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
   | 415                   | Unsupported Media Type   | **ContentType** contained in the request header is neither **application** nor **json**.                      |
   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
   | 500                   | Internal Server Error    | The request is not completed due to a service error.                                                          |
   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
   | 501                   | Not Implemented          | The request is not completed because the server does not support the requested function.                      |
   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
   | 503                   | Service Unavailable      | The request could not be processed by the server because the server is being maintained or overloaded.        |
   +-----------------------+--------------------------+---------------------------------------------------------------------------------------------------------------+
