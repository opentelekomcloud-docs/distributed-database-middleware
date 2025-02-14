:original_name: ddm_06_0041.html

.. _ddm_06_0041:

Configuring SSL
===============

Secure Socket Layer (SSL) is an encryption-based Internet security protocol for establishing secure links between a server and a client. It provides privacy, authentication, and integrity to Internet communications. SSL:

-  Authenticates users and servers, ensuring that data is sent to the correct clients and servers.
-  Encrypts data to prevent it from being intercepted during transfer.
-  Ensures data integrity during transmission

SSL is disabled for new DDM instances by default. Enabling SSL increases CPU usage and makes it take a little longer to establish a network connection, so you are advised to evaluate these impacts on service performance before enabling SSL.

You can connect to a DDM schema through a client using an SSL or non-SSL connection.

-  If SSL is enabled, you can connect to a DDM schema using an SSL or non-SSL connection. SSL encrypts connections to the DB instance, making in-transit data more secure.
-  If SSL is disabled, you can only connect to a DDM schema using a non-SSL connection.

   .. important::

      Enabling or disabling SSL will cause instances to reboot and interrupt connections. Exercise caution when performing this operation.

Enabling SSL
------------

#. On the **Instances** page, locate the instance that you want to connect to and click its name.

#. On the **Basic Information** page, at the **Instance Information** area, click |image1| in the **SSL** field.

#. In the displayed dialog box, click **Yes**.

#. On the **Basic Information** page, view the results. Click |image2| next to the **SSL** field to download the CA certificate.

   You can use SSL to connect to a schema. For details, see :ref:`Step 4: Log In to the DDM Schema <ddm_02_0005>`.

Disabling SSL
-------------

#. On the **Instances** page, locate the instance that you want to connect to and click its name.
#. On the **Basic Information** page, at the **Instance Information** area, click |image3| in the **SSL** field.
#. In the displayed dialog box, click **Yes**.
#. On the **Basic Information** page, view the results.

.. |image1| image:: /_static/images/en-us_image_0000001897028497.png
.. |image2| image:: /_static/images/en-us_image_0000001900945965.png
.. |image3| image:: /_static/images/en-us_image_0000001896908953.png
