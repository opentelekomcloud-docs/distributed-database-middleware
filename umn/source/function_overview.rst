:original_name: ddm_03_0053.html

.. _ddm_03_0053:

Function Overview
=================

Distributed Database Middleware (DDM) is a MySQL-compatible, distributed middleware service designed for relational databases. It can resolve distributed scaling issues to break through capacity and performance bottlenecks of MySQL databases, helping handle highly concurrent access to massive volumes of data.

:ref:`Table 1 <ddm_03_0053__table297216124517>` lists the functions supported by DDM.

.. _ddm_03_0053__table297216124517:

.. table:: **Table 1** DDM functions

   +--------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Category                                   | Function                                                                                                                                                                          |
   +============================================+===================================================================================================================================================================================+
   | Instances                                  | Creating, deleting, renewing, unsubscribing from, and restarting a DDM instance, and changing class of a DDM instance. For details, see :ref:`Instance Management <ddm_06_0001>`. |
   +--------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Backups                                    | Restoring data to a new DDM instance and restoring metadata. For details, see :ref:`Backups and Restorations <ddm_03_0067>`.                                                      |
   +--------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter templates                        | Creating, editing, replicating, and applying a parameter template, and comparing two parameter templates. For details, see :ref:`Parameter Template Management <ddm_05_0005>`.    |
   +--------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Task center                                | Enabling you to view progress and statuses of asynchronous tasks submitted on the console. For details, see :ref:`Task Center <ddm_09_0002>`.                                     |
   +--------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Schemas                                    | Creating, exporting, importing, and deleting schemas. For details, see :ref:`Schema Management <ddm_03_0006>`.                                                                    |
   +--------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Flexible shards configuration for a schema | You can increase shards or data nodes to scale out storage. For details, see :ref:`Shard Configuration <ddm_03_0064>`.                                                            |
   +--------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Accounts                                   | Creating, modifying, and deleting a DDM account, and resetting its password. For details, see :ref:`Account Management <ddm_05_0001>`.                                            |
   +--------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Monitoring                                 | Providing metrics and methods of viewing metrics. For details, see :ref:`Monitoring Management <ddm_03_0050>`.                                                                    |
   +--------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SQL syntax                                 | Describing DDL, DML, global sequence, SQL statements, and sharding algorithms. For details, see :ref:`SQL Syntax <ddm-08-0001>`.                                                  |
   +--------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
