:original_name: ddm_06_0003.html

.. _ddm_06_0003:

Changing Class of a DDM Node
============================

Prerequisites
-------------

-  You have logged in to the DDM console.
-  The DDM instance is in the **Running** state.

.. important::

   Change node class during off-peak hours because services will be interrupted for a while during class changing.

Procedure
---------

.. important::

   After a read-only group is created, the entry for changing node class will be moved to the operation column of the group.

#. In the instance list, locate the DDM instance whose node class you want to change and click its name. Click **Change**.
#. On the displayed page, select the required class.
#. Confirm the configurations and click **Submit**.
#. Switch back to the instance list and check whether the status of the instance changes to **Changing class**. You can also view the change task at Task Center.

   .. note::

      -  Once the change operation is performed, it cannot be undone. To change the class again, submit another request after the class change is complete.
      -  Node class can be upgraded or downgraded.
