:original_name: ddm_api_01_0011.html

.. _ddm_api_01_0011:

Authentication
==============

Token authentication is required to call APIs.

Authentication using tokens: General requests are authenticated using tokens.

Token-based Authentication
--------------------------

.. note::

   The validity period of a token is 24 hours. If a token is required, the system caches the token to avoid frequent calling.

A token specifies temporary permissions in a computer system. Token-based authentication adds a token in a request as its header during API calling to obtain the permissions for operating APIs on IAM.

.. code-block::

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
                    "name": "xxxxxxxx"
                }
            }
        }
    }

In :ref:`Making an API Request <ddm_03_0002>`, the process of calling the API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__ is described.

After obtaining the token, add the **X-Auth-Token** header in a request to specify the token when calling other APIs. For example, if the token is **ABCDEFJ....**, **X-Auth-Token: ABCDEFJ....** can be added to a request as follows:

.. code-block:: text

   POST https://{{Endpoint}}/v3/auth/projects
   Content-Type: application/json
   X-Auth-Token: ABCDEFJ....
