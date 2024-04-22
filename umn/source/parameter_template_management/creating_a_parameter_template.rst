:original_name: ddm_05_0006.html

.. _ddm_05_0006:

Creating a Parameter Template
=============================

A database parameter template acts as a container for parameter configurations that can be applied to one or more DDM instances. You can manage configurations of a DDM instance by managing parameters in the parameter template applied to the instance.

If you do not specify a parameter template when creating a DDM instance, the system uses the default parameter template for your instance. The default parameter template contains multiple default values, which are determined based on the computing level and the storage space allocated to the instance. You cannot modify parameter settings of a default parameter template. You must create your own parameter template to change parameter settings.

If you want to use your custom parameter template, you simply create a parameter template and select it when you create a DDM instance or apply it to an existing DDM instance following the instructions provided in :ref:`Applying a Parameter Template <ddm_05_0013>`.

When you have already created a parameter template and want to provide most of its custom parameters and values in a new parameter template, you can replicate the template you created following the instructions provided in :ref:`Replicating a Parameter Template <ddm_05_0011>`.

The following are the key points you should know when using parameters from a parameter template:

-  Changing a parameter value in a parameter template does not change any parameter in a DDM instance where it has been applied before.
-  When you change a parameter value in a parameter template and save the change, the change will take effect only after you apply the parameter template to a DDM instance and manually restart the instance.
-  Improper parameter settings may have unintended adverse effects, including degraded performance and system instability. Exercise caution when modifying parameters and you need to back up data before modifying parameters in a parameter template. Before applying parameter template changes to a production DDM instance, you should try out these changes on a test DDM instance.

Procedure
---------

#. Log in to the management console.
#. Click |image1| in the upper left corner and select a region and a project.
#. Click |image2| in the upper left corner of the page and choose **Databases** > **Distributed Database Middleware**.
#. Choose **Parameter Templates** and click **Create Parameter Template**.
#. In the displayed dialog box, enter a template name and description and click **OK**.

   -  The template name is case-sensitive and consists of 1 to 64 characters. It can contain only letters, digits, hyphens (-), underscores (_), and periods (.).
   -  The template description consists of a maximum of 256 characters and cannot include carriage return characters and the following special characters: >!<"&'=

      .. note::

         -  Each user can create up to 100 parameter templates.
         -  The parameter template quota is shared by all DDM instances in a project.

.. |image1| image:: /_static/images/en-us_image_0000001733146325.png
.. |image2| image:: /_static/images/en-us_image_0000001733146317.png
