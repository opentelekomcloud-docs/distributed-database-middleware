:original_name: ddm_03_0002.html

.. _ddm_03_0002:

Making an API Request
=====================

This section describes the structure of a REST API and how to call an API. Before calling an API, you need to `obtain the user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__ using the IAM API.

Request URI
-----------

A request URI is in the following format:

**{URI-scheme} :// {Endpoint} / {resource-path} ? {query-string}**

Although a request URI is a part of a request header, most programming languages or frameworks require the request URI to be separately transmitted, rather than being conveyed in a request message.

.. table:: **Table 1** URI parameter description

   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter     | Description                                                                                                                                                                                                                                                                                           |
   +===============+=======================================================================================================================================================================================================================================================================================================+
   | URI-scheme    | Protocol used to transmit requests. All APIs use HTTPS.                                                                                                                                                                                                                                               |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Endpoint      | Domain name or IP address of the server bearing the REST service endpoint. The endpoint varies depending on the service and service region. *Endpoint*: Endpoint of the **Objective-func** function. For details, see `Regions and Endpoints <https://docs.otc.t-systems.com/endpoint/index.html>`__. |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource-path | Access path of an API for performing a specified operation. Obtain the path from the URI of an API. For example, the **resource-path** of the API used to obtain a user token is **/v3/auth/tokens**.                                                                                                 |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Query string  | Query parameter, which is optional. Ensure that a question mark (?) is included before each query parameter that is in the format of "Parameter name=Parameter value". For example, **? limit=10** indicates that a maximum of 10 data records will be displayed.                                     |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   To simplify the URI display, each API is provided only with a resource-path and a request method. This is because the **URI-scheme** value of all APIs is **HTTPS**, and the endpoints in a region are the same. Therefore, the two parts are omitted.

Request Method
--------------

HTTP methods, which are also called operations or actions, specify the type of operations that you are requesting.

.. table:: **Table 2** HTTP methods

   +-----------------------------------+--------------------------------------------------------------------------+
   | Method                            | Description                                                              |
   +===================================+==========================================================================+
   | GET                               | Requests a server to return specified resources.                         |
   +-----------------------------------+--------------------------------------------------------------------------+
   | PUT                               | Requests a server to update specified resources.                         |
   +-----------------------------------+--------------------------------------------------------------------------+
   | POST                              | Requests the server to add a resource or perform special operations.     |
   +-----------------------------------+--------------------------------------------------------------------------+
   | DELETE                            | Requests a server to delete specified resources, for example, an object. |
   +-----------------------------------+--------------------------------------------------------------------------+
   | PATCH                             | Requests a server to update partial content of a specified resource.     |
   |                                   |                                                                          |
   |                                   | If the resource does not exist, a new resource will be created.          |
   +-----------------------------------+--------------------------------------------------------------------------+

For example, for the URI of the API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__, the request method is POST. The request is as follows:

.. code-block:: text

   POST https://{{Endpoint}}/v3/auth/tokens

Request Headers
---------------

You can also add additional header fields to a request, such as the fields required by a specified URI or HTTP method. For example, to request for the authentication information, add **Content-Type**, which specifies the request body type.

You can also add additional fields to the request header, for example, the fields required by a specified URI and an HTTP method. :ref:`Table 3 <ddm_03_0002__en-us_topic_0121682347_table1986821153312>` lists common request header fields.

.. _ddm_03_0002__en-us_topic_0121682347_table1986821153312:

.. table:: **Table 3** Common request headers

   +-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+--------------------------------------------+
   | Field           | Description                                                                                                                                                                           | Mandatory                                                                              | Example                                    |
   +=================+=======================================================================================================================================================================================+========================================================================================+============================================+
   | Content-Type    | MIME type of the request body. You are advised to use the default value **application/json**. For APIs used to upload objects or images, the value varies depending on the flow type. | Yes                                                                                    | application/json                           |
   +-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+--------------------------------------------+
   | Content-Length  | Length of the request body. The unit is byte.                                                                                                                                         | This parameter is optional for POST requests, but must be left blank for GET requests. | 3495                                       |
   +-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+--------------------------------------------+
   | X-Project-Id    | Project ID. Obtain the project ID by following the instructions in :ref:`Obtaining a Project ID <ddm_api_01_0063>`.                                                                   | No                                                                                     | e9993fc787d94b6c886cbaa340f9c0f4           |
   +-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+--------------------------------------------+
   | X-Auth-Token    | User token                                                                                                                                                                            | Yes                                                                                    | The following is part of an example token: |
   |                 |                                                                                                                                                                                       |                                                                                        |                                            |
   |                 | After the request is processed, the value of **X-Subject-Token** in the header is the token value.                                                                                    |                                                                                        | MIIPAgYJKoZIhvcNAQcCo...ggg1BBIINPXsidG9rZ |
   +-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+--------------------------------------------+

The API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__ does not require authentication. Therefore, this API only requires adding the **Content-Type** field. The request with the added **Content-Type** header is as follows:

.. code-block:: text

   POST https://{{endpoint}}/v3/auth/tokens
   Content-Type: application/json

(Optional) Request Body
-----------------------

This part is optional. The body of a request is often sent in a structured format (for example, JSON or XML) as specified in the **Content-Type** header field.

The request body varies depending on APIs. Some APIs do not require the request body, such as the APIs requested using GET and DELETE methods.

For the API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__, the request parameters and parameter description can be obtained in the API request. The following provides an example request with a body included. Replace **username**, **domainname**, **\*******\*** (login password), and **xxxxxxxxxxxxxxxxxx** (project name) with actual values. You can obtain the values from `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.

.. note::

   The **scope** parameter specifies where a token takes effect. You can set **scope** to an account or a project under an account. In the following example, the token takes effect only for the resources in a specified project.

.. code-block::

   POST https://{{endpoint}}/v3/auth/tokens
   Content-Type: application/json

   {
       "auth": {
           "identity": {
               "methods": [
                   "password"
               ],
               "password": {
                   "user": {
                       "name": "username",
                       "password": "********",
                       "domain": {
                           "name": "domainname"
                       }
                   }
               }
           },
           "scope": {
               "project": {
                   "name": "xxxxxxxxxxxxxxxxxx"
               }
           }
       }
   }

If all data required for the API request is available, you can send the request to call the API through `curl <https://curl.haxx.se/>`__, `Postman <https://www.getpostman.com/>`__, or coding. For the API of obtaining a user token, **x-subject-token** in the response header is the required user token. This token can then be used to authenticate the calling of other APIs.

Initiating Requests
-------------------

You can initiate a request based on the constructed request message in one of the following ways:

-  cURL

   cURL is a command-line tool used to perform URL operations and transmit information. It serves as an HTTP client that can send HTTP requests to the server and receive response messages. cURL is used for API debugging. For more information about cURL, visit https://curl.haxx.se/.

   .. note::

      For security purposes, run the **curl** command on the server to query information, and then clear operation records, including but not limited to records in the **~/.bash_history** and **/var/log/messages** directories (if any).

-  Code

   You can call APIs using code to assemble, send, and process request messages.

-  REST client

   Both Mozilla Firefox and Google Chrome provide a graphical browser plug-in, REST client, to send and process requests. For Mozilla Firefox, see `Firefox REST Client <https://addons.mozilla.org/en-US/firefox/addon/restclient/>`__. For Google Chrome, see `Chrome REST Client <https://chrome.google.com/webstore/detail/postman-interceptor/aicmkgpgakddgnaphhhpliifpcfhicfo/?hl=en>`__.
