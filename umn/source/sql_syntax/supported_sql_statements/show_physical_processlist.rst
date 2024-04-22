:original_name: ddm_08_0032.html

.. _ddm_08_0032:

SHOW PHYSICAL PROCESSLIST
=========================

**Command Format 1:**

**show physical processlist**;

This command returns the processes that run on the associated RDS instance.

**Command Format 2:**

**show physical processlist with info**;

This commands filters out the data records whose **info** is empty from result sets of command 1 and returns only the data records whose **info** is not empty.

**Command Output**


.. figure:: /_static/images/en-us_image_0000001685307362.png
   :alt: **Figure 1** Command execution effect

   **Figure 1** Command execution effect

**Output Details:**

**Ip**: indicates the IP address of the associated RDS instance.

**Port**: indicates the port number of the associated RDS instance.

**Instance_id**: indicates the ID of the associated RDS instance.

**Type**: **master** indicates that the associated instance is a primary instance, and **readreplica** indicates that the associated instance is a read replica.

Columns after column **Type** indicate the information about processes running on the associated RDS instance. Such information is the same as the output of command **show processlist** executed on the associated RDS instance.

**Command Format 3:**

Run the following statement to kill the execution thread on the associated RDS instance:

**kill physical** *<physical_thread_id>*\ **@**\ *<rds_ip>*\ **:**\ *<rds_port>*;

**physical_thread_id**: indicates the ID of the execution thread on the associated RDS instance. You can obtain it from the result set in command 2.

**rds_ip**: indicates the IP address of the associated RDS instance. You can obtain it from the result set in command 2.

**rds_port**: indicates the port number of the associated RDS instance. You can obtain it from the result set in command 2.

.. important::

   -  SHOW PHYSICAL PROCESSLIST is available only in kernel 3.0.1 or later.
   -  You need to log in to the target DDM instance and execute the preceding commands on it.
