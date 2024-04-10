:original_name: ddm_api_01_0012.html

.. _ddm_api_01_0012:

Returned Values
===============

Status Code
-----------

After sending a request, you will receive a response, including the status code, response header, and response body.

A status code is a group of digits ranging from 1xx to 5xx. It indicates the status of a response. For more information, see :ref:`Status Codes <ddm_api_01_0060>`.

For example, if status code **201** is returned for calling the API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__, the request is successful.

Response Header
---------------

Similar to a request, a response also has a header, for example, **Content-Type**.

:ref:`Figure 1 <ddm_api_01_0012__fig4865141011511>` shows the response header for the API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__. The **x-subject-token** header field is the desired user token. This token can then be used to authenticate the calling of other APIs.

.. _ddm_api_01_0012__fig4865141011511:

.. figure:: /_static/images/en-us_image_0000001685146158.png
   :alt: **Figure 1** Header fields of the response to the request for obtaining a user token

   **Figure 1** Header fields of the response to the request for obtaining a user token

(Optional) Response Body
------------------------

This part is optional. The body of a response is often returned in structured format (for example, JSON or XML) as specified in the **Content-Type** header field. The response body transfers content except the response header.

For the API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__, the following information is returned. The following describes part of the request body.

.. code-block::

   {
       "token": {
           "expires_at": "2019-02-13T06:52:13.855000Z",
           "methods": [
               "password"
           ],
           "catalog": [
               {
                   "endpoints": [
                       {
                           "region_id": "az-01",
   ......

If an error occurs during API calling, the system returns an error code and message to you. The following shows the format of an error response body:

.. code-block::

   {
       "error_code": "AS.0001",
       "error_msg": "The format of message is error"
   }

In the response body, **error_code** is an error code, and **error_msg** provides information about the error.
