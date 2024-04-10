:original_name: ddm_03_0062.html

.. _ddm_03_0062:

Introduction
============

DDM is compatible with the MySQL license and syntax, but the use of SQL statements is limited due to differences between distributed databases and single-node databases.

Before selecting a DDM solution, evaluate the SQL syntax compatibility between your application and DDM.

MySQL EXPLAIN
-------------

If you add **EXPLAIN** before a SQL statement, you will see a specific execution plan when you execute the statement. You can analyze the time required based on the plan and modify the SQL statement for optimization.

.. table:: **Table 1** Description of the **EXPLAIN** column

   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Column Name   | Description                                                                                                                                                                                                                                                                                  |
   +===============+==============================================================================================================================================================================================================================================================================================+
   | table         | Table that the row of data belongs to                                                                                                                                                                                                                                                        |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | type          | Type of the connection. Connection types from the best to the worst are **const**, **eq_reg**, **ref**, **range**, **index**, and **ALL**.                                                                                                                                                   |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | possible_keys | Index that may be applied to the table                                                                                                                                                                                                                                                       |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | key           | Index that is actually used. If the value is **NULL**, no index is used. In some cases, MySQL may choose to optimize indexes, for example, force MySQL to use an index by adding **USE INDEX(indexname)** to a SELECT statement or to ignore an index by adding **IGNORE INDEX(indexname)**. |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | key_len       | Length of the used index. The shorter the length is, the better the index is if accuracy is not affected.                                                                                                                                                                                    |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ref           | Column where the index is used. The value is generally a constant.                                                                                                                                                                                                                           |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | rows          | Rows of the data returned by MySQL                                                                                                                                                                                                                                                           |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Extra         | Additional information about how MySQL parses queries                                                                                                                                                                                                                                        |
   +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

SQL Restrictions
----------------

-  Temporary tables are not supported.

-  Foreign keys, views, cursors, triggers, and stored procedures are not supported.
-  Customized data types and functions are not supported.
-  Process control statements such as IF and WHILE are not supported.
-  Compound statements such as BEGIN...END, LOOP...END LOOP, REPEAT...UNTIL...END REPEAT, and WHILE...DO...END WHILE are not supported.

DDL Syntax
----------

-  Sharded and broadcast tables do not support foreign keys.
-  Modifying sharding keys is not supported.
-  ALTER DATABASE Syntax is not supported.
-  Creating sharded or broadcast tables from another table is not supported.
-  The CREATE TABLE statement does not support GENERATED COLUMN.
-  Modifying sharding keys or global sequence fields using the **ALTER** command is not supported.
-  Creating TEMPORARY sharded or broadcast tables is not supported.
-  The logical table name contains only letters, digits, and underscores (_).
-  CREATE TABLE tbl_name LIKE old_tbl_name is not supported.
-  The CREATE TABLE tbl_name SELECT statement is not supported.
-  Updating the sharding key by executing INSERT INTO ON DUPLICATE KEY UPDATE is not supported.
-  Cross-schema DDL is not supported, for example, CREATE TABLE db_name.tbl_name (... )
-  Reverse quotation marks are required to quote identifiers such as table names, column names, and index names that are MySQL key words or reserved words.

DML Syntax
----------

-  PARTITION clauses are not supported.
-  Nesting a subquery in an UPDATE statement is not supported.
-  INSERT DELAYED Syntax is not supported.
-  STRAIGHT_JOIN and NATURAL JOIN are not supported.
-  Multiple-table UPDATE is supported if all tables joined across shards have primary keys.
-  Multiple-table DELETE is supported if all tables joined across shards have primary keys.

-  Using or manipulating variables in SQL statements is not supported, for example, SET @c=1, @d=@c+1; SELECT @c, @d.

-  Inserting keyword DEFAULT or updating a sharding key value to DEFAULT is not supported.

-  Repeatedly updating the same field in an UPDATE statement is not supported.

-  Updating a sharding key using UPDATE JOIN syntax is not supported.

-  UPDATE cannot be used to update self-joins.

-  Referencing other object columns in assignment statements or expressions may cause unexpected update results. Example:

   update tbl_1 a,tbl_2 b set a.name=concat(b.name,'aaaa'),b.name=concat(a.name,'bbbb') on a.id=b.id

-  If a text protocol is used, BINARY, VARBINARY, TINYBLOB, BLOB, MEDIUMBLOB, and LONGBLOB data must be converted into hexadecimal data.

-  DDM processes invalid data based on **sql_mode** settings of associated MySQL instances.

-  UPDATE JOIN supports only joins with WHERE conditions.

-  The expression in a SQL statement has a maximum of 1000 factors.

Unsupported Functions
---------------------

-  XML functions
-  GTID functions
-  Full-text search functions
-  Enterprise encryption functions
-  Function **row_count()**

Subqueries
----------

Using subqueries in the HAVING clause and the JOIN ON condition is not supported.

Data Types
----------

Spatial data types are not supported.
