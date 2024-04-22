:original_name: ddm-08-0013.html

.. _ddm-08-0013:

Use Constraints
===============

DDM is compatible with the MySQL license and syntax, but the use of SQL statements is limited due to differences between distributed databases and single-node databases.

Unsupported SQL Statements
--------------------------

-  Triggers
-  Temporary tables
-  DO statement
-  Association with foreign keys
-  RESET statement
-  FLUSH statement
-  BINLOG statement
-  HANDLER statement
-  SHOW WARNINGS statement
-  Assignment operator :=
-  Operators less than (<), assignment (=), and more than (>)
-  Expression IS UNKNOWN
-  INSTALL and UNINSTALL PLUGIN statements
-  Cross-shard stored procedures and custom functions
-  Statements for modifying database names, table names, and sharding field names and types
-  Most of SHOW statements such as SHOW PROFILES and SHOW ERRORS
-  Table maintenance statements, including ANALYZE, CHECK, CHECKSUM, OPTIMIZE, and REPAIR TABLE
-  Statements for assigning a value to or querying variable **session**, for example, set @rowid=0;select @rowid:=@rowid+1,id from user
-  SQL statements that use -- or ``/*...*/`` to comment out a single line or multiple lines of code
-  The result of the REPEAT function contains a maximum of 1,000,000 characters (in version 3.0.9 or later).

Permission Levels
-----------------

Permission levels supported by DDM are as follows:

-  Global level (not supported)
-  Database level (supported)
-  Table level (supported)
-  Column level (not supported)
-  Subprogram level (not supported)
-  User level (supported)
