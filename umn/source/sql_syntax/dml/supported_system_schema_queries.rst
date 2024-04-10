:original_name: ddm_12_0100.html

.. _ddm_12_0100:

Supported System Schema Queries
===============================

.. table:: **Table 1** Supported system schema queries

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | DML Syntax                        | Restriction                                                                                                     |
   +===================================+=================================================================================================================+
   | System schema queries             | The following system schema queries are supported:                                                              |
   |                                   |                                                                                                                 |
   |                                   | -  Version query: **SELECT version()**                                                                          |
   |                                   |                                                                                                                 |
   |                                   |    -  information_schema.SCHEMA_PRIVILEGES                                                                      |
   |                                   |    -  information_schema.TABLE_PRIVILEGES                                                                       |
   |                                   |    -  information_schema.USER_PRIVILEGES                                                                        |
   |                                   |    -  information_schema.SCHEMATA                                                                               |
   |                                   |    -  information_schema.tables                                                                                 |
   |                                   |    -  information_schema.columns                                                                                |
   |                                   |                                                                                                                 |
   |                                   | -  Index query: **SHOW KEYS FROM <table> FROM <database>**                                                      |
   |                                   |                                                                                                                 |
   |                                   | .. note::                                                                                                       |
   |                                   |                                                                                                                 |
   |                                   |    -  Supported operators include **=**, **IN**, and **LIKE**. These operators can be associated using **AND**. |
   |                                   |    -  Complex queries, such as subquery, JOIN, sorting, aggregate query, and LIMIT, are not supported.          |
   |                                   |    -  **information_schema.tables** and **information_schema.columns** support operators **<** and **>**.       |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------+
