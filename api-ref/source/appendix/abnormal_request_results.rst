:original_name: ddm_api_01_0059.html

.. _ddm_api_01_0059:

Abnormal Request Results
========================

Abnormal Response
-----------------

.. table:: **Table 1** Parameter description

   +-----------------+--------+---------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type   | Description                                                                                                         |
   +=================+========+=====================================================================================================================+
   | errCode         | String | Returned error code when a task submission exception occurs. For details, see :ref:`Error Codes <ddm_api_01_0061>`. |
   +-----------------+--------+---------------------------------------------------------------------------------------------------------------------+
   | externalMessage | String | Description of the error returned when a task submission exception occurs.                                          |
   +-----------------+--------+---------------------------------------------------------------------------------------------------------------------+

Example Response
----------------

.. code-block:: text

   {
        "errCode": "DBS.300101",
        "externalMessage": "Failed to delete the schema"
   }
