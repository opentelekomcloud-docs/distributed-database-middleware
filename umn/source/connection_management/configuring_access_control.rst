:original_name: ddm_06_0035.html

.. _ddm_06_0035:

Configuring Access Control
==========================

Scenarios
---------

DDM supports load balancing by default, but some regions may not support. If an application accesses DDM using a private IP address, there are no traffic restrictions. To control access, you need to configure access control for your DDM instance. The security group is still valid for access requests directly sent to DDM nodes.

Procedure
---------

#. Log in to the DDM console.
#. On the **Instances** page, locate the required instance and click its name.
#. On the displayed page, toggle on **Access Control**.

   -  If the DDM instance has only one group, in the **Network Information** area, click |image1| on the right of button **Access Control**.


      .. figure:: /_static/images/en-us_image_0000001685307398.png
         :alt: **Figure 1** Enabling access control for a single group

         **Figure 1** Enabling access control for a single group

   -  If the DDM instance has multiple groups, the access control button is moved to the group information list. On the **Basic Information** page, in the group list, click |image2| in the **Access Control** column.


      .. figure:: /_static/images/en-us_image_0000001685147654.png
         :alt: **Figure 2** Enabling access control for multiple groups

         **Figure 2** Enabling access control for multiple groups

#. Click **Configure** on the right of **Access Control**. In the **Configure Access Control** dialog box, specify **Access Policy**, enter the required IP addresses, and click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001733146461.png
.. |image2| image:: /_static/images/en-us_image_0000001685307394.png
