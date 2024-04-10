:original_name: ddm_05_0007.html

.. _ddm_05_0007:

Editing a Parameter Template
============================

To improve performance of a DDM instance, you can modify parameters in custom parameter templates based on service requirements.

You cannot change parameter values in default parameter templates.

The following are the key points you should know when using parameters from a parameter template:

-  When you modify a custom parameter template, the modifications take effect only after you apply the parameter template to DDM instances. For details, see :ref:`Applying a Parameter Template <ddm_05_0013>`.
-  The time when the modification takes effect is determined by the type of the parameter.
-  Parameters in default parameter templates cannot be modified. You can view these parameters by clicking template names. If a custom parameter template is set incorrectly and causes an instance restart to fail, you can re-configure the custom parameter template according to configurations of the default parameter template.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner and select a region and a project.

#. Click |image2| in the upper left corner of the page and choose **Databases** > **Distributed Database Middleware**.

#. Choose **Parameter Templates**, click the **Custom Templates** tab, locate the required parameter template, and click its name.

#. On the **Parameter Details** page, modify parameters as needed.

   Available operations are as follows:

   -  To save the modifications, click **Save**.
   -  To cancel the modifications, click **Cancel**.

#. After the parameter values are modified, click **Template History** to view details.

   .. important::

      -  The modifications take effect only after you apply the parameter template to DDM instances. For details, see :ref:`Applying a Parameter Template <ddm_05_0013>`.
      -  The instance restart caused by node class changes will not put parameter modifications into effect.

.. |image1| image:: /_static/images/en-us_image_0000001685307326.png
.. |image2| image:: /_static/images/en-us_image_0000001733146397.png
