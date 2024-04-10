:original_name: ddm_06_0027.html

.. _ddm_06_0027:

How Are Read-only Services Split from Read-Write Services
=========================================================

Procedure
---------

#. Log in to the DDM console and choose **Instances** in the navigation pane. In the instance list, locate the required instance and click its name.

#. Choose **Basic Information** in the navigation pane to view node information.

#. In the **Node Information** area, click **Create Group**. After a group is created, existing nodes are included into another read/write group by default, responsible for handling read/write requests to core services.

   .. note::

      -  One DDM instance supports multiple read-only groups. Each group contains at least 2 nodes, and each instance contains up to 32 nodes.
      -  One node belongs to only one group, and its group cannot be changed once determined. Nodes in the same group must be of the same node class.

#. On the **Create Group** page, select the required role, VPC, and node class, specify the quantity of new nodes, and click **Next**.

#. Confirm the information and click **Next** and then **Submit**.

#. After the creation is complete, check whether the original **Node Information** area becomes the **Group Information** area. Then you can manage nodes in the group.

   To delete a group of a DDM instance, locate the group that you want to delete and click **Delete**. The corresponding floating IP address becomes invalid once the group is deleted. This may affect your services. Retain at least one read/write group.
