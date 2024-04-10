:original_name: ddm_03_0032.html

.. _ddm_03_0032:

Database Management Syntax
==========================

Supported Database Management Syntax
------------------------------------

-  SHOW Syntax

-  SHOW COLUMNS Syntax

-  SHOW CREATE TABLE Syntax

-  SHOW TABLE STATUS Syntax

-  SHOW TABLES Syntax

-  SHOW DATABASES

   If the required database is not found, check fine-grained permissions of your account.

-  SHOW INDEX FROM

-  SHOW VARIABLES Syntax

Supported Database Tool Commands
--------------------------------

-  DESC Syntax

-  USE Syntax

-  EXPLAIN Syntax

   Unlike EXPLAIN in MySQL, the output of DDM EXPLAIN describes the nodes that the current SQL statement is routed to.

Unsupported Database Management Syntax
--------------------------------------

.. table:: **Table 1** Restrictions on database management statements

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item                              | Restriction                                                                                                                                                                                     |
   +===================================+=================================================================================================================================================================================================+
   | Database management statements    | -  Executing SET Syntax to modify global variables is not supported.                                                                                                                            |
   |                                   | -  SHOW TRIGGERS is not supported.                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                 |
   |                                   | The following SHOW statements are randomly sent to a database shard. If database shards are on different RDS for MySQL instances, the returned variables or table information may be different. |
   |                                   |                                                                                                                                                                                                 |
   |                                   | -  SHOW TABLE STATUS                                                                                                                                                                            |
   |                                   | -  SHOW VARIABLES Syntax                                                                                                                                                                        |
   |                                   | -  CHECK TABLE does not support sharding tables by hash or sharding key.                                                                                                                        |
   |                                   | -  SHOW WARNINGS Syntax does not support the combination of LIMIT and COUNT.                                                                                                                    |
   |                                   | -  SHOW ERRORS Syntax does not support the combination of LIMIT and COUNT.                                                                                                                      |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
