:original_name: ddm_06_0026.html

.. _ddm_06_0026:

What Is Read-only Service Isolation?
====================================

Overview
--------

DDM provides read-only service isolation by grouping nodes of a DDM instance to provide physically separated compute and storage resources.

DDM provides two types of node groups, read-only and read/write, which handle read-only and read/write requests, respectively. By default, read-only groups handle read requests sent to read replicas at the storage layer, relieving the read pressure of core workloads in the DDM cluster. Read-only and read/write groups use the same data. When there are a large number of concurrent requests, read-only groups handle complex queries or extract data offline from read replicas of data nodes to reduce query response time and provide faster access. It is easy to use node groups without the need of establishing complex links or synchronizing data.

.. note::

   If you want read-only groups to handle SQL queries, make sure that the associated data node has available read replicas. If there are no available read replicas, the following error messages may be returned:

   -  backend database connection error;
   -  query has been canceled
   -  execute error: No read-only node
