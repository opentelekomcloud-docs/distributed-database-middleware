:original_name: ddm_04_0029.html

.. _ddm_04_0029:

How Can I Query RDS for MySQL Information by Running Command **show full innodb status**?
=========================================================================================

After you connect to a DDM instance through the MySQL client, you can run command **show full innodb status** to query information about the associated RDS for MySQL instances. The following information can be queried:

-  Current time and duration since the last output.
-  Status of the master thread.
-  SEMAPHORES including event counts and available waiting threads when there is high-concurrency workload. You can use the information to locate performance bottlenecks if any.
