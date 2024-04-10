:original_name: ddm_06_0021.html

.. _ddm_06_0021:

Administrator Account
=====================

Overview
--------

DDM allows you to create an administrator account for your instance. This account has the superuser permissions to modify permissions of accounts displayed on the **Accounts** page. The administrator account has read/write permissions for all schemas and tables by default, including schemas being created. Once an administrator account is created, it cannot be deleted.

You can configure an administrator account when you create an instance, or create one on the instance details page after your instance has been created.

Prerequisites
-------------

The kernel version of DDM instances must be 3.0.9 or later.

Precautions
-----------

-  After an administrator account is created, its username cannot be modified.
-  The administrator account cannot be duplicated with any DDM account on the **Accounts** page.
-  If the administrator account is modified on the management control plane, all its original permissions are cleared, and the new permissions assigned take effect.

Scenarios
---------

-  If you forget the password of the administrator account, reset it by referring to :ref:`Resetting the Administrator Password <ddm_06_0021__section1545145125010>`.
-  If you select **Skip** when you create a DDM instance, you can create an administrator by referring to :ref:`Creating an Administrator Account <ddm_06_0021__section74841851143710>` on the instance basic information page.

.. _ddm_06_0021__section1545145125010:

Resetting the Administrator Password
------------------------------------

#. Log in to the management console.
#. Click |image1| in the upper left corner and select a region and a project.
#. Click |image2| in the upper left corner of the page and choose **Databases** > **Distributed Database Middleware**.
#. In the instance list, locate the DDM instance whose administrator password you want to reset and click its name. Click **Reset Password**.
#. In the displayed dialog, enter a new password and confirm the password. Click **Yes**.
#. Wait the request is submitted.

.. _ddm_06_0021__section74841851143710:

Creating an Administrator Account
---------------------------------

#. Log in to the management console.
#. Click |image3| in the upper left corner and select a region and a project.
#. Click |image4| in the upper left corner of the page and choose **Databases** > **Distributed Database Middleware**.
#. In the instance list, locate the DDM instance that you want to create an administrator account for and click its name. Click **Create Administrator**.
#. In the displayed dialog box, enter an administrator, password, and confirm password. Click **Yes**.
#. Wait the request is submitted.

.. |image1| image:: /_static/images/en-us_image_0000001733146449.png
.. |image2| image:: /_static/images/en-us_image_0000001733266565.png
.. |image3| image:: /_static/images/en-us_image_0000001685147638.png
.. |image4| image:: /_static/images/en-us_image_0000001733266553.png
