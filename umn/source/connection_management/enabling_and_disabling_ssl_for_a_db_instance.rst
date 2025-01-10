:original_name: ddm_06_0041.html

.. _ddm_06_0041:

Enabling and Disabling SSL for a DB instance
============================================

Secure Socket Layer (SSL) is an encryption-based Internet security protocol for establishing secure links between a server and a client. It provides privacy, authentication, and integrity to Internet communications. SSL:

-  Authenticates users and servers, ensuring that data is sent to correct clients and servers.
-  Encrypts data to prevent data theft.
-  Ensures data integrity during transmission

SSL is disabled for new DDM instances by default. Enabling SSL will prolong network connection response and increase CPU usage. So, evaluate impacts on service performance before enabling SSL.

You can connect to a DDM instance from your client with two methods: using SSL connection or a non-SSL connection.

-  If SSL is enabled, you can connect to the instance using an SSL or non-SSL connection. SSL encrypts connections to the DB instance, making in-transit data more secure.
-  If SSL is disabled, you can only connect to the instance using a non-SSL connection.

   .. important::

      Enabling or disabling SSL will cause the instance to reboot immediately. During the reboot, the instance is unavailable. Rebooting an instance will clear its cache. To prevent traffic congestion during peak hours, you are advised to reboot it during off-peak hours.

Enabling SSL
------------

#. Log in to the DDM console.
#. On the **Instances** page, locate the instance that you want to connect to and click its name.
#. On the **Basic Information** page, at the **Instance Information** area, click |image1| in the **SSL** field.
#. In the displayed dialog box, click **Yes**.
#. On the **Basic Information** page, view the results.

Disabling SSL
-------------

#. Log in to the DDM console.
#. On the **Instances** page, locate the instance that you want to connect to and click its name.
#. On the **Basic Information** page, at the **Instance Information** area, click |image2| in the **SSL** field.
#. In the displayed dialog box, click **Yes**.
#. On the **Basic Information** page, view the results.

Downloading the CA certificate
------------------------------

#. Log in to the DDM console.
#. On the **Instances** page, locate the instance that you want to connect to and click its name.
#. On the **Basic Information** page, at the **Instance Information** area, click **Download** in the **SSL** field.
#. Download the CA certificate.

.. |image1| image:: /_static/images/en-us_image_0000002127674393.png
.. |image2| image:: /_static/images/en-us_image_0000002091995216.png
