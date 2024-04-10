:original_name: ddm_04_0035.html

.. _ddm_04_0035:

What Should I Do If an Error Message Is Returned When I Specify an Auto-Increment Primary Key During Migration?
===============================================================================================================

Execute the following SQL statement to modify the start value of the auto-increment primary key so that the value is greater than the maximum value of primary keys in existing tables:

.. code-block::

   ALTER SEQUENCE <Database_name>.<SEQ_name> START WITH <New_start_value>
