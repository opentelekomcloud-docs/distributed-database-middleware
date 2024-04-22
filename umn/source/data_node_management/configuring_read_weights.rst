:original_name: ddm_10_1002.html

.. _ddm_10_1002:

Configuring Read Weights
========================

If one DDM instance is associated with multiple data nodes, you can synchronize read weight settings of the first data node to other data nodes.

Prerequisites
-------------

You have logged in to the DDM console.

Precautions
-----------

The read weight can be 0 to 100.

Procedure
---------

#. In the instance list, locate the DDM instance whose data nodes you want to configure read weights for.
#. Click the instance name to enter the **Basic Information** page.
#. In the navigation pane, choose **Data Nodes**.
#. Set read weights for associated instances.

   -  Set read weights for multiple instances.

      If you want to set read weights for multiple instances at a time, click **Configure Read Weight** on the **Data Nodes** page.

      In the displayed dialog box, click **Synchronize** to apply the read weight of the first instance to other instances. This operation requires that read weights of all instances should be the same. Otherwise, you need to manually configure a read weight for each instance.

   -  Set a read weight for an instance.

      If you want to set the read weight of an instance, locate the target instance and click **Configure Read Weight** in the **Operation** column.

#. Click **Yes**.
#. After the read weight is configured successfully, you can view the updated read weight on the **Data Nodes** page.
