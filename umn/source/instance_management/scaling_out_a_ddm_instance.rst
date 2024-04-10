:original_name: ddm_06_0011.html

.. _ddm_06_0011:

Scaling Out a DDM Instance
==========================

Scenarios
---------

As service data increases, you can scale out a DDM instance by adding nodes to improve service stability.

.. note::

   -  Scale out your DDM instance during off-peak hours.
   -  Make sure that the associated data nodes are normal and not undergoing other operations.
   -  Each DDM instance supports up to 32 nodes.
   -  After a read-only group is created, the entry for adding nodes will be moved to the operation column of the group.

Procedure
---------

#. In the instance list, locate the DDM instance that you want to scale out and click its name. Click **Scale Out**.
#. On the displayed page, view the current instance configuration, select the required AZ, and specify the number of new nodes.
#. Click **Next**.
#. On the displayed page, click **Submit** if all configurations are correct.
