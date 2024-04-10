:original_name: ddm_01_0007.html

.. _ddm_01_0007:

Regions and AZs
===============

Concepts
--------

The combination of a region and an availability zone (AZ) identifies the location of a data center. You can create resources in a specific AZ in a region.

-  A region is a geographic area where physical data centers are located. Each region is completely independent, improving fault tolerance and stability. After a resource is created, its region cannot be changed.
-  An AZ is a physical location using independent power supplies and networks. Faults in an AZ do not affect other AZs. A region can contain multiple AZs, which are physically isolated but interconnected through internal networks. This ensures the independence of AZs and provides low-cost and low-latency network connections.

:ref:`Figure 1 <ddm_01_0007__fig18764197715>` shows the relationship between regions and AZs.

.. _ddm_01_0007__fig18764197715:

.. figure:: /_static/images/en-us_image_0000001733266557.png
   :alt: **Figure 1** Regions and AZs

   **Figure 1** Regions and AZs

Selecting a Region
------------------

You are advised to select a region close to you or your target users. This reduces network latency and improves access rate.

Selecting an AZ
---------------

When determining whether to deploy resources in the same AZ, consider your applications' requirements on disaster recovery (DR) and network latency.

-  For high DR capability, deploy resources in different AZs in the same region.
-  For low network latency, deploy resources in the same AZ.
