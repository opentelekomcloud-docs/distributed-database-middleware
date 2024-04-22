:original_name: ddm_03_0036.html

.. _ddm_03_0036:

Using NEXTVAL or CURRVAL to Query Global Sequence Numbers
=========================================================

-  NEXTVAL returns the next sequence number, and CURRVAL returns the current sequence number. nextval(n) returns *n* unique sequence numbers.
-  nextval(n) can be used only in **select sequence.nextval(n)** and does not support cross-schema operations.
-  currval(n) is not supported.

Procedure
---------

#. Log in to the required DDM instance using a client.

#. Open the required schema.

#. Run the following command to create a global sequence:

   **create sequence seq_test**;

   |image1|

#. Run the following command to obtain the next sequence number:

   **select seq_test.nextval;**

   |image2|

#. Run the following command to obtain the current sequence number:

   **select seq_test.currval**;

   |image3|

#. Run the following command to obtain sequence numbers in batches:

   **select seq_test.nextval(n)**;

   |image4|

   .. note::

      -  Cross-schema operations are not supported when sequence numbers are obtained in batches.
      -  If no global sequence is used, CURRVAL returns **0**.

.. |image1| image:: /_static/images/en-us_image_0000001685147566.png
.. |image2| image:: /_static/images/en-us_image_0000001733146373.png
.. |image3| image:: /_static/images/en-us_image_0000001685147570.png
.. |image4| image:: /_static/images/en-us_image_0000001733146381.png
