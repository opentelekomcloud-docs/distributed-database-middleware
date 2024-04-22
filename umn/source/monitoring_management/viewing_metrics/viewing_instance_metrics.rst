:original_name: ddm_03_0052.html

.. _ddm_03_0052:

Viewing Instance Metrics
========================

Cloud Eye monitors the running status of DDM instances. You can view instance monitoring metrics on the DDM console.

Monitored data requires a period of time for transmission and display. The status of the monitored object displayed on the Cloud Eye page is the status obtained 5 to 10 minutes before. If you have created a DDM instance, wait for 5 to 10 minutes to view its monitored data on Cloud Eye.

Prerequisites
-------------

-  The DDM instance is running normally.

   Monitored data of faulty or deleted DDM instances are not displayed on Cloud Eye.

-  The DDM instance has been normally running for about 10 minutes.

   It takes a while to view the monitoring data and graphics of a newly created DDM instance.

Procedure
---------

#. Log in to the DDM console.

#. On the **Instances** page, locate the required instance and click **More** > **View Metric** in the **Operation** column.

   Alternatively, click the instance name, on the displayed page, click **View Metric** in the upper right corner.

#. In the instance list, click |image1| in the front of the target instance. Locate a node and click **View Metric** in the **Operation** column.

   You can view instance metrics, including CPU usage, memory usage, network input throughput, network output throughput, QPS, and slow query logs. For details, see :ref:`DDM Instance Metrics <ddm_03_0051>`.

.. |image1| image:: /_static/images/en-us_image_0000001620873737.png
