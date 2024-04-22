:original_name: ddm_06_0036.html

.. _ddm_06_0036:

Changing a Database Port
========================

Scenarios
---------

DDM allows you to change the database port of a DDM instance. After the port is changed, the instance will restart.

Procedure
---------

#. Log in to the DDM console, choose **Instances** in the navigation pane, locate the instance whose database port you want to change, and click its name.

#. In the **Connection Information** area on the **Basic Information** page, click |image1| besides **Database Port**.

   For DDM instances, the database port number ranges from 1025 to 65534 except for ports 1033, 7009, 8888, and 12017 because they are in use by DDM. The default value is **5066**.

   -  Click |image2|.

      Changing the database port requires a restart of the DDM instance. To continue the change, click **Yes** in the displayed dialog box. To cancel the change, click **No**.

   -  To cancel the change, click |image3|.

#. View the results on the **Basic Information** page.

.. |image1| image:: /_static/images/en-us_image_0000001685307214.png
.. |image2| image:: /_static/images/en-us_image_0000001733266389.png
.. |image3| image:: /_static/images/en-us_image_0000001733266393.png
